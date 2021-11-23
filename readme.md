### Ansible multiple inventories template
This structure helps to quickly change the target server for deployment
file structure
~~~
.
|-- ansible.cfg
|-- inventories                         #inventories for diff stand
|   |-- dev
|   |   |-- group_vars
|   |   |   `-- all
|   |   |       `-- alpha_server.yml    #common properties for generate application.properties from .j2 template
|   |   `-- hosts                       #host list for dev stand
|   `-- test
|       |-- group_vars
|       |   `-- all
|       |       `-- alpha_server.yml
|       `-- hosts
|-- playbooks
|   `-- deploy-app.yml
|-- project
|   `-- int.jar                         #simple java app host:port/hello for result 
`-- roles                               #ansible roles. usually created via ansible-galaxy init <role>
    `-- hello
        |-- README.md
        |-- defaults                    #default varriables
        |   `-- main.yml         
        |-- tasks
        |   `-- main.yml               
        `-- templates
            |-- application.properties.j2     #j2 template to create application.properties
            `-- helloapp.service.j2           #j2 template to spec java app
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
