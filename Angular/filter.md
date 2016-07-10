+ 定义filter
  + filter定义在模块上，其作用域在模块内
  + filter返回一个过滤函数，第一个参数为需要过滤的元素，其后为传入实参

        app.filter("DefaultImg",function(){
          return function(input,type){
            if(type==="doc"){
              input = "../contents/img/doc-head.png";
            }
            if(type==="pro"){
              input = "../contents/img/p_defaualt.png"
            }
            return input;
          }
        })
+ 使用filter
  + view中使用filter时， 在表达式中使用"|"标记使用过滤器，参数放置在":"后，多参数使用多个":"

        //user为$scope作用域上的对象
        ng-src="{{user.face|DefaultImg:user}}"
  + 在控制器中使用，添加filter依赖

        $scope.user.face = $filter("DefaultImg")($scope.user.face,"doc");
