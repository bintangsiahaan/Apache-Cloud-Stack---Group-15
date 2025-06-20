# Apache-Cloud-Stack---Group-15
![Logo UI](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Installation/Logo.png)

# Kelompok 15
1. Fathin Umara Aero (2206814186)
2. Fabio Rabbani P (2206829490)
3. Drasseta Aliyyu Darmansyah (2206062913)
4. Bintang Siahaan (2206024322)


# Video Tutorial
[![Tonton Video](https://img.youtube.com/vi/rwTnuCj4cGY/hqdefault.jpg)](https://youtu.be/rwTnuCj4cGY)

# Pendahuluan Apache CloudStack

## Definisi
![CloudStack Logo](https://upload.wikimedia.org/wikipedia/commons/7/70/Apache_CloudStack_Logo.svg)

Apache CloudStack adalah sebuah platform open-source berbasis Java yang dirancang untuk membangun dan mengelola layanan cloud computing Infrastructure as a Service (IaaS). Dengan CloudStack, pengguna dapat melakukan provisioning, pengelolaan, dan pengaturan infrastruktur komputasi seperti mesin virtual, jaringan, dan penyimpanan dari satu interface terpusat, baik melalui GUI berbasis web maupun API.

CloudStack memungkinkan penyedia layanan atau organisasi untuk membangun infrastruktur cloud layaknya Amazon Web Services (AWS) atau Google Cloud, namun dikelola secara mandiri di lingkungan lokal (on-premise) atau hybrid cloud.

## Konsep Dasar Cloud Computing

Sebelum memahami lebih dalam tentang CloudStack, penting untuk memahami konsep dasar **cloud computing**, khususnya model **Infrastructure as a Service (IaaS)**:

- **IaaS (Infrastructure as a Service)** adalah layanan komputasi berbasis cloud di mana pengguna dapat menyewa sumber daya infrastruktur seperti CPU, RAM, storage, dan jaringan untuk menjalankan sistem operasi dan aplikasi mereka.
- CloudStack berperan sebagai platform untuk menyediakan layanan IaaS secara otomatis, efisien, dan skalabel.

## Konsep Virtual Machine (VM)

Virtual Machine (VM) adalah environment komputasi virtual yang berjalan di atas sistem fisik (host) dengan bantuan hypervisor. VM berfungsi seperti komputer fisik, lengkap dengan sistem operasi dan aplikasi, namun dijalankan secara virtual menggunakan sumber daya dari host.

- Dalam konteks Apache CloudStack:
1. VM dapat dibuat, dimodifikasi, dan dihapus melalui interface CloudStack.
2. Pengguna dapat memilih sistem operasi, jumlah CPU, RAM, dan disk saat membuat VM.
3. CloudStack akan secara otomatis menempatkan VM di salah satu host fisik yang tersedia.
4. VM dapat digunakan seperti server biasa untuk hosting aplikasi, website, dan database.

## Konsep Internet dalam VM

Agar VM bisa terhubung ke internet, perlu dilakukan konfigurasi jaringan melalui CloudStack.
- VM biasanya berada dalam jaringan virtual (isolated network).
- Administrator atau pengguna bisa mengaktifkan Source NAT, Firewall, dan Port Forwarding untuk mengakses VM dari luar (internet).
- Public IP dapat dialokasikan untuk VM sehingga bisa diakses dari luar jaringan lokal.

## Konsep SSH (Secure Shell)

SSH adalah protokol jaringan yang memungkinkan pengguna melakukan koneksi remote secara aman ke server atau VM melalui command line.

Dalam CloudStack:
- Saat VM dibuat, pengguna bisa mengatur SSH key pair untuk akses aman.
- Setelah VM aktif, pengguna dapat masuk menggunakan perintah ssh, seperti ssh kelompok15@100.118.141.51

## Konsep HTTP

HTTP (Hypertext Transfer Protocol) adalah protokol yang digunakan untuk mentransfer data web di internet.

Dalam konteks penggunaan VM di CloudStack:
- Pengguna dapat menjalankan server web di dalam VM, misalnya Apache.
- Port HTTP (80) atau HTTPS (443) harus dibuka melalui Firewall Rules atau Port Forwarding di CloudStack agar dapat diakses dari internet.
- VM yang menjalankan layanan web dapat diakses dengan mengetikkan public IP dari VM di browser, seperti http://100.118.141.51

## Fitur Utama Apache CloudStack

Beberapa fitur utama dari Apache CloudStack meliputi:

1. **Manajemen Mesin Virtual (VM)**
   - Pengguna dapat membuat, memodifikasi, dan menghapus VM dengan mudah melalui interface web atau API.
   - Mendukung banyak hypervisor seperti KVM, XenServer, VMware, dan Hyper-V.

2. **Manajemen Jaringan**
   - Mendukung jaringan tingkat Layer 2 dan Layer 3.
   - Dapat mengatur firewall, NAT, VLAN, DHCP, dan load balancing secara otomatis.

3. **Manajemen Penyimpanan**
   - Mendukung penyimpanan primer (untuk disk VM) dan sekunder (untuk ISO, template, snapshot).
   - Kompatibel dengan berbagai solusi storage seperti NFS, Ceph, GlusterFS.

4. **Manajemen Multi-Tenant**
   - Mendukung pembagian akses berdasarkan akun, domain, dan proyek.
   - Cocok untuk lingkungan multi-user dan layanan publik.

5. **Skalabilitas dan Otomatisasi**
   - Mampu mengelola ribuan VM dan sumber daya lainnya secara otomatis.
   - Dukungan auto-scaling, high availability (HA), dan elastic IP.

6. **Interface yang Fleksibel**
   - Interface pengguna berbasis web (UI) dan RESTful API.
   - Integrasi dengan sistem otomasi lainnya seperti Ansible, Terraform, dsb.

## Arsitektur Apache CloudStack
![architecture-apachecloudstack](https://github.com/user-attachments/assets/76bbd96e-09d4-455f-937c-a97635e68eb2)

Apache CloudStack memiliki arsitektur modular yang terdiri dari beberapa komponen utama:

- **Management Server**: Komponen pusat yang menangani semua logika dan komunikasi antar komponen. Ia bertugas mengatur provisioning, monitoring, dan orkestrasi layanan.
- **Database Server**: Menyimpan konfigurasi, status sumber daya, dan metadata lainnya.
- **Hypervisor Hosts**: Server fisik yang menjalankan VM menggunakan hypervisor (misal: KVM).
- **Primary Storage**: Penyimpanan utama untuk disk image VM.
- **Secondary Storage**: Menyimpan ISO, template, dan snapshot.
- **CloudStack UI / API**: Interface pengguna dan endpoint API yang digunakan untuk interaksi pengguna.

## Alur Kerja CloudStack

Berikut adalah gambaran umum alur kerja pada CloudStack:

1. Administrator mengonfigurasi infrastruktur (zone, pod, cluster, host, storage).
2. Pengguna memilih template dan konfigurasi VM melalui UI.
3. Management server menerima permintaan dan mengatur provisioning.
4. VM dibuat di hypervisor host sesuai permintaan.
5. Jaringan dan storage dikonfigurasi otomatis.
6. VM siap digunakan pengguna dengan akses yang telah ditentukan.

## Kelebihan Apache CloudStack

- Open-source dan gratis.
- Mendukung berbagai hypervisor dan infrastruktur.
- Cocok untuk skala kecil maupun besar.
- Mudah digunakan dan dikonfigurasi.
- Dukungan komunitas dan dokumentasi lengkap.

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

# Konfigurasi Zone di Apache CloudStack

Berikut adalah langkah-langkah lengkap untuk konfigurasi Zone di CloudStack

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

![Input the zone details](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/3.%20Input%20the%20zone%20details.png)

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

![Add host](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/8.%20Add%20host.png)

---

## 9. Tambah Primary Storage 

Tentukan penyimpanan utama, misalnya NFS path.

![Input primary storage](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Zone/9.%20Input%20primary%20storage%20details.png)

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

![Install Apache2 sebagai Web Server](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/18.%20Install%20Apache2%20sebagai%20Web%20Server.png)

---

## 19. Akses HTTP Apache2

Verifikasi akses ke web server Apache2 dari browser.

![Akses HTTP Apache2](https://github.com/bintangsiahaan/Apache-Cloud-Stack---Group-15/blob/main/Requirement%20Task/19.%20Akses%20HTTP%20Apache2.png)



## Referensi
- AhmadRifqi86/cloudstack-install-and-configure. (n.d.). GitHub. https://github.com/AhmadRifqi86/cloudstack-install-and-configure/
- Installation guide — Apache CloudStack 4.20.0.0 documentation. (n.d.). Welcome to Apache CloudStack’s Documentation — Apache CloudStack 4.20.0.0 documentation. https://docs.cloudstack.apache.org/en/4.20.0.0/installguide/
- HackMD: Your collaborative Markdown workspace for knowledge sharing. (n.d.). HackMD: Your Collaborative Markdown Workspace for Knowledge Sharing. https://hackmd.io/@_ZfqOpYhTCq5xfvPo9Xb8g/rkQSNa0L3
