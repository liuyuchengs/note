+ Json方式提交
  + Content-Type:application/json
  + angularjs：angularjs默认使用json的方式提交数据，直接post js对象即可

        var params = {
            name:"tom",
            age:12
        }
        $http.post(url,params)
        //chrome调试显示
        Request payLoad:
        {name: "tom", age: 12}
  + jquery：jquery需要使用post json字符串,并设置contentType

        var params = {
            name:"toms",
            age:13
        }
        $.ajax({
            url:"/post",
            contentType:"application/json;charset=UTF-8",
            data:JSON.stringify(params),
            type:"POST",
        })
        //chrome调试显示
        Request payLoad:
        {name: "toms", age: 13}
+ form 方式
  + Content-Type:application/x-www-form-urlencoded，需要传入查询字符串，然后会转换成form data
  + angularjs：需要post 拼接字符串，并设置ContentType

        var params = "name=tom&age=12";
        $http.post(url,params,{
            headers: {
			   'Content-type':'application/x-www-form-urlencoded;charset=UTF-8',
			 }
        })
        //chrome调试显示
        Form date:
        name:tom
        age:12
  + jquery：jquery默认使用form方式提交数据
+ 传输文件
  + Content-Type:multipart/form-data
  + 使用表单时，设置enctype="multipart/form-data"
  + angularjs要设置Content-Type:undifend,jquery设置Content-type为false
+ FormData
  + FormData能够以表单key/value的方式表示数据，并可以作为ajax的提交数据
  + angularjs：直接postFormData对象,默认以json方式提交FormData数据

        var formData = new FormData();
        formData.append("name","tom");
        $http.post(url,formData,{})
  + jquery：需要设置processData为false，不允许jquery对数据进行处理，默认以form方式提交FormData数据

        var formData = new FormData();
        formData.append("name","age");
        $.ajax({
            url:"/post",
            data:formData,
            type:"POST",
            processData : false,
            contentType : false, //jquery不对contentType做处理
        })
  + 两者均可以使用form和json方式提交，FormData数据不会有改变
  
        //angularjs以form方式提交formData数据
        $http.post(url,formData,{
            headers: {
			   'Content-type':'application/x-www-form-urlencoded;charset=UTF-8',
			 }
        })