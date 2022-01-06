Cloud Network

Linux Scripts and Ansible Scripts from my CyberSecurity Course.

Most of the scripts are used to configure cloud servers with different docker containers.

The final setup was 3 servers running vulnerable DVWA containers with a jump box and a server running an ELK stack container.


## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!(/scripts/Images/Network Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  - elk_book.yml,ansible_config.yml,filebeat-playbook.yml and metricbeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive by ensuring servers aren't overloaded with requests, in addition to restricting unauthenticated access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system services.
- Filebeat is included to handle simple log and file forwarding
- Metricbeat is included to collect metrics on the system and other services running on the server.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| DVWA1    |    VM    | 10.0.0.5   | Linux            |
| DVWA2    |    VM    | 10.0.0.6   | Linux            |
| ELK      |    VM    | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Host Machine IP address(s). ie. 71.218.240.141

Machines within the network can only be accessed by JumpBox.
- The same host machine(s) that was allowed to access the Jumpbox were set to have access to the ELK server as well.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 71.218.240.141       |
|   ELK    | Yes                 | 71.218.240.141       |
|  DVWA1   | No                  | 10.0.0.4             |
|  DVWA2   | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
this allows to add any additional machines with consistent setting as previous machines.

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install docker module
- Increase virtual memory
- download and launch a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!/scripts/images/ansible host docker ps.png
!/scripts/images/DVWA1 elk instance docker ps.png
!/scripts/images/DVWA2 elk instance docker ps.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- DVWA1 and DVWA2 with IP addresses 10.0.0.5 and 10.0.0.6 respectively.

We have installed the following Beats on these machines:
- Filebeat and MetricBeat have been installed on current machines.

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects and centralizes logs and files such as system.syslog. Metricbeat collects metrics from the system and services such as Apache and MySQL.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_book.yml file to /etc/ansible.
- Update the host file to include IP(s) of additional target webservers in the elk group.
- Run the playbook, and navigate to the IP of the load balancer at port 5601 to check that the installation worked as expected.