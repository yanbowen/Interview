# 面试总结01 
<hr>   
  
## DIV  
* DIV是层叠样式表中的定位技术   
  
## 创建线程的两种方式？
* 创建线程的第一种方式：继承Thread类
	* 步骤：
	* （1）定义类继承Thread
	* （2）覆写Thread类中的run方法
	* （3）调用线程的start方法，该方法两个作用：启动线程，调用run方法
* 创建线程的第二种方式：实现Runnable接口
	* 步骤：1.定义类实现Runnable接口；
	* 2.覆盖Runnable接口中的run方法，将线程要运行的代码存放在该run方法中
	* 3.通过Thread类建立线程对象；
	* 4.将Runnable接口的子类对象作为实际参数传递给Thread类的构造函数。new Thread(t)；
	* 5.调用Thread类的start方法开启线程并调用Runnable接口子类的run方法 
## 实现方式和继承方式有什么区别呢？（面试题经常考）
* 实现方式好处：避免了单继承的局限性，如果继承了一个类就不能再继承其他类了，在定义线程时，建议使用实现方式。
* 两种方式区别：
	* 继承Thread线程代码存放Thread子类run方法中
	* 实现Runnable，线程代码存放在接口的子类的run方法
 
## 使用多线程机制会提高程序的运行效率吗？
* 不会，因为多个线程都获取cpu的执行权，cpu执行到谁，谁就运行，明确一点，在某个时刻，只能有一个程序在运行。（多核除外）cpu在做着快速的切换，以达到看上去是同时运行的效果，我们可以形象把多线程的运行行为在互相抢夺cpu的执行权，这就是多线程的一个特性：随机性。即谁抢到谁执行，至于执行多长，cpu说的算。但是这样就好像是一个厨师在一个桌子上做馒头变成不停的换到别的桌子上做馒头，做的效率不会提高，而且性能还会更低。
## 为什么会有多线程下载？
* 多线程运行效率并不会快，但是多线程会抢带宽，比如一个线程10k的下载，我们用20个线程就变成了200K，就是20个线程一起下载，这样就快啦。  
  
## 异步任务加载网络数据——AsyncTask使用  

* Android从1.5开始引入了AsyncTask这个类,AsyncTask内部使用Java 1.5的并发库比普通初级Android开发者编写的Thread+Handler稳定很多
* AsyncTask封装了Thread和Handler，使我们用起来更加方便，不用去关注Handler。由于后台线程不能更新UI，而很多情况下，我们在后台线程做完一件事后，一般都会更新UI，一般我们会这样做：在UI线程创建一个handler对象，在后台线程中发送一条message，再在Handler中去处理这个message，进而更新UI。
* 用了AsyncTask后，我们就不用再去关注Handler了。它定义了三种泛型，分别是Params、Progress和Result，分别表示请求的参数、任务的进度和获得的结果数据。
  
### 使用AsyncTask的好处

    底部封装了线程池技术，其中的方法很容易调用。
    直接调用相关方法，进行UI界面的更新。
    一旦任务多，就不用每次都new新的线程，可以直接使用。  
  
### 实现原理  

* 线程池的创建
	* 在创建了AsyncTask的时候，会默认创建一个线程池ThreadPoolExecutor，并默认创建出5个线程放入到线程池中，最多可防128个线程；且这个线程池是公共的唯一一份。
	
* 任务的执行
	* 在execute中，会执行run方法，当执行完run方法后，会调用scheduleNext()不断的从双端队列中轮询，获取下一个任务并继续放到一个子线程中执行，直到异步任务执行完毕。

* 消息的处理：
	* 在执行完onPreExecute()方法之后，执行了doInBackground()方法，然后就不断的发送请求获取数据；在这个AsyncTask中维护了一个InternalHandler的类，这个类是继承Handler的，获取的数据是通过handler进行处理和发送的。在其handleMessage方法中，将消息传递给onProgressUpdate()进行进度的更新，也就可以将结果发送到主线程中，进行界面的更新了。  
	
### JQuery  
	$("button").click(function(){
	    $.post("demo_test.html",function(data,status){
	        alert("Data: " + data + "nStatus: " + status);
	    });
	});
  
---
## HashTable和HashMap的区别详解
1. HashMap是基于哈希表实现的，每一个元素是一个key-value对，其内部通过单链表解决冲突问题，容量不足（超过了阀值）时，同样会自动增长。  
	* HashMap是非线程安全的，只是用于单线程环境下，多线程环境下可以采用concurrent并发包下的concurrentHashMap。
	* HashMap 实现了Serializable接口，因此它支持序列化，实现了Cloneable接口，能被克隆。
  
2. Hashtable 是线程安全的，能用于多线程环境中（Hashtable同样有上面功能）  

HashTable和HashMap区别  
1、继承的父类不同  

	Hashtable继承自Dictionary类，而HashMap继承自AbstractMap类。但二者都实现了Map接口。
2、线程安全性不同  

	Hashtable 中的方法是Synchronize的，而HashMap中的方法在缺省情况下是非Synchronize的。
	在多线程并发的环境下，可以直接使用Hashtable，不需要自己为它的方法实现同步，但使用HashMap时就必须要自己增加同步处理。

3、是否提供contains方法  

    HashMap把Hashtable的contains方法去掉了，改成containsValue和containsKey，因为contains方法容易让人引起误解。
    Hashtable则保留了contains，containsValue和containsKey三个方法，其中contains和containsValue功能相同。  
  
4、key和value是否允许null值  
 
Hashtable中，key和value都不允许出现null值。  
HashMap中，null可以作为键，这样的键只有一个；可以有一个或多个键所对应的值为null。当get()方法返回null值时，可能是 HashMap中没有该键，也可能使该键所对应的值为null。因此，在HashMap中不能由get()方法来判断HashMap中是否存在某个键， 而应该用containsKey()方法来判断。  
  
5、两个遍历方式的内部实现上不同  

Hashtable、HashMap都使用了 Iterator。而由于历史原因，Hashtable还使用了Enumeration的方式 
  
6、hash值不同  

哈希值的使用不同，HashTable直接使用对象的hashCode。而HashMap重新计算hash值。  
  
7、内部实现使用的数组初始化和扩容方式不同   

HashTable在不指定容量的情况下的默认容量为11，而HashMap为16，Hashtable不要求底层数组的容量一定要为2的整数次幂，而HashMap则要求一定为2的整数次幂    
      
8、HashMap采用快速失败机制，而Hashtable不是   

---    
   
ANR：application not responding
当对输入事件（如按键、触摸屏事件）的响应超过5秒、意图接收者（intentReceiver）超过10秒钟仍未执行完毕时都会报ANR。
Android应用程序完全运行在一个独立的线程中。任何在主线程中运行的，需要消耗大量时间的操作都会引发ANR。因此，需要消耗大量时间的操作如访问网络和数据库，都要放到子线程中或者使用异步请求。

Force Close：
一般像空指针、数组越界、类型转换异常等。可以通过logcat查看抛出异常的代码出现的位置，然后到程序对应代码中进行修改。