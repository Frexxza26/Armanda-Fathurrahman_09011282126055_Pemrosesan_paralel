# Aldi Hoirul Fatih_09011282126069_Pemrosesan-pararel
# Tugas MPI

## • Sebelum Pengerjaan
1.	Memastikan bahwa setiap PC/Laptop dalam satu jaringan yang sama 
2.	Menentukan Server dan Slave/worker
3.	Melakukan penginstallan net-tools untuk mengecek IP dan vim untuk teks editor

## •	Konfigurasi IP Server dan Slave didalam file /etc/hosts
1.  Melakukan pengecekan IP dengan perintah berikut:

    $ Ifconfig
    | NAMA    |     Master       |     Slave1        |     Slave2       |     Slave3        |
    |---------|------------------|-------------------|------------------|-------------------|
    | IP      | 192.168.102.170  |  192.168.102.215  |  192.168.102.95  |  192.168.102.236  |

2.	Untuk server, buka file /etc/hosts menggunakan perintah sudo nano /etc/hosts
3.	Di dalam file /etc/hosts tambahkan IP master dan Slave/worker,kemudian save file dan keluar dari file dengan ctrl+x

    ![WhatsApp Image 2023-11-16 at 19 14 04_97ec1e36](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/8f5da45b-0fe7-42c1-b189-3da73e553fce)
  	
4.	Untuk worker/slave, sama seperti master buka file /etc/hosts kemudian masukkan cukup masukkan IP dari master dan worker pemegang file
   
    ![WhatsApp Image 2023-11-16 at 08 58 04_4be95a18](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/4346ae10-b326-45af-8c90-f74fa4fd0db4)

## •	Membuat user baru
1.	Untuk Server dan Worker/slave, Nama user harus sama. Untuk menambahkan User dapat digunakkan perintah sudo adduser(nama user baru)

    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/6c5baace-b9b9-46e2-9f2e-a07c08d588ce)

2.	Kemudian berikan akses root kepada user yang telah dibuat dengan perintah sudo usermod -aG sudo (nama user baru)
3.	Terakhir kita masuk sebagai user baru yang telah dibuat dengan perintah su – (nama user baru)
   
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/97bee918-31fc-45cc-beb9-1dfdfc05fa37)
   
## •	Konfigurasi SSH
1.	Pertama lakukan penginstalan ssh diserver dan slave dengan perintah sudo apt install openssh-server
   
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/84f982fb-b0d6-4c62-951a-17aa112f25f4)
   
    Kemudian lakukan pengecekan ssh dengan perintah ssh (nama user)@(host)
  	
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/16e753f4-f179-4603-88d0-4717c7d14e4c)
  	
2.	Setelahnya lakukan generate keygen diserver dengan perintah ssh-keygen -t rsa
   
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/549844d5-39c9-4f37-a166-ee3e2512431e)
  	
3.	Kemudian lakukan copy key publik ke client dengan perintah cd .ssh
    cat id_rsa.pub | ssh <nama user>@<host> "mkdir .ssh; cat >> .ssh/authorized_keys". Lakukan berkali-kali sesuai dengan jumlah dan host dari setiap slave.
  	
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/c6b0ebf1-26c5-4cf2-b230-ccb91873e71c)

## •	Pengkonfigurasian NFS
1.	Di dalam server dan slave buat sebuah folder dengan nama bebas,gunakan perintah mkdir.Folder setiap pc harus memiliki nama yang sama (nama folder yang ingin dibuat)
   
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/eb7f5af7-2438-4cbb-81b9-61615a0e0589)
  	
2.	Lakukan penginstalan NFS server perintahnnya ialah sudo apt install nfs-kernel-server
   
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/2206fae1-3cad-41ce-b28d-bc9f46fb4d05)
  	
3.	Lakukan konfigurasi file /etc/exports server, dengan perintah sudo vim /etc/exports
    Kemudian masukkan kalimat berikut:
    <lokasi shared folder> *(rw,sync,no_root_squash,no_subtree_check)
    Sesuaikan lokasi shared folder dengan folder yang telah dibuat sebelumnya.
  	
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/92fd4bcd-da0a-41df-ab9a-28c4da8f106f)
  	
    Kemudian masukkan perintah sudo exportfs -a dan sudo systemctl restart nfs-kernel-server
  	
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/8fc520f9-2147-4cb8-9cf5-e0dc1062f0ba)
  	
4.	Kemudian install nfs pada client dengan perintah sudo apt install nfs-common
   
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/5df8cf76-e709-4b60-a62b-d0ecfd4811d4)
  	
5.	Kemudian Mounting dengan perintah sudo mount <server host>:<lokasi shared folder di server> <lokasi shared folder di client> pada slave
   
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/93eb3178-7b98-4dd8-a532-f5d97a906d00)

## •	MPI
   Install MPI dengan perintah sudo apt install openmpi-bin libopenmpi-dev pada server dan slave

   ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/d737a33b-2aa5-4675-bfad-0e75e5543204)

## •	Menjalankan program bubblesort dan numerik
1.	Lakukan penginstallan python dan mpi4py dengan perintah sudo apt install python3-pip dan pip install mpi4py
   
    ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/fa4ee1ce-ba97-40e7-a599-371a0eb68c59)
  	
2.	Pertama buat 2 buah file python yaitu touch bubblesort.py untuk file bubblesort dan touch numeric.py untuk file numeric    
3.	Kemudian masuk kemasing-masing file dengan cara sudo nano bubblesort.py/numeric.py dan didalam file tersebut masukkan program sesuai dengan jenis nama file.
- Program bubblesort

  ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/e8dce825-9e71-424a-8163-710c448cc2eb)
  
- Program numeric

  ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/1b35c1f5-b93b-416c-9204-59cbbb8c4829)
  
4.	Jalankan file menggunakan MPI dengan perintah mpirun -np <jumlah prosesor> -host <daftar host> python3 test.py.
- Hasil program bubblesort

  ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/003a55a8-38c4-488b-bc9e-1f1694ed01bb)
  
- Hasil program numeric

  ![image](https://github.com/aldihf/Aldi-Hoirul-Fatih_09011282126069_Pemrosesan-pararel/assets/151024026/197e02b8-1111-41ac-a73e-0f622b0e49de)
