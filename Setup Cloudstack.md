# Konfigurasi Zone di Apache CloudStack

Berikut adalah langkah-langkah lengkap untuk konfigurasi Zone di CloudStack, dilengkapi dengan gambar referensi berdasarkan urutan.

---

## 1. Pilih Tipe Zone

Pada tahap awal, tentukan tipe zone yang ingin digunakan.

![Choose zone type](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/1.%20Choose%20zone%20type.png)

---

## 2. Pilih Core Zone Type

Tentukan apakah zone yang digunakan adalah Basic atau Advanced.

![Choose core zone type](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/2.%20Choose%20core%20zone%20type.png)

---

## 3. Masukkan Detail Zone

Isi nama zone dan parameter lainnya.

![Input the zone details](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/2.%20Choose%20core%20zone%20type.png)

---

## 4. Tambah Public Traffic

Tentukan jaringan publik untuk akses luar.

![Add public traffic](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/4.%20Add%20public%20traffic.png)

---

## 5. Tambah Pod

Masukkan konfigurasi pod seperti gateway, netmask, dan IP range.

![Add new pod](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/5.%20Add%20new%20pod.png)

---

## 6. Set Guest Traffic

Tentukan jaringan guest yang akan digunakan oleh VM.

![Set guest traffic](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/6.%20Set%20guest%20traffic.png)

---

## 7. Tambah Cluster

Tentukan nama cluster dan jenis hypervisor.

![Add new cluster](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/7.%20Add%20new%20cluster.png)

---

## 8. Tambah Host

Masukkan detail host (IP, username, password).

![Add host](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/7.%20Add%20new%20cluster.png)

---

## 9. Tambah Primary Storage 

Tentukan penyimpanan utama, misalnya NFS path.

