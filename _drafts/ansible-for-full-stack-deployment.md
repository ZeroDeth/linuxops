---
layout: default
title: Ansible for Full Stack Deployment
date: 2017-05-09 22:25:00
---


# Ansible for Full Stack Deployment

Ansible is an automation engine similar to Chef or Puppet, that can be used to ensure deployment and configuration consistency across many servers,&nbsp;

## Prerequisities

### Linux

- ​

# Creating Ansible Lab Servers

## Primary Server

### [Initial Server Setup with CentOS 7](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-centos-7)

### [Install and Configure Ansible on CentOS 7 Server](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-centos-7)

## Primary Server

------

#### switch root

```
<br>sudo su -
<br>```

#### Install ansible and python

```
<br>yum -y install epel-release

yum -y install vim git python python-devel python-pip ansible openssl
<br>```

Go `cd /etc/ansible` &nbsp;`less ansible.cfg`

#### Backup then clear hosts

```
<br>cp hosts hosts.bak
<br>&gt; hosts
<br>```

cat hosts &gt;&gt;
<br>[local]

[centos]

[ubuntu]

[databeses]

[kubernetes]

In order to use `sudo` you first need to configure the sudoers file. The sudoers file is located at `/etc/sudoers`. And you should not edit it directly, you need to use the `visudo` command.

```
<br>#Add user without password
<br>ansible ALL-(ALL) &nbsp; NOPASSWD: ALL

#uncomment Wheel for sudo
<br>%Wheel &nbsp; ALL=(ALL) &nbsp; NOPASSWD: ALL
<br>```

```
<br>ssh-keygen
<br>ssh-copy-id ansible@
<br>```

## Secondary Server

## Ad-Hoc Commands

```
<br>ansible all -m ping

ansible all -a "whoami" -b
<br>```

```
<br>ansible hosts -i myhosts -m setup -a 'filter=ansible_default_ipv4'
<br>```

variables

```
<br>ansible hosts -i myhosts -a "ls -l {{ folder }}"
<br>```

forking (defaults 5)

```
<br>ansible all -a "ls -l" -f 100
<br>```

elinks

```
<br>ansible hosts -i myhosts -m yum -a "name=elinks state=latest"
<br>```

Become (Privilege Escalation)

```
<br>ansible databases -a "touch testfile" --become-user tempuser -b
<br>```

install vim

```
<br>ansible all -m yum -a "name=vim state=latest" -b
<br>```

copy

```
<br>ansible databases -m copy -a "src=/home/ansible/testfile9 dest=./testfile9"
<br>```

changes permissions

```
<br>ansible databases -m file -a "dist=./testfile9 mode=600"
<br>```

outputs a list of matching hosts

```
<br>ansible databases --list-hosts
<br>```

ubuntu without ssh-copy-id

```
<br>ansible la_python -a "whoami" --ask-pass --become-user user
<br>```

## Plays and Playbooks

- What are plays and playbook?
<br>- Playbook is 1 or more ‘plays’.
<br>- Describe a set of steps in a process.
<br>- Describe a policy to enforce.
<br>- Force a specific end state for your systems.
<br>- Designed to be human readable
<br>- Can be broken out to be templates and roles
<br>- More efficient for multiple tasks than ad-hoc
<br>- Likely put under source control.

## Yaml used in playbook

- Playbooks are written in Yaml format.
<br>- Use a minimum of syntax.
<br>- They use standard yaml but without metadata at the start so you define the start of a yaml file in ansible with the dashes on the first line like —-.
<br>- Have a look sample

# [Install Zsh on Linux and Configure](http://computingforgeeks.com/installingconfiguring-and-customizing-zsh-on-linux/)

[Install oh-my-zsh now](http://ohmyz.sh/)

#### Via curl

```
<br>sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
<br>```

#### Via wget

```
<br>sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
<br>```

[Install package shells:zsh-users:zsh-completions / zsh-completions](https://software.opensuse.org/download.html?project=shells%3Azsh-users%3Azsh-completions&package=zsh-completions)

## Amazon Web Services and Ansible

## using private pem file to execute ansible commands

```
<br>ansible all -i /etc/ansible/ec2.py -m ping --private-key=/home/ansible/.ssh/aws-labs-ireland.pem -u ec2-user
<br>```

## Install elinks

```shell
<br>ansible-playbook -i /etc/ansible/ec2.py install_elinks.yml --private-key=/home/ansible/.ssh/aws-labs-ireland.pem
<br>```

## Install Apache

## debug - Print statements during execution

```
<br>$ ansible-playbook echo.yml | grep gateway
<br>```

## Nagios

```
<br>time ansible-playbook -i hosts install/nagios.yml
<br>```

## todos

- [ ] “Chapter 1: Getting Started
<br>- [ ] What Is Configuration Management?
<br>- [ ] Infrastructure as Code
<br>- [ ] About Ansible
<br>- [ ] Puppet, Chef, and Other Configuration Management Tools
<br>- [ ] Installing Ansible”