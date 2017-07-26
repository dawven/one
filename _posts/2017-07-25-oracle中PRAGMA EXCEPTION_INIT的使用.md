---
layout: post
title: "oracle中PRAGMA EXCEPTION_INIT的用法"
date: 2017-07-25 
description: "plsql，数据库，笔记"
tag: oracle，笔记，plsql
---  
学习plsql时遇到一道练习题，我需要的只是报错的不执行，直接跳到下一语句。
如果要处理未命名的内部异常，必须使用OTHERS异常处理器或PRAGMA EXCEPTION_INIT 。PRAGMA由编译器控制，或者是对于编译器的注释。PRAGMA在编译时处理，而不是在运行时处理。EXCEPTION_INIT告诉编译器将异常名 与oracle错误码结合起来，这样可以通过名字引用任意的内部异常，并且可以通过名字为异常编写一适当的异常处理器。  

在子程序中使用EXCEPTION_INIT的语法如下：
　　`PRAGMA EXCEPTION_INIT(exception_name, -Oracle_error_number);`
　　
在该语法中，异常名是声明的异常，下例是其用法：
```sql
　　DECLARE
　　deadlock_detected EXCEPTION;
　　PRAGMA EXCEPTION_INIT(deadlock_detected, -60);
　　BEGIN
　　... -- Some operation that causes an ORA-00060 error
　　EXCEPTION
　　WHEN deadlock_detected THEN
　　-- handle the error
　　END;
```

下面是做练习的一道题，具体分析一下：  
创建一个程序，更改JOBS表内最小和最大工资
   a.创建一个存储过程UPD_SAL来更新JOBS表一个特定job_id的最小工资和最大工资，    传递三个参数给过程：工作编号，新最小工资，新最大工资。增加例外处理无效的的工作编号。当然，当最大工资小于最小工资，抛出一个例外。如果jobs表中数据被锁或者无法改变则在窗口中显示合适的消息；  
```sql
CREATE OR REPLACE PROCEDURE upd_sal(p_jobid  IN jobs.job_id%TYPE,
                                    p_minsal IN jobs.min_salary%TYPE,
                                    p_maxsal IN jobs.max_salary%TYPE) IS 
                                    --存储过程需要的参数输入
  v_dummy VARCHAR2(1);
  e_resource_busy EXCEPTION;
  sal_error       EXCEPTION;
  PRAGMA EXCEPTION_INIT(e_resource_busy, -54);
  --PRAGMA在编译时处理，而不是在运行时处理。EXCEPTION_INIT告诉编译器将异常名 与oracle错误码结合起来
BEGIN
  IF (p_maxsal < p_minsal) THEN
    dbms_output.put_line('错误，最大工资应该大于最小工资');
    RAISE sal_error;
  END IF;
  SELECT ''
    INTO v_dummy
    FROM jobs
   WHERE job_id = p_jobid
     FOR UPDATE OF min_salary NOWAIT;
  UPDATE jobs
     SET min_salary = p_minsal, max_salary = p_maxsal
   WHERE job_id = p_jobid;
EXCEPTION
  WHEN e_resource_busy THEN
    raise_application_error(-20001,'job信息被锁住了，请待会再试');
  WHEN no_data_found THEN
    raise_application_error(-20001, '这个job ID 不存在！');
  WHEN sal_error THEN
    raise_application_error(-20001,'数据错误..最大工资应该大于最小工资');
END upd_sal;
```








