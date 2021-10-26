# Cyber-Security-Activities
These are just some of the work I have done while studying and learning Cyber Security
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram of Cloud Security](https://user-images.githubusercontent.com/87392852/138788711-f061d436-5bf2-45df-94c4-0e3a78236c40.PNG)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

DVWA
https://github.com/Robert99Alexander/Cyber-Security-Activities/blob/b9b734dd41710c15e6efbd748d966dd2ead7eecf/Ansible/DVWA-Playbook.PNG

Elk
https://github.com/Robert99Alexander/Cyber-Security-Activities/blob/b9b734dd41710c15e6efbd748d966dd2ead7eecf/Ansible/Elk-Playbook

Filebeat
https://github.com/Robert99Alexander/Cyber-Security-Activities/blob/b9b734dd41710c15e6efbd748d966dd2ead7eecf/Ansible/Filebeat-Playbook.PNG

Metricbeat
https://github.com/Robert99Alexander/Cyber-Security-Activities/blob/b9b734dd41710c15e6efbd748d966dd2ead7eecf/Ansible/Metricbeat-Playbook.PNG

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting access to the network.
-What aspect of security do load balancers protect? 
The purpose of a load balancing is to help with the flow of traffic throughout a network. The load balancer will dispense traffic evenly for all of the servers, thus lowering the risk of a an attack known as a DoS Attack(Denial of Service) which is an attack that focuses on flooding a target with traffic leading it to being shut down/crash. 

-What is the advantage of a jump box?
The advantage of a jumpbox is simply to control access and not expose other webservers to the public. It is used as a our connection point to "jump" from one VM to another. With the JumpBox, we can easily monitor and logging and handle connectivity features. Also we can use our NSGs to allow certain access to the JumpBox preventing unwanted and untrusted access. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs of machines deployed and system traffic.
- What does Filebeat watch for?
Filebeat logs information in a system, like when and how a file changes. 
- What does Metricbeat record?
Metricbeat records the statistics from operating system.  This helps monitors the servers by recording metrics on a system.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| WEB-1    | webserver| 10.0.0.5   | Linux            |
| WEB-2    | webserver| 10.0.0.6   | Linux            |
| ELK      | monitor  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 99.98.178.119

Machines within the network can only be accessed by JumpBox Virtual Machine.
- The machine I allowed accessed to the Elk machine was only the JumpBox machine and the Ip address is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| JumpBox  | No                  | 99.98.178.119        |
| WEB-1    | No                  | 10.0.0.4             |
| WEB-2    | No                  | 10.0.0.4             |
| Elk      | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible allows us the ability to automate tasks, saving a lot of time. The simplicity of it also helps building an ansible playbook written in YAML, arguably making it a better configuation management tool over other formats like JSON.

The playbook implements the following tasks:
- Install Docker
- Install python3.pip
- Install Docker python module
- download and launch docker web container
- Enable docker service

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![elk-docker ps](https://user-images.githubusercontent.com/87392852/138780256-adc9d2e8-06d1-487f-bf7a-d63319950023.PNG)


This ELK server is configured to monitor the following machines:
- Web1- 10.0.0.5
- Web2- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat collects different log data/files, logging info on file system. You will see data collect such as ssh logins and syslog events. 

Metricbeat collects statistics of a OS and services on a server, where we can see usage of a webserver at a given time. Such as cpu and memory usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk-playbook file to /etc/ansible/Install-Elk.yml
- Update the host file <nano hosts> to include the Elk Ip and then add ansible_python_interpreter=/usr/bin/python3 to specify. 
![project1 elk-host-ansible](https://user-images.githubusercontent.com/87392852/138780234-0a120de7-6592-4112-8c29-f886b9fc6342.PNG)
- Run the playbook, using command <ansible-playbook Install-Elk.yml> and navigate to kibana to check that the installation worked as expected. You will have to do http://[your-elk-public-IP]:5601/app/kibana to see if the installation worked.
 ![Project 1 Kibana1](https://user-images.githubusercontent.com/87392852/138789431-241ecc9c-199d-4780-ae2b-049a0352a695.PNG)

