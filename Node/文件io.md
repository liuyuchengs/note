+ fs文件模块
  + readFile：读取文件，回调接受二进制数据

        fs.readFile("text.txt",(err,data)=>{
            if(err!==null) return err;
            console.log(data.toString());
        })
  + writeFile：写入二进制数据到文件

        fs.writeFile("text.txt",new Buffer("fs writeFile"),(err)=>{
            if(err!==null){
                return err;
            }
            console.log("写入成功!");
        })
  + 同步版本

        var fs = require("fs");
        try{
            var data = fs.readFileSync("test.txt");
            console.log(data.toString());
        }catch(err){
            console.log(err);
        }
+ path
  + normalize:将传入的路径转换成标准的路径
 
            var path = require("path");
            var cache = {};
            function store(key,value){
                cache[path.normalize(key)] = value;
            }
            store("first//second/index",2); //输出{"first/second/index":2}
  + join：拼接路径
 
            var path = require("path");
            var result = path.join("/lib","/test","/index");
  + extname:文件扩展名
 
            var ext = path.extname("script.js");