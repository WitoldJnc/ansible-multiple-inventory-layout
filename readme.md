### Ansible multiple inventories template
This structure helps to quickly change the target server for deployment
file structure
~~~
.
|-- ansible.cfg
|-- inventories
|   |-- dev
|   |   |-- group_vars
|   |   |   `-- all
|   |   |       `-- alpha_server.yml
|   |   `-- hosts
|   `-- test
|       |-- group_vars
|       |   `-- all
|       |       `-- alpha_server.yml
|       `-- hosts
|-- playbooks
|   `-- deploy-app.yml
|-- project
|   `-- int.jar
`-- roles
    `-- hello
        |-- README.md
        |-- defaults
        |   `-- main.yml
        |-- tasks
        |   `-- main.yml
        `-- templates
            |-- application.properties.j2
            `-- helloapp.service.j2
~~~
download source code 

install ansible on ubuntu
~~~
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
~~~

if you run linux in docker container, you can copy files from local pc to container, use :
~~~
docker cp <path_to_source_code> <container_name>:/<destination_on_container>
~~~

replace ansible user and path to your private ssh in inventories/../group_vars/all/alpha_server.yml
replace host to your own vps on dest server in inventories/../hosts
run command 
~~~
ansible-playbook -i inventories/<test or dev> playbooks/deploy-app.yml
~~~


#### todo
- [ ] delete path to ssh and username from group_vars
