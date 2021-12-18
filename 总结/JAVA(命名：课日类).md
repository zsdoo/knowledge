

### IDEA

原始练习位置：D:\Users\86132\IdeaProjects

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031152338635.png" alt="image-20211031152338635" style="zoom:50%;" />



<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031152742723.png" alt="image-20211031152742723" style="zoom:50%;" />

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031153225806.png" alt="image-20211031153225806" style="zoom:50%;" />

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031153357983-16367083193791.png" alt="image-20211031153357983" style="zoom: 67%;" />

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031153540305.png" alt="image-20211031153540305" style="zoom: 67%;" />

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031153643622.png" alt="image-20211031153643622" style="zoom: 67%;" />



<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031154455669.png" alt="image-20211031154455669" style="zoom: 67%;" />

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031154556931.png" alt="image-20211031154556931" style="zoom:50%;" />



<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031155055874.png" alt="image-20211031155055874" style="zoom:50%;" />

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031155402095.png" alt="image-20211031155402095" style="zoom:50%;" />

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031155445346.png" alt="image-20211031155445346" style="zoom:50%;" />

运行：| 显示或隐藏结果：ALT+4 

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031155712143.png" alt="image-20211031155712143" style="zoom: 33%;" />

![image-20211031161024385](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031161024385.png)

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031161821420.png" alt="image-20211031161821420" style="zoom: 33%;" />

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031162114318.png" alt="image-20211031162114318" style="zoom: 67%;" />

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031163336911.png" alt="image-20211031163336911" style="zoom:50%;" />

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031164344508.png" alt="image-20211031164344508" style="zoom: 33%;" />





### Day01-16-17    0315 19:03 常量的概念

常量：在程序运行期间，固定不变的量。
常量的分类：
1 字符串常量：凡是用双引号引起来的部分，叫做字符串常量。例如：“abc” "Hello"  "123"
2 整数常量：直接写上的数字，没有小数点。例如：100、200、0、-250
3 浮点数常量：直接写上的数字，有小数点。例如：2.5  -3.14  0.0
4 字符常量：凡是用单引号引起来的单个字符，叫做字符常量。例如：'A', 'b', '9','中'  //只有一个字符
5 布尔常量：只有两种取值。true   false
6 空常量：null   代表没有任何数据 

打印：
public class Demo01Const {
public static void main(String[] args) {

//字符串常
System.out.println("ABC");
System.out.println(""); //字符串两个引号中间为空
System.out.println("XYZ");

//整数常量
System.out.println(30);
System.out.println(-500);

//浮点数常量（小数）
System.out.println(3.14);
System.out.println(-2.5);

//字符常量
System.out.println('A'); //两个单引号中间有且仅有一个字符，没有不行
System.out.println('0'); //    有两个也不行
//布尔常量
System.out.println(true);
System.out.println(false);
//空常量，空常量不能直接用来打印输出
System.out.println(null);
}

Day01-18    0315 20:50

基本数据类型【今天重点】
	整数型	byte  short int long
	浮点型	float double
	字符型	char
	布尔型	boolean
引用数据类型（今后学习）
	字符串、数组、类、接口、Lambda

注意事项：
1 字符串不是基本类型，而是引用类型。
2 浮点型可能只是一个近似值 ，并非精确的值 
3 数据范围与字节数不一定相关，例如float数据范围比long更加广泛，但是float是4字节，long是8字节。
4 浮点数当中默认类型是double。如果一定要使用float类型，需要加上一个后缀F。
如果是整数，默认为int类型，如果一定要使用long类型，需要加上一个后缀L。推荐使用大写字母后缀。
// System.out.println(100L); 	//long类型

### Day01-19    0315 20:55 变量

/*
变量：程序运行期间，内容可以发生改变的量
创建一个变量并且使用的格式：
数据类型 变量名称； //创建了一个变量
变量名称 = 数据值 ；//赋值，将右边的数据值 ，赋值交给左边的变量
一步到位的格式：
数据类型 变量名称 = 数据值；//在创建一个变量的同时，立刻放入指定的数据值 

### Day01-21    0315 22:11

/*
使用变量的时候，注意事项：
1 如果创建多个变量，变量的名称不可以重复。
2 对于float和long类型来说，字母后缀F和L不要丢掉。
3 如果使用byte 或short 类型的变量，那么右侧的数据值不能超过左侧的类型范围。
4  没有进行赋值的变量不能直接使用；一定要赋值之后才能使用。
5 变量的使用不能超过作用域的范围。
【作用域】：从定义变量的一行开始，一直到直接所属的大括号结束为止。
6 可以通过一个语句来创建多个变量，但是一般情况不推荐这么写。



```java
public class Demo03VariableNotice {
	public static void main(String[ ] args) {
	int num1 = 10; //创建了一个新的变量，名叫num1
// int num1 = 20; //又创建了一个新的变量，名叫num1，错误！

	int num4;//

//	System.out.println(num4);//没有赋值，错误！

//	System.out.println(num5);//在变量之前，不能使用，错误！
	int num5=500;

int num6=60;
System.out.println(num6); //60

System.out.println(num6); //错误！超出了作用域


int a = 10;
int b = 20;
int c = 30;

//同时创建了三个全都是int类型的变量
int a,b,c;
//各自分别赋值
a=10;
b=20;
c=30;

//同时创建三个int变量，并且同时各自赋值
int x=100, y=200, z=300;
System.out.println(x); //100
System.out.println(y); //200
System.out.println(z); //300
}
```


### Day02-1    0315 22:26  自动类型转换

/*
当数据类型不一样时，将会发生数据类型转移。

自动类型转换（隐式）
1 特点：代码不需要特殊处理，自动完成。
2 规则：数据范围从小到大。
强制类型转换（显式）
*/
public class Demo01DataType {
	public static void main(String[] args){
		System.out.println(1024);//这就是一个整数，默认是int类型
		System.out.println(3.14);//这就是一个浮点数，默认是double类型
		
		//左边是long类型，右边默认是int类型，左右不一样
		//一个等号代表赋值，将右侧的int常量，交给左侧的long变量进行存储
		//int --> long，符合了数据范围从小到大的要求
		//这一行代码发生了自动类型转换
		long num1 = 100;
		System.out.println(num1);//100
		
		//左double, 右float,左右不一样
		//float-->double,符合了数据范围从小到大的规则 
		//也发生了自动类型转换
		double num2 = 2.5F;
		System.out.println(num2);//2.5


​		
​		//左边是float类型，右边是long类型，左右不一样
​		//long --> float，范围是float更大一些，符合从小到大的规则 
​		//也发生了自动类型转换
​		float num3 = 30L;
​		System.out.println(num3); // 30.0
​	}
}

### Day02-1    0315 22:46  强制类型转换

/*
强制类型转换
1 特点：代码需要进行特殊的格式处理，不能自动完成。
2 格式：范围小的类型 范围小的变量名 = （范围小的类型） 原本范围大的数据;

注意事项：
1 强制类型转换一般不推荐使用，因为有可能 发生精度损失（小数）、数据溢出（长度）。
2 byte/short/char这三种类型都可以发生数学运算，例如加法 “+”
3 byte/short/char这三种类型在运算的时候，都会被首先提升为int类型，然后再计算。
*/	

### Day02-12-14 0315 23:35 方法

/*
定义：就是将一个功能抽取出来，把代码单独定义在一个大括号内，形成一个单独的功能。
当我们需要这个功能的时候，就可以去调用。这样即实现了代码的复用性，也解决了代码冗余现象。

定义一个方法的格式：
public static void 方法名称(){
	方法体；
}

方法名称的命名规则和变量一样，使用小驼峰。（第一个字母小写，从第二个单词开始每个单词的首字母大写）
方法体：也就是大括号当中可以包含任意条语句

注意事项：
1 方法定义的先后顺序无所谓。
2 方法的定义不能产生嵌套包含关系。
3 方法定义好了之后，不会执行。如果要想执行，一定要进行方法的【调用】 

如何调用方法，格式：
方法名称( );
*/

```java
public class Demo11Method {
public static void main(String[] args){
	famer(); //农民伯伯的方法调用
	cook(); //厨师的调用
	me(); 调用我的方法
}
//农民
public static void famer(){
	System.out.println("播种");
	System.out.println("灌水");
	System.out.println("施肥");
	System.out.println("收获");
}
//厨师
public static void cook(){
	System.out.println("洗菜");
	System.out.println("切菜");
	System.out.println("炒菜");
}
//我
public static void me(){
	System.out.println("吃");
}

}
```



### Day03-1-2   0316 00:03 流程

```java
1 顺序结构 ：按顺序执行
2.1 判断语句：if
格式：
if (关系表达式）{
	语句体；
}

2.2 if...else
if (关系表达式）{
	语句体1；
} else {
	语句体2；
}

2.3 if...else if  ...else
if (判断条件1）{
	执行语句1；
} else if ( 判断条件2) {
	执行语句2；
}
...
} else if (判断条件n){
	执行语句n；
} else {
	执行语句n+1;
}
```



Day03-3-6  0405 20: 33

### Day03-7/8  0405 21: 20 switch

格式：
switch(表达式){
	case 常量值1 :
	  语句体1;
	  break;
	case 常量值2 :
	  语句体2;
	  break;
	……
	default :
	  语句体N+1;
	  break;
}

/*
switch语句使用的注意事项：
1 多个case后面的数值不可以重复。
2 switch 后面小括号当中只能是下列数据类型：
基本数据类型：byte/short/char/int
引用数据类型：String字符串、enum枚举
3 switch 语句格式可以很灵活：前后顺序可以颠倒，而且break语句还可以活略。
“匹配哪一个case就从哪一个位置向下执行，直到遇到了break或者整体结束为止”
 */

### Day03-9/10  0405 22:00  for 循环语句

/*循环四部分：
 * 1初始化语句：只做一次，而且只做唯一一次。
 * 2 条件判断：如果成立则继续;不成立，则退出循环。
 * 3 循环体：重复做的事情内容
 * 4 步进语句：每次循环之后都要进行的扫尾工作。

for 循环语句格式：
for (初始化表达式1； 布尔表达式2； 步进表达式4）{
	循环体3
}

### Day03-11/12/13/14  0405 22:42   while 循环语句

/*
while 循环有一个标准格式，还有一个扩展格式。
标准格式：
while (条件判断) {
	循环体
}

扩展格式：
初始化语句；
while (条件判断）{
	循环体；
	步进语句；
}

*/


 * do-while 循环的标准格式：
do{

 	循环体
 }while(条件判断);

