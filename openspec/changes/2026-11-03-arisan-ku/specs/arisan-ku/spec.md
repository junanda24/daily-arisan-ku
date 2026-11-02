# Spec: ArisanKu

## SHALL requirements

- SHALL-01 Buat grup arisan: nama grup, nominal iuran (Rupiah), frekuensi
  (Mingguan/Bulanan). WHEN pengurus mengisi form dan menyimpan THEN grup aktif
  muncul dengan nominal dan putaran 1 / periode 1.
- SHALL-02 Kelola anggota: tambah anggota dengan nama; hapus anggota.
  WHEN anggota ditambah THEN ia mendapat nomor urut berikutnya dan masuk daftar
  dengan status Belum Bayar pada periode berjalan.
- SHALL-03 Tandai pembayaran per periode: tiap anggota bisa dialihkan
  Lunas/Belum Bayar untuk periode berjalan saja. WHEN status diubah THEN total
  terkumpul dan progres periode dihitung ulang seketika.
- SHALL-04 Ringkasan periode: menampilkan jumlah anggota, jumlah yang sudah lunas,
  total terkumpul (lunas x iuran), target (anggota x iuran), dan progres.
  WHEN ada perubahan bayar THEN semua angka berubah tanpa reload.
- SHALL-05 Kocok adil: hanya anggota yang (a) lunas pada periode berjalan DAN
  (b) belum menang di putaran ini yang masuk undian. WHEN tidak ada yang eligible
  THEN tombol kocok nonaktif disertai penjelasan alasannya (belum ada yang lunas /
  semua sudah menang di putaran ini).
- SHALL-06 Animasi kocok: WHEN tombol kocok ditekan THEN nama-nama eligible
  bergulir cepat di panel kocok selama ~2 detik lalu berhenti di satu pemenang,
  dan pemenang diumumkan dengan kartu khusus (nama, nominal yang diterima =
  total terkumpul periode itu, tanggal).
- SHALL-07 Satu kocokan per periode: WHEN periode sudah dikocok THEN tombol kocok
  terkunci sampai pengurus menekan "Periode berikutnya". Tombol itu mereset status
  bayar semua anggota dan menaikkan nomor periode.
- SHALL-08 Kewajiban pasca-menang: pemenang tetap wajib setor sampai putaran
  selesai. WHEN seseorang menang THEN di daftar anggota ia bertanda "Sudah menang"
  plus sisa kewajiban = (anggota yang belum menang di putaran ini) x iuran, dan
  bila ia Belum Bayar pada periode berjalan setelah menang, ia masuk daftar tagih
  dengan penanda khusus.
- SHALL-09 Putaran selesai: WHEN anggota terakhir yang belum menang memenangkan
  kocokan THEN aplikasi mengumumkan putaran selesai dan menawarkan "Mulai putaran
  baru" yang mereset status menang semua anggota dan memulai putaran berikutnya
  pada periode 1.
- SHALL-10 Riwayat: setiap kocokan tercatat (putaran, periode, pemenang, nominal,
  tanggal) dan tidak hilang saat pindah periode/putaran.
- SHALL-11 Daftar tagih & rekap: menampilkan siapa saja yang Belum Bayar pada
  periode berjalan, dan tombol "Salin rekap untuk grup WA" yang menyalin teks
  ringkas (nama grup, putaran/periode, total terkumpul, pemenang terakhir,
  daftar belum bayar) ke clipboard.
- SHALL-12 Persistensi: seluruh data (grup, anggota, status bayar, riwayat,
  putaran/periode) tersimpan di localStorage dan kembali utuh setelah reload.
- SHALL-13 Contoh & reset: tombol "Coba dengan contoh" memuat satu grup contoh
  yang jelas berlabel contoh (bisa dihapus); tombol "Hapus semua & mulai baru"
  mengosongkan data setelah konfirmasi.
- SHALL-14 Mobile-first, tanpa fungsi mati, tanpa placeholder palsu: semua tombol
  berfungsi; state kosong menampilkan panduan, bukan data pura-pura.

## Di luar scope (disengaja)
- Tanpa login, tanpa sinkronisasi antar-perangkat, tanpa pembayaran/transfer uang
  di dalam aplikasi, tanpa notifikasi otomatis. Alasan: menjaga gratis, privat,
  dan selesai dalam satu sesi; rekap WA menggantikan notifikasi.
