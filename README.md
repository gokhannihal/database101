# MongoDB 4.2.18

#### Docker ' da mongodb 4.2.18 uygulamasını çalıştırmak için gereken komutlar:
```sh
docker pull mongo:4.2.18
docker run -d -p 27017:27017 --name mongo mongo:4.2.18
```
#### Mongodb uygulamasının erişilebilir olduğunu kontrol etmek için gereken komut :
```sh
nc -v localhost 27017     > Başarılı çıktı : Connection to localhost 27017 port [tcp/*] succeeded!
```
#### Ubuntu üzerine Mongodb araçlarını kurmak için gereken komutlar:

```sh
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
sudo add-apt-repository 'deb [arch=amd64] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse'
sudo apt update
sudo apt install mongodb-org-shell -y 
sudo apt install mongodb-org-tools -y 
```
#### Northwind datasını MongoDB ye aktarmak için gereken komut:
```sh
cd ./database101/mongo
mongorestore --db Northwind --verbose dump
```
#### Mongo Client üzerinden localhost da çalışan MongoDB ye erişmek için gereken komut
```sh
mongo
```


# MySQL 

#### Docker ' da MySQL uygulamasını çalıştırmak için gereken komutlar:
```sh
docker pull mysql/mysql-server:latest
docker run -tid -p 3306:3306 --name mysql-server --env="MYSQL_ROOT_PASSWORD=password123" mysql/mysql-server:latest 
```
#### MySQL uygulamasının erişilebilir olduğunu kontrol etmek için gereken komut :
```sh
nc -v localhost 3306     > Başarılı çıktı : Connection to localhost 3306 port [tcp/mysql] succeeded!
```
#### Ubuntu üzerine MySQL araçlarını kurmak için gereken komutlar:

```sh
sudo apt-get install mysql-client -y  
```

#### Kendi sistemimiz üzerinden MySQL 'e erişmek için user oluşturmamız gerekiyor. Bunun için gerekli komutlar.
```sh
docker exec -it mysql-server bash  > "Bu komut ile docker da çalışan mysql containerı içerisine giriş yapıyoruz."
mysql -u root -p   > bu komutun devamında password: password123 olarak giriyoruz.
CREATE USER 'duser'@'%' IDENTIFIED BY 'password'; > Bu komut ile dışarıdan da mysql e erişmek için bir user oluşturuyoruz.
GRANT ALL PRIVILEGES ON *.* TO 'duser'@'%';  > Bu komut ile mysql'de kullanıcıya veritabanları için tüm yetkileri vermiş oluyoruz.
```
#### Northwind veritabanını oluşturmak ve verileri içeri aktarmak için gereken komutlar:
```sh
cd ./database101/mysql/
mysql -uduser -ppassword -h127.0.0.1 -P3306 -e "create database northwind"
mysql -uduser -ppassword -h127.0.0.1 -P3306 northwind < northwind-create.sql
mysql -uduser -ppassword -h127.0.0.1 -P3306 northwind < northwind-data.sql
```
#### MySQL Client üzerinden docker 'da çalışan MySQL uygulamasına erişmek için gereken komut:
```sh
mysql -uduser -ppassword -h127.0.0.1 -P3306
```
