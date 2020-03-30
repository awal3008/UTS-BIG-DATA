# UTS-BIG-DATA
						UTS PENGENALAN BIG DATA
1.	Cari dan sebutkan 3 DBMS yang bisa digunakan untuk mengelola big data.
- Oracle Big Data SQL
- Microsoft SQL Server
- IBM DB2
- SAP Saybase ASE
- Apache Hadoop

2.	Carilah contoh masalah big data yang bisa dikelola menggunakan salah satu DBMS tersebut, jelaskan mulai dari instalasi sampai CRUD untuk data menggunakan DBMS tersebut. Asumsikan anda akan memecahkan masalah big data yang sudah anda cari contoh tadi, jelaskan kira-kira bagaimana arsitektur dari solusi big data menggunakan DBMS tersebut, gambarkan diagramnya.

### Contoh DBMS Hadoop  Dalam pengobatan Kanker dan Genomic

### Instalasi Hadoop pada windows
Software yang dibutuhkan :
1.	Aplikasi Hadoop
2.	Java JDK
Setalah software diatas di install, selanjutnya mengconfigurasinya.
a.	Configurasi
1.	Edit file C: /Hadoop-2.8.0/etc/hadoop/core-site.xml , rekatkan di bawah paragraf xml dan simpan file ini. 
<configuration>
   <property>
       <name>fs.defaultFS</name>
       <value>hdfs://localhost:9000</value>
   </property>
</configuration>
2.	Ganti nama "mapred-site.xml.template" menjadi "mapred-site.xml" dan edit file ini C: /Hadoop-2.8.0/etc/hadoop/mapred-site.xml , tempel di bawah paragraf xml dan simpan file ini.
<configuration>
   <property>
       <name>mapreduce.framework.name</name>
       <value>yarn</value>
   </property>
</configuration>
3.	Buat 3 Folder
-	Buat folder "data" di bawah "C: \ Hadoop-2.8.0"
-	Buat folder "datanode" di bawah "C: \ Hadoop-2.8.0 \ data"
-	Buat folder "namenode" di bawah "C: \ Hadoop-2.8.0 \ data"

4.	Edit file C: \ Hadoop-2.8.0 / etc / hadoop / hdfs-site.xml , rekatkan di bawah paragraf xml dan simpan file ini.
<configuration>
   <property>
       <name>dfs.replication</name>
       <value>1</value>
   </property>
   <property>
       <name>dfs.namenode.name.dir</name>
       <value>/hadoop-2.8.0/data/namenode</value>
   </property>
   <property>
       <name>dfs.datanode.data.dir</name>
       <value>/hadoop-2.8.0/data/datanode</value>
   </property>
</configuration>

5.	Edit file C: /Hadoop-2.8.0/etc/hadoop/yarn-site.xml , rekatkan di bawah paragraf xml dan simpan file ini.
<configuration>
   <property>
    	<name>yarn.nodemanager.aux-services</name>
    	<value>mapreduce_shuffle</value>
   </property>
   <property>
      	<name>yarn.nodemanager.auxservices.mapreduce.shuffle.class</name>  
	<value>org.apache.hadoop.mapred.ShuffleHandler</value>
   </property>
</configuration>
	
6.	dit file C: /Hadoop-2.8.0/etc/hadoop/hadoop-env.cmd dengan menutup baris perintah “JAVA_HOME =% JAVA_HOME%” alih-alih mengatur “JAVA_HOME = C: \ Java” (Pada C: \ java this path ke file jdk.18.0).
# Konfigurasi Hadoop
1.	File Dowload, Hadoop Configuration.zip
2.	Hapus file bin pada C: \ Hadoop-2.8.0 \ bin, diganti dengan file bin pada file yang baru saja diunduh (dari Hadoop Configuration.zip)
3.	Buka cmd dan ketikkan perintah “hdfs namenode –format” . Maka Hasilnya seperti dibawa ini.
![1](https://user-images.githubusercontent.com/55679463/77932686-78042600-72e0-11ea-9903-a4ab2a8c9e8f.PNG)

# Menjalankan Hadoop
1.	Buka cmd dan ubah direktori menjadi "C: \ Hadoop-2.8.0 \ sbin" dan ketik "start-all.cmd" untuk memulai apache.
 ![2](https://user-images.githubusercontent.com/55679463/77933079-feb90300-72e0-11ea-95a4-1099eeda4932.PNG)

2.	Pastikan aplikasi ini berjalan
-	Hadoop Namenode
-	Dadoode Hadoop
-	Manajer Sumber Daya YARN
-	YARN Node Manager
3.	Buka :http://localhost:8088
 ![3](https://user-images.githubusercontent.com/55679463/77933237-28722a00-72e1-11ea-8204-31017852693d.PNG)

# Contoh CRUD Dalam Hadoop
	Agar mempermudah pengelolaan data maka kita perlu software atau framework MapReduce yang di mana MapReduce merupakan sebuah model pemograman yang didesain untuk dapat melakukan pemrosesan data dengan jumlah yang sangat besar dengan cara membagi pemrosesan tersebut ke beberapa tugas yang indipenden satu sama lain. Selanjutnya MapReduceClient.jar dan Data yang akan digunakan taruh di "C: /".
1.	Buka cmd dalam mode Administratif dan pindah ke "C: /Hadoop-2.8.0/sbin" dan mulai cluster.
Start-all.cmd
 ![4](https://user-images.githubusercontent.com/55679463/77933309-3a53cd00-72e1-11ea-93b8-5c4da01d4fe6.PNG)

2.	Buat direktori input dalam HDFS.
hadoop fs -mkdir /input_dir


3.	Salin file teks input bernama input_file.txt(data yang akan digunakan) di direktori input (input_dir) HDFS.
hadoop fs -put C:/input_file.txt /input_dir
4.	Verifikasi input_file.txt tersedia di direktori input HDFS (input_dir).
hadoop fs -ls /input_dir/
5.	Verifikasi konten dari file yang disalin.
hadoop dfs -cat /input_dir/input_file.txt
![5](https://user-images.githubusercontent.com/55679463/77933387-4f306080-72e1-11ea-8cb1-716ca0b27608.PNG)
 
			Contoh Datanya

6.	Jalankan MapReduceClient.jar dan berikan juga masukan dan direktori keluar.
hadoop jar C:/MapReduceClient.jar wordcount /input_dir /output_dir
![6](https://user-images.githubusercontent.com/55679463/77933454-68d1a800-72e1-11ea-97cb-965b15e7ae45.PNG)

 
7.	Untuk melihat file output yang dihasilkan.
hadoop dfs -cat /output_dir/*

![7](https://user-images.githubusercontent.com/55679463/77933517-7c7d0e80-72e1-11ea-93fc-3ab2b7b6ac4b.PNG)
 
			Hasil Outputnya
# Arsitektur Dari Contoh Kasus A
Pada arsitektur ini terdapat 3 bagian utama yaitu All Data Source,Big Data Ecosystem dan Analytic Applications. Yang dimana pada data source terdapat berbagai macam data mulai dari teks,audio,video dll untuk di exstraksi ke data ecosystem sehingga menjadi data yang akan digunakan untuk menganalisis bagaimana penyebab dan pengaruh DNA dan GEN terhadapat penyakit kanker.

![8](https://user-images.githubusercontent.com/55679463/77933558-89016700-72e1-11ea-9336-736e9e4d3bf6.PNG)


 
