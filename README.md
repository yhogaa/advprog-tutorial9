# Pemrograman Lanjut A
> Fadrian Yhoga Pratama - 2206819395

## Module 9 - High Level Networking

### Reflection
**1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?**</br>
>- Unary RPC: Pemanggilan unary RPC terdiri dari satu permintaan dan satu respons antara client dan server. Cocok digunakan ketika client hanya perlu mengirimkan data ke server dan menerima respons tunggal.
>- Server Streaming RPC: Pemanggilan server streaming RPC terdiri dari satu permintaan yang menghasilkan serangkaian respons dari server ke client. Cocok digunakan ketika client membutuhkan respons yang panjang atau berkelanjutan dari server.
>- Bi-directional Streaming RPC: Pemanggilan bi-directional streaming RPC terdiri dari serangkaian permintaan dan respons yang saling terkait antara client dan server. Cocok digunakan ketika client dan server perlu berkomunikasi secara interaktif dan asinkron.

**2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?** </br>
> Dalam mengimplementasikan layanan gRPC di Rust, terdapat beberapa pertimbangan keamanan yang perlu diperhatikan, terutama terkait authentication, authorization, dan data encryption. Beberapa hal yang perlu diperhatikan adalah:
> - Authentication: Pastikan menggunakan metode autentikasi yang kuat, seperti OAuth atau token JWT, untuk memverifikasi identitas pengguna.
> - Authorization: Tentukan peran dan hak akses pengguna dengan jelas untuk mengatur akses ke layanan gRPC berdasarkan otorisasi yang tepat.
> - Enkripsi data: Gunakan TLS (Transport Layer Security) untuk mengenkripsi data yang dikirimkan antara klien dan server, sehingga mencegah peretas dari mengakses data yang sensitif.

**3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?**</br>
>Dalam menghandle streaming bidireksional di gRPC Rust, terdapat beberapa tantangan yang mungkin muncul, terutama dalam aplikasi seperti chat. Beberapa masalah yang bisa terjadi adalah:
> - Sinkronisasi: Mengatur pesan yang masuk dan keluar agar sesuai urutan dan tidak tumpang tindih bisa menjadi rumit, terutama dalam chat yang cepat.
> - Koneksi terputus: Mengelola koneksi yang terputus secara elegan dan memastikan pengiriman pesan yang belum terkirim kembali setelah koneksi pulih.
> - Beban server: Dalam skenario chat yang besar, server harus mampu menangani banyak koneksi secara bersamaan tanpa terlalu membebani performa.

**4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?**</br>
> Kelebihan menggunakan `tokio_stream::wrappers::ReceiverStream` untuk streaming respons dalam layanan Rust gRPC adalah:
>- **Kemudahan Penggunaan**: Mudah digunakan karena memanfaatkan konversi dari `Receiver` ke `Stream`.
>- **Integrasi dengan Tokio**: Dapat diintegrasikan dengan baik dengan Tokio, yang merupakan salah satu platform I/O asinkron di Rust.

> Namun, terdapat juga beberapa kelemahan:
> - **Keterbatasan Fungsionalitas**: Terbatas dalam fungsionalitas dan fleksibilitasnya dibandingkan dengan implementasi kustom menggunakan trait `Stream`.
> - **Ketergantungan pada Tokio**: Memerlukan dependensi pada Tokio, sehingga tidak cocok untuk proyek yang tidak menggunakan Tokio atau ingin menghindari ketergantungan pada library tertentu.

**5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?**</br>
> Untuk meningkatkan kegunaan kembali kode, modularitas, serta kemampuan pemeliharaan dan perluasan kode dari waktu ke waktu dalam Rust gRPC, beberapa pendekatan yang dapat dilakukan antara lain:
> - Menggunakan trait untuk mendefinisikan perilaku bersama, memungkinkan implementasi yang berbeda-beda namun tetap mengikuti aturan tertentu.
> -  Memisahkan logika bisnis dari kode infrastruktur, seperti autentikasi atau penanganan error, untuk mempermudah pengujian dan pemeliharaan.
> - Menggunakan generik untuk membuat kode lebih fleksibel dan dapat digunakan kembali untuk berbagai jenis data.
> - Mengorganisir kode ke dalam modul-modul yang terpisah berdasarkan fungsionalitas atau domain tertentu.
> - Menyediakan dokumentasi yang baik untuk memudahkan penggunaan kembali dan pemahaman kode oleh developer lain.

**6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?**</br>
> Langkah-langkah tambahan yang mungkin diperlukan antara lain:
> - Memerlukan validasi tambahan, seperti pengecekan saldo, verifikasi identitas, atau persetujuan tambahan.
> - Memantau kinerja sistem untuk memastikan bahwa proses pembayaran berjalan dengan cepat dan efisien.
> - Melakukan logging dan monitoring secara lebih intensif untuk melacak dan menganalisis setiap langkah proses pembayaran.
> - Mengelola transaksi secara lebih terperinci, seperti menangani transaksi yang gagal atau terjadi kesalahan.

