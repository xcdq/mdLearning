### 多线程

使用AsyncTask
不过为了更加方便我们在子线程中对UI进行操作，Android还提供了另外
一些好用的工具，比如AsyncTask。借助AsyncTask，即使你对异步消息处
理机制完全不了解，也可以十分简单地从子线程切换到主线程。当然，
AsyncTask背后的实现原理也是基于异步消息处理机制的，只是Android
帮我们做了很好的封装而已。
首先来看一下AsyncTask的基本用法，由于AsyncTask是一个抽象类，所
以如果我们想使用它，就必须要创建一个子类去继承它。在继承时我们
可以为AsyncTask类指定3个泛型参数，这3个参数的用途如下。
Params 。在执行AsyncTask时需要传入的参数，可用于在后台任务中
使用。
Progress 。后台任务执行时，如果需要在界面上显示当前的进度，则
使用这里指定的泛型作为进度单位。
Result 。当任务执行完毕后，如果需要对结果进行返回，则使用这里
指定的泛型作为返回值类型。
因此，一个最简单的自定义AsyncTask就可以写成如下方式：
class DownloadTask extends AsyncTask<Void, Integer, Boolean> {
...
}
这里我们把AsyncTask的第一个泛型参数指定为 Void ，表示在执行
AsyncTask的时候不需要传入参数给后台任务。第二个泛型参数指定
为 Integer ，表示使用整型数据来作为进度显示单位。第三个泛型参数指
定为 Boolean ，则表示使用布尔型数据来反馈执行结果。
当然，目前我们自定义的DownloadTask还是一个空任务，并不能进行任
何实际的操作，我们还需要去重写AsyncTask中的几个方法才能完成对任
务的定制。经常需要去重写的方法有以下4个。

1. onPreExecute()
   这个方法会在后台任务开始执行之前调用，用于进行一些界面上的
   初始化操作，比如显示一个进度条对话框等。

2. doInBackground(Params...)
   这个方法中的所有代码都会在子线程中运行，我们应该在这里去处
   理所有的耗时任务。任务一旦完成就可以通过 return 语句来将任务
   的执行结果返回，如果AsyncTask的第三个泛型参数指定的是 Void ，
   就可以不返回任务执行结果。注意，在这个方法中是不可以进行UI
   操作的，如果需要更新UI元素，比如说反馈当前任务的执行进度，可
   以调用 publishProgress (Progress...) 方法来完成。

3. onProgressUpdate(Progress...)
   当在后台任务中调用了 publishProgress(Progress...) 方法
   后， onProgressUpdate (Progress...) 方法就会很快被调用，该方法
   中携带的参数就是在后台任务中传递过来的。在这个方法中可以对
   UI进行操作，利用参数中的数值就可以对界面元素进行相应的更
   新。

4. onPostExecute(Result)
   当后台任务执行完毕并通过 return 语句进行返回时，这个方法就很
   快会被调用。返回的数据会作为参数传递到此方法中，可以利用返
   回的数据来进行一些UI操作，比如说提醒任务执行的结果，以及关
   闭掉进度条对话框等。
   因此，一个比较完整的自定义AsyncTask就可以写成如下方式：

   

   ```
   class DownloadTask extends AsyncTask<Void, Integer, Boolean> {
   @Override
   protected void onPreExecute() {
   progressDialog.show(); // 显示进度对话框
   }
   @Override
   protected Boolean doInBackground(Void... params) {
   try {
   while (true) {
   int downloadPercent = doDownload(); // 这是一个虚构的方法
   publishProgress(downloadPercent);
   if (downloadPercent >= 100) {
   break;
   }
   }
   } catch (Exception e) {
   return false;
   }
   return true;
   }
   @Override
   protected void onProgressUpdate(Integer... values) {
   // 在这里更新下载进度
   progressDialog.setMessage("Downloaded " + values[0] + "%");
   }
   @Override
   protected void onPostExecute(Boolean result) {
   progressDialog.dismiss(); // 关闭进度对话框
   // 在这里提示下载结果
   if (result) {
   Toast.makeText(context, "Download succeeded", Toast.LENGTH_SHORT).show();
   } else {
   Toast.makeText(context, " Download failed", Toast.LENGTH_SHORT).show();
   }
   }
   }
   ```

   

   在这个DownloadTask中，我们在 doInBackground() 方法里去执行具体的
   下载任务。这个方法里的代码都是在子线程中运行的，因而不会影响到
   主线程的运行。注意这里虚构了一个 doDownload() 方法，这个方法用于计
   算当前的下载进度并返回，我们假设这个方法已经存在了。在得到了当
   前的下载进度后，下面就该考虑如何把它显示到界面上了，由于
   doInBackground() 方法是在子线程中运行的，在这里肯定不能进行UI操
   作，所以我们可以调用 publishProgress() 方法并将当前的下载进度传进
   来，这样 onProgressUpdate() 方法就会很快被调用，在这里就可以进行UI
   操作了。
   当下载完成后， doInBackground() 方法会返回一个布尔型变量，这
   样 onPostExecute() 方法就会很快被调用，这个方法也是在主线程中运行
   的。然后在这里我们会根据下载的结果来弹出相应的Toast提示，从而完
   成整个DownloadTask任务。
   简单来说，使用AsyncTask的诀窍就是，在 doInBackground() 方法中执行
   具体的耗时任务，在 onProgressUpdate() 方法中进行UI操作，
   在 onPostExecute() 方法中执行一些任务的收尾工作。
   如果想要启动这个任务，只需编写以下代码即可：
   new DownloadTask().execute();
   以上就是AsyncTask的基本用法，怎么样，是不是感觉简单方便了许多？
   我们并不需要去考虑什么异步消息处理机制，也不需要专门使用一个
   Handler来发送和接收消息，只需要调用一下 publishProgress() 方法，就
   可以轻松地从子线程切换到UI线程了。









