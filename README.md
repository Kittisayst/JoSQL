# ຍີນດີຕ້ອນຮັບສູ່ JoSQL Library 
Library ທີ່ຊ່ວຍໃຫ້ຂຽນຄຳສັ່ງຈັດການຖານຂໍ້ມູນງ່າຍ ແລະ ສະດວກວ່ອງໄວ ພັດທະນາໂດຍ :man_teacher: `ອຈ ກິດຕິໄຊ ແສງທອງ`
# I. ວິທີການຕິດຕັ້ງ
1. ຄິດຂວາ Libraries > Add JAR/Folder
2. ເລືອກໄຟລ໌ JoSQL.jar
# II. ວິທີການໃຊ້ງານ
1. ສ້າງ Object ຈາກ Class JoSQL

``` java
JoSQL sql = new JoSQL(connect, TableName);
```
* `connect` :point_right: ໝາຍເຖິງການເຊື່ອມຕໍ່ຖານຂໍ້ມູນ
* `TableName` :point_right: ໝາຍເຖິງຊື່ຂອງຕາຕະລາງໃນຖານຂໍ້ມູນ
## ຕົວຢ່າງ
```java
JoConnentMySQL con = new JoConnentMySQL("localhost", "root", "123", "db_eample");
JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
 ```
# III. ວິທີການໃຊ້ງານຄຳສັ່ງ JoSQL (CRUD)
* ໂຄງສ້າງຕາຕະລາງຕົວຢ່າງ

| # | Field | Type | length | Null | Index |
| :--: | :-- | :--: | :--: | :--: | :--: |
| 1 | u_id | int | 10 | :negative_squared_cross_mark: | PK |
| 2 | u_name | varchar | 255 | :white_check_mark: |  |
| 3 | password | varchar | 255 | :white_check_mark: |  |

* ຂໍ້ມູນໃນຕາຕະລາງ

| u_id | u_name | password |
| :--: | :--: | :--: |
| 1 | admin | 123 |
| 2 | user1 | u111 |
| 3 | user2 | u222 |
