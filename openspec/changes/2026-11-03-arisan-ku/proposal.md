# Proposal: ArisanKu — Kelola Arisan Tanpa Drama

## Apa & kenapa
Arisan adalah tabungan bersama paling Indonesia: tiap periode semua anggota setor iuran,
satu orang mendapat giliran menerima dana terkumpul, bergiliran sampai semua dapat bagian.
Riset pagi ini (swarloka.com, starfield.id, kaskita, skorcard.app) menegaskan tiga sumber
drama yang berulang: (1) catatan bayar tercecer di buku/chat sehingga siapa belum bayar
tidak jelas, (2) undian dirasa tidak adil karena pemenang lama ikut kocok lagi atau yang
belum bayar ikut menang, (3) risiko terbesar: anggota yang sudah menang lalu berhenti
setor — dalam kasus penipuan arisan online, kerugian sampai ~Rp1 miliar per kasus.
Aplikasi arisan yang ada umumnya berbayar, butuh daftar/login, atau kasir generik.

ArisanKu menyelesaikan ketiganya dalam satu halaman web gratis tanpa login:
catatan bayar per periode yang transparan, kocok yang hanya melibatkan anggota yang
lunas dan belum menang di putaran ini, dan pelacak kewajiban pasca-menang — setiap
pemenang jelas sisa berapa periode lagi ia wajib setor sampai putaran selesai.

## Kenapa mengejutkan
Bukan sekadar "catatan arisan". Aturan keadilannya dieksekusi oleh aplikasi, bukan
dipercaya begitu saja: yang belum bayar tidak bisa menang, yang sudah menang tidak
bisa menang lagi di putaran yang sama, dan pemenang yang menunggak setelah menang
langsung kelihatan di daftar tagih. Ditambah momen kocok yang seru (nama bergulir lalu
berhenti di pemenang) dan rekap sekali salin untuk ditempel ke grup WhatsApp —
persis alur nyata pengurus arisan.

## Bentuk output & backend
Web app frontend-only (artifact static), tanpa backend dan tanpa login. Alasannya:
seluruh logika adalah aturan deterministik atas data grup kecil; tidak ada data yang
perlu dibagikan antar-perangkat secara server-side. Data tersimpan di localStorage
perangkat pengurus — cukup, privat, dan gratis selamanya. Backend hanya akan menambah
biaya dan kerumitan tanpa menambah nilai. Kekurangan ini dinyatakan jujur di README:
data hidup di satu perangkat; rekap dibagikan lewat teks, bukan tautan kolaboratif.

## Uji bar scope (2026-11-03)
Bukan utilitas satu fungsi: 5 fitur saling nyambung (grup, anggota, iuran per periode,
kocok adil, riwayat + rekap), state bertahan (localStorage), alur end-to-end
(buat grup → catat bayar → kocok → periode berikutnya → putaran baru). Sekelas
BengkelCheck/JUKIR, bukan kata-angka/Berani Resign. Lolos.
