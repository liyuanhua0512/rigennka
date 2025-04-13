#mongodb #db #基本 

| 连接一个数据库   | mongosh "mongodb://root:s5JqDntfUAu~5kE2iQ@localhost:27017/admin"                                                                     |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 查看当前库所有用户 | db.getUsers()                                                                                                                         |
| 创建一个用户    | use admin  <br>db.createUser({ user: "smooth_hall", pwd: "smooth_hall", roles: [{ role: "readWrite", db: "smooth_talk_halltest" }] }) |
| 创建一个数据库   | use myDatabase  <br>db.myCollection.insertOne({ name: "Alice", age: 25 })                                                             |
| 备份库       | mongodump -h 13.228.180.75:9618 -u flake_user -p --forceTableScan -d snowflake -o ./ --authenticationDatabase admin                   |
| 恢复库       | mongorestore -h 13.228.180.75:9717 -u flake -p -d snowflake ./snowflake --authenticationDatabase admin                                |
|           |                                                                                                                                       |

