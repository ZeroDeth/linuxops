---
date:
title: Ansible
categories:
  - Ansible
  - Configuration Management
description:
type: Document
---


&lt;h1&gt;Ansible for Full Stack Deployment&lt;/h1&gt;
<br>&lt;p&gt;Ansible is an automation engine similar to Chef or Puppet, that can be used to ensure deployment and configuration consistency across many servers, &lt;/p&gt;
<br>&lt;h2&gt;Prerequisities&lt;/h2&gt;
<br>&lt;h3&gt;Linux&lt;/h3&gt;
<br>&lt;ul&gt;&lt;li&gt;
<br>The SysAdmin's Guide to Python&lt;/li&gt;
<br>&lt;li&gt;
<br>Python Scripting for DevOps&lt;/li&gt;
<br>&lt;/ul&gt;
<br>&lt;h1 data-breakpage&gt;Creating Ansible Lab Servers&lt;/h1&gt;
<br>&lt;h2&gt;Primary Server&lt;/h2&gt;
<br>&lt;h3&gt;&lt;a href='https://www.digitalocean.com/community/tutorials/initial-server-setup-with-centos-7'&gt;Initial Server Setup with CentOS 7&lt;/a&gt;&lt;/h3&gt;
<br>&lt;p&gt;&lt;/p&gt;
<br>&lt;h3&gt;&lt;a href='https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-centos-7'&gt;Install and Configure Ansible on CentOS 7 Server&lt;/a&gt;&lt;/h3&gt;
<br>&lt;p&gt;&lt;/p&gt;
<br>&lt;p&gt;&lt;/p&gt;
<br>&lt;p&gt;&lt;/p&gt;
<br>&lt;h2&gt;Primary Server&lt;/h2&gt;
<br>&lt;hr /&gt;
<br>&lt;h4&gt;switch root&lt;/h4&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>sudo su -
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;h4&gt;Install ansible and python&lt;/h4&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>yum -y install epel-release

yum -y install vim git python python-devel python-pip ansible openssl
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;Go &lt;code&gt;cd /etc/ansible&lt;/code&gt; &nbsp;&lt;code&gt;less ansible.cfg&lt;/code&gt;&lt;/p&gt;
<br>&lt;h4&gt;Backup then clear hosts&lt;/h4&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>cp hosts hosts.bak
<br>&gt; hosts
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;cat hosts &gt;&gt;
<br>[local]&lt;/p&gt;
<br>&lt;p&gt;[centos]&lt;/p&gt;
<br>&lt;p&gt;[ubuntu]&lt;/p&gt;
<br>&lt;p&gt;[databeses]&lt;/p&gt;
<br>&lt;p&gt;[kubernetes]&lt;/p&gt;
<br>&lt;p&gt;In order to use &lt;code&gt;sudo&lt;/code&gt; you first need to configure the sudoers file. The sudoers file is located at &lt;code&gt;/etc/sudoers&lt;/code&gt;. And you should not edit it directly, you need to use the &lt;code&gt;visudo&lt;/code&gt; command.&lt;/p&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>#Add user without password
<br>ansible ALL-(ALL) &nbsp; NOPASSWD: ALL

#uncomment Wheel for sudo
<br>%Wheel &nbsp; ALL=(ALL) &nbsp; NOPASSWD: ALL
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ssh-keygen
<br>ssh-copy-id ansible@
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;h2&gt;Secondary Server&lt;/h2&gt;
<br>&lt;p&gt;&lt;/p&gt;
<br>&lt;h2&gt;Ad-Hoc Commands&lt;/h2&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible all -m ping

