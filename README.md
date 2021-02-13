## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  filebeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient in distributing incoming network traffic, in addition to restricting unneccesary access to the network.
 Load Balancers help to protect the servers against DDoS attacks. Jumpbox acts as gateway router which allows security professionals to implement strong access controls on a single machine rather than on every individual virtual machine, which reduces the attack surface.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system files.
- Filebeat collects data about the file system.
- Metricbeat records machine metrics._

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1 |Virtual Machine| 10.0.0.9 | Linux            |
| Web-2 |Virtual Machine|10.0.0.10 | Linux            |
| ELK   |Virtual Machine|10.1.0.4  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
65.48.142.105 (local ip address)

Machines within the network can only be accessed by ELK VM.
WEB-1 and WEB-2 can access ELK VM, ip addresses:
10.0.0.9 and 10.0.0.10

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| JumpBox | Yes (from your local computer)| Personal IP    |
|Web-1     | No                 |  10.0.0.9      |
|Web-2     | No                 |   10.0.0.10     |
|Elk VM    |Yes                  |   10.1.0.4 and Personal IP     |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-Ansible allows to configure many machines at the same time, also perform tasks automatically.

The playbook implements the following tasks:
Configures Elk VM with Docker
Installs docker.io
Installs python3-pip
Installs docker module
Increases virutal memory
downloads and launches a docker elk container
enables service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/Picture1.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-        1) Web-1, Public ip: 40.87.108.238 Private ip: 10.0.0.9
         2) Web-2, Public ip: 40.87.108.238 Private ip: 10.0.0.10

We have installed the following Beats on these machines:
    filebeat, metricbeat

These Beats allow us to collect the following information from each machine:
        Filebeat collects data about the file system: syslog.
        Metricbeat collects machine metrics: uptime, cpu usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat.yml file to /etc/ansible/roles/files directory.
- Update the configuration file to include Private IP of the Elk VM.
- Run the playbook, and navigate to Elk VM to check that the installation worked as expected.

The playbook file is called filebeat-playbook.yml, copy it into your /etc/ansible/roles/files/ directory.
 To be able to make Ansible run the playbook on a specific machine you'll need to update filebeat.yml configuration file. You will also need to create a new group in the host.cfg file, add a new group Webservers  and add the Private Elk Server IP address. You also need to configure filebeat.yml and update Private IPs there on 1106 and 1806 lines.

You can verify whether your server is running by going to Kibana url using the Elk VM IP and port 5601. 
example: http://40.75.8.12:5601/app/kibana#/home