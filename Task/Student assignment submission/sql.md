create database student_assignment_submission;

use student_assignment_submission;

create table student(
username varchar(50) primary key
);

describe student;

create table assignment(
shortname varchar (50) primary key, 
due_date date not null,
url varchar(255)
);

describe assignment;

create table submission(
username varchar(50),
 shortname varchar(50),
 version int,
 DATA text,
 
 primary key(username, shortname, version),
 foreign key (username) references student(username),
 foreign key (shortname) references assignment(shortname)
);

describe submission;