**7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?**</br>
> Adopsi gRPC sebagai protokol komunikasi memiliki dampak besar pada arsitektur dan desain sistem terdistribusi, terutama dalam hal interoperabilitas dengan teknologi dan platform lain. Beberapa dampaknya antara lain:
> - **Performa yang Lebih Baik**: gRPC menggunakan HTTP/2 untuk komunikasi, yang dapat meningkatkan performa dan efisiensi penggunaan sumber daya.
> - **Desain Berbasis Kontrak**: gRPC menggunakan Protocol Buffers untuk mendefinisikan kontrak antara layanan, memungkinkan pembangun sistem untuk dengan jelas menentukan struktur pesan dan layanan yang digunakan.
> - **Lintas Bahasa dan Platform**: gRPC mendukung banyak bahasa pemrograman dan platform, sehingga memungkinkan komunikasi antara berbagai sistem yang menggunakan teknologi yang berbeda.
> - **Kode yang Dihasilkan Otomatis**: gRPC dapat menghasilkan kode untuk klien dan server secara otomatis berdasarkan definisi protokol, mempercepat pengembangan aplikasi.
> - **Mendukung Streaming**: gRPC mendukung streaming data baik dari sisi klien maupun server, memungkinkan pengembangan aplikasi real-time yang responsif.
> - **Keamanan Terintegrasi**: gRPC memiliki dukungan bawaan untuk TLS (Transport Layer Security), memberikan lapisan keamanan tambahan untuk komunikasi antar layanan.

**8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?**</br>
> Kelebihan HTTP/2, protokol dasar untuk gRPC, dibandingkan dengan HTTP/1.1 atau HTTP/1.1 dengan WebSocket untuk REST API antara lain:
> - Multiplexing: Memungkinkan banyak permintaan dan respons untuk dikirim secara bersamaan melalui satu koneksi, mengurangi latensi.
> - Header Compression: Menggunakan HPACK untuk mengompresi header, mengurangi overhead.
> - Server Push: Memungkinkan server untuk mengirimkan data ke klien tanpa diminta, meningkatkan performa.

> Kekurangannya, antara lain:
> - Kompleksitas: HTTP/2 lebih kompleks dalam implementasinya dibandingkan dengan HTTP/1.1.
> - Kompatibilitas Mundur: Diperlukan dukungan khusus untuk mengimplementasikan HTTP/2, sementara HTTP/1.1 lebih didukung secara luas.

**9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?**</br>
> Model permintaan-respons pada REST API berbeda dengan kemampuan streaming bidireksional dari gRPC dalam komunikasi real-time dan responsif sebagai berikut:
>- **REST API**:
>   - **Model Permintaan-Respons**: Menggunakan model ini, klien membuat permintaan HTTP ke server dan server merespons dengan data.
>   - **Komunikasi Real-time**: Kurang responsif untuk komunikasi real-time karena klien harus secara aktif melakukan permintaan untuk mendapatkan data terbaru.  
> - **gRPC**:
>   - **Streaming Bidireksional**: Memungkinkan klien dan server untuk saling mengirimkan data secara simultan melalui koneksi yang sudah ada, memungkinkan komunikasi real-time.
>   - **Komunikasi Real-time**: Lebih responsif karena tidak perlu adanya polling atau permintaan ulang untuk mendapatkan data terbaru, sehingga cocok untuk aplikasi yang memerlukan komunikasi real-time.

**10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?**</br>
> Pendekatan berbasis skema yang digunakan oleh gRPC dengan Protocol Buffers memiliki implikasi berbeda dibandingkan dengan pendekatan yang lebih fleksibel dan tanpa skema dari JSON dalam muatan REST API:
> -  **gRPC dengan Protocol Buffers**:
>       - **Keuntungan**: Skema yang didefinisikan dengan jelas memungkinkan validasi data yang ketat dan generasi kode otomatis, meningkatkan keamanan dan kestabilan.
>       - **Kerugian**: Kurangnya fleksibilitas dalam mengubah skema data tanpa mempengaruhi klien yang sudah ada, dan memerlukan waktu dan usaha lebih dalam mengelola skema.
> - **REST API dengan JSON**:
>   - **Keuntungan**: Fleksibel dalam mengubah struktur data tanpa perlu memperbarui skema, memungkinkan evolusi yang lebih mudah dari API.
>   - **Kerugian**: Kurangnya validasi skema yang ketat bisa menyebabkan kesalahan parsing dan keamanan yang lebih rendah jika tidak dikelola dengan baik.
