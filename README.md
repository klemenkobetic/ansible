sudo ansible-galaxy install -r ../requirements.txt --ignore-errors

sudo vagrant up db 
sudo vagrant up web

change :
/etc/ansible/roles/nbz4live.php-fpm/handlers/main.yml

---
- name: restart php-fpm
  command: service php5-fpm restart

- name: reload php-fpm
  command: service php5-fpm reload

