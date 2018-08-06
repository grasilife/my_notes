# 浅拷贝和深拷贝

## <a name="xh21kz"></a>概念
<span data-type="color" style="color:rgb(0, 0, 0)"><span data-type="background" style="background-color:rgba(255, 255, 255, 0.8)">浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存。但深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象。</span></span>
## <a name="ourgay"></a>浅拷贝的实现方式
1. __简单地复制语句__
2. __Object.assign()__
## <a name="66k4qp"></a>深拷贝的实现方式
1. __手动复制__
2. <strong>对象只有一层的话可以使用上面的：</strong><strong><code>Object.assign()函数</code></strong>
3. __转成 JSON 再转回来__
4. __递归拷贝__
5. __使用Object.create()方法__
6. __jquery使用__`$.extend`
7. __lodash使用__`_.cloneDeep`



[https://blog.csdn.net/fungleo/article/details/54931379](https://blog.csdn.net/fungleo/article/details/54931379)


