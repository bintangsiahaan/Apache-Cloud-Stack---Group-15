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
Apache CloudStack adalah sebuah platform open-source berbasis Java yang dirancang untuk membangun dan mengelola layanan cloud computing Infrastructure as a Service (IaaS). Dengan CloudStack, pengguna dapat melakukan provisioning, pengelolaan, dan pengaturan infrastruktur komputasi seperti mesin virtual, jaringan, dan penyimpanan dari satu antarmuka terpusat, baik melalui GUI berbasis web maupun API.

CloudStack memungkinkan penyedia layanan atau organisasi untuk membangun infrastruktur cloud layaknya Amazon Web Services (AWS) atau Google Cloud, namun dikelola secara mandiri di lingkungan lokal (on-premise) atau hybrid cloud.

## Konsep Dasar Cloud Computing

Sebelum memahami lebih dalam tentang CloudStack, penting untuk memahami konsep dasar **cloud computing**, khususnya model **Infrastructure as a Service (IaaS)**:

- **IaaS (Infrastructure as a Service)** adalah layanan komputasi berbasis cloud di mana pengguna dapat menyewa sumber daya infrastruktur seperti CPU, RAM, storage, dan jaringan untuk menjalankan sistem operasi dan aplikasi mereka.
- CloudStack berperan sebagai platform untuk menyediakan layanan IaaS secara otomatis, efisien, dan skalabel.

## Fitur Utama Apache CloudStack

Beberapa fitur utama dari Apache CloudStack meliputi:

1. **Manajemen Mesin Virtual (VM)**
   - Pengguna dapat membuat, memodifikasi, dan menghapus VM dengan mudah melalui antarmuka web atau API.
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

6. **Antarmuka yang Fleksibel**
   - Antarmuka pengguna berbasis web (UI) dan RESTful API.
   - Integrasi dengan sistem otomasi lainnya seperti Ansible, Terraform, dsb.

## Arsitektur Apache CloudStack
![architecture-apachecloudstack](https://github.com/user-attachments/assets/76bbd96e-09d4-455f-937c-a97635e68eb2)

Apache CloudStack memiliki arsitektur modular yang terdiri dari beberapa komponen utama:

- **Management Server**: Komponen pusat yang menangani semua logika dan komunikasi antar komponen. Ia bertugas mengatur provisioning, monitoring, dan orkestrasi layanan.
- **Database Server**: Menyimpan konfigurasi, status sumber daya, dan metadata lainnya.
- **Hypervisor Hosts**: Server fisik yang menjalankan VM menggunakan hypervisor (misal: KVM).
- **Primary Storage**: Penyimpanan utama untuk disk image VM.
- **Secondary Storage**: Menyimpan ISO, template, dan snapshot.
- **CloudStack UI / API**: Antarmuka pengguna dan endpoint API yang digunakan untuk interaksi pengguna.

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
