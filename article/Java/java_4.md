# 第4章 数组

## 4.1 数组的概念

### 4.1.1 容器概述

需求分析：

现在需要统计某公司员工的工资情况，例如计算平均工资、找到最高工资等。假设该公司有50名员工，用前面所学的知识，程序首先需要声明50个变量来分别记住每位员工的工资，然后在进行操作，这样做会显得很麻烦，而且错误率也会很高。因此我们可以使用容器进行操作。将所有的数据全部存储到一个容器中，统一操作。

容器概念：

- **生活中的容器：**水杯（装水等液体），衣柜（装衣服等物品），教室（装学生等人员）。
- **程序中的容器：**是将多个数据存储到一起，每个数据称为该容器的元素。

### 4.1.2 数组的概念

- **数组概念：** 数组就是用于存储数据的长度固定的容器，保证多个数据的数据类型要一致。

百度百科中对数组的定义：

所谓**数组**(array)，就是相同数据类型的元素按一定顺序排列的集合，就是把有限个类型相同的变量用一个名字命名，以便统一管理他们，然后用编号区分他们，这个名字称为**数组名**，编号称为**下标或索引**(index)。组成数组的各个变量称为数组的**元素**(element)。数组中元素的个数称为**数组的长度**(length)。



**数组的特点：**

1、数组的长度一旦确定就不能修改

2、创建数组时会在内存中开辟一整块连续的空间。

3、存取元素的速度快，因为可以通过[下标]，直接定位到任意一个元素。

### 4.1.3 数组的分类

1、按照维度分：

- 一维数组：存储一组数据
- 二维数组：存储多组数据，相当于二维表，一行代表一组数据，这是这里的二维表每一行长度不要求一样。



2、按照元素类型分：

- 基本数据类型的元素：存储数据值
- 引用数据类型的元素：存储对象（本质上存储对象的首地址）（这个在面向对象部分讲解）

注意：无论数组的元素是基本数据类型还是引用数据类型，数组本身都是引用数据类型。

## 4.2 一维数组的声明与使用

### 4.2.1 一维数组的声明

- 一维数组的声明/定义格式


```java
//推荐
元素的数据类型[] 二维数组的名称;

//不推荐
元素的数据类型  二维数组名[];
```

- 数组的声明，就是要确定：

（1）数组的维度：在Java中数组的标点符号是[]，[]表示一维，\[]\[]表示二维

（2）数组的元素类型：即创建的数组容器可以存储什么数据类型的数据。元素的类型可以是任意的Java的数据类型。例如：int, String, Student等

（3）数组名：就是代表某个数组的标识符，数组名其实也是变量名，按照变量的命名规范来命名。数组名是个引用数据类型的变量，因为它代表一组数据。

- 示例

```java
public class Test01ArrayDeclare {
    public static void main(String[] args) {
        //比如，要存储一个小组的成绩
        int[] scores;
        int grades[];
//        System.out.println(scores);//未初始化不能使用

        //比如，要存储一组字母
        char[] letters;

        //比如，要存储一组姓名
        String[] names;

        //比如，要存储一组价格
        double[] prices;

    }
}
```

### 4.2.2 一维数组的静态初始化

- 什么是初始化？
  - 初始化就是确定数组元素的总个数（即数组的长度）和元素的值

- 什么是静态初始化？
  - 静态初始化就是用静态数据（编译时已知）为数组初始化。此时数组的长度由静态数据的个数决定。

- **一维数组静态初始化格式1：**

```java
数据类型[] 数组名 = {元素1,元素2,元素3...};//必须在一个语句中完成，不能分开两个语句写
```

例如，定义存储1，2，3，4，5整数的数组容器

```java
int[] arr = {1,2,3,4,5};//正确

int[] arr;
arr = {1,2,3,4,5};//错误
```

- **一维数组静态初始化格式2：**

```java
数据类型[] 数组名 = new 数据类型[]{元素1,元素2,元素3...};
或
数据类型[] 数组名;
数组名 = new 数据类型[]{元素1,元素2,元素3...};
```

例如，定义存储1，2，3，4，5整数的数组容器。

