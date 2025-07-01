# Team Workstation Setup with Ansible:

<br/>

## Control Machine Requirements:

Ansible installed (version 2.9 or higher recommended)
SSH access to target workstations
Python 3.6+ on the control machine

## Target Workstation Requirements:

SSH server running and accessible
Python installed (most modern distributions include this)
Sudo privileges for the user Ansible will connect as

<br/>


## Overview:

Ansible is an agentless automation tool that uses SSH to configure remote systems. For workstation management, it allows you to define your entire development environment as code, making onboarding new team members faster and ensuring everyone has the same tools and configurations.
#Prerequisites

<br/>

Setting up workstation user accounts with Ansible involves using several key modules and strategies to automate user management across multiple machines. Here's how you'd approach this:

### Core Ansible Modules for User Management:
The primary module is ansible.builtin.user, which handles user creation, modification, and removal. This module can set usernames, UIDs, home directories, shells, groups, and passwords. For group management, you'd use ansible.builtin.group to create groups before assigning users to them.
### User Definition Strategies:
You can define users in several ways. The most flexible approach uses variables in your inventory or group_vars/host_vars files, where you create a list of user dictionaries containing username, full name, groups, shell preferences, and other attributes. Alternatively, you can define users directly in your playbooks for simpler scenarios.

### Home Directory and Environment Setup
The user module automatically creates home directories, but you might want additional configuration. You can use the file module to set specific permissions, create additional directories, or deploy configuration files. The template module is useful for deploying personalized configuration files like .bashrc or .profile with user-specific variables.

### Group and Sudo Configuration
Beyond basic user creation, you'd typically configure group memberships for access control and sudo privileges. The lineinfile module can manage sudoers files, though using community.general.sudoers module provides more robust sudo configuration management.

<br/>

## Project Structure:

```bash
ansible-workstation/
├── inventory/
│   ├── hosts.yml
│   └── group_vars/
│       ├── all.yml
│       ├── developers.yml
│       └── designers.yml
├── playbooks/
│   ├── main.yml
│   ├── base-setup.yml
│   ├── development-tools.yml
│   └── security-hardening.yml
├── roles/
│   ├── common/
│   ├── docker/
│   ├── nodejs/
│   ├── python/
│   └── vscode/
├── ansible.cfg
└...
