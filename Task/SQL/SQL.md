CREATE DATABASE Event_Management;

USE Event_Management;

CREATE TABLE _EVENTS(
event_id INT auto_increment PRIMARY KEY,
event_name VARCHAR(255) NOT NULL
);

DESCRIBE _EVENTS;

CREATE TABLE Attendees(
attendee_id INT AUTO_INCREMENT PRIMARY KEY,
attendee_name VARCHAR(255) NOT NULL
);

DESCRIBE Attendees;

CREATE TABLE Event_attendees(
event_id INT,
attendee_id INT,
FOREIGN KEY (event_id) references _EVENTS(event_id),
FOREIGN KEY (attendee_id) references Attendees(attendee_id)
);

DESCRIBE Event_attendees;

CREATE TABLE event_sponsors(
sponsor_id INT auto_increment PRIMARY KEY,
event_id INT,
sponsor_name VARCHAR (255) NOT NULL,
FOREIGN KEY (event_id) references _EVENTS(event_id)
);

DESCRIBE event_sponsors;