```java
int[] arr = new int[]{1,2,3,4,5};//正确

int[] arr;
arr = new int[]{1,2,3,4,5};//正确
```

- 一维数组静态初始化演示

```java
public class Test02ArrayInitialize {
    public static void main(String[] args) {
        int[] arr = {1,2,3,4,5};//右边不需要写new int[]

        int[] nums;
        nums = new int[]{10,20,30,40}; //声明和初始化在两个语句完成，就不能使用new int[]

        char[] word = {'h','e','l','l','o'};

        String[] names = {"张三","李四","王五"};

        System.out.println("arr数组：" + arr);//arr数组：[I@1b6d3586
        System.out.println("nums数组：" + nums);//nums数组：[I@4554617c
        System.out.println("word数组：" + word);//word数组：[C@74a14482
        System.out.println("names数组：" + names);//names数组：[Ljava.lang.String;@1540e19d
    }
}
```

### 4.2.3 一维数组的使用

- 如何获取数组的元素总个数，即数组的长度


**数组的长度属性：** 每个数组都具有长度，而且是固定的，Java中赋予了数组的一个属性，可以获取到数组的长度，语句为：`数组名.length` ，属性length的执行结果是数组的长度，int类型结果。

```
数组名.length
```

- 如何表示数组中的一个元素？


每一个存储到数组的元素，都会自动的拥有一个编号，从0开始，这个自动编号称为**数组索引(index)或下标**，可以通过数组的索引/下标访问到数组中的元素。

```java
数组名[索引/下标]
```

- 数组的下标范围？

Java中数组的下标从[0]开始，下标范围是[0, 数组的长度-1]，即[0, 数组名.length-1]

- 一维数组的使用演示

```java
public class Test03ArrayUse {
    public static void main(String[] args) {
        int[] arr = {1,2,3,4,5};

        System.out.println("arr数组的长度：" + arr.length);
        System.out.println("arr数组的第1个元素：" + arr[0]);//下标从0开始
        System.out.println("arr数组的第2个元素：" + arr[1]);
        System.out.println("arr数组的第3个元素：" + arr[2]);
        System.out.println("arr数组的第4个元素：" + arr[3]);
        System.out.println("arr数组的第5个元素：" + arr[4]);

        //修改第1个元素的值
        //此处arr[0]相当于一个int类型的变量
        arr[0] = 100;
        System.out.println("arr数组的第1个元素：" + arr[0]);
    }
}
```

### 4.2.4 数组下标越界异常

当访问数组元素时，下标指定超出[0, 数组名.length-1]的范围时，就会报数组下标越界异常：ArrayIndexOutOfBoundsException。

```java
public class Test04ArrayIndexOutOfBoundsException {
    public static void main(String[] args) {
        int[] arr = {1,2,3};
       // System.out.println("最后一个元素：" + arr[3]);//错误，下标越界ArrayIndexOutOfBoundsException
      //  System.out.println("最后一个元素：" + arr[arr.length]);//错误，下标越界ArrayIndexOutOfBoundsException
        System.out.println("最后一个元素：" + arr[arr.length-1]);//对
    }
}

```

创建数组，赋值3个元素，数组的索引就是0，1，2，没有3索引，因此我们不能访问数组中不存在的索引，程序运行后，将会抛出 `ArrayIndexOutOfBoundsException`  数组越界异常。在开发中，数组的越界异常是**不能出现**的，一旦出现了，就必须要修改我们编写的代码。



### 4.2.4 一维数组的遍历

**数组遍历：** 就是将数组中的每个元素分别获取出来，就是遍历。遍历也是数组操作中的基石。for循环与数组的遍历是绝配。

```java
public class Test05ArrayIterate {
    public static void main(String[] args) {
        int[] arr = new int[]{1,2,3,4,5};
        //打印数组的属性，输出结果是5
        System.out.println("数组的长度：" + arr.length);

        //遍历输出数组中的元素
        System.out.println("数组的元素有：");
        for(int i=0; i<arr.length; i++){
            System.out.println(arr[i]);
        }
    }
}
```



### 4.2.5 一维数组动态初始化

- 什么是动态初始化？


