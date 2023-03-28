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

| # | Name | Type | Length/Values | Null | Index |
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

## 3.1 ເພີ່ມຂໍ້ມູນ Create / ເພີ່ມຂໍ້ມູນຄົບທຸກ Column
1. ນຳເຂົ້າຄຳສັ່ງ SQL
```java
import java.sql.*;
```
2. ໃຊ້ງານ Method `getCreate();`
```java
JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
  try {
    PreparedStatement pre = sql.getCreate(); // ສົ່ງຄຳສັ່ງ sql ໃຫ້ກັບ PreparedStatement
    pre.setInt(1, 4); // ຄ່າຂອງ u_id
    pre.setString(2, "user3"); // ຄ່າຂອງ u_name
    pre.setString(3, "u333"); // ຄ່າຂອງ password
    pre.executeUpdate(); // ປະມວນຜົນຄຳສັ່ງ sql
   } catch (Exception e) {
      e.printStackTrace();
   }
   ```
   * ອະທິບາຍ: `getCreate();` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
   ```sql
   INSERT INTO tb_user VALUES(4,'user3','u333')
   ```
## 3.2 ເພີ່ມຂໍ້ມູນ Create / ເພີ່ມຂໍ້ມູນສະເພາະ Column ຕາມລຳດັບ
:warning: ໝາຍເຫດ: ກວດສອບ Column ວ່າລະບຸເປັນ :white_check_mark: Null ຖ້າບໍ່ຕ້ອງການເພີ່ມ
1. ນຳເຂົ້າຄຳສັ່ງ SQL
```java
import java.sql.*;
```
2. ໃຊ້ງານ Method `getCreateByColumnIndexs(new int[]{1, 2});`
* `new int[]{1, 2}` ແມ່ນລະບຸບລຳດັບ index ຂອງ Column
* 1 = `u_id` , 2 = `u_name` , 3 = `password` 
* `password` ເຮົາບໍ່ຕ້ອງການເພີ່ມຄ່າເຮົາກໍ່ຈະບໍ່ໄດ້ລະບົບລົງໃນ Array `new int[]{1, 2}`
```java
JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
 try {
  PreparedStatement pre = sql.getCreateByColumnIndexs(new int[]{1, 2});
  pre.setInt(1, 5);
  pre.setString(2, "user3");
  pre.executeUpdate();
 } catch (Exception e) {
  e.printStackTrace();
}
```
 * ອະທິບາຍ: `getCreateByColumnIndexs(new int[]{1, 2}) ` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
```sql
INSERT INTO tb_user(u_id,u_name) VALUES (5,'user3')
```
## 3.3 ເພີ່ມຂໍ້ມູນ Create / ເພີ່ມຂໍ້ມູນສະເພາະ Column ຕາມຊື່ຈອງ Column
:warning: ໝາຍເຫດ: ກວດສອບ Column ວ່າລະບຸເປັນ :white_check_mark: Null ຖ້າບໍ່ຕ້ອງການເພີ່ມ
1. ນຳເຂົ້າຄຳສັ່ງ SQL
```java
import java.sql.*;
```
2. ໃຊ້ງານ Method `getCreateByColumnNames(new String[]{"u_id","password"});`
* new String[]{"u_id","password"}
* 1 = `u_id` , 2 = `u_name` , 3 = `password`
* `u_name` ເຮົາບໍ່ຕ້ອງການເພີ່ມຄ່າເຮົາກໍ່ຈະບໍ່ໄດ້ລະບົບລົງໃນ Array `new String[]{"u_id","password"}`
```java
JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
try {
  PreparedStatement pre = sql.getCreateByColumnNames(new String[]{"u_id","password"});
  pre.setInt(1, 6);
  pre.setString(2, "1234");
  pre.executeUpdate();
 } catch (Exception e) {
  e.printStackTrace();
}
```
 * ອະທິບາຍ: `getCreateByColumnNames(new String[]{"u_id","password"}) ` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
