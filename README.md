Ansible Roles for AWS Infrastructure Creation
----------------------
There's a series of blog posts that I wrote to go along with these roles. [Check it out!](https://rbgeek.wordpress.com/2016/01/04/aws-infrastructure-creation-with-ansible-part-1/)

The purpose of these Ansible roles are to create the complete infrastructure over AWS using Ansible, which include:

- VPC with public and private subnets in different AZ
- EC2 Key Pair
- Security Groups for EC2,RDS and ELB with tags
- EC2 instance inside the desired AZs
- ELB with SSL support
- RDS instance

I have also written so really small plugins to get the desired information.

Requirement to use these roles:

- Ansible 2.15.3
- boto
- AWS admin access
  
```
pip3 install boto3
ansible-galaxy collection install amazon.aws
```

Specifically, these are the versions of mentioned software that I am using:

```shell
arbab@ansible2:~$ ansible --version
ansible [core 2.15.3]
  config file = None
  configured module search path = ['/home/runner/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/lib/python3.11/site-packages/ansible
  ansible collection location = /home/runner/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/local/bin/ansible
  python version = 3.11.4 (main, Jun  7 2023, 00:00:00) [GCC 13.1.1 20230511 (Red Hat 13.1.1-2)] (/usr/bin/python3)
  jinja version = 3.1.2
  libyaml = True
arbab@ansible2:~$
```



```
export AWS_ACCESS_KEY_ID=YOUR_ACCESS_KEY
export AWS_SECRET_ACCESS_KEY=YOUR_SECRET_KEY
export AWS_DEFAULT_REGION=us-east-2
ansible-playbook aws.yml
```

Ansible uses python-boto library to call AWS API, and boto needs AWS credentials in order to perform all the functions. There are many ways to configure your AWS credentials. The easiest way is to crate a .boto file under your user home directory:

Then add the following:
```shell
curl -OL https://raw.githubusercontent.com/tosin2013/openshift-4-deployment-notes/master/aws/configure-aws-cli.sh
chmod +x configure-aws-cli.sh 
./configure-aws-cli.sh -h
```