### 数据库

数据库创建成功后，下一步要做的就是在数据库中创建表。表是数据在数据库中的一个独立单元，代表了某些实体数据类型，表由行和列组成。每一行代表一项数据，每一列则代表一个数据。表与表之间可以进行关联，形成一定的关系网，这样就可以将数据拆分到不同的表中，减少单表体积并且提升操作速度。创建表的SQL语法为：

注意，每一条SQL语句都以分号结尾，因此，不能少了末尾的“; ”。表创建语法中，如果在table前面加上temp或者temporary，那么表示这是一个临时表，临时表会在这次连接会话结束时自动销毁。table后是表名，然后将各个字段声明在一个括号中。SQL语句中的每个字段就代表了该表中的每一列，用户可以为每一列指定数据类型、添加约束。SQLite中的数据类型只有5种，如表5-1所示。

| 数据类型 | 说明                     |
| -------- | ------------------------ |
| Null     | 数值为空                 |
| INTEGER  | 整型                     |
| REAL     | 浮点型                   |
| TEXT     | 文本类型                 |
| BLOB     | 数据块，完全按照输入存放 |



| 条件          | 作用                         |
| ------------- | ---------------------------- |
| NOT NULL      | 不为空                       |
| UNIQUE        | 唯一                         |
| PRIMARY KEY   | 主键                         |
| CHECK         | 条件检查                     |
| DEFAULT       | 默认值                       |
| AUTOINCREMENT | 自增长                       |
| VARCHAR(20)   | 字符数小于20，20数字可以更改 |

从原始表的数据中创建一个临时表，第二步再删除原始表，然后重新创建一个新表，再将数据从临时表导入到新创建的表中，这样完成了表结构的升级。后续讲Android中的数据库升级时将会介绍具体的示例。

1. 管理类，用于数据库层面的操作。
   * openDatabase：打开指定路径的数据库。
   * isOpen：判断数据库是否已打开。
   * close：关闭数据库。
   * getVersion：获取数据库的版本号。
   * setVersion：设置数据库的版本号。
2. 事务类，用于事务层面的操作。
   * beginTransaction：开始事务。
   * setTransactionSuccessful：设置事务的成功标志。
   * endTransaction：结束事务。执行本方法时，系统会判断是否已执行setTransactionSuccessful，如果之前已设置就提交，如果没有设置就回滚。
3. 数据处理类，用于数据表层面的操作。
   * execSQL：执行拼接好的SQL控制语句。一般用于建表、删表、变更表结构。
   * delete：删除符合条件的记录。
   * update：更新符合条件的记录。
   * insert：插入一条记录。
   * query：执行查询操作，返回结果集的游标。
   * rawQuery：执行拼接好的SQL查询语句，返回结果集的游标。
   * 
   * 
   * 封装保证数据库安全的必要方法，包括获取单例对象、打开数据库连接、关闭数据库连接。获取单例对象：确保App运行时数据库只被打开一次，避免重复打开引起错误。打开数据库连接：SQLite有锁机制，即读锁和写锁的处理；故而数据库连接也分两种，读连接可调用SQLiteOpenHelper的getReadableDatabase方法获得，写连接可调用getWritableDatabase获得。关闭数据库连接：数据库操作完毕后，应当调用SQLiteDatabase对象的close方法关闭连接。

