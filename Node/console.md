+ 关于console
  + console是系统内置的全局模块，不需要使用require导入模块
  + console可输出任何node.js的stream数据

        fs.readFile("text.txt",(err,data)=>{
            if(err!==null){return err};
            console.log(data); //输出二进制流数据
        })
+ 使用console
  + 输出文本时可使用占位符,"$s"->字符,"$d"->数字

        const name = "allen";
        const count = 5;
        console.log("this is %s's pet",name);
        console.log("totle:%d",count);
  + assert：当条件为false时，会使用message参数抛出AssertionError

        const result = false;
        console.assert(result,"it's fail"); //抛出异常
  + time(label)/timeEnd(label)：两个label相同console作为一对，统计两条语句间的执行时间

        console.time("each 100 element");
        for(var i =0;i<100;i++){

        }
        console.timeEnd("each 100 element");
        // print->each 100 element: 0.460ms
  + dir(obj,option)：输出一个对象时，可以设置对象的深度等范围

        const obj = {
            name:"tom",
            age:22,
            children:{
                name:"jack",
                age:1
            }
        }
        console.dir(obj,{depth:0}); //只输出对象的第一层属性
  + log->普通文本,warn->警告,error->错误

        console.log("log text");
        console.warn("warn text");
        console.error("error text");