 * 扩展格式：
 初始化语句
    do{

 		循环体
 		步进语句
 }while(条件判断);

/*三种循环的区别。
1 如果条件判断 从来没有满足过，那么for循环和while循环将会执行0次，但是do-while 循环会执行至少一次。
2 for循环的变量在小括号当中定义，只有循环内部才可以使用。
*/

### Day03-15/16/17/18  0406 13：30

package cn.itcast.day03.Demo03;
public class Demo15Continue {
    public static void main(String[] args) {
        for (int i=1; i<=10; i++){
            if(i==4){
                continue;
                //break;
            }
            System.out.println(i+"层到了。");
        }
    }
}

#### break 关键字的用法有常见的两种：
1 可以在switch语句当中，一旦执行，整个switch语句立刻结束。
2 还可以用在循环语句当中，一旦执行，整个循环语句立刻结束。打断循环。

#另一种循环控制语句是continue关键字
一旦执行，立刻跳过当前次循环剩余内容，马上开始下一次循环

/*
永远停不下来的循环，叫做死循环。
死循环的标准格式：
while (true){
    循环体
}
 */

### Day04-08  0419 12:20 方法定义

方法定义格式：
public static void 方法名称(){
	方法体
}
调用格式：
方法名称（）;

注意事项：
1 方法定义的先后顺序无所谓
2 方法定义必须是挨着的，不能在一个方法的内部定义另一个方法
3 方法定义之后不会自己执行，如果希望执行，要进行方法的调用：

public class DEMO04PrintMethod {
    public static void main(String[] args) {
        printMethod();
    }

    public static void printMethod(){
        for (int j = 0; j < 5; j++) {
            for (int i = 0; i < 20; i++) {
                System.out.print("*");
            }
            System.out.println();
        }
    }
}


Day04-08-09  0419 12:40  Demo02MethodDefine
* 方法就是若干语句的功能集合。（类似存储过程）
####  调用方法：方法名称();
####  脚本，按照你写的编码，一行一行执行
------------------------------------------------
 * 方法好比是一个工厂。
 * 蒙牛工厂  原料：奶牛 、饲料、水
 *        		  产出物：奶制品
 *  钢铁工厂  原料：铁矿石、煤炭
 *                 产出物：钢铁建材
 * 参数（原料）： 就是进入方法的数据
 * 返回值（产出物）：从方法中出来的数据
------------------------------------------------
 * 定义方法的完整格式：
 * 修饰符  返回值类型  方法名称（参数类型 参数名称，。。。）｛
 * 		方法体
 * 		return 返回值；
}

修饰符：现阶段的固定写法，public static
返回值类型，也就是方法最终产生的数据结果是什么类型
方法名称：方法名称，规则和变量一样，小驼峰
参数类型：进入方法的数据类型
参数名称：进入方法的数据对应的变量名称
ps: 参数如果有多个，使用逗号进行分隔
方法体：方法需要做的事情，若干行代码
return: 两个作用，1停止方法，2 将返回值还给调用处。
返回值： 也就是方法执行后最终产生的数据结果

 * 注意： return后面的“返回值”必须和方法前面的“返回类型”一致

#### 定义一个两个int数字相加的方法。三要素：

  返回值类型：int
  方法名称：sum
  参数列表：int a , int b

```java
public static int  sum(int a, int b) {
	int result = a+b;
	return result;
}
```



### Day04-10  0419 12:55    方法的三种调用格式

![image-20211031144404117](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031144404117.png)

  方法的三种调用格式
  1 单独调用：方法名称（参数）; (因没有打印，所以不会显示出内容来)
  2 打印调用 : System.out.println(方法名称（参数));
  3 赋值调用 : 数据类型 变量名称=方法名称（参数））;

  注意：此前的类型写为void，这种只能**单独调用**。

```java
public class Demo02MethodDefine {
    public static void main(String[] args) {
        //单独调用
        sum(10, 20);
        System.out.println("==================");    
        
        //打印调用
    	System.out.println(sum(10,20)); //30
    	System.out.println("==================");

    	//赋值调用
    	int number=sum(15,25);
    	number += 100;
    	System.out.println("变量的值:"+number);
	}
    public static int sum(int a, int b){
        System.out.println("方法执行了");
        int result = a + b;
        return result;
    }
}
```


### Day04-12  0419 13:10   Demo03MethodParam 对比有参数和无参数

```java
/*
有参数：小括号当中有内容。当一个方法需要一些数据条件，才能完成任务的时候，就是有参数。
        例如两个数字相加，必须知道两上数字各是多少，才能相加。
无参数：小括号当中留空。一个方法不需要任何数据条件，自己就能独立完成任务，就是无参数。
        例如定义一个方法，打印固定10次HelloWorld.
*/

public class Demo03MethodParam {
    public static void main(String[] args) {
        method1(10,20);
        System.out.println("====================");
        method2();
    }
    //两个数字相乘，必须知道两个具体数。有参数
    public static void method1(int a, int b){
        int result =a * b;
        System.out.println("结果是："+result);
    }
    //无参数：打印10次文本
	public static void method2(){
    	for (int i = 0; i < 10; i++) {
        	System.out.println("HelloWorld"+i);
    	}
	}
}
```


### Day04-13  0419 13:20  对比有返回值和无返回值

/*
题目要求：定义一个方法，求出两个数字之和（结果告诉我）
题目变形：定义一个方法，打印两个数字之和（结果自己打印，不用返回）
注意：对于无返回值 的方法，只能使用单独调用。
 */



```java
public class Demo04MethodReturn {
    public static void main(String[] args) {
        //我是main方法，我来调用。你把结果告诉我
        int num=getSum(10,20);
        System.out.println("返回值是："+num);
        System.out.println("======================");
        printSum(100,200);
	}
	//两个数字相加，有返回值 "int",结果
	public static int getSum(int a, int b){
    	int result =a+b;
    	return result;
	}
	//没有返回值，结果自己打印 “void”
	public static void printSum(int a, int b){
   	 int result= a+b;
   	 System.out.println("结果是："+ result);
	}
}
```



### Day04-14  0419 13:30

/*
定义一个方法，用来判断两个数字是否相等。
 */
public class Demo01MethodSame {
    public static void main(String[] args) {
        System.out.println(isSame(10,20)); //false
        System.out.println(isSame(20,20)); //true
        System.out.println(isSame(20,10));
    }
    /*
    三要素：
    返回值类型；boolean
    方法名称：isSame
    参数列表：int a, int b
     */
    public static boolean isSame(int a,int b){
        boolean same;
        /*if (a==b){
            same=true;
        } else {
            same=false;
        }*/	--【1】
        // same =a ==b ? ture : false; --【2】
        // boolean same = a == b;  --【3】
        return a == b;  【4】
    }
}

---1到100数字之和
public class Demo01MethodSum {
    public static void main(String[] args) {
        System.out.println("结果是："+getSum());
    }
    public static int getSum(){
        int sum=0;
        for (int i = 0; i <= 100; i++) {
            sum+=i;
        }
        return sum;
    }
}


package cn.itcast.day04.demo03;
/*
打印指定次数的HelloWorld!
 */
public class Demo03MethodPrint {
    public static void main(String[] args) {
    printCount(11);
    }
    public static void printCount(int num){
        for (int i = 0; i < num; i++) {
            System.out.println("HelloWorld!"+(i+1));
        }
    }
}

### Day04-17  0419 13:45 方法使用注意事项

/*

**方法使用注意事项：**

 * 1方法应该定义在类当中，不能嵌套

 * 2方法定义前后顺序无所谓。

 * 3 方法定义后不会执行，一定要调用：单独、打印、赋值调用 。

 * 4如果方法有返回值，必须写上"return"，不能没有

 * 5 return 后面的返回值数据，必须和方法的返回值类型匹配。

 * 6 对于void没有返回值的方法，不能return，只能return自己。

 * 7 对于void 最后一行的return可省略。

 * 8一个方法当中可以有多个return语句，但是必须保证同时只有一个会被执行到。
    --获取两个数的最大值 

  ```java
  public static void getMax(int a, int b){
  	if (a > b) {
  		return a;
  	} else {
  		return b;
  	}
  }
  ```

  */

### Day04-18/19  0419 13:53 方法的重载 Overload

/*
 * 方法的重载（overload ）：多个方法的名称一样，但是参数列表不一样
 * 方法重载与下列因素相关：
 * 1 参数的个数不同
 * 2 参数的类型不同：浮点强制转换为int
 * 3 参数的多类型顺序不同
 * 
 *  方法重载与下列因素无关：
 *  1 与参数名称无关
 *  2 与方法的返回值类型无关

```java
public class Demo01Methodoverload {
    public static void main(String[] args) {
        /*System.out.println(sumTwo(10,20));
        System.out.println(sumThree(10,20,30));
        System.out.println(sumFor(10,20,30,40));*/
        System.out.println(sum(10,20));
        System.out.println(sum(10,20,30));
        System.out.println(sum(10,20,30,40));
