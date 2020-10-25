# Ansible Automation: Successful Onboarding
This repository is a collection of thoughts intended to help customers with a successful Ansible Automation adoption. This repository is by no means a substitution for enterprises that are in need of a full blown consulting/services need. The focus is on SMEs that are looking for guidance to accelerate their Ansible automation journey.

## Table of Content
- [Introduction & Prerequisite](#introduction--prerequisite)
    - [Official Red Hat Workshop (recommended)](#option-1-recommended-official-red-hat-workshops)
    - [Online Resources, example: Udemy](#option-2-online-resources-example-udemy)
    - [Self Learning (Docs)](#option-3-self-learning-docs)
    - [Jeff Geerling (creator & contributor)](#option-4-jeff-geerling-he-deserves-a-mention)

- [Preperation Tasks](#preperation-tasks)
    - [Who](#who)
    - [What](#what)
    - [When](#when)
    - [How](#how)
    - [Why](#why)

- [Day 1](#day-1)
    - [Inventories](#inventories)
    - [Credentials](#credentials)
    - [Source Control](#playbook-scm)
    - [Projects](#projects)
    - [Deliverable 1](#deliverable-1)

- [Week 1](#week-1)
- [Month 1 to 3](#month-1-to-3)
- [Year 1](#year-1)
- [Appendix](#appendix)

# Introduction & Prerequisite 
I think that the most important thing for a successful automation journey is the planning phase. A well planned automation journey will actually allow you to save time while a badly planned automation journey will likely simply introduce another tool that will eat away precious time in an already busy day. This repository is really meant to help you with the planning and execution of a successful automation journey.

To do this, we will look at the tasks neccessary before actually deploying Ansible & Ansible Tower, discuss some of the different deployment options as well as identifying targets for the first year.

Before you can get started, it is essential to gain a basic understanding of how Ansible works and how playbooks are written. There are a variety of sources available to you:

## Option 1: Official Red Hat Workshops (recommended)
A variety of teams within Red Hat offer [monthly Ansible workshops](https://github.com/ansible/workshops) that you can attend free of charge. These workshop come in 5 different flavors, depending on your background and needs, my recommendation is the basic Red Hat Enterprise Linux Workshop as it offers a well rounded curriculum:
-  **Ansible Red Hat Enterprise Linux Workshop** focused on automating Linux platforms like Red Hat Enterprise Linux
- **Ansible Network Automation Workshop** focused on router and switch platforms like Arista, Cisco, Juniper
- **Ansible F5 Workshop** focused on automation of F5 BIG-IP
- **Ansible Security Automation** focused on automation of security tools like Check Point Firewall, IBM QRadar and the IDS Snort
- **Ansible Windows Automation Workshop** focused on automation of Microsoft Windows

## Option 2: Online resources, example Udemy
There are dozens of online resources available nowadays. If you prefer to learn at your own pace and you know that this way of learning works well for you - go ahead! I have used Udemy before and can recommend the following course: [Ansible for the Absolute Beginner - Hands-On - DevOps](https://www.udemy.com/course/learn-ansible/) as well as the advanced course [Ansible Advanced - Hands-On DevOps](https://www.udemy.com/course/learn-ansible-advanced/). I have no affiliation with Udemy or the creator.

## Option 3: Self learning (Docs)
If you have experience with other automation tools such as Chef or Puppet and you like to just do your own thing, [skip to the docs and just get your hands dirty](https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html). There is no reason why you wouldn't be able to do this, Ansible is straight forward in its application and requires a very minimal setup. The only problem here is that this option generally skips Ansible Tower.

## Option 4: Jeff Geerling (he deserves a mention)
Jeff Geerling runs a [great blog and published dozens of videos on Ansible](https://www.jeffgeerling.com/blog/2020/ansible-101-jeff-geerling-youtube-streaming-series). He also published a book called [Ansible for DevOps](https://www.jeffgeerling.com/project/ansible-devops) that has sold >20.000 copies as of 2019. Jeff is a very vocal contributor to the Ansible Open Source project. I can recommend his content as his blogs helped me a lot when starting out.


# Preperation Tasks
Great, you have a basic understanding of Ansible and you know how to write playbooks. That alone would be sufficient to help you with personal projects or enable you to automate specific tasks during your day-to-day work. This of course not a strategy, nor does it scale particulary well. 

Your first step should be to get in touch with your Red Hat account team and discuss evaluation subscriptions, simultaneously you can follow the steps below. If you don't know who your account team is, you can reach [us here](https://www.redhat.com/en/contact) and someone will get in touch with you.

## Who
The first question you need to answer is the *Who* question. Who do you want to include in your automation journey? Will it be mainly system administrators? Windows SysAdmins? Linux SysAdmins? Networking teams? Developers? Infrastructure? On-Prem and Cloud teams? 

This is the first step in my opinion. Others might disagree with this as one could argue that it is more important to identify the *What*. From my experience, both works just fine. I prefer to identify the people that need to be involved as it allows all involved parties to work together from the planning phase. The involved teams can then decide on *What is to be automated*. 

You should also start thinking about [Users](https://docs.ansible.com/ansible-tower/latest/html/userguide/users.html) and [Teams](https://docs.ansible.com/ansible-tower/latest/html/userguide/teams.html) within Tower. There is a designated [RBAC best practices section](https://docs.ansible.com/ansible-tower/latest/html/userguide/security.html#role-based-access-controls) in the Docs, make sure you read it - you don't need to understand everything in detail. If you are using Enterprise Authentication methods such as LDAP or SAML, it is also important that you look at the [relevant section in the docs](https://docs.ansible.com/ansible-tower/latest/html/administration/ent_auth.html).

Again, there is no need yet to apply these. But you should identify a strategy. You should be able to answe the following questions:
- Who will be the core Ansible automation team in the first year?
- Who could extend the core team after this period?
- What RBAC model will be use? Do we need one? If you have only 3 users, the answer is likely *no*.
- Do we want to use LDAP, AD or SAML for authentication?


## What
Decide what you want to achieve. Identify the tasks that you want to automate. This could be onboarding for new users, deploying VMs, configuring cloud VPCs or maintaining networking equipment. You should identify 10-20 small tasks for the first few weeks that you want to automate - (!) important: Keep it realisitc and don't overcomplicate things. Don't come up with something like *I want to automate our on-prem infrastructure*.

Think especially of tasks that are time consuming and error-prone.

Example Tasks:
- **Patching**: Request made, operation team logs into machine, applies patch, reboots server, validate service, closes change request.
- **Provisioning**: Dev Team requests VM, operation team deploys VM template, configures VM to organization standard, installs and configures requested software, passes off VM to Dev team, closes request.

You should be able to:
- Identify 10-20 tasks that you want to deliver within the first month.
- Understand who will deliver these tasks.
- Expand each task into individual steps required to execute on. 

## When
It is important that you give yourself enough time to  adopt your new automation tool. If you know that September and October are a busy time for your business, then delay the rollout until November. Don't put extra stres on yourself. Automation is meant to make your life easier, if you thinl of it *as just another thing that you need to do*, you will likely not succeed. 

Make sure that you can answer the following questions:
- When will you rollout Ansible and Ansible Tower?
- Are there any roadblocks such as holidays or business disruptors during this rollout?
- Is everyone involved aware of the roadmap?
- Do you know how to reach Red Hat Support in case you encounter any technical problems?

## Where
You should have a basic understanding of how [Inventories](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html) work. And you have also identified what you want to automate. Personally, I would recommend spending some time on identifying an Inventory strategy. There are a variety of ways to manage your inventories, my recommendation is to utilize [Dynamic Inventories](https://docs.ansible.com/ansible-tower/latest/html/userguide/inventories.html) in Ansible Tower. Identify a strategy that works for you to group hosts based on the tasks you have identified. 

Examples:
- All RHEL hosts
- All Webservers within a specific VPC
- Windows Servers in AWS EU-West region

## How
The only step left is to make a decision on the deployment. Do you need to a [highly available Ansible Tower deployment](https://medium.com/@florianmoss/highly-available-ansible-tower-deployment-on-aws-d95a0c42b1ef) or is a [basic deployment](https://medium.com/@florianmoss/installing-ansible-tower-on-rhel8-using-aws-ec2-c7ee2acad655?sk=b8a7e3d523f7ba3ff48699b344b7ecb1) sufficient? You can find all the [deployment options listed in the docs](https://docs.ansible.com/ansible-tower/latest/html/quickinstall/prepare.html).

I would recommend to start with a basic one machine deployment for smaller teams that manage up to 100 nodes. As long as you have 8-16GB RAM available and 100 GB of storage, you will be fine. If you will have >10 users and a couple of hundred nodes to manage - a [clustered approach](https://docs.ansible.com/ansible-tower/latest/html/administration/clustering.html#ag-clustering) will be the right decision. The steps for this are explained [here](https://medium.com/@florianmoss/highly-available-ansible-tower-deployment-on-aws-d95a0c42b1ef).

## Why
It is really important to remind yourself why you did all of this. Your main goals are to save money, time and remove sources for errors. All those questions you answered so far will help you to do this. 


# Day 1
Today is the big day, go ahead and deploy your Ansible Tower instance/-s. Implement your authentication model and setup RBAC as you have planned. Then go ahead an setup your inventory.

## Inventories
You can start with a [static inventory](https://docs.ansible.com/ansible-tower/latest/html/userguide/inventories.html) if there are <100 hosts and there is little volatility for your hosts and hostnames. On the other hand, a [dyanamic inventory](https://docs.ansible.com/ansible-tower/latest/html/userguide/inventories.html#inventory-plugins) will allow for greater flexibility and allow you to scale out. 

## Credentials
Set your [credentials](https://docs.ansible.com/ansible-tower/latest/html/userguide/credentials.html) for private SCM repositories and your hosts. I recommend deploying public keys on the target hosts and storing the private key as a credential. Never use passwords if avoidable.

## Playbook SCM
For the first 3 months a single repository that contains all playbooks is sufficient, for most users. If you have different teams that manage vastly different environments, find a model that works for you. You could create one repository that manages all Linux machines, one that manages all networking equipment, one for Windows hosts, etc. 

## Projects
Set up a [project](https://docs.ansible.com/ansible-tower/latest/html/userguide/projects.html) within Tower for each of those repositories. Make sure that the right users and teams have access to those projects.

## Deliverable 1
You should now have a running Ansible Tower deployment, access to 1 or more repositories to manage your playbooks, as well as access to your target hosts either via static inventories or dynamic inventories. 

# Week 1
b

# Month 1 to 3
bla

# Year 1
bla

# Appendix
bla