动态初始化就是先确定元素的个数（即数组的长度），而元素此时只是默认值，并不是真正的数据。元素真正的数据需要后续单独一个一个赋值。

- **格式：**

```java
 数组存储的元素的数据类型[] 数组名字 = new 数组存储的元素的数据类型[长度];

  或

 数组存储的数据类型[] 数组名字;
 数组名字 = new 数组存储的数据类型[长度];
```

- new：关键字，创建数组使用的关键字。因为数组本身是引用数据类型，所以要用new创建数组对象。
- [长度]：数组的长度，表示数组容器中可以存储多少个元素。
- **注意：数组有定长特性，长度一旦指定，不可更改。**和水杯道理相同，买了一个2升的水杯，总容量就是2升是固定的。

例如，定义可以存储5个整数的数组容器，代码如下：

```java
int[] arr = new int[5];

int[] arr;
arr = new int[5];

int[] arr = new int[5]{1,2,3,4,5};//错误的，后面有{}指定元素列表，就不需要在[]中指定元素个数了。
```

- 一维数组的动态初始化演示


```java
public class Test06ArrayInitialize {
    public static void main(String[] args) {
        int[] arr = new int[5];

        System.out.println("arr数组的长度：" + arr.length);
        System.out.print("存储数据到arr数组之前：[");
        for (int i = 0; i < arr.length; i++) {
            if(i==0){
                System.out.print(arr[i]);
            }else{
                System.out.print("," + arr[i]);
            }
        }
        System.out.println("]");

        //初始化
 /*       arr[0] = 2;
        arr[1] = 4;
        arr[2] = 6;
        arr[3] = 8;
        arr[4] = 10;*/

        for (int i = 0; i < arr.length; i++) {
            arr[i] = (i+1) * 2;
        }

        System.out.print("存储数据到arr数组之后：[");
        for (int i = 0; i < arr.length; i++) {
            if(i==0){
                System.out.print(arr[i]);
            }else{
                System.out.print("," + arr[i]);
            }
        }
        System.out.println("]");
    }
}
```

### 4.2.6 数组元素的默认值

当我们使用动态初始化方式创建数组时，元素只是默认值。



```java
public class Test07ArrayElementDefaultValue {
    public static void main(String[] args) {
        //存储26个字母
        char[] letters = new char[26];
        System.out.println("letters数组的长度：" + letters.length);
        System.out.print("存储字母到letters数组之前：[");
        for (int i = 0; i < letters.length; i++) {
            if(i==0){
                System.out.print(letters[i]);
            }else{
                System.out.print("," + letters[i]);
            }
        }
        System.out.println("]");

       //存储5个姓名
        String[] names = new String[5];
        System.out.println("names数组的长度：" + names.length);
        System.out.print("存储姓名到names数组之前：[");
        for (int i = 0; i < names.length; i++) {
            if(i==0){
                System.out.print(names[i]);
            }else{
                System.out.print("," + names[i]);
            }
        }
        System.out.println("]");
    }
}
```



## 4.3 一维数组内存分析

### 4.3.1 内存概述

内存是计算机中重要的部件之一，它是与CPU进行沟通的桥梁。其作用是用于暂时存放CPU中的运算数据，以及与硬盘等外部存储器交换的数据。只要计算机在运行中，CPU就会把需要运算的数据调到内存中进行运算，当运算完成后CPU再将结果传送出来。我们编写的程序是存放在硬盘中的，在硬盘中的程序是不会运行的，必须放进内存中才能运行，运行完毕后会清空内存。

Java虚拟机要运行程序，必须要对内存进行空间的分配和管理。

### 4.3.2 Java虚拟机的内存划分

为了提高运算效率，就对空间进行了不同区域的划分，因为每一片区域都有特定的处理数据方式和内存管理方式。



| 区域名称   | 作用                                                         |
| ---------- | ------------------------------------------------------------ |
| 程序计数器 | 程序计数器是CPU中的寄存器，它包含每一个线程下一条要执行的指令的地址 |
| 本地方法栈 | 当程序中调用了native的本地方法时，本地方法执行期间的内存区域 |
| 方法区     | 存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。 |
| 堆内存     | 存储对象（包括数组对象），new来创建的，都存储在堆内存。      |
| 虚拟机栈   | 用于存储正在执行的每个Java方法的局部变量表等。局部变量表存放了编译期可知长度的各种基本数据类型、对象引用，方法执行完，自动释放。 |

