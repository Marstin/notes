#### 一. 类初始化
首先定义测试类Test.java，定义静态变量、代码块、静态代码块、构造函数和静态方法 ：
```java
package org.test.classload;

public class Test {
	public static int static_var = 10;

	static {
		static_var += 10;
		System.out.println("Test       static block static_var: " + static_var);
	}

	public Test(){
		static_var += 10;
		System.out.println("Test       variable static_var: " + static_var);
	}

	public static void print(){
		static_var += 10;
		System.out.println("Test   	    Function static_var: " + static_var);
	}

	{
		static_var += 10;
		System.out.println("Test       block static_var: " + static_var);
	}
}
```
然后调用Test类中静态方法：
```java
package org.test.classload;

public class Main {
	public static void main(String[] args){
		Test.print();
	}
}
```
结果为：
```
Test       static block static_var: 20
Test       Function static_var: 30
```
从结果中可以看到静态块中的static_var的值是10，证明这时候静态变量static_var是已经完成了赋值的，所以加载优先级应该是 **静态变量>静态代码块**。
#### 二. 类实例化
由于上述例子中该类没有被实例化的，我们看不到非静态块和构造方法的加载表现。接下来，我们修改Main类中的代码，来测试非静态块和构造函数的加载顺序。
```java
package org.test.classload;

public class Main {
	public static void main(String[] args){
		Test test = new Test();
		Test.print();
	}
}
```
结果为：
```
Test       static block static_var: 20
Test       block static_var: 30
Test       variable static_var: 40
Test       Function static_var: 50
```
在这里，我们可以看到，首先静态变量被初始赋值为10；然后执行静态块，值变为20；接下来执行非静态块的代码，值再加10；当以上完成之后，类加载完成才开始实例化对象，执行类的构造函数。所以，我们判断执行优先级是 **静态变量>静态代码块>代码块>构造函数**。
#### 三. 全局变量
现在我们在Test类中添加非静态的全局变量及其赋值方法，观察该变量在类加载过程中，静态变量的赋值。
##### Test.java
```java
package org.test.classload;

public class Test {
	public static int static_var = getStaticValue();
	public int var = getValue();

	public static int getStaticValue(){
		static_var += 10;
		System.out.println("Test       getStaticValue: " +
			static_var);
		return static_var;
	}

	public int getValue(){
		static_var += 10;
		System.out.println("Test       getValue: " +
			static_var);
		return static_var;
	}

	static {
		static_var += 10;
		System.out.println("Test       static block static_var: " +
			static_var);
	}

	public Test(){
		static_var += 10;
		System.out.println("Test       variable static_var: " +
			static_var);
	}

	public static void print(){
		static_var += 10;
		System.out.println("Test       Function static_var: " +
			static_var);
	}

	{
		static_var += 10;
		System.out.println("Test       block static_var: " +
			static_var);
	}
}
```
##### Main.java
```javascript
package org.test.classload;

public class Main {
	public static void main(String[] args){
		Test test = new Test();
	}
}
```
结果为:
```
Test       getStaticValue: 10
Test       static block static_var: 20
Test       getValue: 30
Test       block static_var: 40
Test       variable static_var: 50
```
这里可以看到，这里执行的优先级依次是，**静态变量初始化>静态块>全局变量初始化>非静态块>构造函数**
#### 四. 静态变量之间的顺序
定义三个静态全局变量，给中间变量赋值，然后在前后两个变量初始化方法中设置取中间变量的方法。具体代码如下所示：
##### Test.java
```java
package org.test.classload;

public class Test {
	public static Test instance1 = new Test("instance1");

	public static int static_var = 10;

	public static Test instance2 = new Test("instance2");

	public static void getValue(){
		System.out.println("Test       getValue static_var: " +
			static_var);
	}

	public Test(String name){
		System.out.println("Test       " + name + " Constructor
			static_var: " + static_var);
	}
}
```
##### Main.java
```java
package org.test.classload;

public class Main {
	public static void main(String[] args){
		Test.getValue();
	}
}
```
执行结果如下所示：

```
Test       instance1 Constructor static_var: 0
Test       instance2 Constructor static_var: 10
Test       getValue static_var: 10
```
可以看到静态变量是按照**从上往下顺序**初始化的
