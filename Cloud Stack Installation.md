## Environment Setup

### Hardware Requirement

```
CPU : Intel Core i5 gen 8
RAM : 24 GB
Storage : 250GB
Network : Ethernet 100GB/s
Operating System : Ubuntu Server 24.04
```
Spesifikasi ini memungkinkan server menjalankan peran sebagai controller dan compute node dalam satu mesin, cukup untuk keperluan pengujian atau laboratorium kecil. 

### Network Address

```
Network Address : 10.1.10.0/24
Host IP address : 10.1.10.24/24
Gateway : 10.1.10.1
Public IP : 10.1.10.203
```
Konfigurasi ini menyusun alamat jaringan lokal (private LAN) dan gateway default yang akan digunakan untuk konektivitas internet dan komunikasi internal.

## Configure Network 

Modifikasi file konfigurasi network menggunakan netplan yang digunakan oleh Ubuntu Server 24.04:

```
cd /etc/netplan
sudo nano ./50-cloud-init.yaml
```
![Netplan](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/1.%20Configure%20Network.png)

File konfigurasi awalnya seperti ini:
```
network:
  version: 2
  ethernets:
    enp0s3:                            
      addresses: [x/24]        
      gateway4: x             
      nameservers:
        addresses: [xxx]   
```

Modifikasi konfigurasi agar menggunakan bridged networking, yang cocok untuk virtualisasi:

```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: false
      dhcp6: false
      optional: true
  bridges:
    cloudbr0:
      addresses: [10.1.10.24/24] 
      routes:
        - to: default
          via: 10.1.10.1
      nameservers:
        addresses: [1.1.1.1,8.8.8.8]
      interfaces: [enp1s0]
      dhcp4: false
      dhcp6: false
      parameters:
        stp: false
        forward-delay: 0
```

### Apply Network Configuration
Pastikan file YAML netplan tersimpan dan di apply. Setelah itu cek ip a untuk memastikan IP terkonfigurasi dengan baik.

```
sudo -i  #open new shell with root privileges
netplan generate #generate config file for the renderer
netplan apply  #applies network configuration to the system
reboot #reboot the system
```



### Test Network Connection

```
ip a
ping -c 4 8.8.8.8  
```

### Installing Monitoring Tools

```
apt update -y
apt upgrade -y
apt install htop lynx duf -y
apt install bridge-utils
```
![Installing Monitoring Tools](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/2.%20Installing%20Hardware%20resource%20monitoring%20tools.png)
Penjelasan:

* htop → monitoring penggunaan CPU/memori.
* duf → melihat kapasitas dan penggunaan disk.
* lynx → browser web berbasis CLI, berguna untuk uji koneksi HTTP.
* bridge-utils → manajemen bridge jaringan.

### Configure LVM (optional)
Perlu dijalankan jika volume logis perlu diperluas menggunakan seluruh ruang yang tersedia.

```
#not required unless logical volume is used
lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
resize2fs /dev/ubuntu-vg/ubuntu-lv
```

### Install Networking Services & Editor

```
apt-get install openntpd openssh-server sudo vim tar -y
apt-get install intel-microcode -y
passwd root
#change it to Pa$$w0rd
```
![Install networking service & editor](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/3.%20Installing%20Network%20services%20and%20text%20editor.png)

Penjelasan:
* openntpd → sinkronisasi waktu.
* openssh-server → akses remote.
* vim dan tar → editor dan tool arsip file.
* intel-microcode → firmware patch keamanan CPU Intel.

### Enable SSH Root login

```
sed -i '/#PermitRootLogin prohibit-password/a PermitRootLogin yes' /etc/ssh/sshd_config
#restart ssh service
service ssh restart
#or
systemctl restart sshd.service
```
![Enab;e SSH Root login](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/4.%20Enable%20SSH%20root%20login.png)

### Verifikasi
```
nano /etc/ssh/sshd_config
```
![Verifikasi](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/5.%20Check%20the%20SSH%20Configuration.png)
Cari line 'PermitRootLogin' pastikan diatur ke 'yes'

## Cloudstack Installation 


### Add Repository Key

```
sudo -i
mkdir -p /etc/apt/keyrings 
wget -O- http://packages.shapeblue.com/release.asc | gpg --dearmor | sudo tee /etc/apt/keyrings/cloudstack.gpg > /dev/null
echo deb [signed-by=/etc/apt/keyrings/cloudstack.gpg] http://packages.shapeblue.com/cloudstack/upstream/debian/4.18 / > /etc/apt/sources.list.d/cloudstack.list
```
![Add repository key](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/6.%20Importing%20cloudstack%20repositories%20key.png)

