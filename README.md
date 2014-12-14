============
TweetFetcher
============

=====================
Eclipse Configuration
=====================

To extend Tomcat memory in Eclipse go to:
	Run -> Run Configurations -> Apache Tomcat -> Tomcat Server -> Arguments
At the end put:
	-XX:PermSize=256m -XX:MaxPermSize=256m	
To enhance OpenJPA right click on jpaenhance.xml:
	Run As -> Ant Build

==================
Creating databases
==================

Install mysql database:
```
$ sudo apt-get install mysql
```
Connect to the database:
```
$ mysql -u root -p
```

Copy and paste to populate database:
```
DROP DATABASE twitterdb;
CREATE DATABASE twitterdb DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

CONNECT twitterdb;
DROP TABLE IF EXISTS users;
CREATE TABLE users (
	user_id INT NOT NULL AUTO_INCREMENT,
	username VARCHAR(15) NOT NULL,
	nickname VARCHAR(15) NOT NULL,
	joined_date TIMESTAMP,
	PRIMARY KEY(user_id)
) ENGINE=InnoDB DEFAULT CHARSET=UTF8;

DROP TABLE IF EXISTS tweets;
CREATE TABLE tweets (
	tweet_id INT NOT NULL AUTO_INCREMENT,
	user_id INT NOT NULL,
	tweet VARCHAR(140) NOT NULL,
	date TIMESTAMP,
	PRIMARY KEY(tweet_id),
	FOREIGN KEY(user_id) REFERENCES users(user_id)
) ENGINE=InnoDB DEFAULT CHARSET=UTF8;


INSERT INTO users(username, nickname, joined_date) VALUES("Jan.Neuzil", "@JohnnyCzech", "2014-11-11 22:22:22");
INSERT INTO users(username, nickname, joined_date) VALUES("Michal.Svacha", "@Svachic", "2011-11-11 22:22:22");
INSERT INTO tweets(user_id, tweet, date) VALUES(1, "I got a job in Cisco.", "2014-12-06 22:22:22");
INSERT INTO tweets(user_id, tweet, date) VALUES(1, "I love Prague.", "2014-12-07 22:22:22");
INSERT INTO tweets(user_id, tweet, date) VALUES(2, "I got a job in Ubisoft.", "2014-11-05 22:22:22");
INSERT INTO tweets(user_id, tweet, date) VALUES(2, "I love London.", "2014-11-06 22:22:22");

GRANT ALL on twitterdb.* TO twitter@localhost IDENTIFIED BY 'twitterpwd';
```

=====
Notes
=====

