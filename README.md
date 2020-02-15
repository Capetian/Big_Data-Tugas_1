# Big Data - Tugas 1
Dataset yang digunakan adalah Bixi Montreal Bikeshare Data yang tersedia pada link berikut:

    https://www.kaggle.com/jackywang529/bixi-montreal-bikeshare-data
    
Dalam illustrasi ini data yang akan digunakan adalah data pada folder bixi-montreal-bikeshare-data\BixiMontrealRentals2016\BixiMontrealRentals2016. Pada illustrasi ini file-file dengan nama OD_2016_XX.csv akan dibaca sebagai file, sedangkan file Station_2016.csv akan disimpan di database sebagai tabel station. 

![picture](/img/folder.PNG)

![picture](/img/csv-cont.PNG)

![picture](/img/tabel.PNG)


Workflow ini akan melakukan extraksi data dari masing-masing node, kemudian melakukan join untuk membentuk tabel yang menggantikan kode stasiun dengan nama stasiun, yang kemudian akan di insert ke Databse dan disimpan sebagai file .csv.

## Mengektraksi Data dari Beberapa File

Untuk mengekstraksi data dari beberapa file, kita memerlukan sebuah loop untuk mengiterasi pembacaan setiap file yang ada di suatu folder.

![picture](/img/file-loop.PNG)


### Node List File
List file digunakan untuk me-list file yang kita ingin ekstraksi pada suatu folder sesuai filter yang kita inginkan, dalam kasus ini regex yang digunakan adalah OD_2016-[0-9][0-9].csv .

![picture](/img/LF-conf.PNG)


![picture](/img/LF-res.PNG)



### Node Table Row to Variable Loop Start
Node ini akan mengubah row dari tabel yang dihasilkan node sebelumnya menjadi variabel yang dapat diiterasi untuk node-node berikutnya pada loop, dalam kasus ini nama file-file yang akan dibaca. Selain itu, node ini juga digunakan sebagai titik awal sebuah loop.


### Node File Reader
Node ini digunakan untuk mengektraksi data dari file. Untuk membaca file, lokasi file yang ingin dibaca perlu dicantumkan dalam kasus ini variabel URL yang menyimpan lokasi file. Untuk menkonfigurasi variabel sebagai lokasi, klik simbol V disebelah dropdown lokasi.

![picture](/img/FR-conf.PNG)


### Node Loop End
Node ini akan mengumpulkan hasil iterasi dan mengakhiri loop.

![picture](/img/LE-res.PNG)


## Mengektraksi Data dari Tabel di Database MySQL
Untuk mengekstraksi data dari sebuah tabel di sebuah DB MySQL, kita perlu membuat koneksi ke databse yang diinginkan terlebih dahulu dan melakukan SELECT terhadap suatu tabel.

![picture](/img/DB-read.PNG)


### Node MySQL Connector
Node ini melakukan koneksi ke DB. Untuk menjalankan node ini, kita perlu mencantumkan terlebih da pehulu konfigurasi DB yang kita ingin hubungkan.

![picture](/img/SQL-conf.PNG)


### Node Table Selector
Node ini melakukan SELECT ke tabel di DB. Untuk menjalankan node ini, kita perlu mencantumkan terlebih dahulu tabel yang inigin kita query dalam hal ini tabel stasion.

![picture](/img/Sel-conf.PNG)


### Node DB Reader
Node ini digunakan untuk mengektraksi data dari tabel yang di query.

![picture](/img/DR-res.PNG)

## Join Tabel
Untuk melakukan join tabel kita perlu menghubungkan data yang ingin di-join ke node joiner dan mencantumkan kolom yang akan digunkan untuk join.

![picture](/img/joiner.PNG)

Kita juga bisa memfilter kolom yang diinginkan saat men-join.


![picture](/img/joiner-filter.PNG)


![picture](/img/joiner-res.PNG)


## Mengubah nama kolom
Untuk mengubah nama kolom pada suatu tabel kita perlu menghubungkan tabel yang ingin diubah ke node column rename, mencantumkan kolom yang akan diubah dan nama baru yang diiginkan.

![picture](/img/rename.PNG)

![picture](/img/rename-conf.PNG)

## Mengubah posisi kolom
Untuk mengubah posisi kolom pada suatu tabel kita perlu menghubungkan tabel yang ingin diubah ke node column resorter dan mencantumkan kolom yang akan diubah dan posisi baru yang diiginkan.

![picture](/img/resorter.PNG)

![picture](/img/resorter-conf.PNG)


## Membuat CSV
Untuk membuat tabel menjadi csv kita perlu menghubungkan tabel yang diinginkan ke node CSV writer dan mencatumkan lokasi sekaligus nama file yang diinginkan.

![picture](/img/csv_writer.PNG)


![picture](/img/csv_writer-conf.PNG)


![picture](/img/csv_writer-res.PNG)


![picture](/img/csv_writer-res2.PNG)


## Menginsert ke DB
Untuk menginsert tabel ke DB kita perlu menghubungkan tabel yang diinginkan dan koneksi DB ke node DB writer dan mencatumkan schema dan nama tabel yang diinginkan.

![picture](/img/db_writer.PNG)


![picture](/img/db_writer-conf.PNG)


![picture](/img/db_writer-res.PNG)









