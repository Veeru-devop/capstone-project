CAPSTONE PROJECT Command File
++++++++++++++++++++++++++++++



Ansible installation commands
--------------------------------
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
--------------------------------



------------yaml file for ansible--------------- 
(from website: https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu)

---
- name: installing tools on master
  hosts: localhost
  become: true
  tasks: 
  - name: executing master.sh script
    script: master.sh
- name: installing tools on slaves
  hosts: slave1
  become: true
  tasks: 
  - name: executing slave.sh script
    script: slave.sh
- name: installing tools on slaves
  hosts: slave2
  become: true
  tasks: 
  - name: executing slave.sh script
    script: slave.sh


---------------master & slave scripts---------------------------
(create file slave.sh and paste commands present below)

sudo apt-get update
sudo apt-get install openjdk-11-jdk -y
sudo apt-get install docker.io -y

(create file master.sh and paste commands present below)
(please check the latest jenkins installation commands if you are using weekly release commands)

sudo apt-get update
sudo apt-get install openjdk-11-jdk -y
sudo apt-get install docker.io -y
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y

----------------------------------------------------------------------


github repo: https://github.com/hshar/website/


----------Dockerfile------------
FROM ubuntu
RUN apt update
RUN apt install apache2 -y
ADD . /var/www/html
ENTRYPOINT  apachectl -D FOREGROUND
--------------------------------


===============================================
Jenkins Execute shell commands:
===============================================

CONTAINERS=$(sudo docker ps -a -q)
if [ -n "$CONTAINERS" ]; then
  sudo docker rm -f $CONTAINERS
else
  echo "No containers to remove."
fi
sudo docker buildx create --use
sudo docker buildx build --load -t newimage2 .
sudo docker buildx build --push -t docker.io/veeruawsdevop/newimage2 .
sudo docker buildx build --load -t newimage2 .
sudo docker run -itd -p 80:80 newimage2
===============================================
Running for second time:
===============================================
CONTAINERS=$(sudo docker ps -a -q)
if [ -n "$CONTAINERS" ]; then
  sudo docker rm -f $CONTAINERS
else
  echo "No containers to remove."
fi
sudo docker buildx create --use
sudo docker buildx build --load -t newimage2 .
sudo docker buildx build --push -t docker.io/veeruawsdevop/newimage2 .
sudo docker buildx build --load -t newimage2 .
sudo docker run -itd -p 80:80 newimage2





