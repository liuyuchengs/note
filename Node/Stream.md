+ Stream
  + nodejs的Stream是基于事件机制的
  + 所有数据的传输均是通过Stream以Buffer的形式
  + 包含有Writable,Readable,Duplex,Transform
  + 
+ Stream.Writable：输出流
  + 以下均均会创建Writable类的实例

        HTTP requests, on the client
        HTTP responses, on the server
        fs write streams
        zlib streams
        crypto streams
        TCP sockets
        child process stdin
        process.stdout, process.stderr
  + setDefaultEncoding(encoding)：设置默认的编码格式

        var fs = require("fs");
        const ws = fs.createWriteStream("text.txt");
        ws.setDefaultEncoding("utf8");
  + write(chunk,[encoding],[callback])：向输出流中写入数据

        const fs = require("fs");
        const ws = fs.createWriteStream("write.txt");
        ws.write("start write...");
        ws.write("data...");
  + end(chunk,[encoding],[callback])：结束输出流,触发finish事件

        ws.end("write end");
  + error事件：抛出异常时触发

        ws.on("error",(err)=>{
            console.log(err);
        })


+ Stream.Readable：输入流
  + 以下均会创建Readable类的实例

        HTTP responses, on the client
        HTTP requests, on the server
        fs read streams
        zlib streams
        crypto streams
        TCP sockets
        child process stdout and stderr
        process.stdin
  + data事件:开始读取数据

        rs.on("data",(data)=>{
            console.log(data.toString());
        })
  + error事件：抛出异常时触发

        ws.on("error",(err)=>{
            console.log(err);
        })
  + pause()/resume()：暂停/恢复读取数据
  + isPaused：判断流是否是暂停状态

        rs.pause();
        if(rs.isPasue()){
            rs.resume();
        }
  + pipe()：和输出流组成管道，读取数据大于写入数据时，溢出的数据暂放在内存中

        const fs = require("fs");
        fs.createReadStream("text.txt").pipe(fs.createWriteStream("dest.txt"));

