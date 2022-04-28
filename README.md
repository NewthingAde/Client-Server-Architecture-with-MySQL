# Implement-a-Client-Server-Architecture-using-MySQL
Implement a Client Server Architecture using MySQL Database Management System (DBMS).

Client-Server refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another. In their communication, each machine has its own role: the machine sending requests is usually referred as "Client" and the machine responding (serving) is called "Server".

To develop a basic client-server using MySQL Relational Database Management System (RDBMS), we will use the following procedure and commands 

### Create and configure two Linux-based virtual servers (EC2 instances in AWS)

  1. Server A name - `mysql server`
  2. Server B name - `mysql client`

## On mysql server Linux Server install MySQL Server software.

  #### Installing MYSQL

  - USe the the comman line to install the server

                 sudo apt install mysql-server

  - We can the server using the following command line

                 sudo mysql_secure_installation

  - You can sudo in the the server using the command

                        sudo mysql

  This will be display which shows that it is successful

  <img width="610" alt="Screenshot 2022-04-28 at 22 43 14" src="https://user-images.githubusercontent.com/80678596/165842365-dc5accb8-86b9-47db-a012-73a918bc9086.png">

 - We can exit the server using the following command

                             exit

## On mysql client Linux Server install MySQL Client software.

