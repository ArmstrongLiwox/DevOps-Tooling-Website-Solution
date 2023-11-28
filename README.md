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

### Storage Area Network (SAN) 

### NFS

### (s)FTP

### SMB

### iSCSI

### Block-level storage is and how it is used by Cloud Service providers

### Difference between Block-level storage and Object storage 

### AWS services

### Difference between Block Storage, Object Storage and Network File System.

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

