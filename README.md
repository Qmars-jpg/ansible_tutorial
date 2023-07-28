# ansible_tutorial
this is awesome ansible repository!!!!!

#video 7 ansible 
# this a command to see informatoin about ansible distribution $: ansible all -m gather_facts --limit 172.17.02 | grep ansible_distribution 


#video 8 
# make order in lines, we can write this way :
# apt:
#   name:
#     - apache 2
#     - libapache2-mod-php
#    state: latest
#    when: ansible_distribution =="Ubuntu"
#
#
#here we use variables :
# apt:
#   name:
#     - "{{apache_package}}"     // variable1
#     - "{{php_package}}"        //varieble2
#    state: latest
#    when: ansible_distribution =="Ubuntu"
#after we open inventory file and write variables besides ip addresses:
#172.17.0.2  apache_package=apache2 php_package=libapache2-mod-php
#172.17.0.3  apache_package=apache2 php_package=libapache2-mod-php
#172.17.0.4  apache_package=apache2 php_package=libapache2-mod-php
# instead apt:
# use package:
#
#
#
# video 9
#
#create groups :
# inventory file
#      ***
#[web_servers] -   group 
#172.17.0.2
#      ***
#
#site.yml    // any name of a file .yml
#    ***
#
#- hosts: all
#  pre_tasks:             // it will done firstly for all hosts 
#  - name:  
#    apt:
#     update_only: yes
#     update_cache: yes   //additional tasks 
#     upgrade: dist
#    ***
#  
#
# video 10
#     SITE.YML
#- name:
#    tags: always , centos,db,ubuntu      // adding tags give us opportunity to choose what to install,update or so on. 
#    apt:
#     update_only: yes
#     update_cache: yes   //additional tasks 
#     upgrade: dist
#    *** COMMAND
#~/ansible$: ansible-playbook --list-tags site.yml   // it will reveal all tags we can choose 
#       *** 
#        COMMAND
#~/ansible$: ansible-playbook --tags"apache,db," site.yml    // here we choose tags "apache,db" to be executed 
#          ***
#
# video 11  COPY FILES
#   SITE.YML
#  ***
# - name: copy html file for site 
#   tags: ubunty, db
#   copy:
#     src: default_site.html
#     dest: /var/www/html/index.html      // after coping file has a new name index.html   
#     owner: root
#     group: root
#     mode: 0644
#    ***
# video 12  Managing services
#       ****
# - name: start and enable httpd (CentOS)
#
#
#     tags: apache,centos,httpd
#     service:
#       name: httpd
#
#      state: started              /// start service
#                   
#      enabled: yes                ///  all system starts and this service atoumatically starts
#     when: ansible_distribution == "CentOS"
#
#         ******
#
#  - name: change e-mail address for admin
#     tags: apache,centos,httpd
#     lineinfile:
#       path: /etc/httpd/conf/httpd.conf    // make changes in the line in the file
#       regexp: '^ServerAdmin'                 // line inthe file which we change
#
#       line: ServerAdmin somebody@somewhere.net // new line 
#     when: ansible_distribution == "CentOS"
#     register: httpd     // variable which indicates to change 
# 
#   - name: restart httpd (CentOS)
#     tags: apache,centos,httpd
#     service:
#       name: httpd
#       state: restarted        // it restarts the service    
#     when: httpd.changed    // indication to change 
#
#            *****
#
#
#
#
