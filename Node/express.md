+ 配置express
  + 创建express实例

        var express = require('express');
        var app = express();
  + 输出静态文件

        // public路径下的文件均作为静态文件输出
        app.use(express.static('public'));
        // 创建一个虚拟目录，映射静态文件
        app.use("/static",express.static("./public"));
  + 启动服务

        var server = app.listen(3000, function () {
            console.log("server is run");
        });

+ 路由
  + 路由方法:all,get,post等

        let express = require("express");
        let app = new express();

        app.get("/test",(req,res)=>{
            res.send("hello world");
        })
        app.all("/method",(req,res)=>{
            res.send("all method");
        })
  + 路由路径:可使用字符串，也可使用正则表达式

        // 匹配abc
        app.get("/abc",function(req,res){
            res.send("abc");
        })
        // 匹配 acd 和 abcd
        app.get('/ab?cd', function(req, res) {
            res.send('ab?cd');
        });
  + 多个回调函数,函数传入next参数，函数内使用next()进入下一个回调函数

        function fn1(req,res,next){
            console.log("fn1");
            next();
        }
        function fn2(req,res){
            console.log("fn1");
            res.send("hello");
        }
        app.get("/multer",fn1,fn2);
  + 链式路由：设定一个路径的多个请求方法

        app.route("/book").get((req,res)=>{
            res.send("get");
        }).post((req,res)=>{
            res.send("post");
        })
+ 路由模块化
  + 创建router模块

        // mainRoute.js文件
        let express = require("express");
        let router = express.Router();
        router.get("/book",(req,res)=>{
            res.send("/book get");
        })
        module.exports = router;
  + 使用router模块

        // 导入模块
        let router = require("./routes/mainRoute");
        app.use(router);
+ 关于中间件
  + 中间件是一个函数，函数内可操作request和response对象
  + 中间件可以决定是在此中间件中终结该请求还是通过next()调用下一个中间件来处理

        function fn1(req,res,next){
            if(req.path==="/book"){
                res.send("fn1 end");
            }else{
                next();
            }
        }
        function fn2(req,res){
            res.send("fn2 end");
        }
        router.get("/book",fn1,fn2)
+ 错误中间件
  + 错误中间件必须是四个参数：error,request,response,next
  + 错误中间件一般放置其他中间件的最后，以便处理其他中间件执行期间产生的错误

        app.use((err,req,res,next)=>{
            res.status(500).send("error"+err.message);
        })

