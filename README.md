# Apache-Cloud-Stack---Group-15
![Logo UI](https://github.com/user-attachments/assets/6b900171-e796-4035-920c-06590350d884)

# Kelompok 15
1. Fathin Umara Aero (2206814186)
2. Fabio Rabbani P (2206829490)
3. Drasseta Aliyyu Darmansyah (2206062913)
4. Bintang Siahaan (2206024322)

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
