<h1 align='center'><font color=red>jvm调优</font></h1>

## jvm内存区域
* ### 一、 heap区
  heap区通常称为堆内存，整个堆大小=新生代+老年代。堆内存默认为物理内存的1/64(1<1GB);默认空余堆内存小于40%时，jvm就会增大，一直到-Xmx的最大限制，空余堆内存大于70%时，jvm会减少堆，一直到-Xms的最小限制。
* #### 新生代
 *a) Eden Space（伊甸园）*
 >**Eden Space** 是对象被创建的时候，首先放到该区域。

 *b) Survivor Space（幸存者区）*
 >用于保存 Eden 区经过垃圾回收之后没有被回收的对象。
 **Survivor Space**  有两个：*<font color='graee'>To Survivor</font>* 和 *<font color='graee'>From Survivor</font>*  ，这两个区域空间大小一样。执行垃圾回收后，*<font color='greee'>Edeb Space</font>* 和 *<font color='greee'>From Survivor</font>* 中留下的对象会一起放进 *<font color='gree'>To Survivor</font>*,同时 *<font color='gree'>From Survivor</font>* 被清空，*<font color='graee'>To Survivor</font>* 和 *<font color='graee'>From Survivor</font>* 的标记会互换，始终保证一个 *<font color='gree'>Survivor</font>* 是空的。

* #### 老年代
 *c) Old Gen（老年代）*
 >**Old Gen** 用来存放新生代经过多次垃圾回收仍然存活的对象，或者是新生代分配不了内存的大对象。*（新生代的GC称为 <font color='gree'>Young GC</font> ，<font color='gree'>Young GC</font> 每次完成回收后留下的对象age就会加 1。)*
 当老年代被放满之后，虚拟机会进行垃圾回收，称之为 *<font color='gree'>Major GC</font>* 。*<font color='gree'>Major GC</font>* 。**除了并发GC以外，*<font color='gree'>Major GC</font>* 会对整个heap区域进行扫描和回收 **，也称之为 *<font color='gree'>Full GC</font>* 。


* ### 二、 非heap区
 *d)  Code Cache （代码缓存区）*
 >**Code Cache** 代码缓存区，主要用于存放JIT编译的代码

 *e) Perm Gen （永久代）*
 >**Perm Gen**
