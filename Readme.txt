・Qiita　Spring Bootで簡単な検索アプリケーションを開発する
http://qiita.com/rubytomato@github/items/e4fda26faddbcfd84d16

・Spring Boot 使い方メモ
http://qiita.com/opengl-8080/items/05d9490d6f0544e2351a


環境
Windows7 (64bit)
Java 1.8.0_45
Spring Boot 1.2.4
thymeleaf 2.1.4
logback 1.1.3
MySQL 5.6
Eclipse 4.4
Maven 3.3.3




サンプルデータは下記の通り準備します。
データベース: sample_db
ユーザー： test_user
テーブル: actor, prefecture
データベース
sample_db
create database if not exists sample_db;
ユーザー
create_user
create user 'test_user'@'localhost' identified by 'test_user';
grant
grant all on sample_db.* to 'test_user'@'localhost';
actorテーブル
actor
create table if not exists actor (
  id int not null auto_increment,
  name varchar(30) not null,
  height smallint,
  blood varchar(2),
  birthday date,
  birthplace_id smallint,
  update_at timestamp(6) not null default current_timestamp(6) on update current_timestamp(6),
  primary key (id)
) engine = INNODB;
初期化
init
insert into actor (name, height, blood, birthday, birthplace_id) values
('丹波哲郎', 175, 'O',  '1922-07-17', 13),
('森田健作', 175, 'O',  '1949-12-16', 13),
('加藤剛',   173, null, '1938-02-04', 22),
('島田陽子', 171, 'O',  '1953-05-17',  43),
('山口果林', null, null,'1947-05-10',  13),
('佐分利信', null, null, '1909-02-12', 1),
('緒形拳',   173, 'B',   '1937-07-20', 13),
('松山政路', 167, 'A',   '1947-05-21', 13),
('加藤嘉',   null, null, '1913-01-12', 13),
('菅井きん', 155, 'B',   '1926-02-28', 13),
('笠智衆',   null, null, '1904-05-13', 43),
('殿山泰司', null, null, '1915-10-17', 28),
('渥美清',   173,  'B',  '1928-03-10', 13);
prefectureテーブル
prefecture
create table if not exists prefecture (
  id smallint not null,
  name varchar(6) not null,
  primary key (id)
) engine = INNODB;
初期化
init
insert into prefecture (id, name) values
(1,'北海道'),(2,'青森県'),(3,'岩手県'),(4,'宮城県'),(5,'秋田県'),(6,'山形県'),(7,'福島県'),
(8,'茨城県'),(9,'栃木県'),(10,'群馬県'),(11,'埼玉県'),(12,'千葉県'),(13,'東京都'),(14,'神奈川県'),
(15,'新潟県'),(16,'富山県'),(17,'石川県'),(18,'福井県'),(19,'山梨県'),(20,'長野県'),(21,'岐阜県'),
(22,'静岡県'),(23,'愛知県'),(24,'三重県'),(25,'滋賀県'),
(26,'京都府'),(27,'大阪府'),(28,'兵庫県'),(29,'奈良県'),(30,'和歌山県'),
(31,'鳥取県'),(32,'島根県'),(33,'岡山県'),(34,'広島県'),(35,'山口県'),
(36,'徳島県'),(37,'香川県'),(38,'愛媛県'),(39,'高知県'),
(40,'福岡県'),(41,'佐賀県'),(42,'長崎県'),(43,'熊本県'),(44,'大分県'),(45,'宮崎県'),(46,'鹿児島県'),(47,'沖縄県');


