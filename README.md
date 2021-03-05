## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(/ELK-Stack-Project/Images/network_diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, distributes the network traffic efficiently and make scalability easier.

The ELK server allows users to easily monitor the vulnerable VMs logs and system metrics.

The configuration details of each machine may be found below.

| Name     | Function   | IP Address |        OS         |
|----------|------------|------------|-------------------|
| Jump Box | Gateway    | 10.0.0.4   | Ubuntu 18.04-LTS  |
| Web1     | Web App    | 10.0.0.5   | Ubuntu 18.04-LTS  |
| Web2     | Web App    | 10.0.0.6   | Ubuntu 18.04-LTS  |
| Web3     | Web App    | 10.0.0.7   | Ubuntu 18.04-LTS  |
| ELK-VM   | Monitoring | 10.1.0.4   | Ubuntu 18.04-LTS  |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from one public IP address

Machines within the network can only be accessed by the jump box through SSH.

A summary of the access policies in place can be found in the table below.

|   Name   |  Publicly Accessible | Allowed IP Address/port |
|:--------:|:--------------------:|:-----------------------:|
| Jump Box |          yes         |      Public IP/SSH      |
|   Web1   |          no          |      Public IP/HTTP     |
|   Web2   |          no          |      Public IP/HTTP     |
|   Web3   |          no          |      Public IP/HTTP     |
|  ELK-VM  |          no          |            -            |

### Elk Configuration

Ansible was used to automate the configuration of the ELK machine. No configuration was performed manually, which is advantageous because makes deployment of multiples machines and scalability easier, once a good playbook as been configured properly it reduces the possibility of human error while deploying the same configuration on new machines.

The playbook implements the following tasks:
- First task is to install docker
- Then pip3 is installed to get packages for python3
- Third docker is installed from the pip module
- then the virtual memory of the machine is increased
- then the docker elk container is donwloaded using sebp/elk:761 image, and the ports required to run ELK are configured.
- last the docker service is configured to run upon booting

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(/ELK-Stack-Project/Images/docker_ps_ouput.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 Web1
- 10.0.0.6 Web2
- 10.0.0.7 Web3

We have installed the following Beats on these machines:
- Filebea: which monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat: which periodically collect metrics from the operating system and from services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible/
- Update the host file to include the IP addresses of the VM's you want to run the playbooks for.
- Run the playbook. The installation can by accessing the targeted VM through SSH, run "curl localhost:(port of the service installed)", or http://[your.VM.External.IP]:port, for example: Kibana's installation can be checked by running "curl localhost:5601/app/kibana" from the ELK vm, or by going to a web browser and typing "http://[your.ELK-VM.External.IP]:5601/app/kibana" adding the IP of the ELK machine to the URL. 

The playbooks and configuration files in this repo can be downloaded by copying the files "raw" format URL and running:
curl "URL" > "name of the file"
curl https://raw.githubusercontent.com/gigsforfun/ELK-Stack-Project/main/config_files/ansible.cfg > ansible.cgf