## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Project1Diagram](https://raw.githubusercontent.com/MahendraG7/Project-1/main/Diagrams/FinishedDiagram.JPG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Edited playbook file may be used to install only certain pieces of it, such as Filebeat.

  - [AnsiblePlaybook](https://github.com/MahendraG7/Project-1/tree/main/Ansible) 

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnernable Web Application.

Load balancing ensures that the application will be highly Secure, in addition to restricting Unauthorized Access to the network.
-  They protect web traffic coming in and out of the network, also they protect applications from threats. The jumpbox serves as a gateway into the Subnet of the Virtual Network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Network and system Logs.
- Filebeat watches system log data through various events that is specied and sends it to Kibana
- Metricbeat records metrics from services running on the system and outputs it to kibana

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.6   | Linux            |
| Web-1    |  DVWA    | 10.0.0.8   | Linux            |
| Web-2    |  DVWA    | 10.0.0.9   | Linux            |
| ElkVM    | Kibana   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Host machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Jumpbox:10.0.0.6, Web-1:10.0.0.8, Web-2:10.0.0.9, ElkVM:10.1.0.4

Machines within the network can only be accessed by Docker Containers.
-   The ELK VM can only be accessed through The Jumpbox VM 10.0.0.6

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses       |
|----------|---------------------|----------------------------|
| Jump Box |    yes              | 10.0.0.8 10.0.0.9 10.1.0.4 |
|  Elk     |     yes             | 10.0.0.6                   |
| Web-1    |     No              | 10.0.0.6                   |
| Web-2    |    No               | 10.0.0.6                   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it deploys at higher speeds and it performs without needing to install a software agent 

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
- 10.0.0.8, 10.0.0.9

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
-  Filebeat collects log data and forwards them to logstash or elasticsearch. I expect Filebeat to process inbound traffic data and send it to elasticsearch or logstash to analyze.
-  Metricbeat collects metrics from services running on the system. If im running anything out of web-1 and web-2 I expect Metricbeat to record and output that data on kibana through elastic or logstash.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yml file to ansible.
- Update the ansible file to include the playbook
- Run the playbook, and then navigate to IP address to check that the installation worked as expected.

- install-elk.yml it the playbook and I copied it to nano
- We then changed the host IP to elk IP to make sure the playbook downloaded to the right machine on lines 1105 and 1805 on the filebeat config and metricbeat config
- To check that the ELKserver is running went to http://23.99.204.44:5601/app/kibana
