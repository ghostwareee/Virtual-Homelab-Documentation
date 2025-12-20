1. tujuan 
- Membuat script bash sederhana untuk automasi
- Melakukan update sistem secara otomatis 
- Melakukan pengecekan resource server
- Memahami permission file (chmod & chown)
- Menjadwalkan task menggunakan cron


2.  Environment/Lingkungan
- Host: EndeavourOS
- Guest: Ubuntu Server
- VM: QEMU
- Akses: SSH + tmux
- Tools: bash, cron, vim, chmod, df, free, top/htop, journalctl

1. Langkah Kerja
# A. Membuat Script update Sistem
- Buat file script: 
```bash
vim update.sh
```
isi script: 
```bash
#!/bin/bash

echo "==== Updating package list ===="
sudo apt update 

echo "==== Upgrading packages ===="
sudo apt upgrade -y

echo "==== Update completed! ===="
```
- Beri permission executable:
```bash

chmod +x update.sh

```
- Jalankan script:
```bash
./update.sh
```


---

# B. Monitoring Resource Server
- Cek penggunaan disk: 
```bash
df -h
```
- Cek penggunaan memory:
```bash
free -h
```
- Monitoring realtime:
```bash
htop
```


---
# C. Backup Sederhana Direktori Home
- Buat script backup:
```bash
vim backup_home.sh
```
isi:
```bash
#!/bin/bash

tar -czvf backup-home-$(date +%F).tar.gz /home --exclude=/home/*/.cache
```

- Permission: 
```bash
chmod +x backup_home.sh 
```

catatan : script ini menghasilkan file backup dengan nama berdasarkan tanggal, sehingga memudahkan tracking

--- 

# D. Permission File (chmod & chown)
- Melihat permission file
```bash
ls -l updater.sh
```

contoh output:
```bash
-rwxr-xr-- 1 user user update.sh
```
Penjelasan singkat:
- Owner: rwx
- Group: r-x
- Others: r--
---

4. Hasil & Catatan 
- Script update dan backup berhasil dijalankan 
- Monitoring resource server dilakukan dan hasil pengamatan menunjukkan kondisi operasional server berjalan normal
- Cronjob aktif untuk update dan backup otomatis
- Server siap untuk operasional jangka panjang dengan maintenance dasar