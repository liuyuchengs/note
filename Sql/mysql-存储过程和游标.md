+ 简单的存储过程
  + 存储过程是一系列的SQL语句集合，类似于批处理

        DELIMITER //
        CREATE PROCEDURE avgprice()
        BEGIN
                SELECT AVG(stand_price) as avgprice FROM product;
        END //
        DELIMITER ;
  + 使用存储过程

        CALL avgprice();
        // 输出
        avgprice
        '10688.866608946608'
  + 删除存储过程

        DROP PROCEDURE avgprice IF EXISTS;
    
+ 带参数的存储过程
  + 定义参数: <out/in> paramName Type, out->输出参数，in->输入参数

        DELIMITER //
        CREATE PROCEDURE price(
            in start int(5),
            in end int(5),
            out max DECIMAL(8,2),
            out min DECIMAL(8,2)
        )
        BEGIN
            SELECT MAX(stand_price) INTO max FROM product WHERE id BETWEEN start AND end;
            SELECT MIN(stand_price) INTO min FROM product WHERE id BETWEEN start AND end;
        END //
        delimiter ;
  + 使用带参数的存储过程时，变量可以在其他语句中使用

        CALL price(10000,11000,@max,@min);
        SELECT * FROM product WHERE stand_price = @max;
+ 使用流程控制的存储过程
  + sql的流程控制语句:IF...THEN...ELSEIF...THEN...ELSEIF
  + Boolean变量中0表示false，非0表示true

        DELIMITER //
        CREATE PROCEDURE avgprice(
            in discount Boolean,
            out avgprice Decimal(8,2)
        )
        BEGIN
            IF discount THEN
                SELECT avg(stand_price)*0.8 INTO avgprice FROM product;
            ELSE
                SELECT avg(stand_price) INTO avgprice FROM product;
            END IF;
        END //
        delimiter ;
  + 使用存储过程

        // 不使用折扣
        CALL avgprice(0,@avgprice);
        select @avgprice;
+ 游标
  + DECLARE <name> COUSOR：定义游标
  + OPEN <cousor name>：打开游标
  + CLOSE <cousor name>：关闭游标
  + FETCH <cousor name>：从第一行开始，获取当前行的数据

        DELIMITER //
        CREATE PROCEDURE firstprice(
            out first Decimal(8,2)
        )
        BEGIN
            DECLARE first CURSOR
            FOR
            SELECT stand_price FROM product;
            OPEN first;
            FETCH first INTO first;
            CLOSE first;
        END //
        delimiter ;
  + 循环遍历游标标记的数据

        DELIMITER //
        CREATE PROCEDURE endprice(
            out endprice Decimal(8,2)
        )
        BEGIN
            DECLARE done Boolean DEFAULT 0;
            DECLARE end CURSOR
            FOR
            SELECT stand_price FROM product;
            DECLARE CONTINUE HANDLER FOR SQLSTATE '02000' SET done= 1;
            OPEN end;
            REPEAT
            FETCH end INTO endprice;
            UNTIL done END REPEAT;
            CLOSE end;
        END //
        delimiter ;
