MySQL
=====
#Tìm hiểu về MySQL

#####Mysql
===================
##HƯỚNG DẪN CÀI ĐẶT VÀ SỬ DỤNG MYSQL

### 1. HƯỚNG  DẪN CÀI ĐẶT :


* B1: chuyển sang quyền root :
```
sudo su
```


* B2: Cập nhật các Repository:
```
apt-get update -y
```

* B3: Cài đặt mysql-server bằng lệnh:
```
apt-get install mysql-server -y
```

* B4 : Quá trình cài đặt sẽ diễn ra trong ít phút. Trong quá trình cài đặt MySql sẽ yêu cầu nhập mật khẩu cho tài khoản mặc định root, đây là mật khẩu để kết nối đến MySql 


Nhập lại mật khẩu 


Kết thúc quá trình cài đặt.

###2.Các lệnh  cơ bản trong Mysql

####I.Các câu lệnh liên quan đên Database
1. Tao database: 
```
CREATE DATABASE <ten database>;
```
2.Chọn 1 database để sử dụng:
```
USE DATABASE;
```
3.Xóa một database: 
```
DROP DATABASE <tên database>;
```
4.Hiển thị các database:
```
SHOW DATABASE;
```
####II. Các lệnh liên quan đến bảng:

1.Hiển thị thông tin các bảng trong database: 
```
   SHOW TABLES;
```
2.Hiển thị thông tin 



3.Tạo 1 bảng:
```
CREATE TABLE <tên bảng>;
```
4.Nhập data vào table: 
```
INSERT INTO [TEN TABLE](cột 1, cột 2,...) VALUES (gicột 1,gi côt 2...);
```
5.Lấy thông tin từ bảng: 
```
SELECT {Tên cột muốn hiển thị} FROM {Tên bảng} [WHERE {Điều kiện}];
```
6.Cập nhật thông tin cho các bảng: 

````
UPDATE [Tên TABLE] SET [cột muốn sửa] [Where {Điều kiện}];

```
7.Xóa TABLE :

```
DROP Table <Tên table>;
```
#### III.Các lệnh về User: 
1.Tạo user:
```
  CREATE USER <tên user>;
```
2. Đặt password cho user: 
```
SET PASSWORD FOR <Tên user>=PASSWORD('password');
```
3.Gán quyền cho user:
```
  GRANT [quyền] ON [tên database].[tên table] TO '[user]'@'localhost';
```
- Các  quyền  hạn trong mysql:

```
    ALL PRIVILEGES- tất cả quyền trên hệ thống
    CREATE- cho phép tạo database và table
    DROP- cho phép xóa database hoặc table
    DELETE- cho phép xóa các record trong table
    INSERT- cho phép thêm record trong table
    SELECT-cho phép thực hiện lệnh SELECT để query dữ liệu
    UPDATE- cho phép cập nhật record trong table
    GRANT OPTION- cho phép thực hiện tác vụ phân quyền cho user khác
    (GRANT GRANT OPTION .....)
```

- Để quyền có hiệu lực cần thực hiện lệnh sau:
````
  FLUSH PRIVILEGES;
````

- Xóa  quyền :

```
  REVOKE [quyền] ON [tên database].[tên table] FROM '[user]'@'localhost';
````

#### IV.Phân quyền truy cập : 
 
 - Cho phép các máy truy cập và sử dụng databases;
 
 - B1 : Trên máy client  cài gói:
  ```
    sudo apt-get install mysql-client -y
  ```
 - B2: Trên máy server . Ta chỉnh file cấu hình /etc/mysql/my.cnf
   
    ```
          [mysqld] 
          user            = mysql
          pid-file        = /var/run/mysqld/mysqld.pid
          socket          = /var/run/mysqld/mysqld.sock
          port            = 3306
          basedir         = /usr
          datadir         = /var/lib/mysql
          tmpdir          = /tmp
          language        = /usr/share/mysql/English
          bind-address    = 192.168.1.15 # ip server
         # skip-networking
   ```


- B3: Lưu và đóng tập tin . khởi động lại dịch vụ:
 ```
   sudo service mysql restart
 ```
- B4: Gán quyền truy cập cho địa chỉ IP:

 ```
   mysql -u root -p password
   mysql> CREATE DATABASE foo;
   mysql> GRANT ALL ON foo.* TO demo@'192.168.1.10′ IDENTIFIED BY ‘PASSWORD’;
 ```
- B5 : Mở port mysql 3306:

 ````
   /sbin/iptables -A INPUT -i eth0 -p tcp –destination-port 3306 -j ACCEPT
 ````
  hoặc chỉ cho phép truy cập từ xa từ máy chủ  web đặt ở IP-server:
 ```
   /sbin/iptables -A INPUT -i eth0 -s 10.5.1.3 -p tcp –destination-port 3306 -j ACCEPT
 ```
  hoặc chỉ cho phép truy cập từ xa từ subnet của mạng LAN của bạn 192.168.1.0/24:
  ```
    /sbin/iptables -A INPUT -i eth0 -s 192.168.1.0/24 -p tcp –destination-port 3306 -j ACCEPT
  ```
- B4 :Test :
  Trên máy client :
  ```
    mysql -u demo -pdemo -h 192.168.1.15 
  ```
- Bạn có thể dùng phần mềm navicat để truy cập vào server
#### V.Backup du lieu:

