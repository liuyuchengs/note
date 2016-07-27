+ 视图(虚拟表)
  + 视图是一个虚拟表，将视图中定义的sql语句执行结果作为表
  + 视图能实现复杂sql查询语句的封装重用
  + 视图一般只做查询使用，update,insert等操作不建议
  + 定义视图

        CREATE VIEW alluser AS
        SELECT u.*,t.access_token FROM user AS u LEFT JOIN user_token AS t ON u.id = t.user_id;
  + 使用视图

        SELECT access_token FROM alluser WHERE id = 100014;
+ 触发器(事件)
  + 触发器是针对数据表的，只能用在数据表上
  + 触发器只能在update,insert,delete操作语句中有效
  + 每种操作语句可分别设置before,after两个触发器

        delimiter //
        CREATE TRIGGER afterInsert AFTER INSERT on uokang.money
        FOR EACH ROW 
        begin
        DECLARE result CHAR(10);
        SELECT 'add a row' into result ; 
        end //
        delimiter ;
  + 删除触发器

        DROP TRIGGER afterInsert;
+ 事务
  + 事务可以将多条sql作为一个整体提交，若其中有某条语句出错时，整个事务内的sql语句均会回滚
  + 事务确保了数据的一致性
  + mysql只有InnoDB引擎支持事务

        START TRANSACTION;
        insert into money(money,editTime) values(124,now());
        delete from money where id = 10;
        commit;
  + rollback到指定savepoint

        START TRANSACTION;
        savepoint first;
        insert into money(money,editTime) values(124,now());
        delete from money where id = 10;
        rollback to first;



