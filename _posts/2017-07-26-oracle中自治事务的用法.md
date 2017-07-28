---
layout: post
title: "oracle中sql%rowcount的用法"
date: 2017-07-25 
description: "sql，数据库，笔记"
tag: plsql
---  

sql%rowcount用于记录修改的条数，必须放在一个 **更新或者删除等修改类语句**后面执行，select语句用于查询的话无法使用，  
当你执行多条修改语句时，按照sql%rowcount 之前执行的最后一条语句修改数为准。


####其他游标功能
SQL%ROWCOUNT 受最近的SQL语句影响的行数  
SQL%FOUND 最近的SQL语句是否影响了一行以上的数据  
SQL%NOTFOUND 最近的SQL语句是否未影响任何数据  
SQL%ISOPEN 对于隐式游标而言永远为FALSE  







