saya membuat sebuah script untuk installer ansible
```
#!/bin/bash
sudo apt install -y software-properties-common #instal depedensi yang diperlukan
sudo add-apt-repository --yes --update ppa:ansible/ansible #tambahkan repository untuk ansible
sudo apt update #lakukan update
sudo apt install -y ansible #install ansible
ansible --version #cek versi dari ansible
```
![image](https://user-images.githubusercontent.com/36489276/207254765-68c3de55-73ec-40f8-ba58-e0b78038be41.png)

ubah perizinan scriptnya
```
chmod 700 ansible_installer.sh
```

![image](https://user-images.githubusercontent.com/36489276/207254824-e79b552a-136f-4706-b625-ff7bd3ef2c32.png)

jalankan scriptnya
![image](https://user-images.githubusercontent.com/36489276/207255574-a16c2e04-aa28-4485-8d47-3b3ff8d0c7a4.png)

# setup SSH keyless
saya akan buat sebuah ssh dengan nama dan direktori default
![image](https://user-images.githubusercontent.com/36489276/207267225-d8a029e8-b20b-4c62-85a2-d22578bb8bcf.png)

lalu copy publik key ke server tujan kita menggunakan ssh-copy-id
```
ssh-copy-id -f -i ~/.ssh/id_rsa.pub  appserver@103.187.147.8
```
![image](https://user-images.githubusercontent.com/36489276/207267682-c510de0a-41ac-48c6-a30a-6cc24013a126.png)
ketik yes, lalu masukan password

jika berhasil kita bisa masuk ke server tersebut tanpa menggunakan password
![image](https://user-images.githubusercontent.com/36489276/207267950-c39f1931-e357-43ba-9a4f-06266f4cf7fe.png)

# buat file intentori
buat file inventori yang berfungsi untuk menyimpan informasi server2 yang akan kita konfigurasi, disini saya akan memasukan appserver dan gateway
![image](https://user-images.githubusercontent.com/36489276/207364210-4dbe86c0-1bd4-44e9-8486-f355bb8f2634.png)

# buat file ansible.cfg
buat sebuah file ansible.cfg yang berfungsi untuk mengkonfigurasi ansible kita
![image](https://user-images.githubusercontent.com/36489276/207320891-9872d6d3-2749-4c2d-a76f-c703d680fb50.png)

# buat script ansible-playbook untuk membuat user secara otomatis
buat file yang isinya kurang lebih seperti berikut
```
---
- hosts: appserver
  become: true
  tasks:
  - name: "buat user baru"
    ansible.builtin.user:
      name: "{{username}}"
      password: "{{password}}"
      groups: sudo
      shell: /bin/bash
      state: present
      create_home: true
      home: /home/{{username}}
  - authorized_key:
      user: reiya
      state: present
      manage_dir: yes
      key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}"
  vars:
    - username: "reiya"
    - password: "$6$BnAmwglXdiUj$lvNBlD1xbemWwSrkE3FQ2xqq6Cp.9omcCqqPdSSPvZKi7e5.K28Mvamv4miE/2/6kSEwmxxT9QzK9HYNZC3bC/"
```
![image](https://user-images.githubusercontent.com/36489276/207321635-ab9680e0-233b-46ac-8d1d-ee4b5ba134a8.png)

untuk mengenkripsi password, saya menggunakan whois, install whois terlebih dahulu
![image](https://user-images.githubusercontent.com/36489276/207385008-1ac8bb43-d920-450d-ab50-7820a5cdc168.png)

setelah itu, enkripsi password yang akan kita masukan dengan menggunakan perintah
![image](https://user-images.githubusercontent.com/36489276/207385154-1dcc408b-dce2-4eb1-bb6f-20ace1914c03.png)

setelah itu check syntaknya untuk mengecek apakah ada kesalahan penulisan ansible-playbook kita
```
ansible-playbook add_user_reiya.yml --syntax-check
```
![image](https://user-images.githubusercontent.com/36489276/207321916-6b28350c-f235-45f4-bf62-6ca0056f45b1.png)

jalankan file ansiblenya
```
ansible-playbook add_user_reiya.yml
```
![image](https://user-images.githubusercontent.com/36489276/207321212-4b587d87-9c17-47b8-a66d-f4534025dddc.png)

proses membuat user baru berhasil, kita dapat login menggunakan user reiya
![image](https://user-images.githubusercontent.com/36489276/207322253-29a1c12c-46fd-493f-8b3d-fbf7b7caea47.png)

# buat script ansible-playbook untuk instalasi docker
buat script kurang lebih seperti ini
```
---
- hosts: appserver
  become: true
  gather_facts: true
  tasks:
    - name: install depedensi yang diperlukan untuk docker
      apt:
        pkg:
          - apt-transport-https
          - ca-certificates
          - curl
          - software-properties-common
          - python3-pip
          - virtualenv
          - python3-setuptools
        state: latest
        update_cache: true
    - name: tambahkan docker gpg key
      apt_key:
        url: https://download.docker.com/linux/ubuntu/gpg
        state: present
    - name: tambahkan docker repository
      apt_repository:
        repo: deb https://download.docker.com/linux/ubuntu focal stable
        state: present
    - name: install docker
      apt:
        name:
          - docker-ce
          - docker-ce-cli
          - containerd.io
          - docker-compose-plugin
        state: latest
        update_cache: yes
    - name: tambahkan user appserver ke group docker
      user:
        name: appserver
        groups: sudo, docker
        append: yes    
    - name: tambahkan user reiya ke group docker
      user:
        name: reiya
        groups: sudo, docker
        append: yes
```
![image](https://user-images.githubusercontent.com/36489276/207324252-47cf3e29-c612-47fe-a042-8a8e0ed87f52.png)
![image](https://user-images.githubusercontent.com/36489276/207324296-d826c460-b1cd-4cf4-828b-dbcdf53a727c.png)


check apakah ada kesalahan syntax
![image](https://user-images.githubusercontent.com/36489276/207324399-c8a183a5-6efb-4b09-b54b-1160587aac06.png)

setelah itu jalankan ansible-playbook
```
ansible-playbook install_docker.yml
```
![image](https://user-images.githubusercontent.com/36489276/207325489-7d7c3bae-ab3a-4733-af09-ee5b875c3952.png)

docker berhasil di install di appserver
![image](https://user-images.githubusercontent.com/36489276/207325652-e6a48036-53e7-44d9-ba55-fe849ccc36cc.png)

# buat script ansible-playbook untuk docker deploy docker compose node-exporter dan wayshub-frontend

buat sebuah docker compose untuk mendeploy node exporter dan wayshub frontend
```
version: '3.7'
services:
    node_exporter:
      container_name: node_exporter
      image: bitnami/node-exporter
      stdin_open: true
      restart: unless-stopped
      ports:
        - 9100:9100
    wayshub_frontend:
      container_name: wayshub_frontend
      image: ilhaskam/wayshub-frontend
      stdin_open: true
      restart: unless-stopped
      ports:
        - 3000:3000
```
![image](https://user-images.githubusercontent.com/36489276/207570977-d7bcc8dc-0cac-4abb-ad90-f221416b2014.png)

setelah itu saya akan membuat sebuah ansible playbook yang berfungsi untuk mencopy docker compose dari lokal ke appserver, lalu menjalankannya
```
---
- hosts: appserver
  become: true
  gather_facts: true
  tasks:

    - name: copy docker compose
      copy:
        src: compose/
        dest: /home/appserver

    - name: jalankan docker compose
      shell: "docker compose up -d"
```
![image](https://user-images.githubusercontent.com/36489276/207572448-44250844-e195-4e78-af80-1a72844f3c12.png)

cek syntaxnya untuk memastikan apakah ada kesalahan
![image](https://user-images.githubusercontent.com/36489276/207572578-8a77101a-92c4-44a2-b4eb-8f709f3eb219.png)

jalankan playbooknya
```
$ansible-playbook install_node_exporter_dan_wayshub_ansible_playbook.yml
```
![image](https://user-images.githubusercontent.com/36489276/207572651-954661d5-5573-467f-8030-17fab9df6c62.png)

docker compose berhasil dijalankan
![image](https://user-images.githubusercontent.com/36489276/207573520-6ea64f65-98b6-4a8a-8c94-1f2c0ab2916d.png)

![image](https://user-images.githubusercontent.com/36489276/207573821-303738cb-b142-4134-8fcd-62616ac50689.png)


