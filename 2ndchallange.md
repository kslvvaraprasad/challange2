# BAHMNI INTRODUCTION

* Bahmni is a free and open source hospital system designed for low resource settings

* You can run bahmni on centos, windows, apple and other linux platforms.

### MANUAL INSTALLATION PROCEDURE

* For bahmni installation manually on centos [REFER HERE](https://bahmni.atlassian.net/wiki/spaces/BAH/pages/33128505/Install+Bahmni+on+CentOS)

* For bahmni installation manually on windows,apply,other linux platfors we have to have a centos vm . For installation procedure [REFER HERE](https://bahmni.atlassian.net/wiki/spaces/BAH/pages/1471284)

### AUTOMATION OF BAHMNI USING ANSIBLE

* We can automate bahmni installation using ansible .

* for this we have to write ansible playbooks .

* For writing ansible playbooks please [REFER HERE](https://docs.ansible.com/ansible/latest/user_guide/index.html) .This page describes from basics of ansible to writing playbooks . 

* After installation you can access home page of BAHMNI using ipaddress as following                                    
 http://ipaddress/home  
 
##  Home page of bahmni 

![preview](https://github.com/kslvvaraprasad/challange2/blob/master/images/bahmnihomepage.PNG)


##  HERE incorporated the ansible playbook i wrote to automate bahmni installation using ansible.


```
---
    - hosts: all
      remote_user: root
      tasks:
        - name: Prerequisite for the fresh installation of Bahmni
          yum:
            name: https://kojipkgs.fedoraproject.org//packages/zlib/1.2.11/19.fc30/x86_64/zlib-1.2.11-19.fc30.x86_64.rpm
            state: present
        - name: Install the bahmni command line program
          yum:
            name: https://dl.bintray.com/bahmni/rpm/rpms/bahmni-installer-0.92-147.noarch.rpm
            state: present
        - name: Now setup a configuration file for bahmni command in /etc/bahmni-installer
          shell:
            cmd: curl -L https://tinyurl.com/yyoj98df >> /etc/bahmni-installer/setup.yml
        - name: appending
          copy:
            src: /home/devops/setup.yml
            dest: /etc/bahmni-installer/setup.yml
        - name: abcd
          shell:
            cmd: echo "export BAHMNI_INVENTORY=local" >> ~/.bashrc
        - name: abcdef
          shell:
            cmd: source ~/.bashrc
        - name: installing bahmni
          shell:
            cmd: bahmni install

```
## DEVOPS PIPELINE FOR BAHMNI INSTALLATION

* The plan of action for automating installation of BAHMNI is as follows
   
   - first take a t2.medium machine (i preferred ubuntu ami)and install jenkins.   
   
   - take a t2.medium machine ,tag it as "ANSIBLE" for easy reference. Login in to the machine add a user          
          
       with name (preferrably jenkins or devops) as of your wish. 
  
   -  Add this "ANSIBLE" machine as node to jenkins server so that we can deploy our jobs.
    
   - Now take a centos 7 machine with minimun of 8 Gb RAM .For BAHMNI 0.92 version we have to use centos 7.

   ![preview](https://github.com/kslvvaraprasad/challange2/blob/master/images/3machines.PNG)

   - In our "ACS" machine install ansible and configure it with centos node.

   - In our "ACS" machine we write our ansible play book to install BAHMNI application.The contents of             playbook are described above.
  
    - Now we can call ansible node to install BAHMNI on centos using jenkins.
    
  ![preview](https://github.com/kslvvaraprasad/challange2/blob/master/images/devops1.PNG)

    - wait for few minutes 
    
    
    - now take public ip of machine .you can access home page  http://machine-ip/home
    
       it will be like 

       ![preview](https://github.com/kslvvaraprasad/challange2/blob/master/images/devops3.PNG)

    - you can access openmrs page using http://machine-ip/openmrs

    it looks like 

    ![preview](https://github.com/kslvvaraprasad/challange2/blob/master/images/devops4.PNG)
    


    - and few other application pages looks like 

    
    ![preview](https://github.com/kslvvaraprasad/challange2/blob/master/images/devops5.PNG)


  ## AND FINALLY 


    BUILD SUCCESS FROM JENKINS



    ![Preview](https://github.com/kslvvaraprasad/challange2/blob/master/images/devops6.PNG)


















            ------------------*** THIS IS MY WAY OF DEVOPS PIPELINE  ***---------------------


  ***************************************           THANK YOU        *************************************


