# CyberSecurityA-
Culmination of UCLA Cybersecurity work
Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - Filebeat_Playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable , in addition to restricting access to the network.
Load Balancers distribute the workload between the different Vms preventing overloads due to DoS attacks. The advantage of implementing a JumpBox is to bottleneck access to one administrator machine.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the various Vms and their system logs.
- Filebeat watches for changes in the files and sends this information to Logstash and Elasticsearch to organize these logs.
- MetricBeat records metrics from the operating system and the various services running. The user may then choose to send this information to an outlet such as Logstash or Elasticsearch

The configuration details of each machine may be found below.

| Name       | Function         | IP Address | Operating System |
|------------|------------------|------------|------------------|
| JumpMan    | Gateway          | 10.0.1.4   | Linux            |
| RedTeamVM  | DWVA Container   | 10.0.1.13  | Linux            |
| RedTeamVM1 | DWVA Container   | 10.0.1.8   | Linux            |
| RedTeamVM2 | DWVA Container   | 10.0.1.7   | Linux            |
| ELKVM      | Configuration VM | 10.1.0.4   | Linux            |

Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpMan machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My personal PC at 172.89.13.194

Machines within the network can only be accessed by accessing the Magical_Jang DWVA Container on the JumpMan.

The only machines able to access the ELK server are my personal PC at 172.89.13.194 and the JumpMan Vm at 10.0.1.4.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses    |
|------------|---------------------|-------------------------|
| JumpMan    | Yes                 | 10.0.1.4, 172.89.13.194 |
| RedTeamVM  | No                  | 10.0.1.4                |
| RedTeamVM  | No                  | 10.0.1.4                |
| RedTeamVM1 | No                  | 10.0.1.4                |
| ELKVM      | No                  | 10.1.0.4, 172.89.13.194 |


Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because with the ansible .yml files created the process of configuring the various VM’s becomes easy for anyone in the IT department thus increasing productivity.

The playbook implements the following tasks:
Installs Docker.io and Docker Module
Installs python3-pip
Increases virtual memory
Downloads and launchers ELK docker container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


Path to screenshot above Images/dockerps

Target Machines & Beats

This ELK server is configured to monitor the following machines:
RedTeamVm 10.0.1.13
RedTeamVm1 10.0.1.8
RedTeamVm2 10.0.1.7


We have installed the following Beats on these machines:
Filebeat
Metricbeat


These Beats allow us to collect the following information from each machine:
The Filebeat collects and logs data on changes made to the various files on the system. Within Filebeat logs we would expect to see data regarding the change in a files name, position,contents, etc.

The Metricbeat collects and logs data on changes made to the operating system and the services running on the machine. Within Metricbeat would expect to see data on which services are currently running and how much CPU they are taking compared to others.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Filebeat_config.yml file to etc/ansible/roles.
- Update the filebeat_config.yml file to include the private IP of the ELK server
- Run the playbook, and navigate to the Kibana Dashboard at 40.70.208.135[ELK public IP]/app/Kibana to check that the installation worked as expected.

