#db #mysql #基本 

| 导出数据            | mysqldump -h 13.228.180.75 -u root -pcKBysYKDGFlQ1CSaHX -P 9101 --databases smooth_talk_halltest > smooth_talk_halltest.sql |
| --------------- | --------------------------------------------------------------------------------------------------------------------------- |
| 导入数据            | mysql -h 13.228.180.75 -P 11030 -unacos -pnacos < smooth_talk_halltest.sql                                                  |
| 显示所有用户          | SELECT User, Host FROM mysql.user;                                                                                          |
| 创建用户，在任何地点都可以登录 | CREATE USER 'nacos'@'%' IDENTIFIED BY 'nacos';                                                                              |
| 给用户赋予所有数据库的全部权限 | GRANT ALL PRIVILEGES ON *.* TO 'nacos'@'%' WITH GRANT OPTION;                                                               |
|                 |                                                                                                                             |
