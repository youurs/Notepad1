# NotePad
This is an AndroidStudio rebuild of google SDK sample NotePad

新建笔记：

![image](https://github.com/youurs/Notepad1/blob/master/Photo/Snipaste_2021-05-24_15-08-26.jpg)

创建成功（带有时间戳）：

![image](https://github.com/youurs/Notepad1/blob/master/Photo/Snipaste_2021-05-24_15-09-17.jpg)

删除q1313笔记:

![image](https://github.com/youurs/Notepad1/blob/master/Photo/Snipaste_2021-05-24_15-09-40.jpg)

在笔记本列表中添加时间戳的步骤：

第一步、找到NotesList中的添加视图的语句

![image](https://user-images.githubusercontent.com/62132538/119312565-1ac9f180-bca5-11eb-9bc9-66296d7fd316.png)
前面我们学过，SimpleCursoraAdapter是用来创建ListView的方法之一，这里可以看到dataColumns和viewIDs，分别是数据和视图id。

那么我们第一步：

在视图中添加一个文本框：

在原有的基础上添加一个垂直的线性布局，和一个文本视图，如图所示：
![image](https://user-images.githubusercontent.com/62132538/119312602-26b5b380-bca5-11eb-991e-475542d751b0.png)

将上上图中的java代码行的语句里添加成如图所示：
![image](https://user-images.githubusercontent.com/62132538/119312618-2c12fe00-bca5-11eb-8ac2-2b150ab0a3ce.png)

由于代码是别人的，这个逻辑写出来出错如图：
![image](https://user-images.githubusercontent.com/62132538/119312646-33d2a280-bca5-11eb-8a56-f8f4573d2fdd.png)

查了别人的逻辑之后，在Notelist类中的字符串数组中添加语句如图：
![image](https://user-images.githubusercontent.com/62132538/119312670-39c88380-bca5-11eb-8381-ee2cbbfb35ca.png)


我们现在得到的运行结果是这样的：
![image](https://user-images.githubusercontent.com/62132538/119312692-40ef9180-bca5-11eb-9363-7fcd0cd3b133.png)

有一串数字，对应的是修改时间，你修改一下标签它就会改变。那么这个值在哪里？它又怎么改写成时间格式呢？
![image](https://user-images.githubusercontent.com/62132538/119312708-464cdc00-bca5-11eb-8e0a-e9ae1bbd6bf3.png)

我们第一个思路是在NotesList类里面直接修改

  NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE

的值，将时间赋给它，但是不行，传入
这个构造方法的时候类型错误，尝试修改前面的数组直接加入时间，也不行，于是还是参考别人的逻辑，在编辑保存返回值的时候再改变

  NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE

的值，即在NoteEditor中做如下修改：

  ContentValues values = new ContentValues();
  SimpleDateFormat sf = new SimpleDateFormat("yy/MM/dd HH:mm:ss");
  values.put(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE,sf.format(new Date()));

于是时间戳功能得以实现（成果如图）：
![image](https://github.com/youurs/Notepad1/blob/master/Photo/Snipaste_2021-05-24_15-09-17.jpg)




