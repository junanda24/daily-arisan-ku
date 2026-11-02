# ArisanKu — Kelola Arisan Tanpa Drama

ArisanKu adalah aplikasi web untuk mengelola arisan (tabungan bersama bergilir
khas Indonesia) tanpa login dan tanpa biaya: pengurus mencatat siapa yang sudah
bayar, mengocok pemenang secara adil, dan memantau kewajiban anggota yang sudah
menang sampai putaran selesai — semua dari satu halaman di HP.

## Kenapa ide ini dipilih

Tiga drama arisan yang paling sering terjadi: catatan bayar tercecer di buku
atau chat sehingga tidak jelas siapa belum bayar; undian yang dirasa tidak adil
karena yang belum bayar ikut menang atau pemenang lama ikut kocok lagi; dan
risiko terbesar — anggota yang sudah menang lalu berhenti setor. ArisanKu
mengeksekusi keadilannya lewat aturan, bukan lewat kepercayaan: yang belum
bayar tidak bisa menang, yang sudah menang tidak bisa menang lagi di putaran
yang sama, dan pemenang yang menunggak setelah menang langsung kelihatan di
daftar tagih beserta sisa kewajibannya. Ditambah momen kocok yang seru (nama
bergulir lalu berhenti di pemenang) dan rekap sekali salin untuk ditempel ke
grup WhatsApp — persis alur nyata pengurus arisan.

## Fitur

- Buat grup arisan: nama grup, nominal iuran (Rupiah), frekuensi Mingguan/Bulanan.
- Kelola anggota: tambah (nomor urut otomatis) dan hapus anggota.
- Tandai pembayaran per periode: alih Lunas/Belum Bayar per anggota, ringkasan
  periode terhitung seketika (jumlah lunas, terkumpul, target, progress bar).
- Kocok adil: hanya anggota yang lunas pada periode berjalan DAN belum menang
  di putaran ini yang masuk undian; bila tidak ada yang eligible, tombol
  nonaktif dengan penjelasan alasannya.
- Animasi kocok: nama-nama eligible bergulir ±2 detik lalu berhenti di satu
  pemenang; kartu pemenang emas menampilkan nama, nominal yang diterima
  (total terkumpul periode itu), dan tanggal.
- Satu kocokan per periode: tombol "Periode berikutnya" mereset status bayar
  dan menaikkan nomor periode.
- Kewajiban pasca-menang: pemenang bertanda "Sudah menang" plus sisa kewajiban
  (jumlah anggota yang belum menang x iuran); pemenang yang belum setor masuk
  daftar tagih dengan penanda khusus.
- Putaran selesai: saat anggota terakhir yang belum menang memenangkan kocokan,
  aplikasi mengumumkan putaran selesai dan menawarkan "Mulai putaran baru"
  (reset status menang, putaran +1, periode kembali ke 1).
- Riwayat kocokan: putaran, periode, pemenang, nominal, tanggal — tidak hilang
  saat pindah periode/putaran.
- Daftar tagih + "Salin rekap untuk grup WA": teks ringkas (grup,
  putaran/periode, terkumpul, pemenang terakhir, daftar belum bayar) disalin ke
  clipboard dengan konfirmasi visual dan fallback bila clipboard tidak tersedia.
- Persistensi localStorage: data kembali utuh setelah reload.
- Grup contoh berlabel jelas ("Arisan Contoh — RT 05", 6 anggota, iuran
  Rp100.000) lewat tombol "Coba dengan contoh"; tombol "Hapus semua dan mulai
  baru" dengan konfirmasi.

## Cara pakai

1. Buka aplikasi, isi nama grup, nominal iuran, dan frekuensi, lalu tekan
   "Buat Grup Arisan" (atau "Coba dengan contoh" untuk melihat dulu).
2. Tambahkan anggota satu per satu.
3. Setiap periode, alihkan anggota yang sudah setor menjadi Lunas.
4. Tekan "Kocok Arisan", saksikan nama bergulir, dan umumkan pemenangnya.
5. Tekan "Periode berikutnya" untuk periode selanjutnya; ulangi sampai semua
   anggota menang, lalu "Mulai putaran baru".
6. Kapan pun, tekan "Salin rekap untuk grup WA" dan tempel ke grup chat.

## Cara menjalankan dari source

Aplikasi ini satu file statis, tanpa build step dan tanpa backend:

```bash
# cukup buka src/index.html di browser, atau layani dari folder src:
python3 -m http.server 8000 --directory src
# lalu buka http://localhost:8000/
```

Tidak ada dependency, tidak ada API key, tidak ada variabel environment.

## Tech stack

- HTML + CSS + JavaScript vanilla (satu file, tanpa framework)
- Penyimpanan: `localStorage` browser (kunci `arisanku-v1`)
- Tanpa backend, tanpa login, tanpa database server

## Struktur folder

```
2026-11-03-arisan-ku/
├── README.md
├── src/
│   └── index.html            # aplikasi lengkap (hasil export artifact)
└── openspec/
    └── changes/
        ├── 2026-11-03-arisan-ku/          # proposal, spec, design, tasks
        └── archive/2026-11-03-arisan-ku/  # arsip change yang selesai
```

## Link hasil

- Aplikasi (artifact): card widget `web-artifact-build-completed-226ea82e-0cf3-4805-afd4-f00d8eb34cbf`
  (slug artifact: `arisanku`)
- Repo: https://github.com/junanda24/daily-arisan-ku
- Tanggal rilis: 2026-11-03

## Catatan saat build

- Desain: krem hangat (#FFF8E7), hijau tua (#14532D), aksen emas (#B45309);
  mobile-first, tanpa emoji di label (preferensi pengguna).
- Keputusan yang disengaja tidak dibuat: tanpa login/sinkronisasi
  antar-perangkat, tanpa pembayaran di dalam aplikasi, tanpa notifikasi
  otomatis. Alasannya: menjaga aplikasi gratis, privat, dan selesai dalam
  satu sesi; rekap WhatsApp menggantikan notifikasi dan tautan kolaboratif.
  Konsekuensinya dinyatakan jujur: data hidup di satu perangkat pengurus.
- Verifikasi: audit builder lulus (0 console error, 0 overflow di mobile
  390px). Jalur utama diuji probe langsung (contoh, kocok, periode
  berikutnya, persistensi setelah reload, tombol kocok nonaktif dengan
  alasan). Empat jalur lain (form buat grup, salin rekap, modal hapus,
  penyelesaian satu putaran penuh 6 kocokan) diverifikasi lewat inspeksi
  kode hasil export — handler dan logikanya terhubung benar, tanpa softlock
  (setiap state punya jalan keluar: periode berikutnya atau putaran baru).
  Selama pengujian ditemukan dan diperbaiki builder: timer kocokan yang
  hanya mengandalkan setInterval (kini ada setTimeout penjaga), kontras
  nomor langkah, dan form tambah anggota yang menyempit di mobile.
- Keterbatasan yang diketahui: font Google Fonts diblokir oleh lockdown
  egress pada lingkungan audit builder; font akan termuat normal di halaman
  terbit.
