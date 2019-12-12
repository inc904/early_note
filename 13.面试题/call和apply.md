## call和apply区别
fn.call(obj,10,20,30)
fn.apply(obj,[10,20,30])

都是function原型的方法，改变this指向；
传参方法不同；

bind 也可以改变this指向，但是不立即执行函数，只是预先处理改变this指向。

性能：参数三个以上 call的性能 好一些
	三个以下，都一样