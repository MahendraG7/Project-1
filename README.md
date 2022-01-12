## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Project1Diagram](https://github.com/MahendraG7/Project-1/blob/main/Diagrams/ProjectDiagram.jpg.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _Edited_Playbook_file may be used to install only certain pieces of it, such as Filebeat.

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

Load balancing ensures that the application will be highly _Secure_, in addition to restricting _Unauthorized_Access_ to the network.
- What aspect of security do load balancers protect? They protect web traffic coming in and out of the network, also they protect applications from threats. What is the advantage of a jump box?_The jumpbox serves as a gateway into the Subnet of the Virtual Network_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the __Network___ and system __Logs___.
- What does Filebeat watch for?_Filebeat watches system log data through various events that is specied and sends it ot Kibana
- What does Metricbeat record?_Metricbeat records metrics from services running on the system and outputs it to kibana_

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

Machines within the network can only be accessed by _Docker_Containers_.
-  Which machine did you allow to access your ELK VM? The Jumpbox VM. What was its IP address? 10.0.0.6

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses       |
|----------|---------------------|----------------------------|
| Jump Box |    yes              | 10.0.0.8 10.0.0.9 10.1.0.4 |
|  Elk     |     No              | 10.0.0.6                   |
| Web-1    |     No              | 10.0.0.6                   |
| Web-2    |    No               | 10.0.0.6                   |

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

![Docker ps output](https://raw.githubusercontent.com/MahendraG7/Project-1/main/Docker%20ps%20Output.JPG)
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-  List the IP addresses of the machines you are monitoring:10.0.0.8, 10.0.0.9

We have installed the following Beats on these machines:
-  Specify which Beats you successfully installed:We installed Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
-  In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
-  Filebeat collects log data and forwards them to logstash or elasticsearch. I expect Filebeat to process inbound traffic data and send it to elasticsearch or logstash to analyze.
-  Metricbeat collects metrics from services running on the system. If im running anything out of web-1 and web-2 I expect Metricbeat to record and output that data on kibana through elastic or logstash.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ___yml__ file to _ansible__.
- Update the __ansible__ file to include the playbook
- Run the playbook, and navigate to __IP_address__ to check that the installation worked as expected.

_  Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_install-elk.yml and I copied it to nano
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_We changed the host IP to elk IP to make sure the playbook downloaded to the right machine on lines 1105 and 1805 on the filebeat config and metricbeat config
- _Which URL do you navigate to in order to check that the ELK server is running? http://23.99.204.44:5601/app/kibana
