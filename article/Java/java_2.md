# 第2章 Java基础语法

## 2.1 注释（*annotation*）（掌握）

- **注释**：就是对代码的解释和说明。其目的是让人们能够更加轻松地了解代码。为代码添加注释，是十分必须要的，它不影响程序的编译和运行。

- Java中有`单行注释`、`多行注释`和`文档注释`

  - 单行注释以 `//`开头，以`换行`结束，格式如下：

    ```java
    // 注释内容
    ```

  - 多行注释以 `/*`开头，以`*/`结束，格式如下：

    ```java
    /*
    	注释内容
     */
    ```

  - 文档注释以`/**`开头，以`*/`结束，Java特有的注释，结合 

    ```java
    /**
    	注释内容
     */
    ```

```java
//单行注释
/*
多行注释
*/
/**
文档注释演示
@author chai
*/
public class Comments{
    
	/**
	Java程序的入口
	@param String[] args main方法的命令参数
	*/
    public static void main(String[] args){
        System.out.println("hello");
    }
}
```

常见的几个注释：

- @author 标明开发该类模块的作者，多个作者之间使用,分割

* @version 标明该类模块的版本

* @see 参考转向，也就是相关主题

* @since 从哪个版本开始增加的

* @param 对方法中某参数的说明，如果没有参数就不能写（后面再学）

* @return 对方法返回值的说明，如果方法的返回值类型是void就不能写（后面再学）

* @throws/@exception 对方法可能抛出的异常进行说明 ，如果方法没有用throws显式抛出的异常就不能写（后面再学）

其中 @param  @return 和 @exception 这三个标记都是只用于方法的。

  * @param的格式要求：@param 形参名 形参类型  形参说明
  * @return 的格式要求：@return 返回值类型 返回值说明
  * @exception 的格式要求：@exception 异常类型 异常说明
  * @param和@exception可以并列多个

使用javadoc工具可以基于文档注释生成API文档。

```cmd
用法: javadoc [options] [packagenames] [sourcefiles] [@files]
```

例如：

```java
javadoc -author -d doc Comments.java
```

![image-20211226163731907](尚硅谷-JavaSE课堂笔记.assets/image-20211226163731907.png)

![image-20211226163802649](尚硅谷-JavaSE课堂笔记.assets/image-20211226163802649.png)

![image-20211226163949641](尚硅谷-JavaSE课堂笔记.assets/image-20211226163949641.png)

## 2.2 关键字（*keyword*）（掌握）

**关键字**：是指在程序中，Java已经定义好的单词，具有特殊含义。

- HelloWorld案例中，出现的关键字有 `public ` 、`class` 、 `static` 、  `void`  等，这些单词已经被Java定义好
- 关键字的特点：全部都是`小写字母`。
- 关键字比较多，不需要死记硬背，学到哪里记到哪里即可。

![1555209180504](尚硅谷-JavaSE课堂笔记.assets/关键字表.png)

>  **关键字一共50个，其中const和goto是保留字。**

> **true,false,null看起来像关键字，但从技术角度，它们是特殊的布尔值和空值。**



## 2.3 标识符( identifier)（掌握）

简单的说，凡是程序员自己命名的部分都可以称为标识符。

即给类、变量、方法、包等命名的字符序列，称为标识符。



1、标识符的命名规则（必须遵守的硬性规则）

（1）Java的标识符只能使用26个英文字母大小写，0-9的数字，下划线_，美元符号$

（2）不能使用Java的关键字（包含保留字）和特殊值

（3）数字不能开头

（4）不能包含空格

（5）严格区分大小写



2、标识符的命名规范（建议遵守的软性规则，否则容易被鄙视和淘汰）

（1）见名知意

（2）类名、接口名等：每个单词的首字母都大写，形式：XxxYyyZzz，

例如：HelloWorld，String，System等

（3）变量、方法名等：从第二个单词开始首字母大写，其余字母小写，形式：xxxYyyZzz，

例如：age,name,bookName,main

（4）包名等：每一个单词都小写，单词之间使用点.分割，形式：xxx.yyy.zzz，

例如：java.lang

（5）常量名等：每一个单词都大写，单词之间使用下划线_分割，形式：XXX_YYY_ZZZ，

例如：MAX_VALUE,PI



更多细节详见《代码整洁之道.pdf》《Java开发手册（泰山版）》