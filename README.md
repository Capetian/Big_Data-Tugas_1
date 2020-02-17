Kelas: Big Data

Nama: Raden Bimo Rizki Prayogo

NRP: 0511740000139

# Big Data - Tugas 1
## Business Understanding
Dataset yang digunakan adalah Bixi Montreal Bikeshare Data yang tersedia pada link berikut:

    https://www.kaggle.com/jackywang529/bixi-montreal-bikeshare-data
 
Dataset mengandung data tentang peminjaman sepeda pada pos-pos peminjaman sepeda yang disediakan oleh Bixi Montreal dari tahun 2016 sampai tahun 2019. Karena ukuran dataset yang besar, data yang akan digunakan pada ilustrasi ini hanya data pada tahun 2016.
Workflow ini akan melakukan extraksi data dari masing-masing node, kemudian melakukan join untuk membentuk tabel yang menggantikan kode stasiun dengan nama stasiun, yang kemudian akan di insert ke Database dan disimpan sebagai file .csv.

## Data Understanding

![picture](/img/folder.PNG)

![picture](/img/csv-cont.PNG)

![picture](/img/table.PNG)

File-file dengan nama OD_2016_XX.csv berisi data tentang detil peminjaman sepeda. Masing-masing file terdiri dari lebih dari 100 000 dan 6 kolom. Kolom tersebut antara lain:

* start_date: Waktu dan tanggal peminjaman dimulai ( AAAA-MM-JJ hh:mm )
* start_station_code: ID pos peminjaman awal
* end_date: Waktu dan tanggal peminjaman berakhir ( AAAA-MM-JJ hh:mm )
* end_station_code : ID pos peminjaman akhir
* is_member : tipe user. (1 : Suscriber, 0 : Non-suscriber)
* duration_sec: total waktu peminjaman dalam detik

File Station_2016.csv berisi detil tentang pos peminjaman yang tersedia. File terdiri dari 465 baris dan 4 kolom. Kolom tersebut antara lain:

* code : ID pos peminjaman 
* name : nama pos peminjaman 
* longitude : longitude pos peminjaman
* latitude : latitude  pos peminjaman

## Data Preparation
Pada illustrasi ini file-file dengan nama OD_2016_XX.csv akan dibaca sebagai file, sedangkan file Station_2016.csv akan disimpan di database sebagai tabel station. 

![picture](/img/csv-cont.PNG)

![picture](/img/table.PNG)

## Modelling
### Mengektraksi Data dari Beberapa File

Untuk mengekstraksi data dari beberapa file, kita memerlukan sebuah loop untuk mengiterasi pembacaan setiap file yang ada di suatu folder.

![picture](/img/file-loop.PNG)


#### Node List File
List file digunakan untuk me-list file yang kita ingin ekstraksi pada suatu folder sesuai filter yang kita inginkan, dalam kasus ini regex yang digunakan adalah OD_2016-[0-9][0-9].csv .

![picture](/img/LF-conf.PNG)


![picture](/img/LF-res.PNG)



#### Node Table Row to Variable Loop Start
Node ini akan mengubah row dari tabel yang dihasilkan node sebelumnya menjadi variabel yang dapat diiterasi untuk node-node berikutnya pada loop, dalam kasus ini nama file-file yang akan dibaca. Selain itu, node ini juga digunakan sebagai titik awal sebuah loop.


#### Node File Reader
Node ini digunakan untuk mengektraksi data dari file. Untuk membaca file, lokasi file yang ingin dibaca perlu dicantumkan dalam kasus ini variabel URL yang menyimpan lokasi file. Untuk menkonfigurasi variabel sebagai lokasi, klik simbol V disebelah dropdown lokasi.

![picture](/img/FR-conf.PNG)


### Node Loop End
Node ini akan mengumpulkan hasil iterasi dan mengakhiri loop.

![picture](/img/LE-res.PNG)


### Mengektraksi Data dari Tabel di Database MySQL
Untuk mengekstraksi data dari sebuah tabel di sebuah DB MySQL, kita perlu membuat koneksi ke databse yang diinginkan terlebih dahulu dan melakukan SELECT terhadap suatu tabel.

![picture](/img/DB-read.PNG)


#### Node MySQL Connector
Node ini melakukan koneksi ke DB. Untuk menjalankan node ini, kita perlu mencantumkan terlebih da pehulu konfigurasi DB yang kita ingin hubungkan.

![picture](/img/SQL-conf.PNG)


#### Node Table Selector
Node ini melakukan SELECT ke tabel di DB. Untuk menjalankan node ini, kita perlu mencantumkan terlebih dahulu tabel yang inigin kita query dalam hal ini tabel stasion.

![picture](/img/Sel-conf.PNG)


#### Node DB Reader
Node ini digunakan untuk mengektraksi data dari tabel yang di query.

![picture](/img/DR-res.PNG)

### Join Tabel
![picture](/img/joiner.PNG)

Untuk melakukan join tabel kita perlu menghubungkan data yang ingin di-join ke node joiner dan mencantumkan kolom yang akan digunkan untuk join.

![picture](/img/joiner-conf.PNG)


![picture](/img/joiner-filter.PNG)


Kita juga bisa memfilter kolom yang diinginkan saat men-join. Dalam kasus ini, kolom code dan start_station_code yang digunakan untuk menjoin tabel dihapus. Selain itu, latitude dan longitude pada tabel station dihapus

![picture](/img/joiner-res.PNG)


### Mengubah nama kolom

![picture](/img/rename.PNG)

Untuk mengubah nama kolom pada suatu tabel kita perlu menghubungkan tabel yang ingin diubah ke node column rename, mencantumkan kolom yang akan diubah dan nama baru yang diiginkan.


![picture](/img/rename-conf.PNG)

### Mengubah posisi kolom

![picture](/img/resorter.PNG)

Untuk mengubah posisi kolom pada suatu tabel kita perlu menghubungkan tabel yang ingin diubah ke node column resorter dan mencantumkan kolom yang akan diubah dan posisi baru yang diiginkan.

![picture](/img/resorter-conf.PNG)


## Evaluasi
Apend berhasil, tabel tergabung menjadi tabel dengan total baris 4000080.

![picture](/img/combine.PNG)


Join berhasil, berdasarkan proses filter yang digunakan terbentuk tabel dengan 6 kolom, dengan kode pos peminjaman diubah menjadi nama pos peminjaman.

![picture](/img/join.PNG)

## Deployment 

### Membuat CSV

![picture](/img/csv_writer.PNG)

Untuk membuat tabel menjadi csv kita perlu menghubungkan tabel yang diinginkan ke node CSV writer dan mencatumkan lokasi sekaligus nama file yang diinginkan.

![picture](/img/csv_writer-conf.PNG)


![picture](/img/csv_writer-res.PNG)


![picture](/img/csv_writer-res2.PNG)


### Menginsert ke DB

![picture](/img/db_writer.PNG)

Untuk menginsert tabel ke DB kita perlu menghubungkan tabel yang diinginkan dan koneksi DB ke node DB writer dan mencatumkan schema dan nama tabel yang diinginkan.

![picture](/img/db_writer-conf.PNG)


![picture](/img/db_writer-res.PNG)









