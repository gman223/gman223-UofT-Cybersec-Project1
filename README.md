## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://raw.githubusercontent.com/gman223/gman223-UofT-Cybersec-Project1/main/Images/Network%20Map2.jpg "Network Map")

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. [ELK Playbook](https://github.com/gman223/gman223-UofT-Cybersec-Project1/blob/main/Files/elk-playbook.yml). Once deployed the [Filebeat Playbook](https://github.com/gman223/gman223-UofT-Cybersec-Project1/blob/main/Files/filebeat-playbook.yml) may be used to install Filebeat.

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

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.

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

Only the Jbox, Load Balancer (LB_1) and ELK_VM machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

196.247.57.68

Machines within the internal network can only be accessed by Jbox.

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

### ELK Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually. Which is advantageous because, once one playbook is created, it can be deployed as many times as needed.

The playbook implements the following tasks:
- **Install Docker.io**: Installs Docker onto target machine.
- **Install Python pip3/Install Docker Python Module**: Installs Python modules onto target machine.
- **Enable Docker services on startup**: Enables docker to run on server startup.
- **Increase virtual memory/Use more memory**: Increases the maximum available memory to the ELK container.
- **Download and launch a docker elk container**:  Downloads and launches an ELK container on target machine and states ports in use.

**Using `nano`, update the hosts files in /etc/ansible to include:

Note: Names of Virtual Machines must correspond with the hosts in the .yml file.
This is how you will specify which machine to install the ELK server on versus which to install Filebeat on.<br>
`[webservers] <br>
10.0.0.5 ansible_python_interpreter=/usr/bin/python3<br>
10.0.0.7 ansible_python_interpreter=/usr/bin/python3<br>

[elk]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3
Update the *ansible.cfg* to include:`

Note: ansible.cfg is a User config file, which overrides the default config if present.
`remote_user = ansible`
Update the filebeat-config.yml file to include:

At line 1106:<br>
`hosts: ["10.1.0.4:9200"]
username: "elastic"
password: "changeme" 
At line 1806:
host: "10.1.0.4:5601"`
Run the playbook

ansible-playbook /etc/ansible/elk.yml

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK Instance](https://github.com/gman223/gman223-UofT-Cybersec-Project1/blob/main/Images/elk-running.JPG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 (Web 1)
- 10.0.0.6 (Web 2)
- 10.0.0.10 (Web 3)

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:

**Filebeat**: This beat collects log information from the designated servers. Will be able to sort and view information such as attempted or failed logins.

**Metricbeat**: This beat collects system resource information from the designated servers (CPU%, MEM%, etc.). If there is a sharp rise in resource usage this could be indicative of a DOS attack.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [ELK Playbook](https://github.com/gman223/gman223-UofT-Cybersec-Project1/blob/main/Files/elk-playbook.yml) to your Ansible container.
- Update the Ansible host file to include the private IP of your ELK VM
- Run the playbook, and navigate to `http://{your ELK VM Public IP}:5601/app/kibana` to check that the installation worked as expected.


