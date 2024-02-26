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

    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/d9748d19-71d4-4193-ad09-d0350b419bfe)
  	
4.	Untuk worker/slave, sama seperti master buka file /etc/hosts kemudian masukkan cukup masukkan IP dari master dan worker pemegang file

   ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/758c435f-236d-466f-a5ab-63e902cda52d)
    
## •	Membuat user baru
1.	Untuk Server dan Worker/slave, Nama user harus sama. Untuk menambahkan User dapat digunakkan perintah sudo adduser(nama user baru)

    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/fd5d73be-3206-4459-ac74-54b9861a56a5)

2.	Kemudian berikan akses root kepada user yang telah dibuat dengan perintah sudo usermod -aG sudo (nama user baru)
3.	Terakhir kita masuk sebagai user baru yang telah dibuat dengan perintah su – (nama user baru)
   
    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/330e6491-6b23-4e53-89c5-1779949cac2c)
   
## •	Konfigurasi SSH
1.	Pertama lakukan penginstalan ssh diserver dan slave dengan perintah sudo apt install openssh-server
   
    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/9e3cb637-9e24-4ce6-a3f6-712ef806eaf9)
   
    Kemudian lakukan pengecekan ssh dengan perintah ssh (nama user)@(host)
  	
    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/47d3fb17-8a2a-45db-b7ad-ae05303c1465)
  	
2.	Setelahnya lakukan generate keygen diserver dengan perintah ssh-keygen -t rsa
   
    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/2e85483b-3bd8-4486-9b6c-3773f99087cd)
  	
3.	Kemudian lakukan copy key publik ke client dengan perintah cd .ssh
    cat id_rsa.pub | ssh <nama user>@<host> "mkdir .ssh; cat >> .ssh/authorized_keys". Lakukan berkali-kali sesuai dengan jumlah dan host dari setiap slave.
  	
    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/a88ca6f6-88be-41e4-9448-9d0cd11b0b64)

## •	Pengkonfigurasian NFS
1.	Di dalam server dan slave buat sebuah folder dengan nama bebas,gunakan perintah mkdir.Folder setiap pc harus memiliki nama yang sama (nama folder yang ingin dibuat)

    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/7ba28050-d6d0-42f0-83e9-d040d3938911)
  	
2.	Lakukan penginstalan NFS server perintahnnya ialah sudo apt install nfs-kernel-server
   
    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/ba220687-a959-4981-8e39-2b40937cca98)

3.	Lakukan konfigurasi file /etc/exports server, dengan perintah sudo vim /etc/exports
    Kemudian masukkan kalimat berikut:
    <lokasi shared folder> *(rw,sync,no_root_squash,no_subtree_check)
    Sesuaikan lokasi shared folder dengan folder yang telah dibuat sebelumnya.
  	
    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/d69b9413-0e31-4d35-8e66-3798aae81e54)

    Kemudian masukkan perintah sudo exportfs -a dan sudo systemctl restart nfs-kernel-server
  	
    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/dd647816-941a-46c6-b6be-f31e43dfda99)

4.	Kemudian install nfs pada client dengan perintah sudo apt install nfs-common
   
    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/c9d45f4c-7087-40aa-9e87-5da00e9b3c3f)

5.	Kemudian Mounting dengan perintah sudo mount <server host>:<lokasi shared folder di server> <lokasi shared folder di client> pada slave
   
    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/fb7faa26-99b4-4f54-bb1d-a26a808348a8)

## •	MPI
   Install MPI dengan perintah sudo apt install openmpi-bin libopenmpi-dev pada server dan slave

   ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/ff0dd1aa-2845-44db-aa65-b938a9ae4186)

## •	Menjalankan program bubblesort dan numerik
1.	Lakukan penginstallan python dan mpi4py dengan perintah sudo apt install python3-pip dan pip install mpi4py
   
    ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/1487afe5-1b2f-41ee-a669-30175dec0a9c)

2.	Pertama buat 2 buah file python yaitu touch bubblesort.py untuk file bubblesort dan touch numeric.py untuk file numeric    
3.	Kemudian masuk kemasing-masing file dengan cara sudo nano bubblesort.py/numeric.py dan didalam file tersebut masukkan program sesuai dengan jenis nama file.
- Program bubblesort

   ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/4d62e567-4c50-481e-93a6-e2e06ecee9cf)

- Program numeric

   ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/61b7da07-9e0a-432b-bf5c-b8e547bd4701)

4.	Jalankan file menggunakan MPI dengan perintah mpirun -np <jumlah prosesor> -host <daftar host> python3 test.py.
- Hasil program bubblesort

   ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/8572558f-9714-4982-a303-f90f2218f196)

- Hasil program numeric

  ![image](https://github.com/Frexxza26/Armanda-Fathurrahman_09011282126055_Pemrosesan_paralel/assets/141960679/ac17f25c-2762-4e2a-b455-76bcd5685070)