//        System.out.println(sum(10,20,30,40,50));  //找不到报错
    }
    public static int sum(int a,double b){
        return (int)(a+b);
    }

    public static int sum(double a, int b){
        return (int)(a+b);
    }


    public static int sum(int a,int b){
        System.out.println("有2个参数的方法执行");
        return a+b;
    }
    public static int sum(int a,int b, int c){
        System.out.println("有3个参数的方法执行");
        return a+b+c;
    }
    public static int sum(int a,int b, int c, int d){
        System.out.println("有4个参数的方法执行");
        return a+b+c+d;
    }

}
```

*/

### Day04-20/21/22  0419 14:12-14:40

/*
比较两个数据是否相等
两个byte类型，两个short类型，两个int类型，两个long类型，
并在main方法中进行测试。
 */
public class Demo02MethodOverloadSame {
    public static void main(String[] args) {
    byte a=10;
    byte b=20;
        System.out.println(isSame(a,b));

        System.out.println(isSame((short)20,(short)20));
    
        System.out.println(isSame(11,12));
    
        System.out.println(isSame(10L,10L));
    }
    
    public static boolean isSame(byte a , byte b){
        System.out.println("两个byte的方法执行！");
        boolean same;
        if (a == b) {
            same=true;
        } else {
            same=false;
        }
        return same;
    }
    public static boolean isSame(short a , short b){
        System.out.println("两个short的方法执行！");
        boolean same = a == b ? true : false;
        return same;
    }
    public static boolean isSame(int a , int b){
        System.out.println("两个int的方法执行！");
        return a==b;
    }
    public static boolean isSame(long a , long b){
        System.out.println("两个long的方法执行！");
        if(a==b){
            return true;
        }else{
            return false;
        }
    }

}

--20 多数据类型重载：

//byte short int long float double char boolean
//String

public class Demo04OverloadPrint {
    public static void main(String[] args) {
        myPrint(100);
        myPrint("Hello");
    }
    public static void myPrint(byte num) {
        System.out.println(num);
    }
    public static void myPrint(short num){
        System.out.println(num);
    }
    public static void myPrint(int num){
        System.out.println(num);
    }
    public static void myPrint(float num){
        System.out.println(num);
    }
    public static void myPrint(double num){
        System.out.println(num);
    }
    public static void myPrint(char zifu){
        System.out.println(zifu);
    }
    public static void myPrint(boolean is){
        System.out.println(is);
    }
    public static void myPrint(String str){
        System.out.println(str);
    }
}





# Day 5  

#### 5-1 数组

特点：1数组是一种引用数据类型、2多个数据类型必须统一、3数组长度在程序运行期间不可改变

#### 5-2

数组的初始化：在内存当中创建一个数组，并且赋予默认值
两种方式：
1 动态初始化（指定长度）：创建时，直接指定数组当中数据元素个数。
2 静态初始化（指定内容）：创建时，不指定个数，而是直接指定数据内容。

解释：
左侧数据类型：就是数组当中保存的数据，全部统一是什么类型
左侧中括号[]：代表我是一个数组
左侧数组名称：给数组取一个名字
右侧的new：代表创建数组的动作
右侧数据类型：必须和左侧的数据类型保持一致
右侧中括号的长度：也就是数组当中，到底可以保存多少个数据，是一个int数字

//创建一个数组，里面可以存放300个int数组
动态初始化数组的格式：
  数据类型[] 数组名称=new 数据类型[数组长度];
  int [] arrayA = new int [300];
  double [] arrayB=new double[10];
  String [] arrayC = new String[5];

### Day05-3  0419 17:02

#### 2 静态初始化（指定内容）：创建时，不指定个数，而是直接指定数据内容。

静态初始化数组的格式：

  数据类型[] 数组名称=new 数据类型[]{元素1，元素2，…… };
  int [ ] arrayA=new int [ ] {5,15, 25};
  String [ ] arrayB = new String [ ] { "Hello", "World","Java" };

省略格式：
  数据类型[] 数组名称={元素1，元素2，…… }; 
  int [ ] arrayA = { 10, 20, 30 };

注意事项：
1 静态初始化没有指定长度，但会自动推算得到长度。
2 静态初始化标准格式可以拆分为两个步骤
  int [] arrayA;
  arrayA=new int[] {5,15, 25};
3 动态初始化也可以拆分为两个步骤，同上。
4 静态初始化一旦使用省略格式，就不能拆分为两个步骤了。
  int [] arrayA;
  arrayA={5,15, 25};  《== 错误，缺new int

使用建议：
如果不确定数组当中的具体内容，用动态初始化，
否则，已经确定了数组当中的具体内容，用静态初始化。

### Day05-5 0419 17:20

/*
直接打印数组名称，得到的是数组对应的：内存地址哈希值。
访问数组元素的格式：数组名称 [ 索引值  ] 
索引值：就是一个int数字，代表数组当中元素的编号。
【注意】索引值从0开始，一直到“数组的长度-1”为止
  int [ ] arrayA = { 10, 20, 30 };
  System.out.println(arrayA [0]); //10
  System.out.println(arrayA [1]); //20
  System.out.println(arrayA [2]); //30

*/

### Day05-6 0419 17:42

使用动态初始化数组时，其中的元素会自动拥有一个默认值。规则如下：
整数类型：0
浮点类型：0.0
字符类型：'\u0000'
布尔类型：false
引用类型：null

注意事项：
静态初始化也有默认值的过程，只不过系统自动马上将默认值改为了大括号中的数值。

public class Demo04ArrayUse {
    public static void main(String[] args) {
        int[] array ={10,20,30};
        System.out.println(array);
        System.out.println(array[0]);
        System.out.println(array[1]);
        System.out.println(array[2]);

        //将数组赋值给变量
        int num = array[1];
        System.out.println(num);
    }



5-7  0419 

java内存需要划分成为5个部分：
1 栈（stack)：存放的都是方法中的局部变量。方法的运行一定要在栈当中。
  局部变量：方法的参数，或者是方法｛｝内部的变量
  作用域：一旦超出作用域，立刻从栈内存当中消失。
2 堆（Heap）：凡是new出来的东西，都在堆当中。
  堆内存里面的东西都有一个地址值：16进制
  堆内存里的数据，都 有默认值。规则：
     整数类型：0
     浮点类型：0.0
     字符类型：'\u0000'
     布尔类型：false
     引用类型：null

3 方法区 （Method Area）:存储.class相关信息，包含方法的信息。
4 本地方法栈（）：与操作系统相关。
5 寄存器（pc Register)：与CPU相关。

### Day5-11  0419 

package cn.itcast.day05.demo03;
/*
数组的索引编号从0开始，一直到“数组长度-1”为止
如果数组索引编号不存在，将发生越界异常
 */
public class Demo01ArrayIndex {
    public static void main(String[] args) {
        int[] array={15,25,35};
        System.out.println(array[0]);
        System.out.println(array[1]);
        System.out.println(array[2]);
        //错误写法
        System.out.println(array[3]);
    }
}

### Day5-12  0419 

package cn.itcast.day05.demo03;
/*
所有的引用类型变量，都可赋值为null值，代表什么都没有。
数组必须进行new初始化才能使用其中的元素
如果只是赋值null,没有进行new创建，将会空指针异常nullpointer...


 */
public class Demo02ArrayNull {
    public static void main(String[] args) {
        int[] array=null;
        array =new int[3];
        System.out.println(array[0]);
        // array=new int[3];
    }
}

### Day5-13  0419  获取数组的长度

package cn.itcast.day05.demo03;
/*
获取数组的长度：
数组名称.length

数组一旦创建，程序运行期间，长度不可改变
 */
public class Demo03ArrayLength {
    public static void main(String[] args) {
        int[] arrayA= new int[3];
        int[] arrayB= {10,20,30,3,5,4,6,7,8,8,65,4,44,6,10};
        int len =arrayB.length;
        System.out.println("arrayB数组的长度是："+len);
        System.out.println("=============");

        int[] arrayC=new int[3];
        System.out.println(arrayC.length);
        arrayC=new int[5];
        System.out.println(arrayC.length);
    }
}

### Day5-14  0419  遍历数组

/*
遍历数组，说的是每一个元素，逐一打印。

#### array.fori ####
 */
public class Demo04Array {
    public static void main(String[] args) {
        int[] array={15,25,30,40,50,60,75};
        //System.out.println(array[0-5]);

        //使用循环
        for (int i=0; i<6; i++){
            System.out.println(array[i]);
        }
        System.out.println("================");


        for (int i = 0; i < array.length; i++) {
            System.out.println(array[i]);
        }
    }
}

### Day5-15  0419 

public class Demo05ArrayMax {
    public static void main(String[] args) {
        int[] array = {5,15,30,20,10000,30,35};
        int max = array[0];
        for (int i = 1; i < array.length; i++) {
            //如果当前元素比max大，则替换
            if (array[i]>max) {
                max=array[i];
            }

        }// 谁最大，谁留在max中
        System.out.println("最大值是"+max);
    }
}


public class Demo06ArrayMin {
    public static void main(String[] args) {
        int[] array = {5,15,30,20,10000,-20,30,35};
        int min = array[0];
        for (int i = 1; i < array.length; i++) {
            //如果当前元素比min小，则替换
            if (array[i]<min) {
                min=array[i];
            }

        }// 谁最大，谁留在max中
        System.out.println("最小值是"+min);
    }
}



### Day5-16   0419 

/*
数组元素的反转：
本来的样子：[1,2,3,4]
之后的样子：[4,3,2,1]
 */
public class Demo07ArrayReverse {
    public static void main(String[] args) {
        int[] array ={10,20,30,40,50};

        //遍历打印数组本来的样子	
        for (int i = 0; i < array.length; i++) {
            System.out.println(array[i]);
        }
        System.out.println("==================");
    
        /*
        初始化语句：int min =0 , max=array.length-1
        条件判断：min<max
        步进表达式：min++,max--
        循环体：用第三个变量倒手
         */
        for(int min =0 , max=array.length-1;min<max;min++,max--){
            int temp=array[min];
            array[min]=array[max];
            array[max]=temp;
        }

// 再次打印遍历输出数组后来的样子
        for (int i = 0; i < array.length; i++) {
            System.out.println(array[i]);
        }
    }
}

### Day5-17   0419  打印数组的方法

/*
数组可以作为方法的参数。
当调用方法的时候，向方法的小括号进行传参，传递进去的其实是数组的地址值。
*/

```java
public class Demo01ArrayParam {
    public static void main(String[] args) {
        int[] array={10,20,30,40,50};
        printArray(array);
        System.out.println("======AAAA========");
        printArray(array);
        System.out.println("======BBBB========");
        printArray(array);
    }
	public static void printArray(int[] array){
		for (int i = 0; i < array.length; i++) {
		System.out.println(array[i]);
		}
	}
}
```


### Day5-18  0419 21:40

/*
一个方法可以有0，1多个参数，只能有一个返回值。
如果希望一个方法产生多个结果进行返回，可以使用数组作为返回值类型
任何数据类型都能作为方法的参数类型，或者返回值类型。

数组作为方法的参数，传递进去的其实是数组的地址值。
数组作为方法的返回值，返回的其实也是数组的地址值。

 */


```java
public class Demo02ArrayReturn {
    public static void main(String[] args) {
        int[] ddd=calculate(10,20,30);
        System.out.println("main方法接收的返回值地址是");
        System.out.println(ddd); //地址值
		System.out.println("总和："+ddd[0]);
  		System.out.println("平均数："+ddd[1]);
	}
	public static int[]  calculate(int a, int b, int c){
		int sum=a+b+c;
        int avg=sum /3;  //两个结果都想返回
        //需要一个数组，可以保存多个结果
        /*int[] array = new int[2];
        array[0]=sum;
        array[1]=avg;*/
        int[] array ={sum,avg};
        System.out.println("calculate方法内部数组地址是");
        System.out.println(array); //地址值
    	return array;
   	}
}
```



# Day06

### Day06-1 面向对象

![image-20211031222027095](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031222027095.png)

```java
package cn.itcast.day06.demo01;