ansible all -a &quot;whoami&quot; -b
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible hosts -i myhosts -m setup -a 'filter=ansible_default_ipv4'
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;variables&lt;/p&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible hosts -i myhosts -a &quot;ls -l {{ folder }}&quot;
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;forking (defaults 5)&lt;/p&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible all -a &quot;ls -l&quot; -f 100
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;elinks&lt;/p&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible hosts -i myhosts -m yum -a &quot;name=elinks state=latest&quot;
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;Become (Privilege Escalation)&lt;/p&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible databases -a &quot;touch testfile&quot; --become-user tempuser -b
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;install vim&lt;/p&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible all -m yum -a &quot;name=vim state=latest&quot; -b
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;copy&lt;/p&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible databases -m copy -a &quot;src=/home/ansible/testfile9 dest=./testfile9&quot;
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;changes permissions&lt;/p&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible databases -m file -a &quot;dist=./testfile9 mode=600&quot;
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;outputs a list of matching hosts&lt;/p&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible databases --list-hosts
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;ubuntu without ssh-copy-id&lt;/p&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible la_python -a &quot;whoami&quot; --ask-pass --become-user user
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;h2&gt;Plays and Playbooks&lt;/h2&gt;
<br>&lt;ul&gt;&lt;li&gt;
<br>What are plays and playbook?&lt;/li&gt;
<br>&lt;li&gt;
<br>Playbook is 1 or more ‘plays’.&lt;/li&gt;
<br>&lt;li&gt;
<br>Describe a set of steps in a process.&lt;/li&gt;
<br>&lt;li&gt;
<br>Describe a policy to enforce.&lt;/li&gt;
<br>&lt;li&gt;
<br>Force a specific end state for your systems.&lt;/li&gt;
<br>&lt;li&gt;
<br>Designed to be human readable&lt;/li&gt;
<br>&lt;li&gt;
<br>Can be broken out to be templates and roles&lt;/li&gt;
<br>&lt;li&gt;
<br>More efficient for multiple tasks than ad-hoc&lt;/li&gt;
<br>&lt;li&gt;
<br>Likely put under source control.&lt;/li&gt;
<br>&lt;/ul&gt;
<br>&lt;h2&gt;Yaml used in playbook&lt;/h2&gt;
<br>&lt;ul&gt;&lt;li&gt;
<br>Playbooks are written in Yaml format.&lt;/li&gt;
<br>&lt;li&gt;
<br>Use a minimum of syntax.&lt;/li&gt;
<br>&lt;li&gt;
<br>They use standard yaml but without metadata at the start so you define the start of a yaml file in ansible with the dashes on the first line like —-.&lt;/li&gt;
<br>&lt;li&gt;
<br>Have a look sample&lt;/li&gt;
<br>&lt;/ul&gt;
<br>&lt;h1 data-breakpage&gt;&lt;a href='http://computingforgeeks.com/installingconfiguring-and-customizing-zsh-on-linux/'&gt;Install Zsh on Linux and Configure&lt;/a&gt;&lt;/h1&gt;
<br>&lt;p&gt;&lt;a href='http://ohmyz.sh/'&gt;Install oh-my-zsh now&lt;/a&gt;&lt;/p&gt;
<br>&lt;h4&gt;Via curl&lt;/h4&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>sh -c &quot;$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)&quot;
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;h4&gt;Via wget&lt;/h4&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>sh -c &quot;$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)&quot;
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;p&gt;&lt;a href='https://software.opensuse.org/download.html?project=shells%253Azsh-users%253Azsh-completions&package=zsh-completions'&gt;Install package shells:zsh-users:zsh-completions / zsh-completions&lt;/a&gt;&lt;/p&gt;
<br>&lt;h2&gt;Amazon Web Services and Ansible&lt;/h2&gt;
<br>&lt;h2&gt;using private pem file to execute ansible commands&lt;/h2&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>ansible all -i /etc/ansible/ec2.py -m ping --private-key=/home/ansible/.ssh/aws-labs-ireland.pem -u ec2-user
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;h2&gt;Install elinks&lt;/h2&gt;
<br>&lt;pre&gt;&lt;code class='language-shell' lang='shell'&gt;
<br>ansible-playbook -i /etc/ansible/ec2.py install_elinks.yml --private-key=/home/ansible/.ssh/aws-labs-ireland.pem
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;h2&gt;Install Apache&lt;/h2&gt;
<br>&lt;h2&gt;debug - Print statements during execution&lt;/h2&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>$ ansible-playbook echo.yml | grep gateway
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;h2&gt;Nagios&lt;/h2&gt;
<br>&lt;pre&gt;&lt;code&gt;
<br>time ansible-playbook -i hosts install/nagios.yml
<br>&lt;/code&gt;&lt;/pre&gt;
<br>&lt;h2&gt;todos&lt;/h2&gt;
<br>&lt;taskList&gt;&lt;li&gt;
<br>“Chapter 1: Getting Started&lt;/li&gt;
<br>&lt;li&gt;
<br>What Is Configuration Management?&lt;/li&gt;
<br>&lt;li&gt;
<br>Infrastructure as Code&lt;/li&gt;
<br>&lt;li&gt;
<br>About Ansible&lt;/li&gt;
<br>&lt;li&gt;
<br>Puppet, Chef, and Other Configuration Management Tools&lt;/li&gt;
<br>&lt;li&gt;
<br>Installing Ansible”&lt;/li&gt;
<br>&lt;/taskList&gt;
<br>&nbsp;