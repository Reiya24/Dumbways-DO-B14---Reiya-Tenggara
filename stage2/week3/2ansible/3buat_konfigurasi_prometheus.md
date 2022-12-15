# setup dashboard frontend
masuk ke dashboard grafa

cari ikon dashboard, klik new dashboard
![image](https://user-images.githubusercontent.com/36489276/207672745-f4755184-c6b7-42e4-8ea9-cf7b42cc4d22.png)

pilih add a new panel
![image](https://user-images.githubusercontent.com/36489276/207673532-92dec86f-0010-4dd7-9cfa-4cfe4e361b18.png)

lalu pilih datasource yang digunakan, ubah nama panel,  untuk penggunaan cpu saya menggunakan rumus dibawah, pilih apply untuk menyimpan
```
irate(process_cpu_seconds_total{job="frontend"}[1m])*100
```
![image](https://user-images.githubusercontent.com/36489276/207674040-ab2371f9-5a69-40c5-b87a-c6f3dfa9d39d.png)

untuk penggunaan memory, kurang lebih serupa, saya akan builder untuk menampilan memory yang aktif dalam bentuk bytes

![image](https://user-images.githubusercontent.com/36489276/207676999-83cf3f50-3164-4936-ac2d-878d680f3ad8.png)

lalu untuk penggunaan network di gateway, saya tambahkan monitoring untuk melihat paket 
![image](https://user-images.githubusercontent.com/36489276/207864930-abc2cb35-ac9d-4711-a3d1-0461225a870e.png)



