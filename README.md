# eksperimen_ws

# Eksperimen Komunikasi Real-Time Menggunakan WebSocket 🚀

| Hasil Eksperimen |
|:---:|
| <img src="hasil eksperimen.png" width="1000"> |


Repository ini memuat *source code* dari simulasi aplikasi *Live Chat* sederhana yang diimplementasikan menggunakan Node.js. Proyek ini dibangun untuk memenuhi tugas Ujian Tengah Semester (UTS) guna membuktikan keunggulan protokol WebSocket atas HTTP tradisional dalam menangani komunikasi dua arah (*full-duplex*) berlatensi rendah.

## ⚙️ Alur Kerja Komunikasi (Data Flow)
Berbeda dengan HTTP yang memutus koneksi setelah *response* dikirim, eksperimen ini membuktikan alur kerja WebSocket:
1. **HTTP Handshake & Upgrade:** Klien mengirimkan request HTTP standar dengan header `Upgrade: websocket`. Server merespons dengan status `101 Switching Protocols`.
2. **Persistent Connection:** Koneksi TCP tetap terbuka secara permanen.
3. **Bi-directional Messaging:** Klien dan Server kini dapat saling bertukar data (pesan teks) kapan saja melalui *frames* yang sangat ringan, tanpa *overhead* header HTTP.

## 📂 Penjelasan Teknis Source Code
Proyek ini mengadopsi arsitektur *Client-Server* murni tanpa *framework* tambahan agar konsep inti protokol terlihat jelas:

### 1. Sisi Server / Backend (`server.js`)
File ini bertugas sebagai otak utama yang mengatur lalu lintas data menggunakan *library* `ws`.
* **Inisialisasi:** Membuka *port* `8080` untuk mendengarkan permintaan koneksi masuk.
* **Event `connection`:** Setiap kali ada *browser* klien yang berhasil terhubung, server mengalokasikan *socket* khusus untuk klien tersebut dan langsung mengirimkan pesan sapaan pertama (membuktikan server bisa memulai pengiriman data tanpa diminta).
* **Event `message`:** Sebuah *listener* asinkron yang akan menangkap pesan (*payload*) dari klien secara *real-time*, menampilkannya di *console* terminal, dan memantulkannya kembali ke klien pada detik yang sama.

### 2. Sisi Klien / Frontend (`index.html`)
File ini berisi antarmuka pengguna berbasis HTML5 dan logika Vanilla JavaScript.
* **API `WebSocket` Bawaan:** Menggunakan objek `new WebSocket('ws://localhost:8080')` standar dari *browser* untuk memicu *handshake* ke server lokal.
* **Fungsi `ws.send()`:** Diikat (*bind*) ke tombol HTML untuk mengambil nilai *string* dari kotak input dan menembakkannya ke server melalui jalur *socket*.
* **Event `ws.onmessage`:** Manipulasi DOM (*Document Object Model*) sederhana. Setiap kali ada data masuk dari server, skrip akan langsung menyuntikkannya sebagai elemen `<li>` baru ke dalam antarmuka obrolan tanpa memerlukan *page reload*.

### 3. File Konfigurasi (`package.json`)
Berisi metadata *project* dan mendaftarkan `ws` sebagai satu-satunya *dependency* eksternal yang dibutuhkan untuk menjalankan server Node.js ini.

## 🚀 Panduan Instalasi & Cara Menjalankan
Pastikan **Node.js** telah terinstal di mesin Anda sebelum memulai.

1. **Clone Repository**
   ```bash
   git clone [https://github.com/USERNAME_GITHUB_KAMU/NAMA_REPOSITORY_KAMU.git](https://github.com/USERNAME_GITHUB_KAMU/NAMA_REPOSITORY_KAMU.git)
   cd NAMA_FOLDER_KAMU
