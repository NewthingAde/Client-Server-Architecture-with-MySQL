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

  - Next, we install mysql secure installation utility

                sudo mysql_secure_installation utility

When working with remote servers, you'll want to make sure that the SSH port is open to connections so that you are able to log in to your server remotely. The following command will enable the OpenSSH UFW application profile and allow all connections to the default SSH port on the server: 
  This will be display which shows that it is successful
  
                        sudo ufw enable

<img width="563" alt="Screenshot 2022-04-30 at 08 55 38" src="https://user-images.githubusercontent.com/80678596/166095602-ec510954-6d27-49f5-a3d2-65b624086523.png">


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


- Next is to allow mysql so we can be able to communicate with the server using ssh which will add rule to it

                            sudo ufw allow mysql


<img width="494" alt="Screenshot 2022-04-30 at 08 56 30" src="https://user-images.githubusercontent.com/80678596/166095679-74fe2ee5-e46d-40d8-b1d0-2a5dd421035d.png">

- Next we start the mysql with the command below

                              sudo systemctl start mysql

- Next we will enable mysql

                              sudo systemctl enable mysql
                              
<img width="559" alt="Screenshot 2022-04-30 at 09 06 32" src="https://user-images.githubusercontent.com/80678596/166095768-75e099ac-a7c5-4289-baec-01ef59a65480.png">

- Then we restart mysql to effect the changes

                            sudo systemctl restart mysql
                            
- Next check if the mysql server is working

                             sudo mysql

- We can exit the server using the following command

                             exit


## On mysql client Linux Server install MySQL Client software.

- In the Clint instance, you would use the same steps as we did in installing the server

                                  sudo apt-get update
                                  
                              sudo apt-get install mysql-server
                              
                              sudo mysql_secure_installation utility
                              
                                       sudo ufw enable
                                       
                                      sudo ufw allow mysql
                                      
                                    sudo systemctl start mysql
                                    
                                    sudo systemctl enable mysql
                                    
                                    sudo systemctl restart mysql


By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. Use mysql server's local IP address to connect from mysql client. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘mysql server’ - allow access only to the specific local IP address of your ‘mysql client’.

- Next is to configure MySQL server to allow connections from remote hosts.

                        sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf 
                        
**Replace ‘127.0.0.1’ to ‘0.0.0.0’ like this:**
    ![mysql_bind](https://user-images.githubusercontent.com/80678596/166098952-ff518165-c1e0-48a0-8d30-dc6fff6a0483.png)
