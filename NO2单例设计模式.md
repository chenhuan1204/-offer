##单例模式有 3 个特点：

1. 单例类只有一个实例对象；
2. 该单例对象必须由单例类自行创建；
3. 单例类对外提供一个访问该单例的全局访问点；

###单例模式的实现
>Singleton 模式通常有两种实现形式

> 第 1 种：懒汉式单例

该模式的特点是类加载时没有生成单例，只有当第一次调用 getlnstance 方法时才去创建这个单例。
代码如下：
 
```java

public class LazySingleton
{
    private static volatile LazySingleton instance=null;    //保证 instance 在所有线程中同步
    private LazySingleton(){}    //private 避免类在外部被实例化
    public static synchronized LazySingleton getInstance()
    {
        //getInstance 方法前加同步
        if(instance==null)
        {
            instance=new LazySingleton();
        }
        return instance;
    }
}

```

注意：如果编写的是多线程程序，则不要删除上例代码中的关键字 volatile 和 synchronized，否则将存在线程非安全的问题。如果不删除这两个关键字就能保证线程安全，但是每次访问时都要同步，会影响性能，且消耗更多的资源，这是懒汉式单例的缺点。

>第 2 种：饿汉式单例

	该模式的特点是类一旦加载就创建一个单例，保证在调用 getInstance 方法之前单例已经存在了。 
```java
public class HungrySingleton
{
    private static final HungrySingleton instance=new HungrySingleton();
    private HungrySingleton(){}
    public static HungrySingleton getInstance()
    {
        return instance;
    }
}

/**
* 四种饱汉
*/

// 饱汉0，优点是不会浪费空间，缺点是多线程下会重复创建，造成问题
class Singleton0{

	private static Singleton0 instance = null;

	private Singleton0(){}

	public static Singleton0 getInstance(){
		if(instance == null)
			instance = new Singleton0();
		return Singleton0.instance;
	}

}

// 饱汉1，优点是解决了线程安全问题，缺点是 synchronized 修饰整个方法，多线程抢锁浪费时间
class Singleton1{

	private static Singleton1 instance = null;

	private Singleton1(){}

	public synchronized static Singleton1 getInstance(){
		if(instance == null)
			instance = new Singleton1();
		return Singleton1.instance;
	}
}

// 饱汉2, double check,优点是将同步代码块细粒度话，缺点是如果一个线程刚分配完空间还没有进行初始化，可能就被另一个线程拿去用了
class Singleton2{

	private static Singleton2 instance = null;

	private Singleton2(){}

	public static Singleton2 getInstance(){
		if(instance == null){
			synchronized(Singleton2.class){
				if(instance == null)
					instance = new Singleton2();
			}
		}
		return instance;
	}
}

// 饱汉3，改进版 double check，优点是一定程度上解决了原版的问题，缺点是如果遇到反射还是不能根本上解决不暴露构造函数的问题
class Singleton3{

	private static volatile Singleton3 instance = null;

	private Singleton3(){}

	public static Singleton3 getInstance(){
		if(instance == null){
			synchronized(Singleton3.class){
				if(instance == null)
					instance = new Singleton3();
			}
		}
		return instance;
	}
}

/**
* 静态内部类版
* 优点是：
* 1. 有饿汉的优点，static 关键字只会初始化一次
* 2. 静态内部类的优点在于只有在外部类调用 getInstance 时才会进行内部类的初始化。
* 3. 解决了反射的问题
*/
class Singleton{

	private Singleton(){}

	private static class InstanceHolder{
		private final static Singleton instance = new Singleton();
	}

	public static Singleton getInstance(){
		return InstanceHolder.instance;
	}

}

/**
* 枚举类
* 优点是：
* 除了防止了反射，还能防止反序列化重新创建新的对象的问题，最提倡的写法
*/
class Singleton{

	private Singleton{}

	private static enum SingletonEnum{

		INSTANCE;

		private Singleton instance;

		private SingletonEnum(){
			singleton = new Singleton();
		}

		public Singleton getInstance(){
			return instance;
		}

	}

	public static Singleton getInstance(){
		return SingletonEnum.Instance.getInstance;
	}
}
 ```
	饿汉式单例在类创建的同时就已经创建好一个静态的对象供系统使用，以后不再改变，所以是线程安全的，可以直接用于多线程而不会出现问题。 


