# DevOps-Tooling-Website-Solution - Armstrong

## Introduction

In this Project I will implement a set of DevOps tools that will help a DevOps team in day to day activities in managing, developing, testing, deploying and monitoring different projects.

These tools are well known and widely used by multiple DevOps teams. This single DevOps Tooling Solution will consist of:

1. **Jenkins** - free and open source automation server used to build **CI/CD** pipelines.
2. **Kubernetes** - an open-source container-orchestration system for automating computer application deployment, scaling,  and management.
3. **Jfrog Artifactory** - Universal Repository Manager supporting all major packaging formats, build tools and Cl servers. Artifactory.
4. **Rancher** - an open source software platform that enables organizations to run and manage **Docker** and Kubernetes in production.
5. **Grafana** - a multi-platform open source analytics and interactive visualization web application.
6. **Prometheus** - An open-source monitoring system with a dimensional data model, flexible query language, efficient time series database and modern alerting approach.
7. **Kibana** - Kibana is a free and open user interface that lets you visualize your **Elasticsearch** data and navigate the **Elastic Stack**.


## Side Self Study

### Network-attached storage (NAS)

Network-attached storage (NAS) is a file-level (as opposed to block-level storage) computer data storage server connected to a computer network providing data access to a heterogeneous group of clients. 

The term "NAS" can refer to both the technology and systems involved, or a specialized device built for such functionality (as unlike tangentially related technologies such as local area networks, 
a NAS device is often a singular unit).

### Storage Area Network (SAN) 

A storage area network (SAN) or storage network is a computer network which provides access to consolidated, block-level data storage. 

SANs are primarily used to access data storage devices, such as disk arrays and tape libraries from servers so that the devices appear to the operating system as direct-attached storage. 

A SAN typically is a dedicated network of storage devices not accessible through the local area network (LAN).

### NFS

Network File System (NFS) is a distributed file system protocol originally developed by Sun Microsystems (Sun) in 1984, allowing a user on a client computer to access files over a computer network much like local storage is accessed. 
NFS, like many other protocols, builds on the Open Network Computing Remote Procedure Call (ONC RPC) system. 
NFS is an open IETF standard defined in a Request for Comments (RFC), allowing anyone to implement the protocol.

### FTP

The File Transfer Protocol (FTP) is a standard communication protocol used for the transfer of computer files from a server to a client on a computer network. 

FTP is built on a client–server model architecture using separate control and data connections between the client and the server.

FTP users may authenticate themselves with a plain-text sign-in protocol, normally in the form of a username and password, but can connect anonymously if the server is configured to allow it. 

For secure transmission that protects the username and password, and encrypts the content, FTP is often secured with SSL/TLS (FTPS) or replaced with SSH File Transfer Protocol (SFTP).

### SMB

Server Message Block (SMB) is a communication protocol mainly used by Microsoft Windows equipped computers normally used to share files, printers, serial ports, and miscellaneous communications between nodes on a network. 

SMB implementation consists of two vaguely named Windows services: "Server" (ID: LanmanServer) and "Workstation" (ID: LanmanWorkstation).

It uses NTLM or Kerberos protocols for user authentication. 
It also provides an authenticated inter-process communication (IPC) mechanism.

### iSCSI

Internet Small Computer Systems Interface or iSCSI is an Internet Protocol-based storage networking standard for linking data storage facilities. 

iSCSI provides block-level access to storage devices by carrying SCSI commands over a TCP/IP network. 
iSCSI facilitates data transfers over intranets and to manage storage over long distances. 

It can be used to transmit data over local area networks (LANs), wide area networks (WANs), or the Internet and can enable location-independent data storage and retrieval.

### Block-level storage is and how it is used by Cloud Service providers

Block-level storage is a concept in cloud-hosted data persistence where cloud services emulate the behaviour of a traditional block device, such as a physical hard drive.

Developers use block storage to store containerized applications on the cloud. Containers are software packages that contain the application and its resource files for deployment in any computing environment. Like containers, block storage is equally flexible, scalable, and efficient.

Storage in such services is organised as blocks. 
This emulates the type of behaviour seen in traditional disks or tape storage through storage virtualization. 

Blocks are identified by an arbitrary and assigned identifier by which they may be stored and retrieved, but this has no obvious meaning in terms of files or documents. 

A file system must be applied on top of the block-level storage to map 'files' onto a sequence of blocks.
Amazon EBS (elastic block store) is an example of a cloud block store.

### Difference between Block-level storage and Object storage 

Object storage normally uses a distributed storage environment across multiple different storage nodes or servers. 

On the other hand, block storage uses RAID, SSDs, and hard disk drives (HDDs) for storage. 

Finally, cloud file storage uses network-attached storage (NAS) in an on-premises setup.

### AWS services

Amazon Web Services (AWS) is the world's most comprehensive and broadly adopted cloud, offering over 200 fully featured services from data centers globally.

### Difference between Block Storage, Object Storage and Network File System.

Object storage normally uses a distributed storage environment across multiple different storage nodes or servers. 

On the other hand, block storage uses RAID, SSDs, and hard disk drives (HDDs) for storage. 

Finally, cloud file storage uses network-attached storage (NAS) in an on-premises setup.

## Project Objective

> In this project I will implement a tooling website solution which makes access to DevOps tools within the corporate infrastructure easily accessible.

In this project I will implement a solution that consists of following components:
1. Infrastructure: AWS
2. Webserver Linux: Red Hat Enterprise Linux 8
3. Database Server: Ubuntu 20.04+ MySQL
4. Storage Server: Red Hat Enterprise Linux 8 + NFS Server
5. Programming Language: PHP
6. Code Repository: GitHub

> The diagram below shows a common pattern where several stateless Web Servers share a common database and also access the same files using Network File Sytem (NFS) as a shared file storage. 

![3 tier](<images/3 tier web application.jpg>)

> Even though the NFS server might be located on a completely separate hardware.

> For Web Servers it look like a local file system from where they can serve the same files.


## Implementing a business website using NFS for the backend file storage

### Step 1 - Prepare NFS Server

> 1. Spin up a new EC2 instance with RHEL Linux 8 Operating System.

> 2. Based on your LVM experience from Project 6, Configure LVM on the Server.

• Instead of formating the disks as ext4 you will have to format them as xfs
• Ensure there are 3 Logical Volumes. 1v-opt lv-apps, and lv-logs

> 3. Create mount points on /mnt directory for the logical volumes as follow: Mount lv-apps on /mnt/apps

- To be used by webservers Mount lv-logs on /mnt/logs - To be used by webserver logs Mount Iv-opt on /mnt/opt - To be used by Jenkins server in Project 8

> 4. Install NFS server, configure it to start on reboot and make sure it is u and running.

```
sudo yum -y update
```
```
sudo yum install nfs-utils -y
```
```
sudo systemctl start nfs-server.service
```
```
sudo systemctl enable nfs-server.service
```
```
sudo systemctl status nfs-server.service
```


> 5. Export the mounts for webservers' subnet cidr to connect as clients. 

For simplicity, I will install your all three Web Servers inside the same subnet, but in production set up you would probably want to separate each tier inside its own subnet for higher level of security. 

To check your subnet cidr - open your EC2 details in AWS web console and locate 'Networking' tab and open a Subnet link:




