# Mahjong Table Score — Versi Mandiri

App ini jalan sendiri di browser, tanpa perlu buka aplikasi Claude. Setelah dipasang ke home screen, tampilannya sama seperti app biasa: ikon sendiri, layar penuh, tanpa address bar.

## Isi paket

| File | Fungsi |
|---|---|
| `index.html` | Seluruh app — semua layar, logika skor, panduan, kalkulator |
| `manifest.json` | Bikin app bisa dipasang ke home screen |
| `icon.svg` | Ikon app |
| `sw.js` | Service worker: app tetap kebuka walau tidak ada sinyal |

Keempat file harus berada di satu folder yang sama.

---

## Cara 1 — Netlify Drop (paling cepat, gratis, ±2 menit)

1. Buka **app.netlify.com/drop** di komputer
2. Seret folder berisi keempat file itu ke kotak di halaman tersebut
3. Netlify langsung memberi alamat seperti `https://nama-acak-123.netlify.app`
4. Buka alamat itu di HP → pasang ke home screen (lihat bagian bawah)

Alamatnya bisa diganti jadi lebih rapi lewat menu Site settings → Change site name.

## Cara 2 — GitHub Pages (kalau ingin gratis permanen dan mudah diperbarui)

1. Buat repository baru di GitHub, misalnya `mahjong-score`
2. Unggah keempat file ke root repository
3. Masuk **Settings → Pages**, bagian Source pilih branch `main` folder `/ (root)`, lalu Save
4. Setelah sekitar satu menit, app tersedia di `https://username.github.io/mahjong-score/`

## Cara 3 — Buka langsung dari HP tanpa hosting

Salin `index.html` ke HP lalu buka lewat aplikasi Files. App tetap jalan, tapi ada dua kekurangan: tidak bisa dipasang ke home screen, dan service worker tidak aktif. Cocok untuk mencoba sebentar saja.

---

## Memasang ke home screen

**Android (Chrome / Samsung Internet)**
Buka alamat app → menu titik tiga → **Tambahkan ke layar Utama** / *Install app*

**iPhone (Safari)**
Buka alamat app → tombol Share → **Add to Home Screen**

Setelah terpasang, app dibuka langsung dari ikon, layar penuh, tanpa address bar.

---

## Fitur hitung poin otomatis

Fitur ini memanggil API Anthropic, jadi butuh kunci milikmu sendiri:

1. Buat kunci di **console.anthropic.com** → API Keys
2. Di app, buka **Profil → API Key**, tempel kuncinya, tekan Simpan

Kunci disimpan di penyimpanan lokal browser HP itu saja, tidak dikirim ke server mana pun selain Anthropic.

**Yang perlu diperhatikan:** kunci ini tersimpan di sisi browser, jadi siapa pun yang memegang HP itu dan membuka developer tools bisa membacanya. Untuk pemakaian pribadi di HP sendiri, ini wajar. Yang jangan dilakukan: menempelkan kunci ke dalam file `index.html` lalu membagikan alamat app-nya ke orang lain — kuncimu ikut terbagikan dan pemakaiannya ditagihkan ke akunmu. Kalau app ini mau dipakai ramai-ramai, kuncinya harus dipindah ke server perantara kecil, bukan di browser.

Semua fitur lain — catat skor, leaderboard, riwayat, panduan, latihan — jalan penuh tanpa API key sama sekali.

---

## Penyimpanan data

Semua data tersimpan di browser HP masing-masing lewat localStorage: statistik, riwayat game, nama pemain, game yang sedang berjalan.

Konsekuensinya: data tidak berpindah antar HP dengan sendirinya, dan akan hilang kalau data situs di browser dibersihkan. Fitur Join with Code juga hanya menyambung dalam browser yang sama, bukan antar HP — untuk itu perlu backend sungguhan seperti Supabase.

---

## Kalau ingin dikembangkan lebih jauh

Yang paling masuk akal sebagai langkah berikutnya:

- **Sinkronisasi antar HP** — pindahkan penyimpanan ke Supabase supaya Join with Code benar-benar menyambungkan empat pemain di meja yang sama secara langsung
- **Menyembunyikan API key** — taruh satu fungsi kecil di server sebagai perantara, app memanggil fungsi itu, bukan Anthropic langsung
- **App Play Store** — bungkus dengan Capacitor supaya jadi APK

Kalau mau lanjut ke salah satunya, tinggal bilang.
