## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Screenshot](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Diagrams/RedNet%20Diagram.jpg)

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

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

**Load Balancing**

Load balancing ensures that the application will be highly efficient, accessible and scalable, in addition to restricting traffic overload to the network.
An crucial aspect that load balancers provide to a network is their ability to mitigate Distributed Denial of Service (DDoS) attacks.  This is achieved by a
load balancers inherent functionality of distributing inbound network traffic evenly across the network's backend pool of webservers.

**Jumpbox Provisioner**

The Jumpbox Provisioner VM within my cloudnetwork is essential for scalable deployment of the network.  This is accomplished utilizing a Docker Container 
paired with Ansible, to conduct scripted tasks upon the various VM's within the network, such as installing Filebeat and Metric beat on our webservers.

**ELK Server**

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to specifically designated files and system logs:
- **Filebeat:** Captures data from specified log files (such as Apache) and generates and organizes the files to send to Logstash and/or Elasticsearch.
- **Metricbeat:** Collects and organizes metrics such as CPU usage, disk usage, and RAM

The configuration details of each machine may be found below.

| Name       | Function  | IP Address | Operating System |
|------------|-----------|------------|------------------|
| Jump Box   | Gateway   | 10.0.0.4   | Linux            |
| Web-1      | Webserver | 10.0.0.5   | Linux            |
| Web-2      | Webserver | 10.0.0.6   | Linux            |
| ELK-Server | ELK       | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the **Jumpox-Provisioner** machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- **172.1.1.1** (for replication purposes, identify a workstation IP of your choice)

Machines within the network can only be accessed by SSH-connection via port 22 from the Jumpbox-Provisioner VM.  Additionally, the ELK-server machine is 
only accessible from the following IP address:
- **172.1.1.1** (for replication purposes, identify a workstation IP of your choice)

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | Yes                 | 172.1.1.1            |
| ELK        | Yes                 | 172.1.1.1            |
| Webservers | No                  |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because:
- It reduces the probability of human error associated with manual configuations
- Automation drastically decreases the man hours that would be needed
- Implementing automation greatly increases the scalability of your network

The playbook implements the following tasks:
- **Step 1:** Establishes the "elk" group as the IPs that will be configured by the playbook
- **Step 2:** Installs Docker
- **Steps 3-4:** Installs python 3 and python docker module, respectively
- **Steps 5-6:** Enables our ELK-server VM to utilize more RAM for maximum functionality
- **Step 7:** Installs our ELK stack onto our ELK-server VM.  Establishes that port 5601 will be used to view Kibana
- **Step 8:** Enables the Docker services on the boot of the ELK-server VM

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.0.0.5)
- Web-2 (10.0.0.6)

We have installed the following Beats on these machines:
- [Filebeat](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Ansible/Filebeat%207.4.0%20Script.txt)
- [Metricbeat](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Ansible/Metricbeat%207.4.0%20Script.txt)

These Beats allow us to collect the following information from each machine:
- **Filebeat:** Filebeat is utilized to collect log file data from specific locations.  This data is then organized, compiled and sent to Logstash/Elasticsearch.  For this instance, Filebeat is being utilized for webservers, and is monitoring data packets that are being sent to and from our webservers.
- **Metricbeat:** Metricbeat collects metrics based on a specified service.  This can range from OS of visitors, unique visitors to a website, unique visitors by country etc.  Such metrics are applicable to our webservers due to Metricbeat being used to collect web logs. 

### Using the ELK Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [ELK Script](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Ansible/Ansible%20ELK%20Stack%20Script.txt) file to `/etc/ansible/` within your Ansible node.
- Update the `hosts`, located in the `/etc/ansible` directory
  - `nano hosts` 
- Update the following:
  - Identify which IP address belongs to your elk group (this is the server that will monitor your webservers and where we will install our ELK container onto).  Additionally, establish that python 3 will be the interpreting language.  Here is an example:
   ![Screenshot](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Images/elk%20hosts.jpg)
  
- Run the playbook
  - `ansible-playbook elk-playbook.yml`
- Navigate to ELK-servers IP address and established port to check that the installation worked as expected. Here is an example:
  ![Screenshot](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Images/Kibana%20Website.jpg)
  
### Using the Filebeat Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [Filebeat 7.4.0](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Ansible/Filebeat%207.4.0%20Script.txt) file to `/etc/ansible/roles` within your Ansible node.
- Update the `hosts` file, located in the `/etc/ansible` directory,
  - `nano hosts`
- Update the following:
  - Establish which IP addresses belong to your webservers group (these will have Filebeat and Metricbeat installed onto them). Additionally, establish that python 3 will be the interpreting language. Here is an example:
  
   ![Screenshot](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Images/webservers%20hosts.jpg)
 
- Run the playbook
  - `ansible-playbook filebeat-playbook.yml` 
- Navigate to [ELK-servers IP address:established port/app/kibana#/home/tutorial/systemLogs] (e.g. `http://52.180.145.34:5601/app/kibana#/home/tutorial/systemLogs` to check that the log file data is being collected.  Once at the site, scroll to the bottom and click **"Check Data"** on the right side of the **"Module Status"** section. Here is what you should see after a successful deployment of Filebeat:
  ![Screenshot](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Images/Filebeat%20Check%20Data.jpg)
  - **Note:** Your webserver and ELK-server VMs need to be running to allow Filebeat to collect data. 
  
### Using the Metricbeat Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [Metricbeat 7.4.0](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Ansible/Metricbeat%207.4.0%20Script.txt) file to `/etc/ansible/roles` within your Ansible node.
- Update the `hosts` file, located in the `/etc/ansible` directory 
  - `nano hosts`
- Update the following:
  - Establish which IP addresses belong to your webservers group (these will have Filebeat and Metricbeat installed onto them). Additionally, establish that python 3 will be the interpreting language. Here is an example:
  
   ![Screenshot](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Images/webservers%20hosts.jpg)
 
- Run the playbook
  - `ansible-playbook metricbeat-playbook.yml` 
- Navigate to [ELK-servers IP address:established port/app/kibana#/home/tutorial/systemMetrics (e.g. `http://52.180.145.34:5601/app/kibana#/home/tutorial/systemMetrics` to check that the log file data is being collected.  Once at the site, scroll to the bottom and click **"Check Data"** on the right side of the **"Module Status"** section. Here is what you should see after a successful deployment of Metricbeat:
  ![Screenshot](https://github.com/kylewainwright/Cloud-Security-Network/blob/main/Images/Metricbeat%20Check%20Data.jpg)
  - **Note:** Your webserver and ELK-server VMs need to be running to allow Metricbeat to collect data.



