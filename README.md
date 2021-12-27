## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Screenshot](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Diagrams/RedTeam%20Network%20Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above, or alternatively, select playbooks contained in this repository may be used to install only certain pieces of it, such as Filebeat.

 1. [DVWA](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Ansible/Ansible%20DVWA%20Script.txt)
 2. [ELK Stack](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Ansible/Ansible%20ELK%20Stack%20Script.txt)
 3. [Filebeat 7.4.0](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Ansible/Filebeat%207.4.0%20Script.txt)
 4. [Metricbeat 7.4.0](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Ansible/Metricbeat%207.4.0%20Script.txt)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

**Load Balancing**

Load balancing ensures that the application will be highly efficient, accessible and scalable, in addition to restricting traffic overload to the network.
An crucial aspect that load balancers provide to a network is their ability to mitigate Distributed Denial of Service (DDoS) attacks.  This is achieved by a
load balancers inherent functionality of distributing inbound network traffic evenly across the networks backend pool of webservers.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

**Jumpbox Provisioner**

The Jumpbox Provisioner VM within my cloudnetwork is essential for scalable deployment of the network.  This is accomplished utilizing a Docker Container 
paired with Ansible, to conduct scripted tasks upon the various VM's within the network, such as installing Filebeat and Metric beat on our webservers.

**ELK Server**

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to specifically designated files and system logs.

- _**Filebeat:** Captures data from specified log files (such as Apache) and generates and organizes the files to send to Logstash and/or Elasticsearch.
- _**Metricbeat:** Collects and organizes metrics such as CPU usage, disk usage, and RAM

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function  | IP Address | Operating System |
|------------|-----------|------------|------------------|
| Jump Box   | Gateway   | 10.0.0.4   | Linux            |
| Web-1      | Webserver | 10.0.0.5   | Linux            |
| Web-2      | Webserver | 10.0.0.6   | Linux            |
| ELK-Server | ELK       | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the **Jumpox-Provisioner** machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _**172.83.5.46

Machines within the network can only be accessed by SSH-connection via port 22 from the Jumpbox-Provisioner VM.  Additionally, the ELK-server machine is 
only accessible from the following IP address:
- _**172.83.5.46

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | Yes                 | 172.83.5.46          |
| ELK        | Yes                 | 172.83.5.46          |
| Webservers | No                  |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
