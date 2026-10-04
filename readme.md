# Laporan Praktikum PSW I - Minggu 4 Sesi 3
Topik: Unit, Tipografi, dan Sistem Gaya Dasar  
NIM : 41426012
Nama: Agung Panjaitan  
**Prodi:** D4 Teknologi Rekayasa Perangkat Lunak  

---

## 1. Catatan Pengamatan Langkah Kerja

### Modul 3: Reset Ukuran Kotak
* **Tindakan:** Menerapkan global reset `*, *::before, *::after { box-sizing: border-box; }` serta mengatur wadah utama `main { width: 90%; max-width: 60rem; margin-inline: auto; }`.
* **Perbedaan `width` dan `max-width`:**
  - `width: 90%` membuat lebar wadah relatif fleksibel mengikuti 90% ukuran *viewport* pada layar kecil/layar HP.
  - `max-width: 60rem` (setara 960px pada `1rem = 16px`) membatasi lebar wadah agar tidak melebar tanpa batas saat dibuka di monitor beresolusi besar.
* **Hasil Nyata:** Form tidak pernah melebihi batas wadah `main` dan tetap rapi di tengah layar (*centered*).

### Modul 4: Token Warna dan Jarak (Custom Properties)
* **Tindakan:** Mengisolasi variabel CSS global di dalam `:root` (`--brand`, `--space`, `--surface`, `--ink`).
* **Pengujian:** Mengubah nilai `--brand` dari `#175cd3` menjadi warna hijau `#0f766e` pada `:root`.
* **Hasil Pengamatan:** Seluruh elemen yang merujuk pada `var(--brand)` (seperti border `.notice`, tombol `.btn`, dan indikator `focus-visible`) berubah secara otomatis tanpa perlu mengubah aturan CSS individual atau menambahkan `!important`.

### Modul 5: Tipografi dan Unit
* **Tindakan:** Menggunakan unit relatif `rem` untuk font-size (`1rem` pada body, `2rem` pada `h1`), `line-height: 1.6` tanpa unit, dan pembatasan lebar paragraf `max-width: 65ch`.
* **Pengujian Zoom Browser (200%):**
  - Dilakukan pengujian dengan memperbesar *zoom* browser hingga 200%.
  - **Hasil:** Teks secara otomatis menyesuaikan ukuran relatif terhadap root font-size tanpa terjadi *text clipping* (teks terpotong) atau *horizontal scrollbar* yang merusak tata letak.

### Modul 6: Organisasi dan Audit Accessibility
* **Tindakan:** Menata stylesheet menjadi bagian terstruktur (Reset/Tokens, Base, Wadah, Komponen, dan Interaction States) serta menerapkan `:focus-visible`.
* **Pengujian Navigasi Keyboard:**
  - Menekan tombol `Tab` pada keyboard untuk berpindah antar-input form dan tombol.
  - **Hasil:** Indikator fokus berupa *outline* tebal berwarna brand (`3px solid var(--brand)`) dengan offset `3px` terlihat sangat jelas di sekeliling elemen aktif.

---

## 2. Matriks Uji & Hasil Eksperimen

| Kasus / Kondisi | Input / Kondisi | Tindakan | Hasil Aktual | Status / Bukti |
| :--- | :--- | :--- | :--- | :--- |
| **Kasus Normal** | Ukuran layar desktop standar | Buka halaman di browser monitor | Form menempati lebar maksimum 960px di tengah layar. | `[PASS]` |
| **Kasus Batas (Zoom 200%)** | Zoom browser diatur ke 200% | Tekan `Ctrl + +` hingga 200% | Seluruh teks membesar, layout menyesuaikan tanpa ada teks terpotong. | `[PASS]` |
| **Token Brand Diganti** | Mengubah `--brand: #d92d20` | Edit nilai di `:root` | Komponen tombol, border notice, dan focus state berubah merah bersamaan. | `[PASS]` |
| **Tab Focus Keyboard** | Navigasi dengan tombol `Tab` | Tekan `Tab` berulang kali | Ring fokus terlihat jelas di setiap kontrol form yang aktif. | `[PASS]` |
| **Teks Paragraf Panjang** | Teks `.notice` > 200 karakter | Masukkan teks instruksi panjang | Teks terbungkus rapi dengan lebar maksimum tidak melebihi 65 karakter per baris (`65ch`). | `[PASS]` |

---

## 3. Catatan Diagnosis & Peer Review

* **Sesi Review Sejawat (Peer Check):**
  - **Reviewer:** [Nama Teman Praktikum]
  - **Ulasan Teknis:** Penjelasannya bahwa `line-height` tanpa unit (misal `1.6`) adalah *best practice* karena mengalikan rasio ukuran font masing-masing elemen turunan secara langsung, hindari penggunaan unit absolut seperti `px` pada `line-height`.

---

## 4. AI Use Statement

* **Penggunaan Tools AI:** Saya tidak menggunakan AI
* **Verifikasi Mandiri:** Kode CSS diuji langsung menggunakan VS Code Live Server, diuji responsivitasnya via DevTools Responsive Mode, serta diverifikasi kelayakan fokus keyboard menggunakan tombol `Tab`.