import org.w3c.dom.ls.LSOutput;
/*
面向过程：每个步骤都要处理
面向对象：找个功能，直接得到结果
 */

import java.util.Arrays;

public class Demo01PrintArray {
    public static void main(String[] args) {
        int[] array= {10,20,30,40,50};

        //要求打印格式为[10,20,30,40,50]   面向过程：
        System.out.print("[");
        for (int i = 0; i < array.length; i++) {
            if (i==array.length-1){
                System.out.println(array[i]+"]");
            } else{
                System.out.print(array[i] +", ");
            }
        }
        System.out.println("===================");

        //面向对象：
        System.out.println(Arrays.toString(array));
    }
}
```

### 类和对象

#### 什么是类：
类：是一组相关属性和行为的集合。可以看成是一类事物的模板，使用事物的属性特征和行为特征来描述该类事物。
属性：就是该事物的状态信息。
行为：就是该事物能够做什么。能力就是行为

#### 什么是对象
对象：是一类事物的具体体现。对象是类的一个**实例**，必然具备该类事物的属性和行为。

<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211031225211418.png" alt="image-20211031225211418" style="zoom:67%;" />

### Day06-04 类的定义

**注意事项：**
**1 成员变量是直接定义在类当中的，在方法外。**
**2 成员方法不要写static关键字。**

```java
package cn.itcast.day06.demo01;
/*
定义一个类，用来模拟“学生”事物，其中就有两个组成部分：
属性（是什么）：
    姓名、年龄
行为（能做什么）：
    吃饭、睡觉、学习

对应到Java的类当中：
成员变量（属性）：
    数据类型   变量名称
    String name; //姓名
    int age; //年龄
成员方法（行为）：
    public void eat(){} //吃饭  （成员方法不带static）
    public void sleep(){} //睡觉
    public void study(){} //学习
注意事项：
1 成员变量是直接定义在类当中的，在方法外。
2 成员方法不要写static关键字。
 */
public class Student {
    //成员变量
    String name; //姓名
    int age; //年龄

    //成员方法
    public void eat(){
        System.out.println("吃饭！");
    }
    public void sleep(){
        System.out.println("睡觉！");
    }
    public void study(){
        System.out.println("学习！");
    }
}

```



### Day06-05 创建对象使用类

##### 通常情况下，一个类并不能直接使用，需要根据类创建一个对象，才能使用。

```java
package cn.itcast.day06.demo01;
/*
通常情况下，一个类并不能直接使用，需要根据类创建一个对象，才能使用。
1 导包：也就是指出需要使用的类，在什么位置。
    import 包名称.类名称；
    import cn.itcast.day06.demo01.Student;
    对于和当前类属于同一个包的情况，可以省略导包语句不写。

2 创建,格式：
    类名称  对象名 = new 类名称（）;
    Student stu = new Student();

3 使用,分为两种情况：
    使用成员变量：对象名.成员变量名
    使用成员方法：对象名.成员方法名（参数）
    （也就是，想用谁，就用对象名点儿谁）

注意事项：
如果成员变量没有进行赋值，那么将会有一个默认值，规则和数组一样。
 */
public class Demo02Student {
    public static void main(String[] args) {
        //1 导包，省略

        //2 创建，格式：
        //类名称 对象名 = new 类名称（）；
        //根据Student类，创建了一个名为stu的对象
        Student stu = new Student();

        //3 使用其中的成员变量，格式：
        //对象名.成员变量名
        System.out.println(stu.name); //null
        System.out.println(stu.age); // 0
        System.out.println("-----------------------");

        //改变对象当中的成员变量数值内容
        //将右侧的名字，赋值给stu对象当中的name成员变量
        stu.name="赵丽颖";
        stu.age=18;
        System.out.println(stu.name); //赵丽颖
        System.out.println(stu.age); // 18
        System.out.println("-----------------------");

        //4 使用对象的成员方法，格式：
        //对象名.成员方法名（）
        stu.eat();
        stu.sleep();
        stu.study();

    }
}

```

### Day06-06 定义一个手机类

```java
package cn.itcast.day06.demo02;
/*
定义一个类，手机
属性：品牌、价格、颜色
行为：打电话，发短信

对应到类当中：
成员变量（属性）:
    String brand;
    double price;
    String color;
成员方法（行为）：
    public void call(String who){} //打电话
    public void sendMessage(){} //群发短信
 */
public class Phone {
    //成员变量
    String brand;
    double price;
    String color;

    //成员方法
    public void call(String who){
        System.out.println("给"+who+"打电话");
    }
    public void sendMessage(){
        System.out.println("群发短信");
    }
}
```

##### 根据手机类创建一个对象Demo01PhoneOne

```java
package cn.itcast.day06.demo02;

public class Demo01PhoneOne {
    public static void main(String[] args) {
        //根据Phone类，创建一个名为one的对象
        //格式：类名称  对象名 = new 类名称（）；
        Phone one = new Phone();
        System.out.println(one.brand); //null
        System.out.println(one.price); // 0.0
        System.out.println(one.color); // null
        System.out.println("==============");

        one.brand="苹果";
        one.price=3833.0;
        one.color="黑色";
        System.out.println(one.brand);
        System.out.println(one.price);
        System.out.println(one.color);
        System.out.println("==============");

        one.call("乔布斯");
        one.sendMessage(); //群发短信
    }
}
```

### Day06-07  对象的内存图

![image-20211107160420905](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211107160420905.png)



### Day06-08 两个对象共用一个方法

```java
package cn.itcast.day06.demo02;

public class Demo02PhoneTwo {
    public static void main(String[] args) {
        Phone one = new Phone();
        System.out.println(one.brand); //null
        System.out.println(one.price); // 0.0
        System.out.println(one.color); // null
        System.out.println("==============");

        one.brand="苹果";
        one.price=3833.0;
        one.color="黑色";
        System.out.println(one.brand);
        System.out.println(one.price);
        System.out.println(one.color);
        System.out.println("==============");

        one.call("乔布斯");
        one.sendMessage(); //群发短信
        System.out.println("==============");

        Phone two = new Phone();
        System.out.println(two.brand); //null
        System.out.println(two.price); // 0.0
        System.out.println(two.color); // null
        System.out.println("==============");

        two.brand="三星";
        two.price=2833.0;
        two.color="蓝色";
        System.out.println(two.brand);  //三星
        System.out.println(two.price);  //2833
        System.out.println(two.color);  //蓝色
        System.out.println("==============");

        two.call("欧巴");
        two.sendMessage(); //群发短信
    }
}
```

![image-20211107162548337](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211107162548337.png)



### Day06-09 两个引用指向同一个对象

```java
package cn.itcast.day06.demo02;

public class Demo03PhoneSame {
    public static void main(String[] args) {
        Phone one = new Phone();
        System.out.println(one.brand); //null
        System.out.println(one.price); // 0.0
        System.out.println(one.color); // null
        System.out.println("==============");

        one.brand="苹果";
        one.price=3833.0;
        one.color="黑色";
        System.out.println(one.brand);
        System.out.println(one.price);
        System.out.println(one.color);
        System.out.println("==============");

        one.call("乔布斯");
        one.sendMessage(); //群发短信
        System.out.println("==============");

        //将one当中保存的对象地址值 赋值给two
        Phone two = one;
        System.out.println(two.brand); //苹果
        System.out.println(two.price); // 3833
        System.out.println(two.color); // 黑色
        System.out.println("==============");

        two.brand="三星";
        two.price=2833.0;
        two.color="蓝色";
        System.out.println(two.brand);  //三星
        System.out.println(two.price);  //2833
        System.out.println(two.color);  //蓝色
        System.out.println("==============");

        two.call("欧巴");
        two.sendMessage(); //群发短信
    }
}
```

![image-20211107163748893](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211107163748893.png)



### Day06-10 使用对象类型作为方法的参数

##### 带有static 的方法是普通方法，不需要对象，可以直接调用

```java
package cn.itcast.day06.demo02;

public class Demo04PhoeParam {
    public static void main(String[] args) {
        Phone one = new Phone();
        one.brand="苹果";
        one.price=8388.0;
        one.color="土豪金";

        method(one); //传递进去的参数是地址值
    }

    public static void method(Phone param){ // 带有static是普通方法，不需要对象，可以直接调用
        System.out.println(param.brand); //苹果
        System.out.println(param.price); //8388。0
        System.out.println(param.color); //土豪金
    }
}
```

![image-20211107174351282](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211107174351282.png)

### Day06-11 使用对象类型作为方法的返回值

```java
package cn.itcast.day06.demo02;

public class Demo05PhoneReturn {
    public static void main(String[] args) {
        Phone two = getPhone();
        System.out.println(two.brand); //苹果
        System.out.println(two.price); //8388。0
        System.out.println(two.color); // 玫瑰金
    }
    public static Phone getPhone(){
        Phone one = new Phone();
        one.brand = "苹果";
        one.price = 8388.0;
        one.color = "玫瑰金";
        return one;
    }
}
```

![image-20211107183733224](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211107183733224.png)



### Day06-12 成员变量和局部变量的区别

```java
package cn.itcast.day06.demo03;
/*
局部变量和成员变量
1 定义的位置不一样（重点）
局部变量：在方法的内部
成员变量：在方法的外部，直接写在类中

2 作用范围不一样（重点）
局部变量: 只有方法中才可以使用，出了方法就不能再用
成员变量：整个类全都可以通用。

3 默认值不一样（重点）
局部变量：没有默认值 如果要想使用，必须手动进行赋值
成员变量：如果没有赋值，会有默认值，规则和数组一样

4 内存的位置不一样（了解）
局部变量：位于栈内存
成员变量：位于堆内存

5 生命周期不一样
局部变量：随着方法进栈而诞生，随着方法出栈而消失
成员变量：随着对象创建而诞生，随着对象被垃圾回收而消失
 */
public class Demo01VariableDifference {
    String name; //成员变量

    public void methodA(){
        int num =20; //局部变量
        System.out.println(num);
        System.out.println(name);
    }
    public void methodB(int param){  //方法的参数就是局部变量
        //参数在方法调用的时候，必然会被赋值的。
        System.out.println(param);
        int age; //局部变量
//        System.out.println(age);  //没赋值不能用
//        System.out.println(num);//错误写法！
        System.out.println(name);
    }
}
```



### Day06-13 面向对象三大特征之封装

```java
package cn.itcast.day06.demo03;
/*
面向对象：三大特征：封装、继承、多态。
封装在java当中的体现：
1，方法就是一种封装
2，关键字private也是一种

封装就是将一些细节信息隐藏起来，对于外界不可见。
 */
