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
#