* Line pertama adalah membuat direktori untuk menyimpan kunci publik cloudstack
* wget -O untuk mengunduh URL yang diberikan dan mengalihkan output ke perintah 'gpg --dearmor'
* Perintah 'gpg --dearmor' akan mengonversi dari ASCII armored ke format biner
* Perintah 'sudo tee' akan mengalihkan perintah 'gpg --dearmor' ke file /etc/apt/keyrings/cloudstack.gpg

### Verify Repositories
```
nano /etc/apt/sources.list.d/cloudstack.list
```
![Verify Repositories](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/7.%20Check%20the%20added%20repositories.png)

pastikan melihat ini di line terakhir

```
deb [signed-by=/etc/apt/keyrings/cloudstack.gpg] http://packages.shapeblue.com/cloudstack/upstream/debian/4.18 /
```

### Installing Cloudstack and Mysql Server

```
apt-get update -y
apt-get install cloudstack-management mysql-server
```
![Installing Cloudstack](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/8.%20Installing%20Cloudstack%20and%20Mysql%20Server.png)

Proses ini akan memakan waktu lama...

### Configure mysql

Membuka file konfigurasi mysql

```
nano /etc/mysql/mysql.conf.d/mysqld.cnf
```
![Configure mysql](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/9.%20Configure%20mysql.png)

Tambahkan bagian ini dibawah [mysqld] section

```
server-id = 1
sql-mode="STRICT_TRANS_TABLES,NO_ENGINE_SUBSTITUTION,ERROR_FOR_DIVISION_BY_ZERO,NO_ZERO_DATE,NO_ZERO_IN_DATE,NO_ENGINE_SUBSTITUTION"
innodb_rollback_on_timeout=1
innodb_lock_wait_timeout=600
max_connections=1000
log-bin=mysql-bin
binlog-format = 'ROW'
```

restart MySQL
```
systemctl restart mysql
```

Verifikasi mysql service status
```
systemctl status mysql
```
Seharusnya terdapat kata 'active' pada output

### Setup Database sebagai Root dan Kemudian Buat username "cloud" dengan password "cloud" juga

```
cloudstack-setup-databases cloud:cloud@localhost --deploy-as=root:Pa$$w0rd -i 10.1.10.24
```
![Setup database](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/10.%20Deploy%20Database%20as%20Root%20and%20Then%20Create%20cloud%20User%20with%20Password.png)

### Configure Primary and Secondary Storage

```
apt-get install nfs-kernel-server quota
echo "/export  *(rw,async,no_root_squash,no_subtree_check)" > /etc/exports
mkdir -p /export/primary /export/secondary
exportfs -a
```
![Configure Primary and Secondary](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/11.%20Configure%20Primary%20and%20Secondary%20Storage.png)

### Configure NFS Server

```
sed -i -e 's/^RPCMOUNTDOPTS="--manage-gids"$/RPCMOUNTDOPTS="-p 892 --manage-gids"/g' /etc/default/nfs-kernel-server
sed -i -e 's/^STATDOPTS=$/STATDOPTS="--port 662 --outgoing-port 2020"/g' /etc/default/nfs-common
echo "NEED_STATD=yes" >> /etc/default/nfs-common
sed -i -e 's/^RPCRQUOTADOPTS=$/RPCRQUOTADOPTS="-p 875"/g' /etc/default/quota
service nfs-kernel-server restart
```
![Configure NFS](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/12.%20Configure%20NFS%20Server.png)

Penjelasan:

* `sed -i -e 's/^RPCMOUNTDOPTS="--manage-gids"$/RPCMOUNTDOPTS="-p 892 --manage-gids"/g' /etc/default/nfs-kernel-server`
Mengubah konfigurasi RPCMOUNTDOPTS di file /etc/default/nfs-kernel-server agar NFS menggunakan port 892.
* `sed -i -e 's/^STATDOPTS=$/STATDOPTS="--port 662 --outgoing-port 2020"/g' /etc/default/nfs-common`
Mengubah konfigurasi STATDOPTS di file /etc/default/nfs-common untuk mengatur port statd menjadi 662 dan 2020.
* `echo "NEED_STATD=yes" >> /etc/default/nfs-common`
Menambahkan baris NEED_STATD=yes ke file /etc/default/nfs-common untuk mengaktifkan statd yang diperlukan oleh NFS.
* `sed -i -e 's/^RPCRQUOTADOPTS=$/RPCRQUOTADOPTS="-p 875"/g' /etc/default/quota`
Mengubah konfigurasi RPCRQUOTADOPTS di file /etc/default/quota untuk menggunakan port 875 oleh rpcquotad (pengelola kuota disk).
* `service nfs-kernel-server restart`
Merestart layanan NFS Kernel Server agar perubahan konfigurasi yang baru diterapkan.

