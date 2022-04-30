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

                        sudo systemctl start mysql

When working with remote servers, you'll want to make sure that the SSH port is open to connections so that you are able to log in to your server remotely. The following command will enable the OpenSSH UFW application profile and allow all connections to the default SSH port on the server: 
  This will be display which shows that it is successful
  
                        sudo ufw enable

<img width="563" alt="Screenshot 2022-04-30 at 08 25 41" src="https://user-images.githubusercontent.com/80678596/166094502-1c62a199-9d40-4637-878d-6959101174a2.png">

   #### Point to Note
   
   You can be locked out of SSH with UFW  command in EC2 AWS. if this happends, all you will need to do is to follow the procedure below
    1. Stop your instance
    2. Right click (windows) or ctrl + click (Mac) on the instance to open context menu, then go to `Instance Settings` -> `Edit User Data` or select the instance and go to `Actions` -> `Instance Settings` -> `Edit User Data`
      If you're still on the old AWS console, select the `instance`,  go to `Actions` -> `Instance Settings` -> `View/Change User Data`
    3. And paste this
            
              Content-Type: multipart/mixed; boundary="//"
              MIME-Version: 1.0
              --//
              Content-Type: text/cloud-config; charset="us-ascii"
              MIME-Version: 1.0
              Content-Transfer-Encoding: 7bit
              Content-Disposition: attachment; filename="cloud-config.txt"
              #cloud-config
              cloud_final_modules:
              - [scripts-user, always]
              --//
              Content-Type: text/x-shellscript; charset="us-ascii"
              MIME-Version: 1.0
              Content-Transfer-Encoding: 7bit
              Content-Disposition: attachment; filename="userdata.txt"
              #!/bin/bash
              ufw disable
              iptables -L
              iptables -F
              --//

   4. Once added, restart the instance and ssh should work. The userdata disables ufw if enabled and also flushes any iptable rules blocking ssh access






- Next is to allow mysql so we can be able to communicate with the server

                            sudo systemctl enable mysql
                            
- Next we restart the mysql with the command below

                              sudo systemctl restart mysql

  <img width="610" alt="Screenshot 2022-04-28 at 22 43 14" src="https://user-images.githubusercontent.com/80678596/165842365-dc5accb8-86b9-47db-a012-73a918bc9086.png">


 - We can exit the server using the following command

                             exit

## On mysql client Linux Server install MySQL Client software.

