# Enterprise macOS Software Deployment Lab with Munki & MunkiReport

## Overview

This project demonstrates a centralized macOS software deployment and monitoring solution built using **Munki** and **MunkiReport**.

### Goals

- Deploy software silently to macOS devices.
- Assign software based on device hostname or group.
- Maintain a common software baseline across clients.
- Monitor deployment status and installation errors.
- Simulate a small enterprise Mac administration environment.

---

## Technologies

### Infrastructure

- Ubuntu Server 26.04.1
- MacOS for repo administration (macOS 10.13 or later)
- Apache2
- DNS
- SMB


### Software Distribution

- Munki
- MunkiAdmin
- MunkiTools

### Monitoring

- MunkiReport
- PHP
- MySQL

### Clients

- macOS Sonoma (or from macOS 10.13 or later)

---

## Features

### Munki

- Centralized software distribution
- Silent application deployment
- Manifest-based package assignment
- Support for `.pkg` and `.dmg` packages
- Device-specific software deployment
- Shared baseline software catalog

### MunkiReport

- Centralized web dashboard
- Client inventory
- Deployment monitoring
- Error reporting and troubleshooting
- Hardware and software inventory collection

---

## Demo Video

A demonstration video is available showing:

- Repository management
- Package deployment
- Client synchronization
- Automatic installation
- MunkiReport monitoring
- Error detection and reporting




https://github.com/user-attachments/assets/88f8e2ea-69a7-4b54-8c80-92e53e512bcd




https://github.com/user-attachments/assets/3a4070c7-53fe-4257-9de9-0089236f803c

---

## Architecture

```text
Mac Admin (MunkiAdmin)
          |
         SMB
          |
          v
     Munki Server
   (Apache + Repo)
          |
       HTTP/HTTPS
          |
          v
     macOS Clients
    (Munki Agent)
          |
      Reporting
          |
          v
      MunkiReport
     (PHP + MySQL)
```

---

## Build Process

### 1. Munki Server

Configured:

- Apache virtual host
- Munki repository
- SMB share for repository management
- Internal DNS records

Repository publishing is handled through Apache using a symbolic link between the web root and repository location.

### 2. MunkiReport Server

Configured:

- Apache virtual host
- PHP environment
- MySQL database
- Database migrations
- DNS records

The web application provides centralized visibility of all enrolled clients.

### 3. Mac Administration Workstation

Installed:

- MunkiTools
- MunkiAdmin

Used to:

- Upload packages
- Create catalogs
- Manage manifests
- Maintain the repository

### 4. Client Enrollment

Configured:

- Munki client
- Repository URL
- DNS resolution
- Communication with MunkiReport

---

## What I Learned

- Enterprise software deployment concepts
- Apache Virtual Host management
- DNS configuration and troubleshooting
- Repository-based application management
- macOS package deployment
- PHP and MySQL application hosting
- Munki and MunkiReport integration
- Troubleshooting permissions, DNS, database, and deployment issues

---

## Challenges Faced

During the implementation I encountered and solved several issues:

- Apache virtual hosts serving the wrong site.
- Repository access problems caused by filesystem permissions.
- Munki manifest retrieval failures (HTTP 404).
- DNS resolution issues between clients and services.
- MySQL permission errors during MunkiReport setup.
- Communication issues between Munki clients and the repository.

---

## Possible Improvements

- Enable HTTPS with trusted TLS certificates for both Munki and MunkiReport.
- Automate infrastructure deployment and maintenance using Ansible.
- Integrate with an MDM platform such as Jamf Pro, Mosyle, or Kandji to streamline device enrollment and management.

---

## Documentation

More images and some configuration details are available in the `docs/` directory:

```text
docs/
├── munki-server.md
├── munki_admin.md
├── munki_client.md
└── munkireport_server.md
```
