+ Immediate和Timeout
  + Immediate：将执行函数添加到调用栈中，等待执行,node.js的异步回调均是使用该方法
  + Timeout：将执行函数延迟指定时间后执行

+ create
  + setImmediate(callback)：创建一个Immediate实例，将callback添加到执行栈中，等待执行

        console.log("immediate start:"+Date.now());
        setImmediate(()=>{
            console.log(Date.now());
            console.log("immediate is doing");
        })
  + setTimeout(callback,delay,[..arg])：创建一个Timeout实例，delay毫秒后执行callback，可为callback传入实参[..arg]

        console.log("timeout start:"+Date.now());
        setTimeout(function(info) {
            console.log(info+Date.now());
        }, 2000,"timeout is doing");
  + setInterval(callback,delay,[...arg])：创建一个Interval实例，每delay毫秒都会执行一次callback,同样可传入[...arg]作为实参

        console.log("interval start:"+Date.now());
        setInterval(function(info) {
            console.log(info+Date.now());
        }, 2000,"interval is doing");
+ cancel
  + clearImmediate(immediate)：取消一个immediate对象
  + clearInterval(interval)/clearTimeout(timeout)：取消interval和timeout

        var interval = setInterval(function(info) {
            console.log(info+Date.now());
            console.log("cancel interval:");
            clearInterval(interval);
        }, 2000,"interval is doing");