public class Demo02Method {
    public static void main(String[] args) {
        int[] array = {5,15,25,20,100};
        int max= getmax(array);
        System.out.println("最大值："+max);
    }
    //给我一个数组，我给你一个最大值
    public static int getmax(int[] array){
        int max = array[0];
        for (int i = 1; i < array.length; i++) {
            if (array[i]> max ){
                max = array[i];

            }
        }
        return max;
    }
}
```



### Day06-14 private关键字的作用及使用

```java
封装在java当中的体现：
1，方法就是一种封装
2，关键字private也是一种
    
package cn.itcast.day06.demo03;
/*
问题描述：无法阻止不合理数值，如-20岁
解决方案：用private关键字将需要保护的成员变量进行修饰
一量使用了private进行修饰，那么本类当中仍然可以随意访问。
但是！超出了本类范围之外就不能再直接访问了

间接访问private成员变量，就是定义一对儿Getter/Setter方法

必须叫setXxx 或者getXx命名规则
对于Getter来说，不能有参数，返回值类型和成员变量对应。
对于Setter来说，不能有返回值，参数类型和成员变量对应。
 */
public class Person {
    String name; //姓名
    private int age; //年龄
    public void show() {
        System.out.println("我叫:"+name+",年龄是："+age);
    }
    //这个成员方法，专门用于向age设置数据
    public void setAge(int num){
        if(num<100 && num>=0) { //如果是合理情况
            age = num;
        } else{
            System.out.println("数据不合理！");
        }

    }
    //这个成员方法，专门用于获取age的数据
    public int getAge(){
        return age;
    }
}
```

```java
package cn.itcast.day06.demo03;

public class Demo03Person {
    public static void main(String[] args) {
        Person person= new Person();
        person.show();

        person.name="赵丽颖";
//        person.age=-20; //直接访问private内容，错误写法！
        person.setAge(50);
        person.show();
    }
}
```



### Day06-15 用private定义学生类，boolean特殊

```java
package cn.itcast.day06.demo03;
/*
对于基本类型当中的boolean值，Getter方法一定要写成isXxx，而setXxx规则不变
 */
public class Student {
    private String name; //姓名
    private int age;
    private boolean male; //是不是爷们儿

    public void setMale(boolean b){
        male=b;
    }
    public boolean isMale(){
        return male;
    }

    public void setName(String str){
        name = str;
    }

    public String getName(){
        return name;
    }

    public void setAge(int num){
        age=num;
    }

    public int getAge(){
        return age;
    }
}
```

```java
package cn.itcast.day06.demo03;

public class Demo04Student {
    public static void main(String[] args) {
        Student stu = new Student();
            stu.setName("鹿晗");
            stu.setAge(20);
            stu.setMale(true);

        System.out.println("姓名："+stu.getName());
        System.out.println("年龄："+stu.getAge());
        System.out.println("是不是爷们儿："+stu.isMale());
    }
}
```

### Day06-16 this 关键字

```java
package cn.itcast.day06.demo04;
/*
当方法的局部变量和类成员的变量重名时，根据就近原则 优先使用局部变量。
如果 需要访问本类当中的成员变量，需要使用格式：
this.成员变量名
通过谁调用的方法，谁就是this!
 */

public class Person {
    String name; //我自己的名字

    //参数who 是对方的名字
    //成员变量name 是自己的名字
    public void sayHello(String name){
        System.out.println(name+",你好。我是"+this.name);
        System.out.println(this);
    }
}
```

```java
package cn.itcast.day06.demo04;

public class Demo1Person {
    public static void main(String[] args) {
        Person person = new Person();
        //设置自己的名字
        person.name="王健林";
        person.sayHello("王思聪");
        System.out.println(person); //地址值
    }
}
```

### Day06-17 构造方法

#### 构成类的4部分！！！！

```java
package cn.itcast.day06.demo04;
/*
构造方法是专门用来创建对象的方法，当我们通过关键字new来创建对象时，其实就是在调用构造方法
格式：
public 类名称（参数类型  参数名称）{
    方法体
注意事项：
1 构造方法的名称必须和所在的类名称完全一样，就连大小也要一样
2 构造方法不要写返回值 类型，连void都不写
3 构造方法不能return一个具体的返回值
4 如果没有编写构造方法，那么编译器将会默认赠送一个构造方法，没有参数、方法体什么事情 都不做
}
 */
public class Student {

    //成员变量
    private String name;
    private int age;
    //无参数的构造方法
    public Student(){
        System.out.println("构造方法执行啦！");
    }
    //全参数的构造方法
    public Student(String name, int age){
        System.out.println("全参构造方法执行啦！");
        this.name = name;
        this.age = age;
    }
    //Getter Setter
    public void setName(String name){
        this.name=name;
    }
    public String getName(){
        return name;
    }
    public void setAge (int age){
        this.age = age;
    }
    public int getAge(){
        return age;
    }
}
```

```java
package cn.itcast.day06.demo04;

public class Demo02Student {
    public static void main(String[] args) {
        Student stu1 = new Student(); //无参构造
        System.out.println("==============================");
        Student stu2 = new Student("赵丽颖", 20);//全参构造
        System.out.println("姓名："+stu2.getName()+",年龄："+stu2.getAge() );
        //有改变的需要
        stu2.setAge(21);//改变年龄
        System.out.println("姓名："+stu2.getName()+",年龄："+stu2.getAge());
    }
}
```



## Day06-18 定义一个标准的类

##### 快速生成get set 和无参、全参构造方法。定义好成员变量后，在下方按快捷键：Alt+insert

```java
package cn.itcast.day06.demo05;
/*
一个标准的类通常拥有下面的四个组成部分：
1 所有的成员变量都要使用private关键字修改饰
2 为每一个成员变量编写一对儿Getter/Setter方法
3 编写一个无参数的构造方法
4 编写一个全参数的构造方法

这样标准的类也叫做Java Bean
 */
public class Student {