```sql
INSERT INTO tb_user(u_id,password) VALUES (6,'1234')
```
## 3.4 ອ່ານຂໍ້ມູນ Read ຫຼື Select / ອ່ານຂໍ້ມູນທັງໝົດໃນຕາຕະລາງ
1. ເຮົາໃຊ້ Method `getSelectAll();`
```java
JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
try {
  ResultSet rs = sql.getSelectAll();
  while (rs.next()) {
   System.out.println(rs.getInt(1));
   System.out.println(rs.getString(2));
   System.out.println(rs.getString(3));
  }
} catch (Exception e) {
  e.printStackTrace();
}
```
 * ອະທິບາຍ: `getSelectAll();` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
```sql
SELECT * FROM tb_user
```
### Output
`1 admin 123 | 2 user1 u111 | 3 user2 u222`
* rs.getInit(Column Index) ແມ່ນການອ່ານຂໍ້ມູນຕາລຳດັບຂອງ Column
* 1 = `u_id` , 2 = `u_name` , 3 = `password`
* :information_source: ອະທະບາຍ: ຄ່າ parameter ຂອງ Resuset ສາມມາດໃຊ້ຄ່າ Column index ຫຼື ຊື່ຂອງ Column ກໍ່ໄດ້
* :desktop_computer: Ex: `rs.getInt(1)` ຫຼື `rs.getInt("u_id")`
* ເຮົາສາມາດຈັດການກັບຂໍ້ມູນຂອງ Resultset ໄດ້ຕາມຕ້ອງການດັ່ງຈາຈະລາງລຸ່ມນີ້

| Type | Resultset | Example |
| ---- | --------- | ------- |
| int | getInt | rs.getInt(1) |
| String | getString | rs.getString(1) |
| Date | getDate | rs.getDate(1) |
| Double | getDouble | rs.getDouble1) |
| Boolean | getBoolean | rs.getBoolean(1) |

## 3.5 ອ່ານຂໍ້ມູນ Read ຫຼື Select / ອ່ານຂໍ້ມູນຈາກໄອດີ
1. ເຮົາໃຊ້ Method `getSelectByID(1);`
```java
        JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
        try {
            ResultSet rs = sql.getSelectByID(1);
            while (rs.next()) {
                System.out.println(rs.getInt(1));
                System.out.println(rs.getString(2));
                System.out.println(rs.getString(3));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
```
 * ອະທິບາຍ: `getSelectByID(1);` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
```sql
SELECT * FROM tb_user WHERE u_id = '1'
```
### Output
`1 admin 123`
* ອະທິບາຍ getSelectByID(1) ເລກ 1 ແມ່ນໄອດີຂອງຂໍ້ມູນ
## 3.6 ອ່ານຂໍ້ມູນ Read ຫຼື Select / ອ່ານຂໍ້ມູນຕາມ Column Index
1. ເຮົາໃຊ້ Method `getSelectByColumnIndex(ລຳດັບ Column, Value);`
```java
        JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
        try {
            ResultSet rs = sql.getSelectByColumnIndex(2, "admin");
            while (rs.next()) {
                System.out.println(rs.getInt(1));
                System.out.println(rs.getString(2));
                System.out.println(rs.getString(3));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
 ```
  * ອະທິບາຍ: `getSelectByColumnIndex(2, "admin");` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
 ```sql
 SELECT * FROM tb_user WHERE u_name= 'admin'
 ```
 ### Output
`1 admin 123`
* ອະທິບາຍ getSelectByColumnIndex(2, "admin"); 
* `2` ລຳດັບຂອງ Column
* `"admin"` ແມ່ນຂໍ້ມູນທີ່ຕ້ອງການອ່ານ
## 3.7 ອ່ານຂໍ້ມູນ Read ຫຼື Select / ອ່ານຂໍ້ມູນຕາມເງື່ອນໄຂ
```java
        JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
        try {
            ResultSet rs = sql.getSelectByWhere("u_name='admin' AND password='123'");
            while (rs.next()) {
                System.out.println(rs.getInt(1));
                System.out.println(rs.getString(2));
                System.out.println(rs.getString(3));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
```
  * ອະທິບາຍ: `getSelectByWhere("u_name='admin' AND password='123'");` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
