# setup grafana agar terintegrasi dengan prometheus

masuk ke halaman dashboard grafana menggunakan ip publik dan port yang sudah kit definisikan.

setelah itu lakukan login, username dan password default saat kita pertama kali mendaftar adalah "admin"
![image](https://user-images.githubusercontent.com/36489276/207026461-60547cfb-9aec-44c4-a35a-172b69300d7a.png)

setelah itu, akan muncul form penggantian password, masukan password baru, atau kita bisa skip
![image](https://user-images.githubusercontent.com/36489276/207026623-3cb2e634-0e0e-4ad4-a4ca-c7578b8b6e7b.png)

setelah itu, kita tambahkan data source dari prometheus, klik menu seting yang ada di kiri bawah, lalu pilih data source
![image](https://user-images.githubusercontent.com/36489276/207026794-33db240c-66b9-4dd6-848d-bdcb2a303569.png)

pilih add data source
![image](https://user-images.githubusercontent.com/36489276/207027862-1e7b5be8-34bf-403d-9792-25a13d219efc.png)

pilih prometheus
![image](https://user-images.githubusercontent.com/36489276/207028039-c29df3df-0354-4295-b922-d36578d4cf19.png)

nama bisa disesuaikan, setelah itu, URL masukan ip private dan port dari prometheus
![image](https://user-images.githubusercontent.com/36489276/207028176-0e74d108-466c-4984-92cd-186e6b73ca8c.png)

tambahkan scrape interval dan query timeout atau biarkan default.
scrape interval: berapa lama perubahan akan di refresh
query timeout: berapa lama prometheus dinyatakan timeout bila tidak ada data selama detik yang didefinisikan
![image](https://user-images.githubusercontent.com/36489276/207029863-199c0449-f31c-45b2-89a8-514b1afb1c1b.png)


setelah itu, klik save & test, bila muncul notifikasi berwarna hijau "Data Source is working", artinya grafana berhasil terintegrasi dengan prometheus

# setup dashboard untuk monitoring CPU dan RAM

## CPU
pada halaman grafana, pilih menu dashboard di kiri (logo kotak empat) klik +new dashboard
![image](https://user-images.githubusercontent.com/36489276/207031457-e592d927-a7b4-4e7e-9228-b9154f8c688d.png)

pilih add new panel

![image](https://user-images.githubusercontent.com/36489276/207035968-ac163b69-f628-4529-b592-051d677b7c62.png)

lalu saya akan memasukan rumus, klik code, lalu masukan rumus, saya akan memasukan rumus
```
irate(process_cpu_seconds_total{job="prometheus"}[1m])*100
```
artinya, saya akan memasukan rata - rata penggunaan CPU dari job prometeus, dan data akan di amabil setiap 1 menit
![image](https://user-images.githubusercontent.com/36489276/207065375-fb249eef-cf78-449f-8086-b18d9b16df6b.png)

kita bisa kostumisasi di panel sebelah kanan, contohnya saya akan mengubah judul panel menjadi cpu usage
![image](https://user-images.githubusercontent.com/36489276/207067179-cb88162c-7a1c-427f-9dca-7658f20e6917.png)

setelah itu klik tombol apply di kanan atas untuk menyimpan

![image](https://user-images.githubusercontent.com/36489276/207065922-1eaf72e8-fcf5-4b42-96cb-001aff050ba9.png)

panel cpu berhasil ditambahkan
![image](https://user-images.githubusercontent.com/36489276/207067472-a720e03e-6bbd-49be-b43a-4b1900b8688e.png)



## RAM
