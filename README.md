# CybersecurityP1
Elk Project 1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![CybersecurityP1/Images](https://github.com/slichtfuss/CybersecurityP1/blob/main/Images/FullNetwork.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the **Host** file may be used to install only certain pieces of it, such as Filebeat.

  - [Elk_Install](https://github.com/slichtfuss/CybersecurityP1/blob/main/Ansible/elk_install.yml)
  - [DVWA](https://github.com/slichtfuss/CybersecurityP1/blob/main/Ansible/dvwa_playbook.yml)
  - [Filebeat](https://github.com/slichtfuss/CybersecurityP1/blob/main/Ansible/filebeat_playbook.yml)
  - [Metricbeat](https://github.com/slichtfuss/CybersecurityP1/blob/main/Ansible/metricbeat_playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- **Load balancing is an important application that protects organizations from Denial of Service Attacks (DDoS). They will evenly distribute traffic among all servers     that are connected to it.**
- **A Jump Box allows for greater control over network access. In order to gain access, individuals must have the IPs of the machines and the firewall can assist in limiting the traffic.**

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **log files** and system **resources**.
- **Filebeat watches and gathers system logs and forwards any changes to Elastisearch**
- **Metricbeat is used for gathering metrics and sending them to Elastisearch and Kibana**

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Server   | 10.0.0.9   | Linux            |
| Web-2    | Server   | 10.0.0.6   | Linux            |
| Web-3    | Server   | 10.0.0.7   | Linux            |
| Elk-VM   | Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the **Jump Box** machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
  - **69.245.220.158**
  - **68.74.233.250**
  - **99.45.122.90**

Machines within the network can only be accessed by **the Jump Box**.
  -  Jump Box
    -  **Public IP: 13.64.193.107**
    - **Private IP: 10.0.0.4**

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses    |
|----------|---------------------|-------------------------|
| Jump Box | Yes                 | 10.0.0.4                |
| Web1,2,3 | No                  | Web LB - 52.160.162.222 |
| Web LB   | Yes - HTTP          | *                       |
| ELK      | Yes - Kibana - 5601 | *                       |
| ELK      | SSH - No - 22       | 99.45.122.90            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
  - Ansible automation helps considerably with the representation of infrastructure as code (IAC). It allows for full automation of a specific server and reduces configuration errors. 

The playbook implements the following tasks:
-**Install Docker: Installs the core docker code to the remote server** 
- **Install Python3_pip: Pip is an installation module to allow additional docker modules to be installed.**
- **Docker Module: Tells the previous PIP module to install the necessary docker component modules.**
- **Increase Memory/Use More Memory: This helps fix the limited memory issue of the ELK Docker image.**
- **Download and Launch ELK Container: Downloads the ELK Docker container and initializes it with the specified published ports.**

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![CybersecurityP1/Images](https://github.com/slichtfuss/CybersecurityP1/blob/main/Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- **Web1: 10.0.0.9** 
- **Web2: 10.0.0.6**
- **Web3: 10.0.0.7**

We have installed the following Beats on these machines:
- **Filebeat and Metricbeat have been installed on Web-1, Web-2, Web-3**

These Beats allow us to collect the following information from each machine:
- **Filebeat collects system type events such as logins to see who is actively logging into the system**
![Filebeat Example](https://github.com/slichtfuss/CybersecurityP1/blob/main/Images/Sample%20Log%20Data.png)
- **Metricbeat collects CPU usage, memory, and other useful information**
![Metricbeat Example](https://github.com/slichtfuss/CybersecurityP1/blob/main/Images/Metricbeat_example.png)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the **install-elk.yml** file to **/etc/ansible/roles/install-elk.yml**.
- Update the **hosts** file to include...
- ![Cybersecurity/Images](https://github.com/slichtfuss/CybersecurityP1/blob/main/Images/Hosts.png)
- Run the playbook, and navigate to **http://your_elk_server_ip:5601/app/kibana** to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it?_
  **Copy the install-elk.yml file to /etc/ansible/roles/install-elk.yml**
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? **Update filebeat-config.yml. Specify which machine to install by updating the host file with ip addresses of web and elk servers and selecting a group to run on.**
 
- _Which URL do you navigate to in order to check that the ELK server is running?
   **http://your_elk_server_ip:5601/app/kibana**

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
