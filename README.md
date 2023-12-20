# FINAL-PROJECT-OS-SERVER-SYSTEM-ADMIN---22.83.0829
Repository ini berisi Dokumentasi Instalasi dan Konfigurasi berbagai layanan Server pada Linux Distro Debian.
Beberapa service dalam repository ini masih dalam tahap pengembangan sehingga akan ada pengembangan lagi ke depannya.
Service yang telah jalan di antaranya adalah SSH, Apache2, Monitoring.

## DAFTAR ISI
1. [Instalasi dan Konfigurasi SSH Server](#1-Instalasi-dan-Konfigurasi-SSH-Server)
2. [Instalasi dan Konfigurasi Web Server](#2-Instalasi-dan-Konfigurasi-Web-Server)
3. [Instalasi dan Konfigurasi Monitoring Server](#3-Instalasi-dan-Konfigurasi-Monitoring-Server)

## 1. Instalasi dan Konfigurasi SSH Server
#### 1.a Instalasi SSH
**Lakukan Instalasi Paket SSH**
```
apt-get install openssh-server
```
#### 1.b Konfigurasi SSH
**Konfigurasi menggunakan nano (bisa juga pakai yang lainnya)**
```
nano /etc/ssh/sshd_config
```
**Edit konfigurasi**
```
Hilangkan tanda # pada PermitRootLogin dan ubah ke yes
```
**Restart SSH Server**
```
systemctl restart sshd
```
#### 1.c Uji Konfigurasi
Sesuaikan dengan IPADDR ataupun Port yang digunakan
```
ssh root@IPADDR -p 22
```
## 2. Instalasi dan Konfigurasi Web Server
#### 1.a Instalasi Apache2
**Instalasi Paket Apache2**
```
apt update
apt-get install apache2
```
#### 1.b Konfigurasi Apache2
**Open File Konfigurasinya**
```
nano /etc/apache2/sites-available/000-default.conf
```
**Edit Konfigurasi Sesuai dengan Domain yang digunakan**
```
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@Fadhil.com
        ServerName Fadhil.com
        DocumentRoot /var/www/html
```
**Restart Service Apache2**
```
systemctl restart apache2
```
## 3. Instalasi dan Konfigurasi Monitoring Server
#### 1.a Instalasi 
**Instalasi paket Prometheus dan Node-exporter**
```
apt-get install prometheus prometheus-node-exporter
```
**Instalasi Paket Grafana**
```
wget -q -O /usr/share/keyrings/grafana.key https://packages.grafana.com/gpg.key
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://packages.grafana.com/oss/deb stable main" | tee -a /etc/apt/sources.list.d/grafana.list
apt-get update
apt-get install grafana
```
#### 1.b Konfigurasi
**Open Direktori Prometheus**
```
nano /etc/prometheus/prometheus.yml
```
**Add Monitoring Target untuk membuat Metrics dari node-exporter**
```
#menggunakan port default yaitu 9100,kita bisa mengganti ini

  - job_name: node
    # If prometheus-node-exporter is installed, grab stats about the local
    # machine by default.
    static_configs:
      - targets: ['localhost:9093']
```
**Open Direktori Grafana**
```
nano /etc/grafana/grafana.ini
```
**Edit Direktori Grafana**
```
##################### Grafana Configuration Example #####################
#
# Everything has defaults so you only need to uncomment things you want to
# change

# possible values : production, development
;app_mode = production

# instance name, defaults to HOSTNAME environment variable value or hostname if HOSTNAME var is empty
;instance_name = ${HOSTNAME}

# force migration will run migrations that might cause dataloss
# Deprecated, use clean_upgrade option in [unified_alerting.upgrade] instead.
;force_migration = false

#################################### Paths ####################################
[paths]
# Path to where grafana can store temp files, sessions, and the sqlite3 db (if that is used)
;data = /var/lib/grafana

# Temporary files in `data` directory older than given duration will be removed
;temp_data_lifetime = 24h

# Directory where grafana can store logs
;logs = /var/log/grafana
```
**Enable & Restart Grafana**
```
systemctl enable grafana-server
systemctl restart grafana-server
```
