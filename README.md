# 标题栏部分*(TheTitleAndMenu)*说明文档

$$
*kanyooooo*
$$

*于3/15/2022修改完成*
*工程与说明文档同名*


### 〇、说明解释

**每一篇说明文档都会讲的事：**

众所周知AndroidStudio是一个垃圾软件，迫害可怜的Android开发者和可怜的物联网学习人员因为各种奇葩的，不知道从哪里出来的bug而头疼。不过当你开始准备学习AndroidStudio的时候，我相信你一定已经准备好了面对各种各样奇怪的，可能出现的bug了。当然，有幸的是这个软件几乎不会出什么bug，主要还是编程人员(也就是你)可能会用出问题来，不过如果真的出现了某些怎么解决也解决不了的问题，为何不试一试直接重新创一个工程项目然后试一试呢？

### 一、 标题栏左上角: 返回按钮

有些脑瘫的题目会要求我们在左上角搞一个返回按钮，这简直就和弱智一样，我android自带的返回键tnnd不能用嘛？

算了，我们这些做题目的爹总是要宽容那些出题员的，那只能大发慈悲的做一个吧。

首先我们需要用到一个叫做ActionBar的类，那么第一步当然还是创建对象：

```java
ActionBar
actionBar = getSupportActionBar();
```

然后，我们先要让左上角的按钮出现，并且设置可以被点击的属性：

```java
actionBar.setDisplayHomeAsUpEnabled(true);
//给左上角图标的左边加上一个返回的图标  

actionBar.setHomeButtonEnabled(true);
//设置左上角的图标是否可以点击
```

好，恭喜你，现在拥有了一个没有任何功能的按钮！

然后我们需要给他设置一个被点击就关掉的事件吧！

哈哈，其实人家自带了一个叫做onOptionsItemSelected()的函数，但是这个函数本身啥用也没有，他只是嵌在了你对其中某个控件点击之后，执行此函数罢了。所以我们需要通过重写本函数的方式，让这个函数有用，以我们认为有用的方式有用。比如这里，就是要给这个返回的ImageButton编写一个点击事件。利用onOptionsItemSelected写出来的是这样的：

```java
public boolean onOptionsItemSelected(MenuItem item){
    switch (item.getItemId()){
        case android.R.id.*home*:   //返回键的id
            this.finish();  
        default:
            break;
    }    
    return true;  
}
```

这里唯一需要注意的就是android.R.id.*home:*了，这个home id是自带的，也就是说我们不需要去写任何xml来定义这个id叫做home的控件长什么样子。这里的this.finish();就是结束本活动的意思。如果你是在第一个activity里面使用这个函数的话，那么本程序会直接结束掉。而结束掉之后打开的界面时，用这个函数只是关掉了后来打开的界面，而不是关掉这个程序。这个逻辑应该很好理解。

### 二、 标题栏右上角: 菜单按钮

说实话，这个菜单按钮比上面的那个玩意有用多了，让我写我自然而然还是算比较乐意的。

写这个前，现需要准备一个xml文件。

如图所示，先需要在res中创建一个Android Resource Directory来储存我们的xml文件，配置文件夹如图所示：

Resource type必须选为menu类型。随后在创建完的文件夹内再创建一个xml文件，默认情况是直接创建一个menu类型的xml文件。我在这里默认起名为menu：

在里面设置一个控件item，设置他的id属性和标题属性，代码如下:

<?xml version="1.0" encoding="utf-8"?>

```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android">  
  <item android:id="@+id/setting" android:title="setting"></item>  
</menu>
```





这样，这个控件的id就叫做setting，他的字会显示为setting（通过title属性显示）。

这里的控件越多，弹出的窗口可选选项就越多。

回到主函数，重写onCreateOptionsMenu()方法

```java
public boolean onCreateOptionsMenu(Menu menu){  
    getMenuInflater().inflate(R.menu.*menu*,menu);  
    return true;  
}
```

此刻，运行我们的程序，右上角就会出现三个点：

点击这三个点，就可以看到我们之前设置标题和id都为setting的控件了：

              在此之后，我们需要用在上一部分学到的方法，让我们的手碰到这个控件的时候，进行操作。

```java
public boolean onOptionsItemSelected(MenuItem item){
    switch (item.getItemId()){
        case android.R.id.*setting*:   //返回键的id  
            //你所要执行的部分 可以不加break
        default:
            break;    
    }
    return true;  
}
```

              至此，有关标题栏部分的内容就结束了。
