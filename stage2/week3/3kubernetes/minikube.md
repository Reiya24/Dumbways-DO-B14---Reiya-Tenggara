# instalasi minikube

install docker terlebih dahulu

setelah itu, kita bisa install minikube dengan menggunakan perintah
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
![image](https://user-images.githubusercontent.com/36489276/208060183-8e0bd1cf-99af-45dc-9c05-e3714eef8e42.png)

buat sebuah cluster
![image](https://user-images.githubusercontent.com/36489276/208060678-55436707-ded4-4676-b004-a724e7dab540.png)

install kubectl
![image](https://user-images.githubusercontent.com/36489276/208063243-653b90cb-31b7-4e27-8470-beb85716bfb6.png)

buat alias agar kita printah minikube kubectl bisa disingkat jadi kubectl
![image](https://user-images.githubusercontent.com/36489276/208062160-1b1867c1-9ac5-4145-b105-a65787a84699.png)

deploy service dari image nginx
![image](https://user-images.githubusercontent.com/36489276/208063912-a89e6947-861d-4e2f-ac8b-3747c0e9ad21.png)

expose port agar dapat diakses di lokal system kita
![image](https://user-images.githubusercontent.com/36489276/208064685-68d3703c-c337-4866-b2e8-4a9f8ff9018a.png)

test apakah service sudah berjalan
![image](https://user-images.githubusercontent.com/36489276/208064751-7a371b21-edb0-4529-aa9d-bdcca976bc9f.png)

nginx telah berjalan
![image](https://user-images.githubusercontent.com/36489276/208064834-9ab0f4a1-230f-4fcf-897a-19ceea1d497d.png)

