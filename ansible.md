# Ansible Scenario-Based Questions and Answers

## 1. Write a playbook to install Nginx
```yaml
---
- name: Install Nginx
  hosts: all
  become: true
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

2. What is an Ansible role? Write a role to install and start Nginx.

An Ansible role is a reusable and modular structure to organize tasks, variables, templates, and files for better playbook management.

Role Structure:

roles/
├── nginx/
│   ├── tasks/
│   │   └── main.yml
│   ├── defaults/
│   │   └── main.yml

tasks/main.yml:

---
- name: Install Nginx
  apt:
    name: nginx
    state: present

- name: Start and enable Nginx
  service:
    name: nginx
    state: started
    enabled: true

defaults/main.yml:

---
nginx_version: latest

3. What are the prerequisites to use Ansible?
	•	Python installed on the control node and managed nodes.
	•	SSH access between control and managed nodes.
	•	Inventory file for specifying hosts.
	•	Ansible installed on the control node.

4. What language is Ansible written in?

Ansible is written in Python.

5. Is Ansible idempotent?

Yes, Ansible is idempotent. It ensures that tasks produce the same result irrespective of how many times they are run.

6. What are the types of modules in Ansible?
	•	Core Modules: Maintained by the Ansible team and included by default.
	•	Extra Modules: Community-maintained and may require manual installation.

7. How can you install Nginx on a group of servers but skip installation on a specific server?

---
- name: Install Nginx
  hosts: group_name
  become: true
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
      when: inventory_hostname != 'specific_server'

8. How do you perform a dry run for your Ansible playbook?

Use the --check flag:

ansible-playbook playbook.yml --check

9. How do you handle sensitive information such as API keys or passwords in Ansible?

Use Ansible Vault to encrypt sensitive data:

ansible-vault encrypt secrets.yml

10. How can you rollback changes if one of your tasks fails during playbook execution?

Use the block and rescue directives:

---
- name: Rollback example
  hosts: all
  tasks:
    - block:
        - name: Task that might fail
          command: some_command
      rescue:
        - name: Rollback changes
          command: rollback_command

11. How can you continue playbook tasks if some of the tasks fail?

Set ignore_errors: true for tasks:

- name: Task that might fail
  command: some_command
  ignore_errors: true

12. How can you run a playbook for different machines with different users and different ports?

Specify inventory details with user and port:

[servers]
host1 ansible_user=user1 ansible_port=22
host2 ansible_user=user2 ansible_port=2222

13. How can you create an empty file using an Ansible playbook?

- name: Create an empty file
  file:
    path: /path/to/file
    state: touch

14. What are the advantages of Ansible over Chef?
	•	Agentless (uses SSH).
	•	Easier learning curve.
	•	Written in YAML, which is simpler than Chef’s Ruby DSL.
	•	Better for ad-hoc tasks.

15. What is Ansible cowsay?

Cowsay is a graphical enhancement in Ansible that adds a cow figure in output messages. It can be disabled with:

export ANSIBLE_NOCOWS=1

16. What is an Ansible ad-hoc command?

An ad-hoc command is a one-time command run directly in the CLI without a playbook:

ansible all -m ping

17. What is an Ansible loop?

Ansible loops allow repetitive tasks:

- name: Install packages
  apt:
    name: "{{ item }}"
    state: present
  loop:
    - nginx
    - git

18. What is dynamic inventory? Name one practical use case for it.

Dynamic inventory is generated programmatically, e.g., pulling AWS EC2 instances. Use case: managing auto-scaling environments.

19. Can you create infrastructure using Ansible?

Yes, using modules like ec2, gcp_compute, or azure_rm.

20. What is a callback plugin in Ansible?

Callback plugins customize playbook outputs or trigger specific actions during execution.

21. What is Ansible Tower? How do you implement RBAC in Ansible Tower?

Ansible Tower is a web-based UI for Ansible. RBAC is implemented by assigning roles to users, teams, or organizations.

22. Describe how Ansible helps your organization.

Ansible automates repetitive tasks, improves consistency, reduces manual errors, and simplifies deployments.

23. How would you handle a situation where an Ansible playbook fails due to a network issue?

Retry tasks using retries and delay:

- name: Retry task
  command: some_command
  retries: 3
  delay: 5

24. Can you write an Ansible playbook to deploy a Docker container?

- name: Deploy Docker container
  hosts: all
  become: true
  tasks:
    - name: Install Docker
      apt:
        name: docker.io
        state: present

    - name: Run a Docker container
      docker_container:
        name: my_container
        image: nginx
        state: started

25. How would you use Ansible to automate the deployment of cloud infrastructure?

Use cloud modules like ec2, gcp_compute, and azure_rm to define infrastructure as code.

26. Can you explain how Ansible uses SSH to connect to remote servers?

Ansible uses SSH for communication, executing tasks remotely without requiring an agent.

27. How can you use Ansible to manage user accounts and permissions on a Linux server?

- name: Create user
  user:
    name: new_user
    state: present

- name: Add user to group
  user:
    name: new_user
    groups: sudo
    append: true

28. Can you write an Ansible playbook to configure a load balancer using HAProxy?

- name: Configure HAProxy
  hosts: all
  become: true
  tasks:
    - name: Install HAProxy
      apt:
        name: haproxy
        state: present

    - name: Configure HAProxy
      template:
        src: haproxy.cfg.j2
        dest: /etc/haproxy/haproxy.cfg

    - name: Restart HAProxy
      service:
        name: haproxy
        state: restarted

29. How would you use Ansible to automate the backup and restore of a MySQL database?

- name: Backup MySQL
  mysql_db:
    name: mydb
    state: dump
    target: /path/to/backup.sql

- name: Restore MySQL
  mysql_db:
    name: mydb
    state: import
    target: /path/to/backup.sql

30. Can you explain how Ansible uses Jinja2 templating to generate configuration files?

Jinja2 is used to create dynamic templates. Variables and logic can be embedded in templates:

server {
  listen 80;
  server_name {{ server_name }};
  location / {
    proxy_pass http://{{ backend }};
  }
}

- name: Deploy template
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf

