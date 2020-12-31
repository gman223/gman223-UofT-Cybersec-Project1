## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://raw.githubusercontent.com/gman223/gman223-UofT-Cybersec-Project1/main/Images/Network%20Map2.jpg "Network Map")

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. [ELK Playbook](https://github.com/gman223/gman223-UofT-Cybersec-Project1/blob/main/Files/elk-playbook.yml). Alternatively, select portions of the [Filebeat Playbook](https://github.com/gman223/gman223-UofT-Cybersec-Project1/blob/main/Files/filebeat-playbook.yml) may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resouces.

The configuration details of each machine may be found below.
| Name   | Function           | IP Address                  | Operating System |
|--------|--------------------|-----------------------------|------------------|
| Jbox   | Gateway            | 40.118.241.44<br>10.0.0.4   | Linux            |
| Web 1  | Collects DVWA Logs | 10.0.0.5                    | Linux            |
| Web 2  | Collects DVWA Logs | 10.0.0.6                    | Linux            |
| Web 3  | Collects DVWA Logs | 10.0.0.10                   | Linux            |
| LB_1   | Load Balancer      | 104.42.227.147              | Linux            |
| ELK_VM | Running ELK Stack  | 40.121.7.30<br>10.1.0.4 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

196.247.57.68

Machines within the network can only be accessed by Jbox.

A summary of the access policies in place can be found in the table below.

**Internal Private IPs:**
10.0.0.4
10.0.0.5
10.0.0.6
10.0.0.10
10.1.0.4

| Name   | Publicly Accessible | Allowed IP Addresses          |
|--------|---------------------|-------------------------------|
| Jbox   | Yes                 | 196.247.57.68<br>Internal IPs |
| Web 1  | No                  | Internal IPs                  |
| Web 2  | No                  | Internal IPs                  |
| Web 3  | No                  | Internal IPs                  |
| LB_1   | Yes                 | 196.247.57.68<br>Internal IPs |
| ELK_VM | Yes                 | 10.0.0.4 <br>196.247.57.68    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because once one playbook is created, it can be deployed as many times as needed.

The playbook implements the following tasks:
- **Install Docker.io**: Installs Docker onto target machine.
- **Install Python pip3/Install Docker Python Module**: Installs Python modules onto target machine.
- **Enable Docker services on startup**: Enables docker to run on server startup.
- **Increase virtual memory/Use more memory**: Increases the maximum available memory to the ELK container.
- **Download and launch a docker elk container**:  Downloads and launches an ELK container on target machine and states ports in use.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK Instance](https://github.com/gman223/gman223-UofT-Cybersec-Project1/blob/main/Images/elk-running.JPG)