## Configure CloudStack KVM Host

### Install KVM & Agent

```
apt-get install qemu-kvm cloudstack-agent -y
```
![Install KVM & Agent](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/13.%20Install%20KVM%20and%20Cloudstack%20Agent.png)

### Configure KVM Virtualization Management

#### Mengubah beberapa baris

```
sed -i -e 's/\#vnc_listen.*$/vnc_listen = "0.0.0.0"/g' /etc/libvirt/qemu.conf

# On Ubuntu 22.04, add LIBVIRTD_ARGS="--listen" to /etc/default/libvirtd instead.

sed -i.bak 's/^\(LIBVIRTD_ARGS=\).*/\1"--listen"/' /etc/default/libvirtd
```

Penjelasan
* `sed -i -e 's/\#vnc_listen.*$/vnc_listen = "0.0.0.0"/g' /etc/libvirt/qemu.conf`
Mengubah baris yang diawali #vnc_listen di file /etc/libvirt/qemu.conf menjadi vnc_listen = "0.0.0.0", yang memungkinkan VNC mendengarkan pada semua alamat IP lokal. Opsi -i menyimpan perubahan langsung pada file.
* `sed -i.bak 's/^\(LIBVIRTD_ARGS=\).*/\1"--listen"/' /etc/default/libvirtd`
Mengubah baris LIBVIRTD_ARGS= di file /etc/default/libvirtd menjadi LIBVIRTD_ARGS="--listen", yang mengaktifkan opsi --listen untuk libvirtd. Opsi -i.bak membuat salinan cadangan file sebelum mengubahnya.

#### Menambahkan beberapa baris

```
echo 'listen_tls=0' >> /etc/libvirt/libvirtd.conf
echo 'listen_tcp=1' >> /etc/libvirt/libvirtd.conf
echo 'tcp_port = "16509"' >> /etc/libvirt/libvirtd.conf
echo 'mdns_adv = 0' >> /etc/libvirt/libvirtd.conf
echo 'auth_tcp = "none"' >> /etc/libvirt/libvirtd.conf
```
Penjelasan:
* `echo 'listen_tls=0' >> /etc/libvirt/libvirtd.conf`
Menonaktifkan TLS untuk mendengarkan pada daemon libvirt, artinya koneksi TLS tidak akan diterima.
* `echo 'listen_tcp=1' >> /etc/libvirt/libvirtd.conf`
Mengaktifkan TCP untuk mendengarkan pada daemon libvirt, memungkinkan koneksi TCP diterima.
* `echo 'tcp_port = "16509"' >> /etc/libvirt/libvirtd.conf`
Menentukan port 16509 sebagai tempat daemon mendengarkan koneksi TCP.
* `echo 'mdns_adv = 0' >> /etc/libvirt/libvirtd.conf`
Menonaktifkan multicast DNS, sehingga layanan libvirt tidak dapat ditemukan melalui nDNS.
* `echo 'auth_tcp = "none"' >> /etc/libvirt/libvirtd.conf`
Menonaktifkan autentikasi untuk koneksi TCP ke daemon libvirt, memungkinkan koneksi tanpa autentikasi.

#### Restart libvirtd

```
systemctl mask libvirtd.socket libvirtd-ro.socket libvirtd-admin.socket libvirtd-tls.socket libvirtd-tcp.socket
systemctl restart libvirtd
```

Penjelasan:
* `systemctl mask libvirtd.socket libvirtd-ro.socket libvirtd-admin.socket libvirtd-tls.socket libvirtd-tcp.socket`
Perintah ini menonaktifkan soket-soket yang digunakan oleh libvirtd untuk komunikasi, sehingga mencegah libvirtd menerima koneksi melalui soket tersebut.
* `systemctl restart libvirtd`
Perintah ini me-restart layanan libvirtd setelah perubahan konfigurasi atau soket, agar perubahan yang dilakukan dapat diterapkan.
libvirtd
libvirtd adalah daemon yang mengelola mesin virtual, jaringan, dan penyimpanan untuk teknologi virtualisasi seperti KVM dan QEMU. Layanan ini memberikan API konsisten untuk mengelola sumber daya virtualisasi secara aman.

### Enable Docker Compatibility

```
echo "net.bridge.bridge-nf-call-arptables = 0" >> /etc/sysctl.conf
echo "net.bridge.bridge-nf-call-iptables = 0" >> /etc/sysctl.conf
sysctl -p
```
Penjelasan:
Perintah ini menonaktifkan pemrosesan paket ARP dan IP pada jembatan jaringan (bridge) oleh arptables dan iptables, sehingga bridge akan meneruskan paket tanpa diproses oleh firewall. Ini penting agar Docker dapat bekerja tanpa gangguan dari filter jaringan sistem.
Perintah sysctl -p digunakan untuk menerapkan perubahan tersebut secara langsung.

