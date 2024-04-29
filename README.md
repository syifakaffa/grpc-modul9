## Tutorial 9
Nama: Syifa Kaffa Billah

NPM: 2206816430

Kelas: C

**1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure 
Call) methods, and in what scenarios would each be most suitable?**


Unary RPC adalah cara komunikasi di mana klien mengirimkan satu permintaan dan menunggu satu jawaban dari server. 
RPC ini cocok untuk kasus di mana klien hanya perlu mengirimkan sedikit data dan menunggu jawaban sederhana. Di sisi lain
ada Server Streaming RPC, yaitu saat klien mengirimkan satu permintaan dan menerima banyak jawaban dari server. Rpc ini
berguna jika server harus mengirimkan banyak data atau melakukan komputasi yang menghasilkan banyak jawaban. 
Terakhir, Bi-directional Streaming RPC yang memungkinkan klien dan server saling berkomunikasi dengan mengirim dan 
menerima banyak pesan. Ini baik digunakan jika klien dan server perlu berinteraksi secara _real-time_ dan saling bertukar 
data secara terus-menerus.

**2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly 
regarding authentication, authorization, and data encryption?** 

Saat membuat layanan gRPC di Rust, ada beberapa hal penting terkait keamanan yang perlu diperhatikan, yaitu:
- Autentikasi: cara untuk memastikan bahwa klien dan server yang sedang menggunakan layanan benar-benar orang tersebut
(Terautentikasi). Untuk autentikasi ini, kita bisa menggunakan _Transport Layer Security_ (TLS) yang membuat  
komunikasi antara klien dan server terenkripsi. Selain itu, penggunaan sertifikan untuk autentikasi timbal balik (mTLS),
juga bisa dilakukan yang mana kedua hal tersebut akan saling memverifikasi. Untuk user, bisa menggunakan protokol
autentikasi seperti JWT.
- Otoriasi: memberi izin kepada klien untuk mengakses sumber daya tertentu. Ini bisa dilakukan dengan menetapkan peran 
atau atribut kepada klien dan menegakkan kebijakan otorisasi.
- Data encryption: Digunakan untuk melindungi data yang dikirim dan disimpan. TLS bisa digunakan untuk mengenkripsi 
data dan mengamankan data di rest.
- Memastikan kode Rust kita tulis aman dan melakukan konfigurasi server dan klien dengan benar.

**3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, 
especially in scenarios like chat applications?** 

Tantangan yang mungkin dihadapi pada saat menangani bi-direction streaming dalam Rust gRPC, khususnya dalam skenario 
aplikasi chat, yaitu mengenai konkurensi dimana kita harus menyelaraskan pesan antara klien dan server. Selain itu, 
hak yang cukup chalenging pada saat error handling dan mengatur aliran data agar tetap terkontrol dengan baik. Lalu
masalah lain seperti pengaturan koneksi yang efisien dan menjaga performa juga perlu diperhatikan. Solusi pada saat
kita menghadapi hal-hal tersebut adalah dengan menggunakan kemampuan Rust dalam pemrograman asinkron, 
menerapkan error handling yang baik, dan melakukan pengujian secara menyeluruh untuk memastikan aplikasi berjalan dengan baik.

**4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming 
responses in Rust gRPC services?**

Menggunakan tokio_stream::wrappers::ReceiverStream untuk response streaming dalam gRPC Rust memberikan keuntungan 
berupa integrasi yang lancar dengan runtime asinkron Tokio. Adanya tokio stream tersebut akan memberikan fleksibilitas
terhadap berbagai jenis aliran data dan streaming asinkron, menjaga layanan Rust gRPC tetap responsif tanpa menghambat 
kinerjanya. Namun, penggunaan ReceiverStream akan membuat adanya dependency pada Tokio, yang mungkin tidak cocok untuk 
proyek yang menggunakan runtime asinkron lain. Selain itu, fitur dan opsi kustomisasi ReceiverStream mungkin tidak 
sekomprehensif pustaka streaming lainnya, dan untuk orang yang baru mempelajari Rust atau Tokio mungkin perlu waktu 
lebih untuk memahami cara kerjanya.