    private String name; //姓名
    private int age; //年龄

    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

```java
package cn.itcast.day06.demo05;

public class Demo01Student {
    public static void main(String[] args) {

    Student stu1 = new Student();
    stu1.setName("迪丽热巴");
    stu1.setAge(20);
        System.out.println("姓名："+stu1.getName()+"，年龄："+stu1.getAge());
        System.out.println("=====================================");

        Student stu2 = new Student("古力那查",21);
        System.out.println("姓名："+stu2.getName()+"，年龄："+stu2.getAge());
        stu2.setAge(22);
        System.out.println("姓名："+stu2.getName()+"，年龄："+stu2.getAge());
    }
}
```







































# Day08

### Day08-1  demo01   --2020-02-29   创建字符串

```java
java.lang.String类代表字符串。
就是说：程序当中所有的双引号字符串，都是String类的对象。（没有new也是）

字符串特点：
1、字符串的内容永不可变。【重点】
2、正是因为字符串不可改为，所以字符串是可以共享使用的。
3、字符串效果上相当于是char[]字符数组，但底层原理是byte[]字节数组。

创建字符串的常见3+1种方式：
三种构造方法：
public String(): 创建一个空白字符串，不含有任何内容。
public String(char[ ] array):根据字符数组的内容，来创建对应的字符串。
public String(byte[] array): 根据字节数组的内容，来创建对应的字符串。
一种直接创建：
String str="hello"; //右边直接用双引号

注意：直接写上双引号，就是字符串对象。
```



### Day08-3 demo02StringPool 0229

/*
字符串常量池：程序当中直接写上的双引号字符串，就在字符串常量池中；new的不在池当中，而在堆当中。

对于基本类型来说，== 是进行数值的比较。
对于引用类型来说，==是进行地址值的比较。

### Day8-4 0229  demo01StringEquals

/*
== 是对进行对象的地址值比较，如果确实需要字符串的内容比较，可以使用两个方法：
一、public boolean equals(Object obj): 参数可以是任何对象，只有参数是一个字符串并且内容相同的才会给true；否则返回false。
注意事项：
1、任何对象都能用Object进行接收。
2、equals方法具有对称怀，也就是a.equals(b)与b.equals(a)效果一样。
3、如果比较双方一个常量一个变量，推荐把常量字符串写在前面。
推荐："abc".equals(str)  不推荐：str.equals("abc")

二、public boolean equalsIgnoreCase(String str) ：忽略大小写，进行内容比较。
*/

### Day08-5  0229  Demo02StringGet

/*
String当中与获取相关的常用方法有：
public int length(): 获取字符串当中含有的字符个数，获取长度。
public String concat(String str): 将当前字符串与参数字串拼接成为返回值新的字符串。
public char charAt(int index)：获取指定索引位置的单个字符。（索引从0开始）
public int indexOf(String str)：查找参数字符串在本字符串当中首次出现的索引位置，如果没有返回值则为-1值。
*/ 

### Day08-6  0301 Demo03Substring

```java
/*
字符串的截取方法：

public String substring(int index)：截取从参数位置一直到字符串末尾，返回新字符串。
public String substring(int begin, int end)：截取从begin开始，一直到end结束，中间的字符串。
备注：[begin,end)，包含左边，不包含右边。
*/
```



### Day08-7 0301-0926  Demo04StringConvert

/*
String当中与转换相关的常用方法有：

public char[] toCharArray()：将当前字符串拆分成为字符数组作为返回值。
public byte[] getBytes()：获得当前字符串底层的字节数组。
public String replace(CharSequence oldString, CharSequence newString)：将所有出现的场比赛字符串替换成为新的字符串，返回替换之后的结果新字符串。
备注：CharSequence（接口）意思是说可以接收字符串类型。
*/

### Day08-8 0301-1005 Demo05StringSplit

/*
分割字符串的方法：
public String[] split(String regex)：按照参数的规则，将字符串切分成为若干部分。
注意事项：
split方法的参数其实是一个“正则表达式”，如果按照英文句点进行切分，必须写“\\.”。（两个反斜杠）
*/

### Day08-9 0301-1025 Demo06StringPratise

/*
题目：
定义一个方法，把数组{1，2，3}按照指定格式拼接成一个字符串。格式参照如下：[word1#word2#word3].

分析：
1 首先准备一个int[]数组，内容是1，2，3
2 定义一个方法，用来将数组变成字符串
三要素
返回值类型：String
方法名称：fromArrayToString
参数列表：int[]
3 格式：[word1#word2#word3]
用到：for循环、字符串拼接、每个数组元素之前都有一个word字样、分隔使用的是#、区分一下是不是最后一个
4 调用方法，得到返回值，并打印结果字符串。
*/

### Day08-10  0301-1043  Demo07StringCount

/*
题目：
键盘输入一个字符串，并且统计其中各种字符出现的次数。
各类有：大写字母、小写字母、数字、其他

思路：
1 既然用到键盘输入，肯定是Scanner
2 键盘输入的是字符串，那么：String str = sc.next();
3 定义四个变量，分别代表四种字符各自的出现次数。
4 需要对字符串的一个字、一上字检查，String-->char[] ,方法就是toCharArray()
5 遍历char[] 字符数组，对当前字符的各类进行判断，并且用 四个变量进行++动作。
6 打印输出四个变量，分别代表四种字符出现次数。
*/

### Day08-11  0301-1118  static关键字

一个班级中：
对于姓名、年龄、学号来说，每个对象都有“自己独立的数据”。
但是对于所在教室来说，这应该是“多个对象共享同一数据”。
一旦用了“static关键字”，
那么这样的内容不再属于对象自己，
而是属于类的，
所以凡是本类的对象，都共享一份

### Day08-12  0301-1128-53 Demo01StaticFiled  Student

Day08-13  0301-1537 MyClass Demo02Staticmethod

/*
一旦使用static修饰成员方法，那么这就成为了静态方法。静态方法不属于对象，而是属于类的。
如果没有static关键字，那么必须首先创建对象，然后通过对象才能使用它。
如果有了static关键字，那么不需要创建对象，直接就能通过类名称来使用它。

无论是成员变量，还是成员方法。如果有了static，都推荐使用类名称进行调用。
静态变量：类名称.静态变量
静态方法：类名称.静态方法（）

注意事项：
1 静态不能直接访问非静态。
原因： 因为在内存当中是“先”有的静态内容，“后”有的非静态内容。
“先人不知道后人，但是后人知道先人。”
2 静态方法当中不能用this。
原因：this代表当前对象，通过谁调用的方法，谁就是当前对象。 
*/ 

### Day08-14  0301-1602  Demo03StaticStudent

注意：
根据类名称访问静态成员变量的时候，
全程“和对象就没有关系，只和类有关系”。

### Day08-15  0301-1626 Person Demo04Static

/*
静态代码块的格式是：
public class 类名称{
	static {
		//静态代码块的内容
}
}
特点：当第一次用到本类时，静态代码块执行唯一的一次。
静态内容总是优先于非静态，所以静态代码块比构造方法先执行。

**静态代码块的典型用途：**
**用来一次性地对静态成员变量进行赋值。**

### Day08-16  0301-1643  Demo01Arrays

/*
java.util.Arrays 是一个与数组相关的工具类，里面提供了大量静态方法，用来实现数组常见的操作。
public static String toString(数组)：将参数数组变成字符串（按照默认格式：[元素1，元素2，元素3……]
public static void sort(数组)：按照默认升序（从小到大）对数组的元素进行排序。
备注：如果是数值，sort默认按照升序从小到大
如果是字符串，sort默认按照字母升序
如果是自定义的类型，那么这个自定义的类需要有Comparable或者Comparator接口的支持。（今后学习）
*/

Day08-17  0301-1700 练习题 Demo02ArraysPractise

### Day08-18  0301-1715 Demo03Math

/*
java.util.Math 类是数学相关的工具类，里面提供了大量的静态方法，完成与数学 运算相关的操作。

public static double abs(double num)：获取绝对值，有多种重载。
public static double ceil(double num)：向上取整
public static double floor(double num)：向下取整
public static double long round(double num)：四舍五入。
Math.Pi（念pai）代表近似的圆周率常量（double）。
*/

### Day08-19  0301-1737 练习小学真题Demo04MathPractise

/*
题目：计算10.8到5.9之间，绝对值大于6或小于2。1的整数有多少个？
分析：
1 既然已经确定了范围，for循环
2 起点位置-10.8应该转换成为-10，两种办法：
  2.1 可以使用Math.ceil方法，向上取整
  2.2 强转成为int，自动舍弃所有小数位
3 每一个数字都是整数，所以步进表达式应该是num++，这样每次都是+1。
4 如何拿到绝对值：Math.abs方法。
5 一旦发现了一个数字，需要让计数器++进行统计。

备注：如果使用Math.ceil方法，-10.8可以变成-10.0。注意double也是可以++的。

# Day09-1-2  0303-1940 继承的概述

 /*
继承主要解决的问题是：共性抽取。
父类：也叫基类、超类。
子类：也叫派生类
继承关系当中的特点：

1. 子类可以拥有父类的“内容”
2. 子类还可以拥有自己专有的内容。
*/

### Day09-3  0303-1952 Demo01Extends

/*
在继承的关系中，“子类就是一个父类”。也就是说，子类可以被当做父类看待。
例如父类是员工，子类是老师，**那么“老师就是一个员工”**。关系：is-a

定义父类的格式：（一个普通的类定义）
public class 父类名称 {
	//...
}

定义子类的格式：
public class 子类名称 extends 父类名称 {
	//...
}
*/

### Day09-4  0303-2208 Fu

/*
在父子类的继承关系中，如果成员变量重名，则创建子类对象时，访问有两种方式：
直接 通过子类对象访问成员变量：
	等号左边是谁，就优先用谁，没有则向上找。
间接 通过成员方法访问成员变量
	该方法属于谁，就优先用谁，没有则向上找。
*/

### Day09-5-6  0303-2228 Demo01ExtendsField

