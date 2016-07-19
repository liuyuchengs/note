##### Event
+ 触发事件
  + emit(eventName,[args])：触发eventName事件

        emitter.emit("valueChange");
+ 监听事件
  + node.js中通过EventEmitter类来处理事件
  + on(eventName,listener)：监听eventName事件，每次捕获后调用listener

        emitter.on("on",()=>{
            console.log("emitter is doing");
        })

        emitter.emit("on");
  + once(eventName,listener)：监听eventName事件，只在第一次捕获后调用listener

        emitter.once("on",()=>{
            console.log("emitter is doing"); // 只执行一次
        })

        emitter.emit("on");
        emitter.emit("on");
  + prependListener(eventName,listener)：监听eventName事件，并将listener提交到队列首部

        emitter.on("on",()=>{
            console.log("listener A");
        })
        emitter.prependListener("on",()=>{
            console.log("listener B"); //先执行
        })

        emitter.emit("on");
+ 取消监听
  + removeListener(eventName,listener)：取消eventName事件的指定监听器
  + removeAllListener(eventName)：取消eventName事件的所有监听器

##### Error事件
+ 异常处理
  + try...catch只能捕获同步代码运行时产生的错误，不能捕获异步代码运行时产生的错误
 
        try {
            setTimeout(function(){
                throw new Error("error");
            },1)
        } catch (err) {
            //can not catch it
            console.log(err);
        }
  + 可以将错误处理代码也放到异步中执行
 
        function async(cb, err) {
            setTimeout(function() {
                try {
                    if (true)
                        throw new Error("woops!");
                    else
                        cb("done");
                } catch(e) {
                    err(e);
                }
            }, 2000)
        }
  + node.js的异步异常处理是将异常对象作为第一个参数传入回调函数中

        fs.readFile('/foo.txt', function(err, data) {
            if (err !== null) throw err;
            console.log(data);
        });
+ 异常对象
  + 异常类型：Error,RangeError,ReferenceError,TypeError等

        const error = new Error("this is error");
        const typeError  = new TypeError("this is type error");
  + message：异常对象的异常信息

        const typeError  = new TypeError("this is type error");
        console.log(typeError.message);
  + stack：异常对象的堆栈信息

        console.log(typeError.stack);
+ 抛出异常
  + node.js的异常抛出是基于事件的，通过events模块的EventsEmitter对象来抛出异常

        const events = require("events");
        const em = new events();

        em.emit("error",new TypeError("this is type error"));
  + 通过try...catch...捕获异常

        try{
            em.emit("error",new TypeError("this is type error"));
        }catch(err){
            console.log(err.message);
        }
  + 通过事件捕获

        // 先设定事件监听，再触发事件
        em.on("typeError",(err)=>{
            console.log(err.message);
        })
        em.emit("typeError",new TypeError("this is type error"));
  + 未处理的异常最终会触发uncaughtException事件,可在线程中监听该事件

        process.on("uncaughtException",(err)=>{
            console.log(err.message);
        })
        em.emit("error",new Error("this is type error"));