**5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability 
and extensibility over time?**

Kita dapat menggunakan pendekatan seperti memecah logika bisnis ke dalam modul terpisah, membuat fungsi dan struktur 
yang dapat digunakan kembali, dan menerapkan pola desain seperti Dependency Injection. Hal ini akan memudahkan pengelolaan 
dan pemeliharaan kode, serta memungkinkan penambahan fitur baru secara lebih mudah di kemudian hari.

**6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment 
processing logic?**

Untuk mengatasi logika pembayaran yang lebih kompleks di MyPaymentService, kita perlu melakukan beberapa langkah 
tambahan. Pertama, kita harus memastikan bahwa data yang dimasukkan benar-benar valid dan melakukan error handling dengan 
baik. Setelah itu, kita perlu mengintegrasikan layanan dengan penyedia pembayaran luar atau financial institutions. 
Penting juga untuk menyimpan riwayat transaksi dengan baik dan melakukan pemrosesan secara paralel untuk meningkatkan 
kinerja. Kita juga harus memastikan bahwa sistem aman dan memenuhi standar keamanan yang diperlukan. Terakhir, 
jangan lupa untuk memantau system health secara berkala dan menguji sistem dengan baik untuk memastikan  scalability
dan high availability.

**7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of 
distributed systems, particularly in terms of interoperability with other technologies and platforms?**

Penggunaan gRPC sebagai protokol komunikasi dapat memengaruhi cara kita merancang sistem terdistribusi. 
gRPC menggunakan HTTP/2 sebagai lapisan transport. Hal tersebut membuat komunikasi antar layanan lebih cepat dan efisien. 
Namun, ada tantangan dalam berinteraksi dengan teknologi dan platform lain. Jika platform tersebut tidak secara langsung 
mendukung gRPC, kita perlu mencari cara untuk menghubungkannya, misalnya dengan menggunakan bridge protocol atau 
middleware seperti gRPC-Gateway atau protobuf.

**8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 
or HTTP/1.1 with WebSocket for REST APIs?**

* HTTP/2:
  - Fitur Multiplexing: Memungkinkan pengiriman data secara paralel, mengurangi waktu tunggu.
  - Kompresi Header: Mengurangi ukuran data yang dikirimkan, meningkatkan efisiensi.
  - Tapi, memerlukan dukungan server dan klien yang sesuai.


* HTTP/1.1 dengan WebSocket:
  - Overhead lebih rendah.
  - Lebih mudah diadopsi tanpa perubahan besar pada infrastruktur.
  - Namun, kurang efisien dalam mengelola koneksi dan multiplexing

**9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in 
terms of real-time communication and responsiveness?**

Model request-response pada REST API berbeda dengan kemampuan bidirectional streaming gRPC dalam hal komunikasi 
real-time dan responsivitas. Pada REST API, klien mengirimkan permintaan ke server dan menunggu tanggapan, yang membuatnya 
lebih cocok untuk skenario di mana tanggapan diperlukan segera. Di sisi lain, gRPC memungkinkan komunikasi dua arah yang 
terus menerus antara klien dan server, hal ini memungkinkan pertukaran data secara real-time tanpa memerlukan request 
ulang. Hal tersebut membuatnya lebih cocok untuk aplikasi yang memerlukan responsivitas tinggi dan pembaruan data secara 
aktif, seperti game application atau aliran data real-time.

**10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more 
flexible, schema-less nature of JSON in REST API payloads?**

Pendekatan gRPC dengan Protocol Buffers menggunakan schema-based yang sudah ditentukan, seperti aturan main yang pasti 
saat mengirim data. Ini membantu memastikan data yang dikirim sesuai dengan format yang diharapkan dan efisien dalam 
penggunaan ruang data. Di sisi lain, REST API dengan JSON yang tanpa skema lebih fleksibel, seperti mampu menyesuaikan 
struktur data tanpa aturan ketat. Meskipun begitu, JSON ini bisa kurang efisien dalam penggunaan ruang data dan 
memerlukan lebih banyak validasi manual.