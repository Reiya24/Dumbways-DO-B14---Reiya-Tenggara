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
![image](https://user-images.githubusercontent.com/36489276/207269044-d459886e-f68b-4135-9243-c1a5639eac10.png)

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

