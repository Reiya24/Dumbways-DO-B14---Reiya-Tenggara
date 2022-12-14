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

buata 
