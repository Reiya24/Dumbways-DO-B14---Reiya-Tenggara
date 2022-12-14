# kirim publik key ke webserver dan buat user dengan ansbile playbook
gunakan perintah
```
ssh-copy-id -f -i ~/.ssh/id_rsa.pub  webserver@103.250.11.144
```
![image](https://user-images.githubusercontent.com/36489276/207526269-7a6b98e6-9847-4c5f-9887-75ce13514b17.png)

ketik yes, dan masukan password

![image](https://user-images.githubusercontent.com/36489276/207527155-1c6af4cb-019f-4d4f-ba79-29af6a5c883b.png)

setelah itu kita bisa masuk tanpa password

karena kita sudah setup inventory dan ansible.cfg sebelumnya, saya tinggal membuat sebuah script untuk membuat user baru untuk webserver, isikan kurang lebih sebagai berikut
```
---
- hosts: webserver
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

![image](https://user-images.githubusercontent.com/36489276/207528223-fe1baeaf-1faf-48ae-b3d6-209e3081bb92.png)


check syntaxnya
![image](https://user-images.githubusercontent.com/36489276/207528186-431f5a0c-d0ce-4daa-b7c7-38aa49891659.png)

jalankan
![image](https://user-images.githubusercontent.com/36489276/207528530-0d2a8421-32b7-4678-9c7b-2cb1fcc7c7f4.png)

# isntalasi nginx dengan ansible playbok
```
buat ansible playbook 
---
- hosts: webserver
  become: true
  gather_facts: true
  tasks:
    - name: install nginx menggunakan apt
      apt:
        name: nginx
        state: latest
    - name: jalankan service nginx
      service:
        name: nginx
        state: started
```
![image](https://user-images.githubusercontent.com/36489276/207583785-5fe90802-14ad-4dcd-bc39-0110c45487d3.png)

cek apakah ada kesalahan syntax
```
ansible-playbook install_nginx_ansible_playbook.yml --syntax-check
```
![image](https://user-images.githubusercontent.com/36489276/207584846-d54b7da9-c6b0-4daf-b9d4-0cb68543fb97.png)

jalankan playbooknya
![image](https://user-images.githubusercontent.com/36489276/207586259-c6c58851-8a2f-407a-a8ff-840b3b6251b7.png)

# konfigurasi reverse proxy

## setup cloudflare
buka dashboard cloudflare, pilih dns, lalu add record, masukan nama domain, ip webserver, matikan proxy status
![image](https://user-images.githubusercontent.com/36489276/207594067-d8f433e7-1304-4124-9aea-6aff53e8bf4b.png)
![image](https://user-images.githubusercontent.com/36489276/207594175-dca29bc0-2aa2-4229-9de6-04ea7c3fb932.png)

# setup reverse proxy

saya akan membuat folder berisi file2 konfigurasi nginx

![image](https://user-images.githubusercontent.com/36489276/207595697-141416f0-294a-4ca6-86f1-a35f8f6cfc4a.png)
![image](https://user-images.githubusercontent.com/36489276/207596673-ceeda63e-5462-49fa-bdbe-09477441a480.png)