 /*
在父子类的继承关系当中，创建子类对象，访问成员方法的规则：
	创建的对象是谁，就优先用谁，如果没有则向上找。
注意事项：
无论是成员方法还是成员变量，如果没有都是向上找父类，绝对不会向下找子类的。

重写（Override)
概念：在继承关系当中，方法的名称一样，参数列表也一样。

重写（Override）：方法的名称一样，参数列表【也一样】。覆盖、覆写。
重载（Overload）：方法的名称一样，参数列表【不一样】。

方法的覆盖重写特点：创建的是子类对象，则优先使用子类方法。
*/

### Day09-7  0304-1956 Demo01Override

/*
方法覆盖重写的注意事项：

1. 必须保证父子类之间方法的名称相同，参数列表也相同。
@Override: 写在方法前面，用来检测是不是有效正确的覆盖重写
这个注解如果不写，也算正确的覆盖重写
2. 子类方法的返回值必须【小于等于】父类方法的返回值范围。
注意：java.lang.Object 类是所有类的公共最高父类（祖宗类）
3. 子类方法的权限必须 大于等于 父类方法的权限修饰符。
扩展：public > protected > (default) > private
备注：（default) 不是关键字default，而是什么都不写，留空。 [() int num]
*/ 

### Day09-8  0304-2013 继承

/*
设计原则:
对于已经投入使用的类，尽量不要进行修改。推荐定义一个新的类，来重复利用其中共性内容，并且添加改动新内容。--》继承
*/

### Day09-9   2020-0305-2149

/*
继承关系中，父子类构造方法的访问特点：

1. 子类构造方法当中有一个默认隐含的“super()”调用，所以一定是先调用父类构造，后执行子类构造。
2. 子类构造可以通过super关键字来调用父类重载构造。
3. super 的父类构造调用，必须是子类构造方法的第一个语句。不能一个子类构造调用多次super构造。
总结：
子类必须调用父类构造方法，不写则赠送super();写了则用写的指定的super调用，super只能有一个，还必须是第一个。
*/ 

### Day09-9   0305-2221

/*
super关键字的用法有三种：
1  在子类的成员方法中，访问父类的成员变量。
2  在子类的成员方法中，访问父类的成员方法。
3  在子类的构造方法中，访问父类的构造方法。
*/

### Day09-10-11   0305-2231

/*
super关键字用来访问父类内容，而this关键字用来访问本类内容。用法也有三种：
1  在本类的成员方法中，访问本类的成员变量
2  在本类的成员方法中，访问本类的另一个成员方法
3  在本类的构造方法中，访问本类的另一个构造方法
在第三种用法当中要注意：
1  this(...)调用也必须是构造方法的第一个语句，唯一一个。
2  super和this两种构造调用，不能同时使用。
 */

Day09-12    0307-1428

### Day09-13    0307-1500 继承的三个特点

1 Java语言是单继承的。一个目标类的直接父类只能有唯一一个。
2 Java语言可以多级继承。
3 一个子类的直接父类是唯一的，但一个父类可以有多个子类。

### Day09-14   0307-1518 抽象的概念

子类就是一个父类，所以是继承关系。
如果父类当中的方法不确定如何进行{}方法体实现，那么这就应该是一个抽象方法

### Day09-15    0307-1528 抽象方法和抽象类的格式 Animal

/*
抽象方法：就是加上abstract关键字，然后去掉大括号，直接分号结束。
抽象类：抽象方法所在的类，必须是抽象类才行。在class前加上abstract即可。
 */

### Day09-16    0307-1536  抽象方法和抽象类的格式  

/*
如何使用抽象类和抽象方法：
1 不能直接创建new抽象类对象；
2 必须用一个子类来继承抽象父类；
3 子类必须覆盖重写抽象父类当中的所有抽象方法。
覆盖重写（实现）：子类去掉抽象方法的abstrct关键字，然后补上方法体大括号。
4 创建子类对象进行使用。
*/

Day09-17    0307-1605 

### Day09-18-19     0307-1629 发红包案例

### Day10-01    0308-1438  接口：  就是一种公共的规范标准。

/*
接口就是多个类的公共规范。
**接口是一种引用数据类型，最重要的内容：抽象方法。**
如何定义一个接口的格式：
public interface 接口名称{
    接口内容
}
备注：换成了interface之后，仍然是.java-->.class
如果是java7,接口中可以包括的内容有：
1 常量（不能发生改变的量）
2 抽象方法（）

如果是java8,还可以额外包含有：
3 默认方法
4 静态方法

如果是java9,还可以额外包含有：
5 私有方法

接口使用步骤：
1 接口不能直接使用，必须有一个实现类来实现该接口。
 格式：
public class 实现类名称 implements 接口名称{
    //...
}
2 接口的实现类必须覆盖重写（实现）接口中所有的抽象方法。
实现：去掉abstract关键字，加上方法体大括号。
3 创建实现类的对象，进行使用。

注意事项：
如果实现类并没有覆盖重写接口中的所有抽象方法，那么这个实现类自己就必须是抽象类。
 */

### Day10-04    0308-1458

/*
任何版本的java中，接口都能定义抽象方法。
格式：
public abstract 返回值类型 方法名称（参数列表）；//不写大括号
注意：
1 接口当中的抽象方法，修饰符必须是两个固定的关键字：public abstract
2 修饰符可省略或省略任何一个。（今天新学，所以不推荐）
3 方法的三要素，可以随意定义。
 */

### Day10-05    0308-1510

/*
从Java 8 开始，接口里允许定义默认方法。
格式：
public default 返回值类型 方法名称（参数列表）{
    方法体
}
备注：接口当中的默认方法，可以解决接口升级的问题。
 */

/*
1 接口的默认方法，可以通过接口实现类对象，直接调用。
2 接口的默认方法，也可以被接口实现类进行覆盖重写。
 */

### Day10-07    0308-1528

/*
从Java8 开始，接口当中允许定义静态方法。
格式：
public static 返回值类型 方法名称（参数列表）{
    方法体
}
提示：就是将abstract 或者default换成static即可，带上方法体。
 */
/*
注意：不能通过接口实现类的对象来调用接口当中的静态方法
正确用法：通过接口名称，直接调用其中的静态方法
格式：接口名称.静态方法名（参数）；
 */

### Day10-09    0308-1539  接口的私有方法定义

接口的私有方法定义使用：
/*
问题描述：
我们需要抽取一个公共方法，来解决两个默认方法之间代码重复的问题
不应该让实现类使用，应该是私有化的
解决方法：
从java9开始接口当中允许定义私有方法
1 普通私有方法，解决多个默认方法之间重复代码问题
格式：
private 返回值类型 方法名称（参数列表）{
        方法体
}

2 普通私有方法，解决多个静态方法之间重复代码问题
格式
private static 返回值类型 方法名称（参数列表）{
        方法体
}
 */

### Day10-11   0308-1550  接口的常量定义和使用

/*
接口当中也可以定义“成员变量”，但是必须使用public static final 三个关键字
从效果上看，这其实就是接口的【常量】。
格式：
public static final 数据类型 常量名称=数据值 ；
注意：一旦使用final关键字进行修饰，说明不可改变。
1 接口当中的常量，可以省略public static final，注意：不写也照样是这样。
2 接口当中的常量，必须进行赋值！
3 接口当中常量名称，使用全大写字母，用下划线分隔（推荐命名）
 */

### Day10-12   0308-1550  接口的内容小结

/* 下方的“[ ]”符号中内容，表明可以省略
在Java 9+ 版本中，接口的内容可以有：
1 成员变量其实是常量，格式：
[public] [static] [final] 数据类型 常量名称 = 数据值 ；
注意：
    常量必须进行赋值，而且一旦赋值不能改变。
    常量名称完全大写，用下划线进行分隔。

2 接口当中最重要的就是抽象方法，格式：
[public] [abstract] 返回值类型，方法名称(参数列表)；
注意：实现类必须覆盖重写接口所有的抽象方法，除非实现类是抽象类。

3 从Java 8 开始，接口里允许定义默认方法，格式：
[public] default 返回值类型 方法名称(参数列表){方法体}；
注意: 默认方法也可以被覆盖重写

4 从Java 8 开始，接口允许地定义静态方法，格式：
[public] static 返回值类型 方法名称(参数列表){方法体}；
注意：应该通过接口名称进行调用，不能通过实现类对象调用接口静态方法

5 从Java 9 开始，接口里允许定义私有方法，格式：
普通私有方法：private 返回值类型  方法名称（参数列表）{方法体}
静态私有方法：private static 返回值类型  方法名称（参数列表）{方法体}
注意：private的方法只有接口自己才能调用，不能被实现类或别人调用。
 */


/*
使用接口的时候，需要注意：
1 接口是没有静态代码块或者构造方法的。
2 一个类的直接父类是唯一的，但是一个类可以同时实现多个接口。
格式：
public class MyInterfaceImpl implements MyInterfaceA, MyInterfaceB{
    //覆盖重写所有抽象方法
}
3 如果实现类所实现的多个接口当中，存在重复的抽象方法，那么只需要覆盖重写一次即可。
4 如果实现类没有覆盖所有接口当中的所有抽象方法，那么实现类就必须是一个抽象类。
5 如果实现类所实现的多个接口当中，存在重复的默认方法，那么实现类一定要对冲突的默认方法覆盖重写
6 一个类如果直接父类当中的方法，和接口当中的默认方法，产生了冲突，优先用父类当中的方法。
 */

### Day10-14   0308-1628  接口之间的多继承

/*
1 类与类之间是单继承的，直接父类只有一个。
2 类与接口之间是多实现的，一个类可以实现多个接口。
3 接口与接口之间是多继承的。

注意事项：
1 多个父接口当中的抽象方法如果重复，没关系
2 多个父接口当中的默认方法如果重复，那么子接口必须进行默认方法的覆盖重写，【而且带着default关键字】
 */

### Day10-15   0308-1636  多态的概述

小明是一个对象，
这个对象即有“学生形态”，也有“人类形态”。
一个对象拥有多种形态，这就是“对象的多态性。
/*
代码当中体现多态性，其实就是一句话：父类引用指向子类对象。
格式：
父类名称 对象名= new 子类名称（）；
或者
接口名称 对象名= new 实现类名称（）；
 */

## Day10-17   0308-1650  多态中成员变量的两种形式

！！!只有方法可以进行覆盖重写，变量不能覆盖重写！！！

/*
访问成员变量的两种形式：
1 直接通过对象名称访问：看等号左边是谁，优先用谁，没有则向上找（父之父）
2 间接通过成员方法访问：看该方法属于谁，优先用谁，没有则向上找
 */

## Day10-18   0308-1705  多态中成员方法的特点

/*
在多态的代码当中，成员方法的访问规则是：
看new的是谁，就优先用谁，
口决：
成员变量：编译看左边，运行还看左边。
成员方法：编译看左边，运行看右边。
 */

Day10-19   0308-1717  多态的好处
好处：无论右边new的时候换成了哪个类对象，等号左边调用方法都不会变化。



### Day10-20-21   0308-19:37 对象的向上转型和向下转型

1 对象的向上转型，其实就是多态写法：
格式：父类名称 对象名=new 子类名称();
Animal animal = new Cat();
创建了一只猫，当做动物来看待，没问题。
含义：右侧创建一个子类对象，把它当做父类来看待使用。
注意事项：向上转型一定是安全的。从小范围转身了大范围，从小范围的猫，向上转换成为更大范围的动物。

向上转型一定是安全的，没有问题的，正确的。但也有个弊端
对向一旦向上转型为父类，那就无法调用子类原本特有内容。
解决方案：用对象的向下转型还原。

2 对象的向下转型，其实是一个“还原”动作。
格式：子类名称 对象名 = (子类名称) 父类对象；
含义：将父类对象，”还原“成为本来的子类对象。

Animal animal = new Cat(); //本来是猫，向上转型成为动物
Cat cat = (Cat) animal;//本来是猫，转型成动物，还原回来成为本来的猫

注意事项：
a 必须保证对象本来创建的时候就是猫，才能向下转型成为猫。
b 如果对象创建的时候本来不是猫，现在非要向下为猫，就会报错。
类似于：基本数据类型当中的，强制类型转换错误；类转换异常
int num = (int) 10.0; //可以
int num = (int) 10.5; //不可以，精度损失

### Day10-22   0309-21:10

/*
如何知道一个父类引用的对象，本来是什么子类？
格式：
对象 instanceof 类名称
这将会得到一个boolean值结果，也就是判断前面的对象能不能当做后面类型的实例。
 */

Day10-23   0314 20:16-21:10 笔记本电脑案例

## Day11-1-5     0314 21:12-22:09  final 关键字

/*
final关键字代表最终、不可改变的。
常见的四种用法：
1 可以用来修饰一个类
2 可以用来修饰一个方法
3 还可以用来修饰一个局部变量
4 还可以用来修饰一个成员变量
*/

/*
当final关键字用来修饰一个类的时候，格式：
public final class 类名称 {
    // ...
}
含义：当前这个类不能有任何的子类。（太监类）
注意：一个类如果是final类，那么其中所有的成员方法都无法进行覆盖重写（没有儿子）
 */

/*
当final关键字用来修饰一个方法的时候，这个方法就是最终方法，不能被覆盖重写。
格式：
修饰符 final 返回值类型 方法名称（参数列表）{
    //方法体
}
注意事项：
对于类、方法来说，abstract关键字和final关键字不能同时使用，因为矛盾。
 */
//一旦使用final用来修饰局部变量，那么这个变量就不能进行更改。
        //“一次赋值，终生不变”
 //对于基本类型来说，不可变说的是变量当中的数据不可改变
        //对于引用类型来说，不可变说的是变量当中的地址值不可改变
/*
对于成员变量来说，如果使用final 关键字修饰，那么这个变量也照样是不可变。
1 由于成员变量具有默认值，所以用了final之后必须手动赋值，不会再给默认值了。
2 对于final的成员变量，要么直接赋值，要么通过构造方法赋值。二选一。
3 必须保证类当中所有的重载的构造方法，都最终会对final的成员变量进行赋值。
 */

## Day11-6-7    0314 22:16

/*
Java中有四种权限修饰符：
                                   public  >  protected  >  (default)  >  private
同一个类 (我自己)            yes    	   yes 	          yes          yes
同一个包（我邻居）        yes    	   yes                   yes          no
不同包子类（我儿子）    yes   	    yes                  no           no
不同包非子类（陌生人）  yes  	     no                    no           no
注意事项：（default)并不是关键字“default"，而是根本不写
 */

### Day11-8-9    0314 22:38 成员内部类 与局部内部类

/*
如果一个事物的内部包含另一个事物，那么这就是一个类内部包含另一个类。
例如：身体和心脏的关系。又如：汽车和发动机的关系。
分类：
1 成员内部类
2 局部内部类（包含匿名内部类）
成员内部类的定义格式：
修饰符 class 外部类名称 {
      修饰符 class 内部类名称 {
            //...
       }
       //...
}
#### 注意：内用外，随意访问；外用内，需要内部类对象。    
如何使用成员内部类？有两种方式：
 1 间接使用：在外部类的方法当中，使用内部类：然后main只是调用外部类的方法。
 2 直接方式：公式：
 类名称 对象名=new 类名称（）；
 【外部类名称.内部类名称  对象名= new 外部类名称（）.new 内部类名称（）；】
 */

### Day11-10    0315 13:30

//如果出现了重名现象，那么格式是：外部类名称.this.外部类成员变量名
 //外部类名称.内部类名称 对象名 = new 外部类名称（）.new 内部类名称（）；

### Day11-11    0315 13:40  局部内部类

/*
如果一个类是定义在一个方法内部的，那么这就是一个局部内部类。
“局部”：只有当前所属的方法才能使用它，出了这个方法外面就不能用了。

定义格式：
修饰符 class 外部类名称 {
    修饰符 返回值类型 外部类方法名称（参数列表）{
            class 局部内部类名称 {
                //。。。
            }
     }
}

小结一下类的权限修饰符：
public > protected > (default) > private
定义一个类的时候，权限修饰符规则 ：
1 外部类： public  / (default)
2 成员内部类： public /protected / (default) / private
3 局部内部类： 什么都不能写
 */

### Day11-12    0315 13:54

/*
局部内部类，如果希望访问所在方法的局部变量，那么这个局部变量必须是【有效final】
备注：从Java 8+开始，只要局部变量事实不变，那么final关键字可以省略。
原因：
1 new 出来的对象在堆内存当中。
2 局部变量是跟着方法走的，在栈内存当中。
3 方法运行结束之后，立刻出栈，局部变量就会立刻消失。
4 但是new出来的对象会在堆当中持续存在，直到垃圾回收消失。
 */

### Day11-13    0315 14:03 最重要的：匿名内部类

### Day11-14    0315 14:20-14:40

/*
如果接口的实现类（或者是父类的子类），只需要使用唯一的一次。
那么这种情况下就可以省略掉该类的定义，而改为使用【匿名内部类】。
匿名内部类的定义格式：
接口名称 对象名 = new 接口名称（）{
    //覆盖重写所有抽象方法
};

对格式“new 接口名称（）{……}”进行解析：
1 new 代表创建对象的动作
2 接口名称就是匿名内部类需要实现哪个接口
3 {……}这才是匿名内部类的内容
另外还要注意几点问题：
1 匿名内部类，在创建对象的时候，只能使用唯一一次。
如果希望多次创建对象，而且类的内容一样的话，那么就必须使用单独定义的实现类了。
2 匿名对象，在【调用方法】的时候，只能调用唯一一次。
如果希望同一个对象，调用多次方法，那么必须给对象起个名字。
3 匿名内部类是省略了【实现类/子类名称】，但是匿名对象是省略了【对象名称】
强调：匿名内部类和匿名对象不是一回事！！！
 */

Day11-15    0315 15:02-15:14
Day11-16    0315 16:36
Day11-17    0315 
Day11-18-20    0315 17:06



### 快捷键：

添加空行 shift + enter

复制Ctrl+D：无论光标在一行的哪个位置，按ctrl+d，都可以在下方复制一行同样的代码。
移动 Ctrl+Shift+↑/↓ 或者 Alt+Shift+↑/↓：那就是Ctrl+Shift+↑/↓移动的其实是语句，而 Alt+Shift+↑/↓ 任何情况下都移动的是行。
删除Ctrl+Y

IntelliJ Idea 常用快捷键列表
Ctrl+Shift + Enter，语句完成
“！”，否定完成，输入表达式时按 “！”键
Ctrl+E，最近的文件
Ctrl+Shift+E，最近更改的文件
Shift+Click，可以关闭文件
Ctrl+[ OR ]，可以跑到大括号的开头与结尾
Ctrl+F12，可以显示当前文件的结构
Ctrl+F7，可以查询当前元素在当前文件中的引用，然后按 F3 可以选择
Ctrl+N，可以快速打开类
Ctrl+Shift+N，可以快速打开文件
Alt+Q，可以看到当前方法的声明
Ctrl+P，可以显示参数信息
Ctrl+Shift+Insert，可以选择剪贴板内容并插入
Alt+Insert，可以生成构造器/Getter/Setter等
Ctrl+Alt+V，可以引入变量。例如：new String(); 自动导入变量定义
Ctrl+Alt+T，可以把代码包在一个块内，例如：try/catch
Ctrl+Enter，导入包，自动修正
Ctrl+Alt+L，格式化代码
Ctrl+Alt+I，将选中的代码进行自动缩进编排，这个功能在编辑 JSP 文件时也可以工作
Ctrl+Alt+O，优化导入的类和包
Ctrl+R，替换文本
Ctrl+F，查找文本
Ctrl+Shift+Space，自动补全代码
Ctrl+空格，代码提示（与系统输入法快捷键冲突）
Ctrl+Shift+Alt+N，查找类中的方法或变量
Alt+Shift+C，最近的更改
Alt+Shift+Up/Down，上/下移一行
Shift+F6，重构 – 重命名
Ctrl+X，删除行
Ctrl+D，复制行
Ctrl+/或Ctrl+Shift+/，注释（//或者/**/）
Ctrl+J，自动代码（例如：serr）
Ctrl+Alt+J，用动态模板环绕
Ctrl+H，显示类结构图（类的继承层次）
Ctrl+Q，显示注释文档
Alt+F1，查找代码所在位置
Alt+1，快速打开或隐藏工程面板
Ctrl+Alt+left/right，返回至上次浏览的位置
Alt+left/right，切换代码视图
Alt+Up/Down，在方法间快速移动定位
Ctrl+Shift+Up/Down，向上/下移动语句
F2 或 Shift+F2，高亮错误或警告快速定位
Tab，代码标签输入完成后，按 Tab，生成代码
Ctrl+Shift+F7，高亮显示所有该文本，按 Esc 高亮消失
Alt+F3，逐个往下查找相同文本，并高亮显示
Ctrl+Up/Down，光标中转到第一行或最后一行下
Ctrl+B/Ctrl+Click，快速打开光标处的类或方法（跳转到定义处）
Ctrl+Alt+B，跳转到方法实现处
Ctrl+Shift+Backspace，跳转到上次编辑的地方
Ctrl+O，重写方法
Ctrl+Alt+Space，类名自动完成
Ctrl+Alt+Up/Down，快速跳转搜索结果
Ctrl+Shift+J，整合两行
Alt+F8，计算变量值
Ctrl+Shift+V，可以将最近使用的剪贴板内容选择插入到文本
Ctrl+Alt+Shift+V，简单粘贴
Shift+Esc，不仅可以把焦点移到编辑器上，而且还可以隐藏当前（或最后活动的）工具窗口
F12，把焦点从编辑器移到最近使用的工具窗口
Shift+F1，要打开编辑器光标字符处使用的类或者方法 Java 文档的浏览器
Ctrl+W，可以选择单词继而语句继而行继而函数
Ctrl+Shift+W，取消选择光标所在词
Alt+F7，查找整个工程中使用地某一个类、方法或者变量的位置
Ctrl+I，实现方法
Ctrl+Shift+U，大小写转化
Ctrl+Y，删除当前行


Shift+Enter，向下插入新行
psvm/sout，main/System.out.println(); Ctrl+J，查看更多
Ctrl+Shift+F，全局查找
Ctrl+F，查找/Shift+F3，向上查找/F3，向下查找
Ctrl+Shift+S，高级搜索
Ctrl+U，转到父类
Ctrl+Alt+S，打开设置对话框
Alt+Shift+Inert，开启/关闭列选择模式
Ctrl+Alt+Shift+S，打开当前项目/模块属性
Ctrl+G，定位行
Alt+Home，跳转到导航栏
Ctrl+Enter，上插一行
Ctrl+Backspace，按单词删除
Ctrl+”+/-”，当前方法展开、折叠
Ctrl+Shift+”+/-”，全部展开、折叠
【调试部分、编译】
Ctrl+F2，停止
Alt+Shift+F9，选择 Debug
Alt+Shift+F10，选择 Run
Ctrl+Shift+F9，编译
Ctrl+Shift+F10，运行
Ctrl+Shift+F8，查看断点
F8，步过
F7，步入
Shift+F7，智能步入
Shift+F8，步出
Alt+Shift+F8，强制步过
Alt+Shift+F7，强制步入
Alt+F9，运行至光标处
Ctrl+Alt+F9，强制运行至光标处
F9，恢复程序
Alt+F10，定位到断点
Ctrl+F8，切换行断点
Ctrl+F9，生成项目
Alt+1，项目
Alt+2，收藏
Alt+6，TODO
Alt+7，结构
Ctrl+Shift+C，复制路径
Ctrl+Alt+Shift+C，复制引用，必须选择类名
Ctrl+Alt+Y，同步
Ctrl+~，快速切换方案（界面外观、代码风格、快捷键映射等菜单）
Shift+F12，还原默认布局
Ctrl+Shift+F12，隐藏/恢复所有窗口
Ctrl+F4，关闭
Ctrl+Shift+F4，关闭活动选项卡
Ctrl+Tab，转到下一个拆分器
Ctrl+Shift+Tab，转到上一个拆分器
【重构】
Ctrl+Alt+Shift+T，弹出重构菜单
Shift+F6，重命名
F6，移动
F5，复制
Alt+Delete，安全删除
Ctrl+Alt+N，内联
【查找】
Ctrl+F，查找
Ctrl+R，替换
F3，查找下一个
Shift+F3，查找上一个
Ctrl+Shift+F，在路径中查找
Ctrl+Shift+R，在路径中替换
Ctrl+Shift+S，搜索结构
Ctrl+Shift+M，替换结构
Alt+F7，查找用法
Ctrl+Alt+F7，显示用法
Ctrl+F7，在文件中查找用法
Ctrl+Shift+F7，在文件中高亮显示用法

 * 

 * swich注意事项

 * 1 值 不可以

 * 2 只有四种基本类型和两种引用数据类型

 * 基本：byte/short/char/int

 * 引用：String字符串、enum枚举

 * 3 顺序可颠倒，break可以省略，但会穿透；

   

   

   ![image-20211112171605066](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112171605066.png)

![image-20211112171130555](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112171130555.png)

![image-20211112171924656](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112171924656.png)

![image-20211112172328182](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112172328182.png)

![image-20211112172346290](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112172346290.png)





![image-20211112181752052](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112181752052.png)





![image-20211112181902469](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112181902469.png)



![image-20211112182253102](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112182253102.png)

![image-20211112182453540](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112182453540.png)

![image-20211112182503411](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112182503411.png)

![image-20211112182615402](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112182615402.png)

![image-20211112182843548](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112182843548.png)

![image-20211112183049565](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112183049565.png)

![image-20211112183315123](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211112183315123.png)