- Back up du lieu:
   ```
           mysqldump -u root -p [tendatabase] > [name.sql];
   ```




3. Ví dụ:


BAI 1:
  
BANG KHUVUC
 
| Trường        |     Kiểu DL   |
| ------------- | ------------  | 
|  IDKHUVUC     |   VARCHAR(20) |
| TENLKHUVUC    |  VARCHAR(30)  |
| PhongQL       |  VARCHAR(10)  |



BANG DAY

| Trường        |     Kiểu DL   |
| ------------- | ------------  | 
|  STTDay       |    INT        |
| IDKHUVUC      |  VARCHAR(20)  |
|  TEN          |  VARCHAR(30)  |
| PHONGbv       |  VARCHAR(10)  |



| Trường        |     Kiểu DL   |
| ------------- | ------------  | 
|  IDKHUVUC     |  VARCHAR(20)  |
|  IDPHONG      |  VARCHAR(10)  |
|  STT          |  INT          |
|  SucChua

  

```
mysql> CREATE DATABASE KTX;

mysql> USE KTX;

mysql> SHOW TABLE;
mysql> CREATE TABLE KHUVUC(
-> IDKHUVUC VARCHAR(20)
-> TENKHUVUC VARCHAR(30)
-> PhongQL VARCHAR(10);
-> PRIMARY KEY (IDKHUCVUC)
->);

mysql> CREATE TABLE DAY(
-> STTDay int ,
-> IDKHUVUC VARCHAR(20),
-> TEN VARCHAR(30),
-> PHONGbv VARCHAR(10),
-> PRIMARY KEY (STTDay),
-> FOREIGN KEY (IDKHUVUC) REFERENCE KHUVUC(IDKHUVUC)
->)
->;
mysql> CREATE TABLE PHONG
-> (
-> IDKHUVUC VARCHAR(20),
-> IDPHONG VARCHAR(10),
-> STTDay INT,
-> SucChua INT,
-> PHONGtb VARCHAR(10),
-> PRIMARY KEY (IDPHONG),
-> CONSTRAINT KEY_1 FOREIGN KEY (IDKHUVUC) REFERENCES KHUVUC(IDKHUVUC),
-> CONSTRAINT KEY_2 FOREIGN KEY (STTDay) REFERENCES DAY(STTDay)
-> )
-> ;
Query OK, 0 rows affected (0.08 sec)

mysql> SHOW TABLES;
+---------------+
| Tables_in_KTX |
+---------------+
| DAY |
| KHUVUC |
| PHONG |
+---------------+
3 rows in set (0.00 sec)

mysql> INSERT INTO KHUVUC VALUES ('2','KHU_VUC_2','PHONG2');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO KHUVUC VALUES ('3','KHU_VUC_3','PHONG3');
Query OK, 1 row affected (0.11 sec)

mysql> INSERT INTO DAY VALUES ('1','1','DAY_1','1');
Query OK, 1 row affected (0.03 sec)

mysql> INSERT INTO DAY VALUES ('2','2','DAY_2','2');
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO DAY VALUES ('3','3','DAY_3','3');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO PHONG VALUES ('1','1','1','10','PHONG_1');
Query OK, 1 row affected (0.06 sec)

mysql> INSERT INTO PHONG VALUES ('2','2','2','10','PHONG_2');
Query OK, 1 row affected (0.05 sec)
````


-Bài 2:

```
mysql> CREATE DATABASE QLTSX;
Query OK, 1 row affected (0.00 sec)

mysql> USE QLTSX;
Database changed
mysql> CREATE TABLE DOISX(
-> IDDOISX VARCHAR(10),
-> TENDOI VARCHAR(30),
-> IDDOITRUONG VARCHAR(10),
-> PRIMARY KEY (IDDOISX)
->)
-> ;

Query OK, 0 rows affected (0.04 sec)

mysql> CREATE TABLE TOSX
-> (
-> IDDOISX VARCHAR(10),
-> STT INT,
-> TEN VARCHAR(30),
-> IDTOTRUONG VARCHAR(10),
-> PRIMARY KEY (IDTOTRUONG),
-> FOREIGN KEY (IDDOISX) REFERENCES DOISX(IDDOISX)
-> )
-> ;
Query OK, 0 rows affected (0.07 sec)

mysql> CREATE TABLE CONGNHAN
-> (
-> IDDOISX VARCHAR(10),
-> IDCONGNHAN VARCHAR(10),
-> HOTEN VARCHAR(30),
-> NAMSINH INT,
-> STT INT,
-> IDNQL VARCHAR(10),
-> PRIMARY KEY (IDCONGNHAN),
-> CONFOREIGN KEY (IDDOISX) REFERENCES DOISX(IDDOISX)
CONCAT CONCURRENT CONNECTION CONSISTENT CONTAINS CONV CONVERT_TZ
CONCAT_WS CONDITION CONNECTION_ID CONSTRAINT CONTINUE CONVERT
-> CONSTRAINT KEY_1 FOREIGN KEY (IDDOISX) REFERENCES DOISX(IDDOISX),
-> CONSTRAINT KEY_2 FOREIGN KEY (STTTO) REFERENCES TOSX(STT),
-> )
-> ;

mysql> INSERT INTO DOISX VALUES ('1','DOI_1','1',);
mysql> INSERT INTO DOISX VALUES ('2','DOI_2','2',);
mysql> INSERT INTO DOISX VALUES ('3','DOI_3','3',);
```
