<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->
- [Directory layout](#directory-layout)
	- [Directory Layout (copy from ansible doc)](#directory-layout-copy-from-ansible-doc)
- [Running ansible](#running-ansible)
	- [Running ansible from cygwin enviroment](#running-ansible-from-cygwin-enviroment)
		- [Pre-requisites](#pre-requisites)
<!-- /TOC -->

# Directory layout
The directory needs to be layed out in a specific way for ansible to work. Unfortunately changing the structure of the directory can have odd effects on the deploy script. So we stick to the proposal of the ansible guys which can be ready below or at [ansible directory layout](http://docs.ansible.com/ansible/playbooks_best_practices.html#directory-layout).

## Directory Layout (copy from ansible doc)

The top level of the directory would contain files and directories like so:

    production                # inventory file for production servers
    staging                   # inventory file for staging environment

    group_vars/
       group1                 # here we assign variables to particular groups
       group2                 # ""
    host_vars/
       hostname1              # if systems need specific variables, put them here
       hostname2              # ""

    library/                  # if any custom modules, put them here (optional)
    filter_plugins/           # if any custom filter plugins, put them here (optional)

    site.yml                  # master playbook
    webservers.yml            # playbook for webserver tier
    dbservers.yml             # playbook for dbserver tier

    roles/
        common/               # this hierarchy represents a "role"
            tasks/            #
                main.yml      #  <-- tasks file can include smaller files if warranted
            handlers/         #
                main.yml      #  <-- handlers file
            templates/        #  <-- files for use with the template resource
                ntp.conf.j2   #  <------- templates end in .j2
            files/            #
                bar.txt       #  <-- files for use with the copy resource
                foo.sh        #  <-- script files for use with the script resource
            vars/             #
                main.yml      #  <-- variables associated with this role
            defaults/         #
                main.yml      #  <-- default lower priority variables for this role
            meta/             #
                main.yml      #  <-- role dependencies

        webtier/              # same kind of structure as "common" was above, done for the webtier role
        monitoring/           # ""
        fooapp/               # ""

# Running ansible

There are two ways to run ansible. First would be from your local pc (cygwin environment) and secondly it can be run from the server itself.

## Running ansible from cygwin enviroment

Installing ansible on cygwin is not part of the documentation here. Please refer to other guides for this.

### Pre-requisites
  1. ansible installed on cygwin
  1. folder with the following checkouts inside (in their sub directories)
    * checkout of this git repository
  1. vault passwords in files in the home directory
    * ~/dev-vault-id (password is the same as for the ewsasadm)
