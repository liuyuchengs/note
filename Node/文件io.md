+ Stream
  + nodejs的Stream是基于事件机制的
  + WriteStream：将二进制数据写入文件

        var fs = require("fs");
        const ws = fs.createWriteStream("text.txt");

        ws.write(new Buffer("hello world"),(err)=>{
            if(err!==null){return err};
            console.log("write success!");
        })
  + ReadStream：通过回调函数来接受读取的数据,数据均已二进制形式

        var rs = fs.createReadStream("test.txt");
        rs.on("data",function(chunk){
            //读取的是二进制数据
            console.log(chunk.toString());
        })
        rs.on("end",function(){
            console.log(" read end");
        })
  + readStream和writeStream可组成一个数据管道，读取数据大于写入数据时，溢出的数据暂放在内存中

        const fs = require("fs");
        fs.createReadStream("text.txt").pipe(fs.createWriteStream("dest.txt"));

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