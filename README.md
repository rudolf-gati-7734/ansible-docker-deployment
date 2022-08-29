# ansible-docker-deployment
Since I am using a windows host first I installed virtualbox, vagrant and cmder just to make my life easier.
Created 2 virtual machines one named ansible and one named server with the attached Vagrantfile.
Ansible is the main control unit and server is where the app will be deployed. The network setup is a bridge with ip 192.168.10.20 and 192.168.10.21 for server.
In the ansible-playbook there is a task that copies a template to the main folder, before the docker compose, it contains some small fixes and a port variable that can be set from the inventory.
