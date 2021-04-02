# ReadMeElk
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram Azure cloud topology homework "C:\Users\silvo\OneDrive\Desktop\Northwestern Cybersecurity\12. Cloud Security and Virtualization\Azure cloud topology homework.docx"

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file.ansible-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly availability, in addition to restricting traffic to the network.
- _TODO: What aspect of security do load balancers protect? Load balacers proctect agaist DDoS attacks. What is the advantage of a jump box? Jump box prevents all azure VM's to be expose to the public. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- _TODO: What does Filebeat watch for? the logs
- _TODO: What does Metricbeat record? the performace of the machine

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name          | Function       | IP Address               |   OS  |
|----------     |----------      |--------------------------|-------|
| Jump Box      | Gateway        |  10.0.0.4/52.136.124.58  | Linux |
| ELK-SERVER    | Elk-server     |  10.1.0.4/20.36.0.231    | Linux |
| Web-1         | Web server     |  10.0.0.5/137.117.38.52  | Linux |
| Web-2         | Web server     |  10.0.0.6/137.117.38.52  | Linux |
| DVWA-VM       | Web server     |  10.0.0.8/137.117.38.52  | Linux |
| Load Balancer | load balancer  |  137.117.38.52           | Linux |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK-SERVER machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:52.136.124.58
- _TODO: Add whitelisted IP addresses: 52.136.124.58

Machines within the network can only be accessed by Jump-box-provisioner.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address? 
Jump-Box-Provisioner IP 10.0.0.4 via SSH port 22


A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses     |
|---------------|---------------------|----------------------    |
| Jump Box      |     No              |  10.0.0.1 10.0.0.2       |
| ELK-SERVER    |     Yes             |  20.36.0.231             |
| Web-1         |     No              |  10.0.0.5/137.117.38.52  | 
| Web-2         |     No              |  10.0.0.6/137.117.38.52  | 
| DVWA-VM3      |     No              |  10.0.0.8/137.117.38.52  | 
| Load Balancer |     Yes             |  137.117.38.52           | 

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because ansible lets you deploy multiple apps. 
- _TODO: What is the main advantage of automating configuration with Ansible? You do not need to write custom code to automate your sistems, you only require to write playbook. Ansible automitation helps considerably with representation as a code. 

The playbook implements the following tasks:

- Create a new Ansible playbook to use for your new ELK virtual machine.
- - name: Config elk VM with Docker
  hosts: elk
  remote_user: azadmin
  become: true
  tasks:

-  Increase the memory
- name: Use more memory
  sysctl:
    name: vm.max_map_count
    value: '262144'
    state: present
    reload: yes

- The playbook should then install the following services:
docker.io
python3-pip
docker, which is the Docker Python pip module.

The container should be started with these published ports:
5601:5601
9200:9200
5044:5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
"C:\Users\silvo\Downloads\Docker installation screenshot.jpg"
"C:\Users\silvo\Downloads\Docker installation screenshot1.jpg"

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web1  10.0.0.5
Web2  10.0.0.6
DVW-VM3  10.0.0.8

We have installed the following Beats on these machines:
ELK server, Web1, Web2, DVW-VM3
The ELK Stack installed are: FileBeat and MetricBeat

These Beats allow us to collect the following information from each machine:
- Filebeats: log events.Collects data about the file system
- Metricbeat: metrics and system statics. Collects machine metrics, such as uptime

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

For ELK VM Configuration:
- Copy the Ansible ELK Istallation file and VM configuration.
- Update the Ansible file to include a group of machines as well as a differet remote user. 
- Increase the memory
- Run the playbook using the following command:
ansible-playbook install-elk.ymland 
- Navigate to ELK container to check that the installation worked as expected.

- Which file is the playbook? elk.yml
- Where do you copy it? ansible-playbook
- Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible/hosts
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- Which URL do you navigate to in order to check that the ELK server is running? http://20.36.0.231:5601/app/kibana

Create a new Ansible playbook to use for your new ELK virtual machine.

Commads to download and configure the ELK VM
- SSH into your Jump-Box using ssh RedAdmin@52.136.124.58
- check for the ansible container: sudo docker ps
-locate the container: sudo docker container list -a
- start the container: sudo docker container start Lederber
- connect to the ansible container: sudo docker container attach Lederberg
copy SSH key from the ansible container on your jump box: cat ~/.ssh/id_rsa.pub

The header of the Ansible playbook can specify a different group of machines as well as a different remote user (in case you did not use the same admin name):
- name: Config elk VM with Docker
  hosts: elk
  remote_user: RedAdmin
  become: true
  tasks:


Before you can run the elk container, we need to increase the memory:

- name: Use more memory
  sysctl:
    name: vm.max_map_count
    value: '262144'
    state: present
    reload: yes

This is a system requirement for the ELK container. More info at the elk-docker documentation.
The playbook should then install the following services:

docker.io
python3-pip

docker, which is the Docker Python pip module.

 Launching and Exposing the Container
After Docker is installed, download and run the sebp/elk:761 container.

The container should be started with these published ports:

5601:5601
9200:9200
5044:5044
//////////////////////////////

Your Ansible output should resemble the output below and not contain any errors:
root@6160a9be360e:/etc/ansible# ansible-playbook elk.yml


PLAY RECAP *****************************************************************************
10.1.0.4                   : ok=1    changed=7    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 


SSH from your Ansible container to your ELK machine to verify the connection before you run your playbook.


After the ELK container is installed, SSH to your container and double check that your elk-docker container is running.


Run sudo docker ps
sysadmin@elk:~$ sudo docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                                                              NAMES
842caa422ed8        sebp/elk            "/usr/local/bin/star…"   3 hours ago         Up 3 hours          0.0.0.0:5044->5044/tcp, 0.0.0.0:5601->5601/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   elk
sysadmin@elk:~$

Ansible YAML scripts 

2.	Create a YAML playbook file that you will use for your configuration.

root@1f08425a2967:~# nano /etc/ansible/pentest.yml
 
4.	To test that DVWA is running on the new VM, SSH to the new VM from your Ansible container.
o	SSH to your container:
5.	root@1f08425a2967:~# ssh sysadmin@10.0.0.6
6.	Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 5.0.0-1027-azure x86_64)
7.	
8.	* Documentation:  https://help.ubuntu.com
9.	* Management:     https://landscape.canonical.com
10.	* Support:        https://ubuntu.com/advantage
11.	
12.	  System information as of Mon Jan  6 20:01:03 UTC 2020
13.	
14.	  System load:  0.01              Processes:              122
15.	  Usage of /:   9.9% of 28.90GB   Users logged in:        0
16.	  Memory usage: 58%               IP address for eth0:    10.0.0.6
17.	  Swap usage:   0%                IP address for docker0: 172.17.0.1
18.	
19.	
20.	18 packages can be updated.
21.	0 updates are security updates.
22.	
23.	
Last login: Mon Jan  6 19:33:51 2020 from 10.0.0.4

o	Run curl localhost/setup.php to test the connection. If everything is working, you should get back some HTML from the DVWA container.
ansible@Pentest-1:~$ curl localhost/setup.php

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">

  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />

    <title>Setup :: Damn Vulnerable Web Application (DVWA) v1.10 *Development*</title>

    <link rel="stylesheet" type="text/css" href="dvwa/css/main.css" />

    <link rel="icon" type="\image/ico" href="favicon.ico" />

    <script type="text/javascript" src="dvwa/js/dvwaPage.js"></script>

  </head>