![Input primary storage details](http://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/9.%20Input%20primary%20storage%20details.png)

---

## 10. Tambah Secondary Storage

Tambahkan lokasi penyimpanan image/template ISO.

![Input secondary storage details](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/10.%20Input%20secondary%20storage%20details.png)

---

## 11. Launch the Zone

Setelah semua konfigurasi selesai, klik **Launch Zone**.

![Launch the zone](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/11.%20Launch%20the%20zone.png)

---

# Membuat Instance di Apache CloudStack

Dokumentasi ini menjelaskan proses membuat virtual machine (Instance) di Apache CloudStack mulai dari compute offering hingga VM berjalan.

---

## 1. Tambah Compute Offering

Buat compute offering sebagai konfigurasi resource (CPU, RAM) untuk VM.

![Add compute offering](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Instance/1.%20Add%20compute%20offering.png)

---

## 2. Daftarkan ISO

Daftarkan file ISO (misal Ubuntu, Debian, dsb.) untuk digunakan dalam instalasi instance.

![Register the ISO](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Instance/2.%20Register%20the%20ISO.png)

---

## 3. Masukkan Detail Instance (1)

Mulai proses pembuatan instance dengan memilih zona, template, dan offering.

![Add instance details (1)](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Instance/3.%20Add%20instance%20details%20(1).png)

---

## 4. Masukkan Detail Instance (2)


![Add instance details (2)](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Instance/4.%20Add%20instance%20details%20(2).png)

---

## 5. Masukkan Detail Instance (3)


![Add instance details (3)](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Instance/5.%20Add%20instance%20details%20(3).png)

---

## 6. Masukkan Detail Instance (4)

![Add instance details (4)](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Instance/6.%20Add%20instance%20details%20(4).png)

---

## 7. Instance Berjalan

Instance berhasil dibuat dan statusnya sekarang **Running**.

![Instance running](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Instance/7.%20Instance%20running.png)

---


# Requirement Task - Apache CloudStack

Dokumentasi langkah-langkah pengaturan firewall, port forwarding, akses SSH, dan HTTP untuk VM CloudStack.

---

## 1. Ubuntu Error (Before Detach)

Masalah saat VM tidak bisa booting karena perangkat ISO belum dilepas.

![Ubuntu Error (Before Detach)](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/1.%20Ubuntu%20Error%20(Before%20Detach).png)

---

## 2. Detach ISO

Lepaskan ISO agar VM dapat boot dari disk.

![Detach ISO](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/2.%20Detach%20ISO.png)

---

## 3. Ubuntu Fixed (After Detach)

VM berhasil booting setelah ISO dilepas.

![Ubuntu Fixed (After Detach)](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/3.%20Ubuntu%20Fixed%20(After%20Detach).png)

---

## 4. Egress Rule

Atur egress rule agar VM bisa keluar ke internet.

![Egress Rule](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/4.%20Egress%20Rule.png)

---

## 5. Firewall 22

Aktifkan firewall port 22 untuk SSH.

![Firewall 22](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/5.%20Firewall%2022.png)

---

## 6. VM bisa akses internet

Verifikasi VM sudah bisa akses internet.

![VM bisa akses internet](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/6.%20VM%20bisa%20akses%20internet.png)

---

## 7. Port Forwarding 22

Lakukan port forwarding dari host ke VM untuk port 22 (SSH).

![Port Forwarding 22](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/7.%20Port%20Forwarding%2022.png)

---

## 8. Mengatur VM agar membuka Port 22

Buka port 22 pada firewall di dalam VM.

![Mengatur VM agar membuka Port 22](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/8.%20Mengatur%20VM%20agar%20membuka%20Port%2022.png)

---

## 9. Bisa SSH dari luar

Verifikasi bahwa VM dapat diakses via SSH dari luar.

![Bisa SSH dari luar](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/9.%20Bisa%20SSH%20dari%20luar.png)

---

## 10. Firewall 2222

Tambahkan aturan firewall untuk port 2222 (akses alternatif SSH).

![Firewall 2222](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/10.%20Firewall%202222.png)

---

## 11. Port Forwarding 2222

Lakukan port forwarding dari port 2222 host ke port 22 VM.

![Port Forwarding 2222](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/11.%20Port%20Forwarding%202222.png)

---

## 12. Mengatur Port Forwarding 2222 di Ubuntu Host

Konfigurasi port forwarding 2222 pada Ubuntu host menggunakan `iptables` atau `netplan`.

![Mengatur Port Forwarding 2222 di Ubuntu Host](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/12.%20Mengatur%20Port%20Forwarding%202222%20di%20Ubuntu%20Host.png)

---

## 13. Mengatur VM agar membuka Port 2222

Pastikan firewall di VM membuka port 2222.

![Mengatur VM agar membuka Port 2222](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/13.%20Mengatur%20VM%20agar%20membuka%20Port%202222.png)

---

## 14. Bisa Port Forwarding 2222

Verifikasi bahwa port forwarding ke 2222 berhasil.

![Bisa Port Forwarding 2222](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/14.%20Bisa%20Port%20Forwarding%202222.png)

---

## 15. Mengatur Port Forwarding 80 di Ubuntu Host

Konfigurasi forwarding port 80 untuk akses web (HTTP).

![Mengatur Port Forwarding 80 di Ubuntu Host](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/15.%20Mengatur%20Port%20Forwarding%2080%20di%20Ubuntu%20Host.png)

---

## 16. Firewall 80

Aktifkan firewall port 80 untuk HTTP.

![Firewall 80](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/16.%20Firewall%2080.png)

---

## 17. Port Forwarding 80

Lakukan port forwarding dari port 80 host ke port 80 VM.

![Port Forwarding 80](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/17.%20Port%20Forwarding%2080.png)

---

## 18. Install Apache2 sebagai Web Server

Install Apache2 di VM sebagai web server.

![Install Apache2 sebagai Web Server](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/17.%20Port%20Forwarding%2080.png)

---

## 19. Akses HTTP Apache2

Verifikasi akses ke web server Apache2 dari browser.

![Akses HTTP Apache2](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/19.%20Akses%20HTTP%20Apache2.png)

