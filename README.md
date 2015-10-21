# Ansible scripts for proxmox server
Configuration of proxmox server

To install the server the first time, use:

    ansible-playbook -i host playbook/install.yml

Then to create containers, create it first from proxmox interface and add then an entry to `vhosts.yml` like the following:

    vhosts:
      - address: "10.0.0.3"
        web:
          - prefix: "blog"
            dest: "80"
            is_ssl: yes
        nat:
          - src: "1003"
            dest: "22"

To apply configuration, you have to run:

    ansible-playbook -i host playbook playbook/update_vhosts.yml