```sql
SELECT * FROM tb_user WHERE u_name='admin' AND password='123'
```
## 3.7 ແກ້ໄຂຂໍ້ມູນ Update / ແກ້ໄຂຂໍ້ມູນຕາມໄອດີ
```java
        try {
            PreparedStatement pre = sql.getUpdate(1);
            pre.setString(1, "userEdit");
            pre.setString(2, "pass123");
            pre.executeUpdate();
        } catch (Exception e) {
            e.printStackTrace();
        }
```
  * ອະທິບາຍ: `sql.getUpdate(1);` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
  * `1` ແມ່ນຄ່າຂອງໄອດີທີ່ອ້າງອີງການອັບເດດ
```sql
UPDATE tb_user SET u_name='userEdit',password='pass123' WHERE u_id='1'
```
## 3.8 ແກ້ໄຂຂໍ້ມູນ Update / ແກ້ໄຂຂໍ້ມູນຕາມລຳດັບ Column
```java
        JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
        try {
            PreparedStatement pre = sql.getUpdateByColumnIndex(2, "userEdit");
            pre.setString(1, "5555");
            pre.executeUpdate();
        } catch (Exception e) {
            e.printStackTrace();
        }
```
  * ອະທິບາຍ: `getUpdateByColumnIndex(2, "userEdit");` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
  ``sql
  UPDATE tb_user SET password='5555' WHERE u_name='userEdit'
  ``
  ## 3.9 ແກ້ໄຂຂໍ້ມູນ Update / ແກ້ໄຂຂໍ້ມູນຕາມລຳດັບ Column ແບບ Array
  ```java
          JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
        try {
            PreparedStatement pre = sql.getUpdateByColumnIndexs(new int[]{2,3}, 2);
            pre.setString(1, "user222");
            pre.setString(2, "321");
            pre.executeUpdate();
        } catch (Exception e) {
            e.printStackTrace();
        }
```
  * ອະທິບາຍ: `getUpdateByColumnIndexs(new int[]{2,3}, 2);` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
  ```sql
  UPDATE tb_user SET u_name='user222',password='321' WHERE u_id='2'
  ```
## 3.10 ລົບຂໍ້ມູນ Delete / ລົບຂໍ້ມູນຕາມໄອດີ
```java
        JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
        try {
            PreparedStatement pre = sql.getDelete(2);
            pre.executeUpdate();
        } catch (Exception e) {
            e.printStackTrace();
        }
        ```
  * ອະທິບາຍ: `getDelete(2);` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
```sql
DELETE FROM tb_user WHERE u_id ='2'
```
## 3.11 ລົບຂໍ້ມູນ Delete / ລົບຂໍ້ມູນລຳດັບ Column
    ```java
        JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
        try {
            PreparedStatement pre = sql.getDeleteByColumnIndex(2, "user3");
            pre.executeUpdate();
        } catch (Exception e) {
            e.printStackTrace();
        }
        ```
 * ອະທິບາຍ: `getDeleteByColumnIndex(2, "user3");` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້
 ```sql
 DELETE FROM tb_user WHERE u_name ='user3'
 ```
## 3.12 ລົບຂໍ້ມູນ Delete / ລົບຂໍ້ມູນຕາມຊື່ Column
```java
        JoSQL sql = new JoSQL(con.getConnectMySQL(), "tb_user");
        try {
            PreparedStatement pre = sql.getDeleteByColumnName("password", "1234");
            pre.executeUpdate();
        } catch (Exception e) {
            e.printStackTrace();
```
   * ອະທິບາຍ: `getDeleteByColumnName("password", "1234");` ຈະສົ່ງຄຳສັ່ງກັບມາດັ່ງລຸ່ມນີ້   
   ```sql
   DELETE FROM tb_user WHERE password ='1234'
   ```
