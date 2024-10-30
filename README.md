
---
- name: Installer et configurer Nginx
  hosts: webservers
  become: yes
  tasks:
    - name: Installer le paquet Nginx
      apt:
        name: nginx
        state: present

    - name: Démarrer et activer le service Nginx
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Déployer la page d'accueil personnalisée
      copy:
        src: html/index.html 
        dest: /var/www/html/index.html
        owner: www-data
        group: www-data
        mode: '0644'
