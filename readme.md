# ICAP server - MinIO & RabbitMQ communication
# Description of the work
This is an initial code that upload a file and send it to MinIO and retrieve a MinIO path and it send a message to the RabbitMQ queue with the MinIO URL  path 

---
# Installation   
**Go intsall**

A sample installation of go version 1.14:

 1.for Linux
 
 Prepare the apt packages
 
 `` sudo apt update                    
  ``
  
 ``sudo apt upgrade
 ``

Link of download of version 1.14 (https://dl.google.com/go/go1.14.linux-amd64.tar.gz)

2.for windows

Link of download of vesion 1.15 (https://golang.org/dl/go1.15.1.windows-amd64.msi)

**RabbitMQ**

RabbitMQ should be  installed and running on localhost on standard port (5672). 

---
To test the code, use the go run command
``go run main.go
``



    
   
    