### Generate Unique Host ID

```
apt-get install uuid -y
UUID=$(uuid)
echo host_uuid = \"$UUID\" >> /etc/libvirt/libvirtd.conf
systemctl restart libvirtd
```
![Generate Unique Host ID](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/14.%20Generate%20Unique%20Host%20ID.png)

### Configure Firewall Rules

```
NETWORK=10.1.10.1/24
iptables -A INPUT -s $NETWORK -m state --state NEW -p udp --dport 111 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 111 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 2049 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 32803 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p udp --dport 32769 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 892 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 875 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 662 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 8250 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 8080 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 8443 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 9090 -j ACCEPT
iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 16514 -j ACCEPT
#iptables -A INPUT -s $NETWORK -m state --state NEW -p udp --dport 3128 -j ACCEPT
#iptables -A INPUT -s $NETWORK -m state --state NEW -p tcp --dport 3128 -j ACCEPT

apt-get install iptables-persistent
```
![Configure Firewall Rules](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/15.%20Configure%20Iptables%20Firewall%20and%20Make%20it%20persistent.png)

Saat instalasi iptables-persistent, cukup jawab yes untuk menyimpan rules secara permanen. Langkah ini memastikan semua port layanan yang digunakan oleh cloudstack tidak diblokir oleh firewall dan dapat diakses oleh jaringan
* `-A INPUT` menambahkan aturan ke rantai INPUT (incoming traffic).
* `-s $NETWORK` menentukan sumber paket, misalnya jaringan x/24.
* `-m state --state NEW` menggunakan modul *state* untuk mencocokkan paket yang memulai koneksi baru.
* `-p udp/tcp --dport [PORT]` menerapkan aturan untuk protokol dan port tujuan tertentu.
* `-j ACCEPT` menerima paket yang cocok dengan aturan tersebut.


### Disable apparmour on libvirtd

```
ln -s /etc/apparmor.d/usr.sbin.libvirtd /etc/apparmor.d/disable/
ln -s /etc/apparmor.d/usr.lib.libvirt.virt-aa-helper /etc/apparmor.d/disable/
apparmor_parser -R /etc/apparmor.d/usr.sbin.libvirtd
apparmor_parser -R /etc/apparmor.d/usr.lib.libvirt.virt-aa-helper
```

Penjelasan:
* `ln -s /etc/apparmor.d/usr.sbin.libvirtd /etc/apparmor.d/disable/`
Membuat symlink ke direktori `disable/` untuk menandai bahwa profil AppArmor `libvirtd` dinonaktifkan. Ini mencegah profil aktif kembali saat reboot.
* `ln -s /etc/apparmor.d/usr.lib.libvirt.virt-aa-helper /etc/apparmor.d/disable/`
Melakukan hal yang sama untuk `virt-aa-helper`, tool bantu keamanan libvirt.
* `apparmor_parser -R /etc/apparmor.d/usr.sbin.libvirtd`
Menghapus profil `libvirtd` dari kernel agar langsung tidak aktif tanpa perlu reboot.
* `apparmor_parser -R /etc/apparmor.d/usr.lib.libvirt.virt-aa-helper`
Menghapus profil `virt-aa-helper` dari kernel secara langsung.


### Launch Management Server

```
cloudstack-setup-management
systemctl status cloudstack-management
tail -f /var/log/cloudstack/management/management-server.log #if you want to troubleshoot 
#wait until all services (components) running successfully
```
![Launch Management Server](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/16.%20Launch%20management%20Server.png)

Penjelasan:
* `cloudstack-setup-management`
Digunakan untuk mengatur *management server* CloudStack. Perintah ini mengonfigurasi koneksi ke database, menetapkan IP server, dan memulai layanan manajemen CloudStack.
* `systemctl status cloudstack-management`
Menampilkan status layanan `cloudstack-management`. Berguna untuk memastikan apakah layanan sudah aktif dan berjalan dengan benar.
* `tail -f /var/log/cloudstack/management/management-server.log`
Melihat log terbaru dari server manajemen secara real-time. Sangat membantu untuk troubleshooting jika terjadi masalah selama proses startup atau konfigurasi.


### Open Web Browser

```
http://100.118.141.51:8080
```
![Dashboard](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/17.%20Open%20Cloudstack%20dashboard.png)

### Halaman Utama Apache Cloud Stack

![apache_cloudstack](https://github.com/user-attachments/assets/a5e0c1e7-81ab-45f3-84d1-cbba8e3d49ba)

