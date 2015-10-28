# Ansible scripts for proxmox server
Configuration of proxmox server

To install the server the first time, use:

    ansible-playbook -i host playbooks/install.yml

Then to create containers, create it first from proxmox interface and add then an entry to `vhosts.yml` like the following:

    vhosts:
      - address: "10.0.0.3"
        web:
          - prefix: "blog"
            dest: ":80"
            is_ssl: yes
            custom_config: |
              if ($http_x_plex_device_name = '') {
                rewrite ^/$ http://$http_host/web/index.html;
              }
        nat:
          - src: "1003"
            dest: "22"

To apply configuration, you have to run:

    ansible-playbook -i hosts playbooks/update_vhosts.yml

To install provision the media container, you have to create it from Proxmox, then reapply configuration with the command above and then run this playbook:

    ansible-playbook -i hosts playbooks/media.yml
