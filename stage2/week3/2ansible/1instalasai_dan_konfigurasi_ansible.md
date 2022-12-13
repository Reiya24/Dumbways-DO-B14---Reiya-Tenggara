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
