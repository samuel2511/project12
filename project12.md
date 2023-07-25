# ANSIBLE REFACTORING AND STATIC ASSIGNMENTS

In this project you i continue working with ansible-config-mgt repository, set-up for project 11, I created a directory to copy all the artifacts in the jenkins ansible job. Then I change the permission of the file to allow anybody to read, write and execute on the directory so that jenkins will also be able to add to the directory
![](./image/1.PNG)

then i Change permissions to this directory, so Jenkins could save files there – chmod -R 0777 /home/ubuntu/ansible-config-artifact
after changing my permissions i went to my jenkins web console  Manage Jenkins -> Manage Plugins -> on Available tab i search for Copy Artifact and install it without restarting,then i create a new freestlye project and name it save_artifacts.
![](./image/2.PNG)
![](./image/3.PNG)
![](./image/4.PNG)
![](./image/5.PNG)
![](./image/6.PNG)

## REFACTOR ANSIBLE CODE BY IMPORTING OTHER PLAYBOOKS INTO SITE.YML

 Within the playbook directory I created new file **site.yml** then move the common.yml to a new directory **static-assignment
 ![](./image/7.PNG)

 Create a new folder in root of the repository and name it static-assignments, then i Move common.yml file into the newly created static-assignments folder.
 ![](./image/8.PNG)

 Inside site.yml file,i import common.yml playbook.
![](./image/9.PNG)

then i Run ansible-playbook command against the dev environment
![](./image/10.PNG)

after that i Make sure that wireshark is deleted on all the servers by running wireshark --version

### Configure UAT Webservers with a role 'Webserver'

i Launch 2 fresh EC2 instances using RHEL 8 image, and name it – Web1-UAT and Web2-UAT.
![](./image/11.PNG)

 create a directory called roles, after that i Update my inventory ansible-config-mgt/inventory/uat.yml file with IP addresses of the 2 UAT Web servers,then i connect using ssh agent.
 ![](./image/12.PNG)

In /etc/ansible/ansible.cfg file uncomment roles_path string and provide a full path to your roles directory roles_path    = /home/ubuntu/ansible-config-mgt/roles, so Ansible could know where to find configured roles.

in **tast** directory  within the main.yml file,i start writing configuration tasks to do the following:

Install and configure Apache (httpd service)
Clone Tooling website from GitHub https://github.com/<your-name>/tooling.git.
Ensure the tooling website code is deployed to /var/www/html on each of 2 UAT Web servers.
Make sure httpd service is started
![](./image/13.PNG)

## Reference ‘Webserver’ role

Within the static-assignments folder,i create a new assignment for uat-webservers uat-webservers.yml. This is where i will reference the role.
![](./image/14.PNG)

i Commit changes, create a Pull Request and merge them to master branch,then i  run the playbook against your uat inventory.
![](./image/15.PNG)
![](./image/16.PNG)

now i will  able to see both of my UAT Web servers configured so i can try to reach them from my browser
![](./image/17.PNG)
![](./image/18.PNG)

Thank you
`