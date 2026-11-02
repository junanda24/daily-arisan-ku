# Design: ArisanKu

## Stack & arsitektur
Web artifact static, single-file client-side sesuai ARCHITECTURE.md §1:
satu objek state, data terpisah dari logika, fungsi render murni (state → DOM),
handler tipis, satu modul store untuk localStorage (kunci `arisanku-v1`),
IIFE/module scope, tidak ada variabel global berserakan. Tanpa backend
(lihat proposal.md), tanpa dependency eksternal berat.

## Model data
```js
state = {
  group: { name, amount, frequency } | null,
  members: [ { id, name, order, wonRound: bool } ],
  round: number, period: number, drawnThisPeriod: bool,
  payments: { [memberId]: bool }, // periode berjalan
  history: [ { round, period, winnerId, winnerName, amount, date } ],
  lastWinner: history entry | null
}
```
Turunan (dihitung saat render, bukan disimpan ganda): eligible = lunas AND
!wonRound; terkumpul = count(lunas) * amount; target = members.length * amount;
sisaKewajiban(pemenang) = count(!wonRound) * amount.

## Struktur layar (mobile-first, satu halaman, Operate mode)
1. Header + kartu ringkasan (anggota, lunas, terkumpul/target + progress bar,
   putaran & periode).
2. Panel Kocok (delight): layar nama bergulir, tombol Kocok, kartu pemenang.
3. Anggota: form tambah, daftar dengan toggle Lunas/Belum, badge Sudah menang +
   sisa kewajiban, tombol hapus.
4. Daftar tagih + tombol salin rekap WA.
5. Riwayat kocokan + aksi putaran (periode berikutnya / putaran baru) + reset.

## Visual (local-impeccable, Operate)
Krem hangat (#FFF8E7) sebagai dasar, hijau tua (#14532D) sebagai primer,
emas (#B45309 / #D9A441) sebagai aksen kemenangan — nuansa hajatan yang rapi,
bukan ungu-biru generik. Tipografi sistem yang tebal untuk angka Rupiah.
Tanpa emoji di label (preferensi user); penanda status berupa teks dan warna.
Momen delight: nama bergulir saat kocok, kartu pemenang membesar dengan aksen
emas, progress bar bergerak saat status bayar berubah. Copy Bahasa Indonesia
natural, tanpa lorem ipsum.