### 4.4.3 一维数组在内存中的存储

#### 1、一个一维数组内存图

```java
public static void main(String[] args) {
  	int[] arr = new int[3];
  	System.out.println(arr);//[I@5f150435
}

```



> 思考：打印arr为什么是[I@5f150435，它是数组的地址吗？
>
> 答：它不是数组的地址。
>
> 问？不是说arr中存储的是数组对象的首地址吗？
>
> 答：arr中存储的是数组的首地址，但是因为数组是引用数据类型，打印arr时，会自动调用arr数组对象的toString()方法，该方法默认实现的是对象类型名@该对象的hashCode()值的十六进制值。
>
> 问？对象的hashCode值是否就是对象内存地址？
>
> 答：不一定，因为这个和不同品牌的JVM产品的具体实现有关。例如：Oracle的OpenJDK中给出了5种实现，其中有一种是直接返回对象的内存地址，但是OpenJDK默认没有选择这种方式。

#### 2、数组下标为什么是0开始

因为第一个元素距离数组首地址间隔0个单元格。

#### 3、两个一维数组内存图

两个数组独立

```java
public static void main(String[] args) {
    int[] arr = new int[3];
    int[] arr2 = new int[2];
    System.out.println(arr);
    System.out.println(arr2);
}

```



#### 4、两个变量指向一个一维数组

两个数组变量本质上代表同一个数组。

```java
public static void main(String[] args) {
    // 定义数组，存储3个元素
    int[] arr = new int[3];
    //数组索引进行赋值
    arr[0] = 5;
    arr[1] = 6;
    arr[2] = 7;
    //输出3个索引上的元素值
    System.out.println(arr[0]);
    System.out.println(arr[1]);
    System.out.println(arr[2]);
    //定义数组变量arr2，将arr的地址赋值给arr2
    int[] arr2 = arr;
    arr2[1] = 9;
    System.out.println(arr[1]);
}
```



## 4.4 一维数组的常见算法

### 4.4.1 数组统计：求总和、均值、统计偶数个数等

示例代码1：

```java
public class Test08ArrayElementSum {
    public static void main(String[] args) {
        int[] arr = {4,5,6,1,9};
        //求总和、均值
        int sum = 0;//因为0加上任何数都不影响结果
        for(int i=0; i<arr.length; i++){
            sum += arr[i];
        }
        double avg = (double)sum/arr.length;

        System.out.println("sum = " + sum);
        System.out.println("avg = " + avg);
    }
}
```

示例代码2：

```java
public class Test09ArrayElementMul {
    public static void main(String[] args) {
        int[] arr = {4,5,6,1,9};

        //求总乘积
        long result = 1;//因为1乘以任何数都不影响结果
        for(int i=0; i<arr.length; i++){
            result *= arr[i];
        }

        System.out.println("result = " + result);
    }
}
```

示例代码3：

```java
public class Test10ArrayElementEvenCount {
    public static void main(String[] args) {
        int[] arr = {4,5,6,1,9};
        //统计偶数个数
        int evenCount = 0;
        for(int i=0; i<arr.length; i++){
            if(arr[i]%2==0){
                evenCount++;
            }
        }

        System.out.println("evenCount = " + evenCount);
    }
}
```

### 4.4.2 数组找最值

#### 1、找最大值/最小值



思路：

（1）先假设第一个元素最大/最小

（2）然后用max/min与后面的元素一一比较

示例代码：

```java
public class Test11ArrayMax {
    public static void main(String[] args) {
        int[] arr = {4,5,6,1,9};
        //找最大值
        int max = arr[0];
        for(int i=1; i<arr.length; i++){//此处i从1开始，是max不需要与arr[0]再比较一次了
            if(arr[i] > max){
                max = arr[i];
            }
        }

        System.out.println("max = " + max);
    }
}
```

#### 2、找最值及其第一次出现的下标

思路：

（1）先假设第一个元素最大/最小

（2）用max/min变量表示最大/小值，用max/min与后面的元素一一比较

（3）用index时刻记录目前比对的最大/小的下标

示例代码：

```java
public class Test12MaxIndex {
    public static void main(String[] args) {
        int[] arr = {4,5,6,1,9};
        //找最大值以及第一个最大值下标
        int max = arr[0];
        int index = 0;
        for(int i=1; i<arr.length; i++){
            if(arr[i] > max){
                max = arr[i];
                index = i;
            }
        }

        System.out.println("max = " + max);
        System.out.println("index = " + index);
    }
}
```

或

思路：

（1）先假设第一个元素最大/最小

（2）用maxIndex时刻记录目前比对的最大/小的下标，那么arr[maxIndex]就是目前的最大值

```java
public class Test12MaxIndex2 {
    public static void main(String[] args) {
        int[] arr = {4,5,6,1,9};
        //找最大值
        int maxIndex = 0;
        for(int i=1; i<arr.length; i++){
            if(arr[i] > arr[maxIndex]){
                maxIndex = i;
            }
        }
        System.out.println("最大值：" + arr[maxIndex]);
    }
}
```

#### 3、找最值及其所有最值的下标（选讲）

有一种情况是元素是重复的，那么最大值就有多个。

思路：

（1）先找最大值

①假设第一个元素最大

②用max与后面的元素一一比较

（2）遍历数组，看哪些元素和最大值是一样的

示例代码：

```java
public class Test13AllMaxIndex {
    public static void main(String[] args) {
        int[] arr = {4,5,6,1,9,9,3};
        //找最大值
        int max = arr[0];
        for(int i=1; i<arr.length; i++){
            if(arr[i] > max){
                max = arr[i];
            }
        }
        System.out.println("最大值是：" + max);
        System.out.print("最大值的下标有：");

        //遍历数组，看哪些元素和最大值是一样的
        for(int i=0; i<arr.length; i++){
            if(max == arr[i]){
                System.out.print(i+"\t");
            }
        }
        System.out.println();
    }
}
```

优化

```java
public class Test13AllMaxIndex2 {
    public static void main(String[] args) {
        int[] arr = {4,5,6,1,9,9,3};
        //找最大值
        int max = arr[0];
        String index = "0";
        for(int i=1; i<arr.length; i++){
            if(arr[i] > max){
                max = arr[i];
                index = i + "";
            }else if(arr[i] == max){
                index += "," + i;
            }
        }

        System.out.println("最大值是" + max);
        System.out.println("最大值的下标是[" + index+"]");
    }
}
```



### 4.4.3  数组的元素查找

#### 1、顺序查找

顺序查找：挨个查看

要求：对数组元素的顺序没要求

顺序查找示例代码：

```java
public class Test14ArrayOrderSearch {
    //查找value第一次在数组中出现的index
    public static void main(String[] args){
        int[] arr = {4,5,6,1,9};
        int value = 1;
        int index = -1;

        for(int i=0; i<arr.length; i++){
            if(arr[i] == value){
                index = i;
                break;
            }
        }

        if(index==-1){
            System.out.println(value + "不存在");
        }else{
            System.out.println(value + "的下标是" + index);
        }
    }
}
```

#### 2、二分查找

```java
import java.util.Scanner;

public class Test15ArrayBinarySearch {
    public static void main(String[] args){
        //数组一定是有序的
        int[] arr = {8,15,23,35,45,56,75,85};

        Scanner input = new Scanner(System.in);
        System.out.print("请输入你要查找的值：");
        int target = input.nextInt();

        int index = -1;
        for(int left = 0,right = arr.length-1; left<=right; ){
            //int mid = (left+right)/2;
            int mid = left + (right-left)/2;

            if(arr[mid] == target){
                index = mid;
                break;
            }else if(target > arr[mid]){
                //说明target在[mid]右边
                left = mid+1;
            }else{
                //说明target<arr[mid]，target在[mid]左边
                right= mid-1;
            }
        }
        if(index!=-1){
            System.out.println("找到了，下标是"+index);
        }else{
            System.out.println("不存在");
        }

    }
}
```







### 4.4.5 数组元素的反转

**实现思想：**数组对称位置的元素互换。



```java
    public class Test17ArrayReverse {
    public static void main(String[] args) {
        int[] arr = {1,2,3,4,5};
        System.out.println("反转之前：");
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }

        //反转
         /*
        思路：首尾对应位置的元素交换
        （1）确定交换几次
           次数 = 数组.length / 2
        （2）谁和谁交换
        for(int i=0; i<次数; i++){
             int temp = arr[i];
             arr[i] = arr[arr.length-1-i];
             arr[arr.length-1-i] = temp;
        }
         */
        for(int i=0; i<arr.length/2; i++){
            int temp = arr[i];
            arr[i] = arr[arr.length-1-i];
            arr[arr.length-1-i] = temp;
        }

        System.out.println("反转之后：");
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }

}
```

或



```java
public class Test17ArrayReverse2 {
    public static void main(String[] args) {
        int[] arr = {1,2,3,4,5};
        System.out.println("反转之前：");
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }

        //反转
        //左右对称位置交换
        for(int left=0,right=arr.length-1; left<right; left++,right--){
            //首  与  尾交换
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
        }

        System.out.println("反转之后：");
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }
}
```



### 4.4.6 数组元素排序

#### 1、排序算法概述

数组的排序算法很多，实现方式各不相同，时间复杂度、空间复杂度、稳定性也各不相同：



- 时间复杂度：

常见的算法时间复杂度由小到大依次为：Ο(1)＜Ο(log2n)＜Ο(n)＜Ο(nlog2n)＜Ο(n<sup>2</sup>)＜Ο(n<sup>3</sup>)＜…＜Ο(2<sup>n</sup>)＜Ο(n!)

	一个算法执行所耗费的时间，从理论上是不能算出来的，必须上机运行测试才能知道。但我们不可能也没有必要对每个算法都上机测试，只需知道哪个算法花费的时间多，哪个算法花费的时间少就可以了。并且一个算法花费的时间与算法中语句的执行次数成正比例，哪个算法中语句执行次数多，它花费时间就多。一个算法中的语句执行次数称为语句频度或时间频度。记为T(n)。n称为问题的规模，当n不断变化时，时间频度T(n)也会不断变化。但有时我们想知道它变化时呈现什么规律。为此，我们引入时间复杂度概念。 一般情况下，算法中基本操作重复执行的次数是问题规模n的某个函数，用T(n)表示，若有某个辅助函数f(n),使得当n趋近于无穷大时，T(n)/f(n)的极限值为不等于零的常数，则称f(n)是T(n)的同数量级函数。记作T(n)=Ｏ(f(n)),称Ｏ(f(n)) 为算法的渐进时间复杂度，简称时间复杂度。

- 空间复杂度：

```
类似于时间复杂度的讨论，一个算法的空间复杂度(Space Complexity)S(n)定义为该算法所耗费的存储空间，它也是问题规模n的函数。
```

- 稳定性：

```
排序一定会设计到数组元素位置的交换。如果两个元素相等，无论它们原来是否相邻，在排序过程中，最后它们变的相邻，但是它们前后顺序并没有改变，就称为稳定的，否则就是不稳定的。
```



#### 2、直接选择排序

```java
/*
1、直接选择排序

思想：每一轮找出本轮的最大值/最小值，然后看它是否在它应该在的位置。
      如果不在正确的位置，就与这个位置的元素交换。

过程：arr{6,9,2,9,1}  目标：从小到大
第1轮：最大值是9，它现在在arr[1]，它应该在arr[4]，不对，交换arr[1]和arr[4]，{6,1,2,9,9}
第2轮：最大值是9，它现在在arr[3]，它应该在arr[3]，对，不动
第3轮：最大值是6，它现在在arr[0]，它应该在arr[2]，不对，交换arr[0]和arr[2]，{2,1,6,9,9}
第4轮：最大值是2，它现在在arr[0]，它应该在arr[1]，不对，交换arr[0]和arr[1]，{1,2,6,9,9}

过程：arr{6,9,2,9,1}  目标：从小到大
第1轮：最小值是1，它现在在arr[4]，它应该在arr[0]，不对，交换arr[4]和arr[0]，{1,9,2,9,6}
第2轮：最小值是2，它现在在arr[2]，它应该在arr[1]，不对，交换arr[2]和arr[1]，{1,2,9,9,6}
第3轮：最小值是6，它现在在arr[4]，它应该在arr[2]，不对，交换arr[4]和arr[2]，{1,2,6,9,9}
第4轮：最小值是7，它现在在arr[3]，它应该在arr[3]，对，不动

*/
public class Test18SelectSort{
    public static void main(String[] args){
        int[] arr = {6,9,2,9,1};

        //直接选择排序，轮数 = 数组的元素总个数-1
		/*
		arr.length=5
		i=0
		i=1
		i=2
		i=3
		*/
        for(int i=0; i<arr.length-1; i++){
            //找出本轮的最小值，及其下标
			/*
			i=0，第1轮，查找的范围是[0,4]，一开始假设arr[0]最小
			i=1，第2轮，查找的范围是[1,4]，一开始假设arr[1]最小
			i=2，第3轮，查找的范围是[2,4]，一开始假设arr[2]最小
			i=3，第4轮，查找的范围是[3,4]，一开始假设arr[3]最小
			int min = arr[i];
			*/
            int min = arr[i];
            int index = i;
            //用[i+1,  arr.length-1]范围的元素与min比较
            for(int j=i+1; j<arr.length; j++){
                if(arr[j] < min){
                    min = arr[j];
                    index = j;
                }
            }

            //判断min是否在它应该在的位置
			/*
			i=0，第1轮，最小值应该在arr[0]位置，它现在在arr[index]位置
			i=1，第2轮，最小值应该在arr[1]位置，它现在在arr[index]位置
			i=2，第3轮，最小值应该在arr[2]位置，它现在在arr[index]位置
			i=3，第4轮，最小值应该在arr[3]位置，它现在在arr[index]位置
			
			最小值应该在arr[i]位置,	如果index!=i，说明它不在应该在的位置，
			就交换arr[i]和arr[index]位置
			*/
            if(index!=i){
                int temp = arr[i];
                arr[i] = arr[index];
                arr[index] = temp;
            }

        }

        //完成排序，遍历结果
        for(int i=0; i<arr.length; i++){
            System.out.print(arr[i]+"  ");
        }

    }
}
```

#### 3、冒泡排序

Java中的经典算法之冒泡排序（Bubble Sort）

原理：比较两个相邻的元素，将值大的元素交换至右端。

思路：依次比较相邻的两个数，将小数放到前面，大数放到后面。

​	即第一趟，首先比较第1个和第2个元素，将小数放到前面，大数放到后面。

​			然后比较第2个和第3个元素，将小数放到前面，大数放到后面。

​			如此继续，直到比较最后两个数，将小数放到前面，大数放到后面。

​	重复第一趟步骤，直至全部排序完成。

```java
/*
1、冒泡排序（最经典）
思想：每一次比较“相邻（位置相邻）”元素，如果它们不符合目标顺序（例如：从小到大），
     就交换它们，经过多轮比较，最终实现排序。
	 （例如：从小到大）	 每一轮可以把最大的沉底，或最小的冒顶。
	 
过程：arr{6,9,2,9,1}  目标：从小到大

第一轮：
	第1次，arr[0]与arr[1]，6>9不成立，满足目标要求，不交换
	第2次，arr[1]与arr[2]，9>2成立，不满足目标要求，交换arr[1]与arr[2] {6,2,9,9,1}
	第3次，arr[2]与arr[3]，9>9不成立，满足目标要求，不交换
	第4次，arr[3]与arr[4]，9>1成立，不满足目标要求，交换arr[3]与arr[4] {6,2,9,1,9}
	第一轮所有元素{6,9,2,9,1}已经都参与了比较，结束。
	第一轮的结果：第“一”最大值9沉底（本次是后面的9沉底），即到{6,2,9,1,9}元素的最右边

第二轮：
	第1次，arr[0]与arr[1]，6>2成立，不满足目标要求，交换arr[0]与arr[1] {2,6,9,1,9}
	第2次，arr[1]与arr[2]，6>9不成立，满足目标要求，不交换
	第3次：arr[2]与arr[3]，9>1成立，不满足目标要求，交换arr[2]与arr[3] {2,6,1,9,9}
	第二轮未排序的所有元素 {6,2,9,1}已经都参与了比较，结束。
	第二轮的结果：第“二”最大值9沉底（本次是前面的9沉底），即到{2,6,1,9}元素的最右边
第三轮：
	第1次，arr[0]与arr[1]，2>6不成立，满足目标要求，不交换
	第2次，arr[1]与arr[2]，6>1成立，不满足目标要求，交换arr[1]与arr[2] {2,1,6,9,9}
	第三轮未排序的所有元素{2,6,1}已经都参与了比较，结束。
	第三轮的结果：第三最大值6沉底，即到 {2,1,6}元素的最右边
第四轮：
	第1次，arr[0]与arr[1]，2>1成立，不满足目标要求，交换arr[0]与arr[1] {1,2,6,9,9}
	第四轮未排序的所有元素{2,1}已经都参与了比较，结束。
	第四轮的结果：第四最大值2沉底，即到{1,2}元素的最右边

*/
public class Test19BubbleSort{
    public static void main(String[] args){
        int[] arr = {6,9,2,9,1};

        //目标：从小到大
        //冒泡排序的轮数 = 元素的总个数 - 1
        //轮数是多轮，每一轮比较的次数是多次，需要用到双重循环，即循环嵌套
        //外循环控制 轮数，内循环控制每一轮的比较次数和过程
        for(int i=1; i<arr.length; i++){ //循环次数是arr.length-1次/轮
			/*
			假设arr.length=5
			i=1,第1轮，比较4次
				arr[0]与arr[1]
				arr[1]与arr[2]
				arr[2]与arr[3]
				arr[3]与arr[4]
				
				arr[j]与arr[j+1]，int j=0;j<4; j++
				
			i=2,第2轮，比较3次
				arr[0]与arr[1]
				arr[1]与arr[2]
				arr[2]与arr[3]
				
				arr[j]与arr[j+1]，int j=0;j<3; j++
				
			i=3,第3轮，比较2次
				arr[0]与arr[1]
				arr[1]与arr[2]
				
				arr[j]与arr[j+1]，int j=0;j<2; j++
			i=4,第4轮，比较1次
				arr[0]与arr[1]
			
				arr[j]与arr[j+1]，int j=0;j<1; j++
				
				int j=0; j<arr.length-i; j++
			*/
            for(int j=0; j<arr.length-i; j++){
                //希望的是arr[j] < arr[j+1]
                if(arr[j] > arr[j+1]){
                    //交换arr[j]与arr[j+1]
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }

        //完成排序，遍历结果
        for(int i=0; i<arr.length; i++){
            System.out.print(arr[i]+"  ");
        }
    }
}
```

#### 4、冒泡排序优化（选讲）

```java
/*
思考：冒泡排序是否可以优化
*/
class Test19BubbleSort2{
	public static void main(String[] args){
		int[] arr = {1,3,5,7,9};
		
		//从小到大排序
		//int lun = 0;//声明lun变量，统计比较几轮
		//int count = 0;//声明count变量，统计比较的次数
		for(int i=1; i<arr.length; i++){ 
			//lun++;
			boolean flag = true;//假设数组已经是有序的
			for(int j=0; j<arr.length-i; j++){
				//count++;
				//希望的是arr[j] < arr[j+1]
				if(arr[j] > arr[j+1]){
					//交换arr[j]与arr[j+1]
					int temp = arr[j];
					arr[j] = arr[j+1];
					arr[j+1] = temp;
					
					flag = false;//如果元素发生了交换，那么说明数组还没有排好序
				}
			}
			if(flag){
				break;
			}
		}
		
		//System.out.println("一共比较了" + lun +"轮");
		//System.out.println("一共比较了" + count +"次");
		
		//完成排序，遍历结果
		for(int i=0; i<arr.length; i++){
			System.out.print(arr[i]+"  ");
		}
	}
}
```

