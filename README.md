----
### nw_testproject

###About
Using ansible 2.3.0 this project will provision 4 servers on RHEL 7 hosts in Amazon Cloud (AWS)

1 loadbalancer - haproxy (listening on port 80)

2 appservers - apache and PHP. apache listening on port 8080 

1 dbserver - mysql on port 3306


###Requirements and changes

- AWS Command Line Interface and boto set up on the ansible controller enviroment

- The file groups_var/all will need to be changed to have revelant values for

ec2_keypair: ****

ec2_security_group: ****

- The secutiry group will need the following ports opened:

22

80

8080

3306

- In this instance the ansible controller server was also hosted in AWS. 

If this is not the case you will need to change the file inventory/ec2.ini to have public_dns_name

Use either

destination_variable = public_dns_name

destination_variable = private_dns_name


- KeyPair files.  Save ***.pem file in inventory directory with permissions chmod 600





###To Run:

cd ~/ansible/

git clone https://github.com/emcrush/nw_testproject.git

cd nw_testproject

To Provision the Servers

ansible-playbook -i ./inventory/ec2.py aws-launch.yml -f 10

To Install and run the application 

ansible-playbook -i ./inventory/ec2.py  site.yml --private-key ./inventory/***.pem



###To Test
Once complete test with http://loadbalancerIP/index.php