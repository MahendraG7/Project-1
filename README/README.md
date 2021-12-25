## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Project1Diagram](https://github.com/MahendraG7/Project-1/blob/main/Diagrams/ProjectDiagram.jpg.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - [AnsiblePlaybook](https://github.com/MahendraG7/Project-1/tree/main/Ansible) 

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _Secure____, in addition to restricting _Public_Access___ to the network.
- What aspect of security do load balancers protect? They protect web traffic coming in and out of the network What is the advantage of a jump box?_The jumpbox serves as a gateway into the Subnet of the Virtual Network_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the __Network___ and system __Logs___.
- What does Filebeat watch for?_Filebeat watches system log data through various events
- What does Metricbeat record?_Metricbeat records metrics from services running on the system and outputs it to elastic or logstash_

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.6   | Linux            |
| Web-1    |  DVWA    | 10.0.0.8   | Linux            |
| Web-2    |  DVWA    | 10.0.0.9   | Linux            |
| ElkVM    | Kibana   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __Host___ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Jumpbox:10.0.0.6, Web-1:10.0.0.8, Web-2:10.0.0.9, ElkVM:10.1.0.4

Machines within the network can only be accessed by _Docker_Containers____.
-  Which machine did you allow to access your ELK VM? The Jumpbox VM. What was its IP address? 10.0.0.6

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses       |
|----------|---------------------|----------------------------|
| Jump Box |     No              | 10.0.0.8 10.0.0.9 10.1.0.4 |
|          |                     |                            |
|          |                     |                            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?_The main advantage of using Ansible to automate configuration files is that it deploys at higher speed because it performs without needing to install a software agent 

The playbook implements the following tasks:
-  Use apt module to Install Docker.io
-  Use apt module to Install pip3
-  Use pip3 module to Install docker python module
-  Use sysctl module to use more memory
-  Use docker container module to download and launch a docker elk container
-  Use systemd module to enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker ps output](Documents/GitHub/Project-1/Docker_ps_output)

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