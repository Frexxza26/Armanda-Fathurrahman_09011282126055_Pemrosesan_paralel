# Armanda Fathurrahman_09011282126055_Pemrosesan-pararel
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
3.	Tambahkan IP Master dan Slave/worker ke dalam file /etc/hosts, lalu simpan file dan keluar dari file dengan ctrl+x

    ![image](https://web.whatsapp.com/a98deb4f-68b2-4663-b4a8-37f4f85755c9)
  	
4.	Untuk worker/slave, sama seperti master buka file /etc/hosts kemudian masukkan cukup masukkan IP dari master dan worker pemegang file
   
    ![image]()

## •	Membuat user baru
1.	Untuk Server dan Worker/slave, Nama user harus sama. Untuk menambahkan User dapat digunakkan perintah sudo adduser(nama user baru)

    ![image]()

2.	Kemudian berikan akses root kepada user yang telah dibuat dengan perintah sudo usermod -aG sudo (nama user baru)
3.	Terakhir kita masuk sebagai user baru yang telah dibuat dengan perintah su – (nama user baru)
   
    ![image]()
   
## •	Konfigurasi SSH
1.	Pertama lakukan penginstalan ssh diserver dan slave dengan perintah sudo apt install openssh-server
   
    ![image]()
   
    Kemudian lakukan pengecekan ssh dengan perintah ssh (nama user)@(host)
  	
    ![image]()
  	
2.	Setelahnya lakukan generate keygen diserver dengan perintah ssh-keygen -t rsa
   
    ![image]()
  	
3.	Kemudian lakukan copy key publik ke client dengan perintah cd .ssh
    cat id_rsa.pub | ssh <nama user>@<host> "mkdir .ssh; cat >> .ssh/authorized_keys". Lakukan berkali-kali sesuai dengan jumlah dan host dari setiap slave.
  	
    ![image]()

## •	Pengkonfigurasian NFS
1.	Di dalam server dan slave buat sebuah folder dengan nama bebas,gunakan perintah mkdir.Folder setiap pc harus memiliki nama yang sama (nama folder yang ingin dibuat)
   
    ![image]()
  	
2.	Lakukan penginstalan NFS server perintahnnya ialah sudo apt install nfs-kernel-server
   
    ![image]()
  	
3.	Lakukan konfigurasi file /etc/exports server, dengan perintah sudo vim /etc/exports
    Kemudian masukkan kalimat berikut:
    <lokasi shared folder> *(rw,sync,no_root_squash,no_subtree_check)
    Sesuaikan lokasi shared folder dengan folder yang telah dibuat sebelumnya.
  	
    ![image]()
  	
    Kemudian masukkan perintah sudo exportfs -a dan sudo systemctl restart nfs-kernel-server
  	
    ![image]()
  	
4.	Kemudian install nfs pada client dengan perintah sudo apt install nfs-common
   
    ![image]()
  	
5.	Kemudian Mounting dengan perintah sudo mount <server host>:<lokasi shared folder di server> <lokasi shared folder di client> pada slave
   
    ![image](https)

## •	MPI
   Install MPI dengan perintah sudo apt install openmpi-bin libopenmpi-dev pada server dan slave

   ![image]()

## •	Menjalankan program bubblesort dan numerik
1.	Lakukan penginstallan python dan mpi4py dengan perintah sudo apt install python3-pip dan pip install mpi4py
   
    ![image]()
  	
2.	Pertama buat 2 buah file python yaitu touch bubblesort.py untuk file bubblesort dan touch numeric.py untuk file numeric    
3.	Kemudian masuk kemasing-masing file dengan cara sudo nano bubblesort.py/numeric.py dan didalam file tersebut masukkan program sesuai dengan jenis nama file.
- Program bubblesort

  ![image]()
  
- Program numeric

  ![image]()
  
4.	Jalankan file menggunakan MPI dengan perintah mpirun -np <jumlah prosesor> -host <daftar host> python3 test.py.
- Hasil program bubblesort

  ![image]()
  
- Hasil program numeric

  ![image]()