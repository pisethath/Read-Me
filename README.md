# Student & Book Management - Microservices (REST API)

This projects backend microservices (REST API) was build follow the requirement to allow student browse all library books and hold a maximum of 3 books for not more than 2 weeks. The mobile or website will notify the student with relevant information such as returning withheld books or whenever new books are added.

## Table of Contents
* [About](#about)
* [Required tools](#required_tools)
* [Installation](#installation)
* [Usage](#usage)

## About
This project is backend microservices (REST API). It was build under spring boots - maven project with sql server database.

## Required tools & material
- Eclipse IDE
- Docker
- Postman
- SQL Server Database
- SQL Server Management Studio

## Installation
1. Copy projects to Eclipse-Workspace folder
2. Open Eclipse IDE  and import projects
	2.1 Import "sereg" project: click on file-> import... -> Maven -> Existing Mavent Projects -> browse to folder "sereg" project -> Select Folder -> Finish
	2.2 Import "auth" project: click on file-> import... -> Maven -> Existing Mavent Projects -> browse to folder "auth" project -> Select Folder -> Finish
	2.3 Import "book" project: click on file-> import... -> Maven -> Existing Mavent Projects -> browse to folder "book" project -> Select Folder -> Finish
	2.4 Import "student" project: click on file-> import... -> Maven -> Existing Mavent Projects -> browse to folder "student" project -> Select Folder -> Finish
	2.5 Import "clould-getway" project: click on file-> import... -> Maven -> Existing Mavent Projects -> browse to folder "clould-getway" project -> Select Folder -> Finish
3. The "auth", "book" and "student" project connect to sql server database. So, you may change the connect to your sql server database if your sql server does not the same IP, username and password in existing config.
	3.1 Update sql server connection of "auth" project: open project folder\src\main\resources -> open file "application.properties" -> edit spring.datasource.url, spring.datasource.username and spring.datasource.password to your sql server connection.
	3.2 Update sql server connection of "book" project: open project folder\src\main\resources -> open file "application.properties" -> edit spring.datasource.url, spring.datasource.username and spring.datasource.password to your sql server connection.
	3.3 Update sql server connection of "student" project: open project folder\src\main\resources -> open file "application.properties" -> edit spring.datasource.url, spring.datasource.username and spring.datasource.password to your sql server connection.
4. Create database sql server for The "auth", "book" and "student" project via SQL Server Management Studio
	4.1 "aps_auth" database for "auth" project: Open SQL Server Management Studio -> Login connect to SQL Server -> righ click on "Database" -> new Database... -> Input Database name: aps_auth -> click on "OK"
	4.1 "aps-book" database for "book" project: Open SQL Server Management Studio -> Login connect to SQL Server -> righ click on "Database" -> new Database... -> Input Database name: aps-book -> click on "OK"
	4.1 "aps-student" database for "student" project: Open SQL Server Management Studio -> Login connect to SQL Server -> righ click on "Database" -> new Database... -> Input Database name: aps-student -> click on "OK"
5. We need to build JAR file from Eclipse IDE. 
	5.1 "sereg" project: Eclipse IDE -> go to "Project Explorer" -> click on project folder -> src/main/java -> main package -> right click on main class of application -> Run As -> Maven Install
	5.2 "auth" project: Eclipse IDE -> go to "Project Explorer" -> click on project folder -> src/main/java -> main package -> right click on main class of application -> Run As -> Maven Install
	5.3 "book" project: Eclipse IDE -> go to "Project Explorer" -> click on project folder -> src/main/java -> main package -> right click on main class of application -> Run As -> Maven Install
	5.4 "student" project: Eclipse IDE -> go to "Project Explorer" -> click on project folder -> src/main/java -> main package -> right click on main class of application -> Run As -> Maven Install
	5.5 "clould-getway" project: Eclipse IDE -> go to "Project Explorer" -> click on project folder -> src/main/java -> main package -> right click on main class of application -> Run As -> Maven Install
6. Build project to Docker Image
	6.1 "sereg" project: open CMD -> go the folder of project -> tyep: docker build -t sereg-app:latest . -> enter
	6.2 "auth" project: open CMD -> go the folder of project -> tyep: docker build -t auth-app:latest . -> enter
	6.3 "book" project: open CMD -> go the folder of project -> tyep: docker build -t book-app:latest . -> enter
	6.4 "student" project: open CMD -> go the folder of project -> tyep: docker build -t student-app:latest . -> enter
	6.5 "clould-getway" project: open CMD -> go the folder of project -> tyep: docker build -t getway-app:latest . -> enter
7. Run Docker Imange of projects
	7.1 open CMD -> tyep: docker network create eureka-s1 -> enter
	7.2 open CMD -> tyep: docker run --network eureka-s1 --name eureka-server -d -p 8761:8761 sereg-app:latest
	7.3 open CMD -> tyep: docker run --network eureka-s1 --name auth-service -d -p 9898:9898 auth-app:latest
	7.4 open CMD -> tyep: docker run --network eureka-s1 --name student-service -d -p 8081:8081 student-app:latest
	7.5 open CMD -> tyep: docker run --network eureka-s1 --name book-service -d -p 8082:8082 book-app:latest
	7.6 open CMD -> tyep: docker run --network eureka-s1 --name getway-service -d -p 8080:8080 getway-app:latest

## Usage
Open Postman and test REST API
Follow the "Student-Book Swagger Design".
*Note:  
	- API of create new student and create new book do not need authentication token, so they are free to use. other API require authentication token to use.
	- API of signup required student_id exist in student, so we need to create student first and then student can signup.
