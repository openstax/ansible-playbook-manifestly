# ansible-role-manifestly
An Ansible role to generate a deployment manifest file and upload it to Github and the server itself

# Requirements (on localhost or deployment server):
```
  - rbenv
  - ruby
```

# Required Role Variables
```
  - manifestly_dirs
  - manifestly_rbenv_init
  - manifestly_repo_filename
  - manifestly_environment_name
  - manifestly_host_public_dir
```

# Recommended Role Variables (variable: default)
```
  - manifestly_hosts: []
  - manifestly_host_owner: www-data
```

# Optional Role Variables (variable: default)
```
  - manifestly_repo: openstax/deploy-manifests
  - manifestly_src_root: "{{ playbook_dir }}/.."
  - manifestly_src_filename: "{{ manifestly_repo_filename }}-{{ manifestly_environment_name }}-manifest.txt"
  - manifestly_src_filepath: "{{ manifestly_src_root }}/{{ manifestly_src_filename }}"

  - manifestly_commit_message: "deployed to {{ manifestly_environment_name }}"
  - manifestly_tag: "deployed_to_{{ manifestly_environment_name }}"

  - manifestly_host_filename: rev.txt
  - manifestly_host_filepath: "{{ manifestly_host_public_dir }}/{{ manifestly_host_filename }}"
  - manifestly_host_group: www-data
```

# Example Playbook
```
---
- name: 'manifestly : generate and upload deployment manifest'
  hosts: localhost
  connection: local
  become: False
  roles:
    - role: manifestly
      manifestly_dirs: myapp myapp-js myotherapp
      manifestly_rbenv_init: . ~/rbenv-init
      manifestly_repo_filename: myapp
      manifestly_environment_name: "{{ environment_name }}"
      manifestly_host_public_dir: /home/myappuser/www/myapp/public
      manifestly_hosts: "{{ groups.myapp }}"
      manifestly_owner: myappuser
```
