# FINAL-PROJECT-OS-SERVER-SYSTEM-ADMIN---22.83.0829
Repository ini berisi Dokumentasi Instalasi dan Konfigurasi berbagai layanan Server pada Linux Distro Debian.
Beberapa service dalam repository ini masih dalam tahap pengembangan sehingga akan ada pengembangan lagi ke depannya.
Service yang telah jalan di antaranya adalah SSH, Apache2, Monitoring.

## DAFTAR ISI
1. [Instalasi dan Konfigurasi SSH Server](#1-Instalasi-dan-Konfigurasi-SSH-Server)
2. [Instalasi dan Konfigurasi Web Server](#2-Instalasi-dan-Konfigurasi-Web-Server)


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
