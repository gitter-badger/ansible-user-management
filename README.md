# Ansible Role: manage_users
[![Build Status](https://travis-ci.org/smiller171/ansible-user-management.svg?branch=master)](https://travis-ci.org/smiller171/ansible-user-management)

An Ansible role that sets up users and their ssh keys on unix-based systems  
Users can have multiple keys (add each as a list item)  
any keys not listed will be removed from the authorized_keys file

## Requirements
Set up sudoers file to allow passwordless sudo as passwords will not be set

## Role Variables

Available variables are listed below, along with default values:

The default shell that will be assigned to all users  
    shell: /bin/bash  

List of users that should exist, with a list of authorized keys

    manage_users_allowed:
      - name: foo
        authorized:
        - "ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAlPYybp3CWDzRPo0uF/woyqkfhpZK2T7zn16z+fGYlRQl6gXATIUB4JYfr9pfD+SOW2T4X78P+/h1o4QPCwoesLacaFEFGwUb+SzhVVm6B6q4WMAiJWD6OVXh+SVVvD9rdcz5RMVLqQngrRqBlj4kBIMQ3S8h1cCESbR2P6jszgFj0I6p3tQCpo9yjcVwLqvWFKJgzEm2E2wV/gmrc0PhVRP2guIRN4p6M2ZyIPprdZ6PA8m7Rs4yN3jQ/0alrQ23ECCU4lHoVG9fwvLIq1vh4ikPcUrdA8sSHTE1pkpzvrTv7FtkuUcBrDMedFE7E8dB9pPS+vXIBWVUYJhp9WzVkQ== user@domain.com"

Users that should be removed if they exist

    manage_users_unauthorized:
      - foobar

Groups that users should belong to

    manage_users_groups: "sudo,adm,dialout,cdrom,floppy,audio,video,plugdev"

## Dependencies

None.

## Example Playbook

    ---
    - hosts: all
      sudo: yes
      roles:
      - scott.miller171.manage_users
      vars:
      - manage_users_allowed:
        - name: foo
          authorized:
          - "ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAlPYybp3CWDzRPo0uF/woyqkfhpZK2T7zn16z+fGYlRQl6gXATIUB4JYfr9pfD+SOW2T4X78P+/h1o4QPCwoesLacaFEFGwUb+SzhVVm6B6q4WMAiJWD6OVXh+SVVvD9rdcz5RMVLqQngrRqBlj4kBIMQ3S8h1cCESbR2P6jszgFj0I6p3tQCpo9yjcVwLqvWFKJgzEm2E2wV/gmrc0PhVRP2guIRN4p6M2ZyIPprdZ6PA8m7Rs4yN3jQ/0alrQ23ECCU4lHoVG9fwvLIq1vh4ikPcUrdA8sSHTE1pkpzvrTv7FtkuUcBrDMedFE7E8dB9pPS+vXIBWVUYJhp9WzVkQ== user@domain.com"
          
      - manage_users_unauthorized:
        - foobar
        
      - manage_users_groups: "sudo,adm,dialout,cdrom,floppy,audio,video,plugdev"

## License

MIT