1．SQLiteOpenHelper类SQLiteOpenHelper是SQLiteDatabse的一个帮助类，用来管理数据的创建和版本的更新。

一般的用法是定义一个类继承SQLiteOpenHelper，并实现两个回调方法：OnCreate（SQLiteDatabase db）和onUpgrade（SQLiteDatabse, int oldVersion, intnewVersion）来创建和更新数据库。

onCreate（）方法在初次生成数据库时才会被调用，在onCreate（）方法中可以生成数据库表结构及添加一些应用使用到的初始化数据。

onUpgrade（）方法在数据库的版本发生变化时会被调用，一般在软件升级时才需改变版本号。

当程序调用SQLiteOpenHelper类的getWritableDatabase（）方法或者getReadableDatabase（）方法获取用于操作数据库的SQLiteDatabase实例的时候，如果数据库不存在，则Android系统会自动生成一个数据库，接着调用onCreate（）方法。

2．SQLiteDatabase类Android提供了一个名为SQLiteDatabase的类（SQLiteOpenHelper类中的getWritableDatabase（）和getReadableDatabase（）方法返回这个类的对象），

使用该类可以完成对数据的添加（Create）、查询（Retrieve）、更新（Update）和删除（Delete）操作（这些操作简称为CRUD）。SQLiteDatabase类的常用方法如下所示。

* long insert（String table, String nullColumnHack, ContentValues values）

  * table代表想插入数据的表名；

  * nullColumnHack代表强行插入null值的数据列的列名；

  * values代表一行记录的数据。insert方法插入的一行记录使用ContentValues存放，ContentValues类似于Map，它提供了put（String key, Xxx value）（其中key为数据列的列名）方法用于存入数据，getAsXxx（String key）方法用于取出数据。·　

    

* update（Stringtable, ContentValuesvalues, StringwhereClause,String[]whereArgs）——修改满足条件的数据。

* delete（String table, String whereClause, String[]whereArgs）——删除满足特定条件的数据。

* exceSQL（String sql, Object[]bindArgs）——执行一条占位符SQL语句。

* close（）——关闭数据库。

* Cursor query（boolean distinct, String table, String[]columns, Stringselection, String[]selectionArgs, String groupBy, String having, String orderBy,String limit）——该方法用于查询数据。

3．Cursor接口

可被SQLite直接使用的数据结构是ContentValues类，类似于映射Map，提供put和get方法用来存取键值对。区别之处在于ContentValues的键只能是字符串，查看ContentValues的源码会发现其内部保存键值对的数据结构就是HashMap“private HashMap<String,Object>mValues;”。ContentValues主要用于记录增加和更新操作，即SQLiteDatabase的insert和update方法。对于查询操作来说，使用的是另一个游标类Cursor。

调用SQLiteDatabase的query和rawQuery方法时，返回的都是Cursor对象，因此获取查询结果要根据游标的指示一条一条遍历结果集合。

| 参数名        | 作用                             |
| ------------- | -------------------------------- |
| Table         | 要操作的表名                     |
| Columns       | 要获取的字段数组                 |
| Selection     | 条件语句，也就是where部分        |
| SelectionArgs | where语句中的字段值              |
| GroupBy       | 结果集按照一定的规则划分为多个组 |
| having        | Group by里的having语句           |
| OrderBy       | 排序语句                         |
| Limit         | 限制返回数量与偏移量             |
|               |                                  |



Cursor的常用方法可分为3类，说明如下：

1. 游标控制类方法，用于指定游标的状态。close：关闭游标。isClosed：判断游标是否关闭。isFirst：判断游标是否在开头。isLast：判断游标是否在末尾。
2.  游标移动类方法，把游标移动到指定位置。moveToFirst：移动游标到开头。moveToLast：移动游标到末尾。moveToNext：移动游标到下一条记录。moveToPrevious：移动游标到上一条记录。move：往后移动游标若干条记录。moveToPosition：移动游标到指定位置的记录。
3. 获取记录类方法，可获取记录的数量、类型以及取值。getCount：获取结果记录的数量。getInt：获取指定字段的整型值。getFloat：获取指定字段的浮点数值。getString：获取指定字段的字符串值。getType：获取指定字段的字段类型。

Cursor是一个游标接口，在数据库中作为返回值，相当于结果集ResultSet。

Cursor的一些常用方法如下所示：

