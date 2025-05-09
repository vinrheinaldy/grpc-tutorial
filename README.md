<details> <summary>1. Perbedaan Unary, Server Streaming, dan Bidirectional Streaming</summary>
Unary RPC melibatkan satu permintaan klien dan satu respons server, seperti API REST tradisional. Server streaming memungkinkan server mengirim beberapa respons setelah menerima satu permintaan klien, cocok untuk mengambil data besar secara bertahap. Bi-directional streaming memungkinkan klien dan server mengirim beberapa pesan secara bersamaan, ideal untuk aplikasi chat atau pembaruan real-time seperti terlihat pada implementasi ChatService

</details> <details> <summary>2. Pertimbangan Keamanan di Rust gRPC (Autentikasi, Otorisasi, Enkripsi)</summary>
Autentikasi dengan token JWT atau OAuth2; Otorisasi berbasis peran; Enkripsi data dengan TLS/SSL

</details> <details> <summary>3. Tantangan Bidirectional Streaming di Rust gRPC (mis. Chat App)</summary>
Pengelolaan status koneksi jika klien terputus; Penanganan error pada kedua sisi; Manajemen memori untuk koneksi yang berjalan lama
  
</details> <details> <summary>4. Kelebihan dan Kekurangan ReceiverStream di Rust gRPC</summary>
Kelebihan:
-Integrasi sempurna dengan ekosistem Tokio
-Dukungan backpressure bawaan
-Pengelolaan konkurensi yang baik

Kekurangan:
-Kompleksitas tambahan dibanding metode sinkron
-Potensi kebocoran memori jika pengirim/penerima tidak ditutup dengan benar
-Memerlukan pemahaman tentang model konkurensi async/await

</details> <details> <summary>5. Struktur Kode Modular & Reusable di Rust gRPC</summary>
Pisahkan setiap layanan (misalnya PaymentService, TransactionService) dalam modul sendiri, gunakan traits dan generic untuk logic yang bisa diabstraksi, dan gunakan builder pattern atau factory untuk inisialisasi service. Pastikan handler logic tidak langsung berada di dalam implementasi trait agar mudah dites dan digunakan ulang.
  
</details> <details> <summary>6. Pengembangan MyPaymentService untuk Kasus Nyata</summary>
Validasi pembayaran (jumlah, mata uang), Integrasi dengan gateway pembayaran, Penanganan transaksi dan rollback
  
</details> <details> <summary>7. Dampak gRPC terhadap Arsitektur Sistem Terdistribusi</summary>
Standardisasi komunikasi antar layanan, Peningkatan performa karena menggunakan HTTP/2
  
</details> <details> <summary>8. HTTP/2 vs HTTP/1.1 dan WebSocket dalam Konteks REST API</summary>
Kelebihan:

-Multiplexing (banyak request dalam satu koneksi)
-Prioritisasi permintaan
-Protokol binary yang lebih efisien

Kekurangan:

-Kompleksitas implementasi
-Debugging lebih sulit karena format binary
-Support yang lebih terbatas di beberapa lingkungan

</details> <details> <summary>9. REST Request-Response vs gRPC Streaming dalam Komunikasi Real-Time</summary>
REST menggunakan model request-response yang memerlukan polling atau WebSockets tambahan untuk komunikasi real-time. gRPC dengan bidirectional streaming memungkinkan komunikasi dua arah tanpa overhead koneksi berulang, sangat cocok untuk aplikasi chat atau monitoring real-time seperti terlihat pada implementasi ChatService
  
</details> <details> <summary>10. Protobuf vs JSON: Konsekuensi Pendekatan Skema</summary>
gRPC menggunakan Protocol Buffers yang lebih cepat dan efisien dari sisi ukuran dan parsing, namun butuh kompilasi dan skema eksplisit. Sebaliknya, JSON bersifat fleksibel dan mudah dibaca manusia, tapi rentan kesalahan akibat ketidakkonsistenan struktur, serta lebih lambat karena parsing teks dan payload yang besar.

</details>
