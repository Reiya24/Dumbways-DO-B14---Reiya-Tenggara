buat sebuah file konfigurasi prometheus yang akan kita mount di docker volume (karena di kasus sayajika saya jalankan volume terlebih dahulu,
container akan selalu restart)
![image](https://user-images.githubusercontent.com/36489276/207019371-d65ca133-805d-4b40-9001-9fe78782a14b.png)

isikan kurang lebih sebagai berikut:
```
global:
  scrape_interval: 5s 
  evaluation_interval: 5s 

scrape_configs:
  - job_name: prometheus
    static_configs:
      - targets: ["localhost:9090"]
```
![image](https://user-images.githubusercontent.com/36489276/207019812-208be368-ea4f-4282-95ec-d6e4f36a1fd9.png)

buat sebuah docker compose file untuk node exporter, prometheus, dan grafana
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
    prometheus:
      container_name: prometheus
      image: bitnami/prometheus:latest
      stdin_open: true
      restart: unless-stopped
      ports:
          - 9090:9090
      volumes:
        - ~/konfigurasi_prometheus/prometheus.yml:/etc/prometheus/prometheus.yml
    grafana:
      container_name: grafana
      image: grafana/grafana:latest
      stdin_open: true
      restart: unless-stopped
      ports:
        - 3123:3000
```
![image](https://user-images.githubusercontent.com/36489276/207018221-51cfd04c-60fe-4958-8db1-f09c510c13e1.png)

jalankan docker compose
```
docker compose -f monitoring_compose.yml up -d
```
![image](https://user-images.githubusercontent.com/36489276/207018404-2e91eec4-6d1a-432e-8f99-c0845b919325.png)

untuk mengecek apakah node exporter berhasil, akses publik IP kita dan tambahkan port yang sudah kita forward
![image](https://user-images.githubusercontent.com/36489276/207020933-5f80266a-7384-4ee7-b6d2-3c35010f2f27.png)
node exporter berhasil, dan setiap di refresh selalu berubah nilainya

untuk mengecek apakah prometheus berhasil di deploy, akses publik IP kita dan tambahkan port yang sudah kita forward
![image](https://user-images.githubusercontent.com/36489276/207021141-73371c84-041e-4b19-9d29-640e1e46d0d8.png)
node exporter berhasil, dan setiap di refresh selalu berubah nilainya