* moveToFirst（）——移动光标到第一行。
* moveToLast（）——移动光标到最后一行。
* moveToNext（）——移动光标到下一行。
* moveToPosition（int position）——移动光标到一个绝对的位置。
* moveToPrevious（）——移动光标到上一行。
* getColumnCount（）——返回所有列的总数。
* getColumnIndex（String columnName）——返回指定列的名称，如果不存在，则返回-1。
* getColumnName（int columnIndex）——从给定的索引返回列名。
* etColumnNames（）——返回一个字符串数组的列名。
* getCount（）——返回Cursor中的行数。以上就是SQLite数据库常用的操作类以及接口，熟练掌握这些能够更好地进行数据库的开发。



去创建一个分支，
命令如下：
git branch version1.0
这样就创建了一个名为version1.0的分支，我们再次输入 git branch 这个
命令来检查一下



可以看到，果然有一个叫作version1.0的分支出现了。你会发现，master分
支的前面有一个“*”号，说明目前我们的代码还是在master分支上的，那
么怎样才能切换到version1.0这个分支上呢？其实也很简单，只需要使
用 checkout 命令即可，如下所示：
git checkout version1.0



在version1.0分支上修改并提交的代码将不会影响到
master分支。同样的道理，在master分支上修改并提交的代码也不会影响
到version1.0分支。因此，如果我们在version1.0分支上修复了一个bug，在
master分支上这个bug仍然是存在的。这时将修改的代码一行行复制到
master分支上显然不是一种聪明的做法，最好的办法就是使用 merge 命令
来完成合并操作，如下所示：
git checkout master
git merge version1.0



不再需要version1.0这个分支的时候，可以使用如下命令将
这个分支删除掉：
git branch -D version1.0



就可以使用如下的命令将代码下载
到本地：
git clone https://github.com/example/test.git
之后你在这份代码的基础上进行了一些修改和提交，那么怎样才能把本
地修改的内容同步到远程版本库上呢？这就需要借助 push 命令来完成
了，用法如下所示：
git push origin master
其中 origin 部分指定的是远程版本库的Git地址， master 部分指定的是同
步到哪一个分支上，上述命令就完成了将本地代码同步
到https://github.com/example/test.git这个版本库的 master 分支上的功能。



知道了将本地的修改同步到远程版本库上的方法，接下来我们看一下如
何将远程版本库上的修改同步到本地。Git提供了两种命令来完成此功
能，分别是 fetch 和 pull ， fetch 的语法规则和 push 是差不多的，如下所示：
`git fetch origin master`
执行这个命令后，就会将远程版本库上的代码同步到本地，不过同步下
来的代码并不会合并到任何分支上去，而是会存放到一个 origin/master
分支上，这时我们可以通过 diff 命令来查看远程版本库上到底修改了哪
些东西：
`git diff origin/master`
之后再调用 merge 命令将 origin/master 分支上的修改合并到主分支上即
可，如下所示：
`git merge origin/master`
而pull命令则是相当于将fetch和merge这两个命令放在一起执行了，它可
以从远程版本库上获取最新的代码并且合并到本地，用法如下所示：
`git pull origin master`
也许你现在对远程版本库的使用还是感觉比较抽象，没关系，因为暂时
我们只是了解了一下命令的用法，还没进行实践，

### 修改标题栏文字

![image-20200426160403475](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200426160403475.png)

![image-20200426160251118](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200426160251118.png)

我们通过 <item> 标签来定义 action 按钮， android:id 用于指定
按钮的id， android:icon 用于指定按钮的图标， android:title 用于指定按
钮的文字。
接着使用 app:showAsAction 来指定按钮的显示位置，之所以这里再次使
用了app命名空间，同样是为了能够兼容低版本的系统。 showAsAction 主
要有以下几种值可选：always表示永远显示在Toolbar中，如果屏幕空间不
够则不显示；ifRoom表示屏幕空间足够的情况下显示在Toolbar中，不够
的话就显示在菜单当中；never则表示永远显示在菜单当中。注意，
Toolbar中的action按钮只会显示图标，菜单中的action按钮只会显示文
字。

### MD

使用 app:layout_behavior 属性指定了一个布局行为。其
中 appbar_scrolling_view_behavior 这个字符串也是由Design Support库
提供的。
现在重新运行一下程序，

这里在Toolbar中添加了一个 app:layout_scrollFlags 属性，并将这个属
性的值指定成了 scroll|enterAlways|snap 。其中， scroll 表示当
RecyclerView向上滚动的时候，Toolbar会跟着一起向上滚动并实现隐
藏； enterAlways 表示当RecyclerView向下滚动的时候，Toolbar会跟着一
起向下滚动并重新显示。 snap 表示当Toolbar还没有完全隐藏或显示的时
候，会根据当前滚动的距离，自动选择是隐藏还是显示。