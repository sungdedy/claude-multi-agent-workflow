# Troubleshooting — Karakter Drift

Format: **Gejala → Penyebab paling mungkin → Perbaikan.** Selalu perbaiki di tahap paling awal
(keyframe/gambar) — lebih murah daripada mengulang video.

---

### Wajah berubah antar shot
- **Penyebab:** prompt mendeskripsikan ulang wajah dengan kata berbeda; referensi tidak
  ditempel; memakai text-to-video.
- **Perbaikan:** copy Character Bible secara identik; tempel sheet/Soul ID di setiap generasi;
  pakai alur keyframe → image-to-video; di prompt video hapus semua deskripsi wajah.

### Shot pertama drift padahal referensi sudah ditempel
- **Penyebab:** shot pertama diproduksi dengan konteks paling sedikit; model "menafsir ulang".
- **Perbaikan:** bandingkan shot 1 dengan sheet secara khusus; regenerate dengan sheet
  ditempel ulang dan kalimat "the same character as the reference image" di awal prompt.

### Wajah "plastik"/rusak di wide shot
- **Penyebab:** wajah terlalu kecil dalam frame, model kekurangan piksel untuk identitas.
- **Perbaikan:** hindari wide shot panjang untuk momen penting; generate wide di resolusi
  lebih tinggi; atau ganti wajah dari panel close-up saat post-production; potong ke medium/CU
  untuk momen emosional.

### Outfit berubah (warna, detail, sisi aksesori tertukar)
- **Penyebab:** outfit ditulis generik; tidak ada anchor feature; state baru dibuat hanya lewat
  teks.
- **Perbaikan:** tulis outfit spesifik (bahan, warna, detail, sisi kiri/kanan); tetapkan 3
  anchor features dan sebutkan di setiap keyframe; buat sheet terpisah per outfit.

### Karakter jadi terlihat lebih muda / "babyface"
- **Penyebab:** bias model ke wajah muda-bulat.
- **Perbaikan:** tambahkan `defined adult jawline, mature adult bone structure` dan negatif
  `no babyface, no overly youthful rounded proportions`.

### Kulit terlalu mulus / "AI look"
- **Perbaikan:** tambahkan modul realisme: `visible fine skin texture with natural pores, subtle
  asymmetry, no digital smoothing, no beauty filter, matte-to-natural complexion`; kurangi kata
  seperti "flawless", "perfect", "beautiful".

### Style bergeser antar klip (warna, grain, gaya gambar)
- **Penyebab:** Style Formula tidak dipakai identik; model video berbeda-beda per shot.
- **Perbaikan:** satu Style Formula byte-identik; pakai satu model video utama untuk seluruh
  proyek bila memungkinkan; samakan grading saat editing.

### Muncul orang tambahan / duplikat karakter
- **Perbaikan:** `single subject only, exactly one person, no other people, no duplicate
  figures`; hindari istilah "over-the-shoulder" bila tidak ada karakter kedua (model akan
  menciptakan orang).

### Banyak karakter: wajah tercampur
- **Penyebab:** referensi beberapa karakter tanpa label; deskripsi campur aduk.
- **Perbaikan:** satu sheet per karakter; beri nama/kode tiap karakter dan rujuk "the woman
  from reference 1 (RARA_V1) on the left, the man from reference 2 (BAYU_V1) on the right";
  buat lineup sheet berdua bila sering tampil bersama; tentukan posisi layar tetap
  (kiri/kanan) untuk menjaga screen direction.

### Kerumunan jadi "klon" karakter utama
- **Penyebab:** hanya ada referensi satu karakter.
- **Perbaikan:** buat "variety sheet" berisi beberapa figuran berbeda dan sebutkan sebagai
  referensi keragaman, terpisah dari sheet karakter utama.

### Gerakan aneh / wajah meleleh saat gerak cepat
- **Perbaikan:** kurangi aksi per klip (satu aksi utama); perpendek durasi; gerakan kamera
  lebih lambat; tambahkan `end_image` agar model tahu tujuan gerakan; atau gunakan motion
  control dengan video referensi gerakan.

### Klip awal "diam" sebentar baru bergerak
- **Perbaikan:** tulis gerakan sejak frame pertama ("already walking as the shot begins");
  regenerate klip yang pembukaannya statis.

### Drift menumpuk saat last-frame chaining
- **Perbaikan:** reset setiap 2–3 klip dengan keyframe baru dari sheet asli; jangan pakai
  frame terakhir yang blur.

### Mulut bergerak padahal pakai narator
- **Perbaikan:** `the character does not speak, only gestures and emotes`; matikan audio native
  bila tidak perlu.

### Suara karakter berubah
- **Perbaikan:** kunci satu `voice_id`; jangan campur audio native model video yang berbeda
  untuk dialog karakter yang sama — pakai TTS/voice yang sama lalu lip-sync.
