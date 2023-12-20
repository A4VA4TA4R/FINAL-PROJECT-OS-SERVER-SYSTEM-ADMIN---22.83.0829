# FINAL-PROJECT-OS-SERVER-SYSTEM-ADMIN---22.83.0829
Repository ini berisi Dokumentasi Instalasi dan Konfigurasi berbagai layanan Server pada Linux Distro Debian.
Beberapa service dalam repository ini masih dalam tahap pengembangan sehingga akan ada pengembangan lagi ke depannya.
Service yang telah jalan di antaranya adalah SSH, Apache2, Monitoring.

## DAFTAR ISI
1. [Instalasi dan Konfigurasi SSH Server]


## 1. Instalasi dan Konfigurasi SSH Server
#### 1.a Instalasi SSH
**Lakukan Instalasi Paket SSH**
```
apt-get install openssh-server
```
#### 1.b Konfigurasi SSH
**Konfigurasi menggunakan text editor (nano, bisa juga pakai yang lainnya)**
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
