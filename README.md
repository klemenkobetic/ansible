sudo ansible-galaxy install -r ../requirements.txt --ignore-errors

sudo vagrant up db 
sudo vagrant up web

change :
/etc/ansible/roles/nbz4live.php-fpm/handlers/main.yml

---
- name: restart php-fpm
  command: service php5-fpm restart
#  service: name={{php_fpm_binary_name}} state=restarted

- name: reload php-fpm
  command: service php5-fpm reload
#  service: name={{php_fpm_binary_name}} state=reloaded

