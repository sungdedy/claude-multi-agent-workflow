---
name: character-build
description: Pintu masuk untuk membuat karakter baru yang konsisten dengan sistem character sheet, dari foto referensi user sendiri (Soul / Element di Higgsfield) atau di-generate dari nol oleh Claude. Pakai saat user bilang "buat karakter", "character build", "bikin karakter dari foto saya", "digital twin", "AI influencer baru", atau minta character sheet untuk karakter yang belum ada.
---

# Character Build

Skill ini membangun **satu karakter baru yang terkunci** (Character Bible + character sheet
terpilih + Asset Pack) memakai sistem character sheet dari skill `consistent-character-video`.
Skill ini berhenti di karakter terkunci. Pembuatan video dilanjutkan dengan
`consistent-character-video` (Fase 4–7) hanya bila user memintanya.

Referensi yang dipakai ulang (jangan diduplikasi, baca bila perlu):
- `../consistent-character-video/references/prompt-templates.md`: format Character Bible (§1) dan prompt sheet (§2).
- `../consistent-character-video/references/new-character.md`: tabel data wajib/opsional + default, checklist QC sheet, format Asset Pack, panduan manual.
- `../consistent-character-video/references/troubleshooting.md`: perbaikan drift.
- Higgsfield MCP: `get_workflow_instructions({ workflow: "character-sheet" })` untuk arsitektur slot prompt sheet.

---

## Langkah 1: Pertanyaan pembuka (SELALU pertama, tidak boleh dilewati)

Sebelum menanyakan hal lain atau memanggil tool apa pun, tanyakan satu hal ini:

> **"Karakternya mau dibuat dari foto referensi Anda sendiri, atau saya yang generate dari nol?"**
> 1. **Foto referensi sendiri**: wajah Anda (atau orang yang sudah memberi izin) jadi dasar karakter.
> 2. **Saya generate dari nol**: karakter orisinal, Anda tentukan detailnya.

Pakai `AskUserQuestion` bila tersedia; kalau tidak, tanyakan sebagai teks. Kalau jawaban user
sudah jelas di pesan sebelumnya (mis. "pakai foto saya"), konfirmasi singkat lalu lanjut ke
cabang yang sesuai.

---

## Cabang A: Foto referensi sendiri

### A1. Izin & batasan
- Foto harus milik user sendiri, atau milik orang yang sudah memberi izin.
- Tolak foto selebriti/tokoh publik/orang lain tanpa izin. Tawarkan cabang B (karakter orisinal "terinspirasi vibe").
- Karakter di bawah umur: hanya untuk konteks aman, dan hanya bila yang mengunggah adalah orang tua/wali.

### A2. Pertanyaan lanjutan (satu kali, maks. 3–4 pertanyaan)
1. **Jalur penguncian wajah**:
   | Jalur | Foto | Waktu | Bisa dipakai di | Cocok untuk |
   |---|---|---|---|---|
   | **Latih Soul** | 5–20 foto orang yang sama (idealnya mendekati 20) | ±10 menit | Gambar: hanya Soul 2.0 & Soul Cinema (photoreal), 1 orang per generasi. Video: tidak langsung. Gambar hasil Soul dipakai sebagai `start_image`/referensi di Seedance, Kling, dll. | Kemiripan paling tinggi, series/AI influencer photoreal |
   | **Element** | 1 foto terbaik | Instan | Nano Banana Pro/2, GPT Image 2, Seedream, Cinema Studio, Seedance 2.0, Kling 3.0; bisa multi-karakter | Gaya non-photoreal, video, adegan dengan karakter lain |
   | **Keduanya** | 5–20 foto | ±10 menit | Semua di atas | Proyek serius: Soul untuk gambar photoreal, Element untuk video/gaya lain |
2. **Gaya visual**: photoreal / 3D stylized / anime 2D / lainnya. Gaya non-photoreal = **wajib Element** (Soul hanya photoreal).
3. **Tujuan/peran**: konten sosmed (9:16), iklan/brand, film/series (16:9), dll.
4. **Outfit**: pakai outfit di foto, atau buat outfit "signature" baru (sebutkan gaya/warna bila ada).
Vibe/kepribadian (3 kata) boleh ditanyakan di sini atau diisi `[default]` dari tujuan.

### A3. Panduan foto (kirim ke user sebelum upload)
- Wajah jelas dan tajam, cahaya rata (dekat jendela/siang hari), tanpa filter/beauty mode.
- Tanpa kacamata hitam, topi, masker, atau rambut menutupi wajah.
- Hanya satu orang di foto; tidak ada wajah lain di latar.
- Variasi (khusus Soul): depan, 3/4 kiri, 3/4 kanan, samping, beberapa ekspresi (netral, senyum), beberapa jarak (close-up, setengah badan, full body), beberapa outfit/latar.
- Element: pilih satu foto depan atau 3/4, ekspresi netral/senyum tipis, resolusi tinggi.
- Hindari foto lama yang penampilannya sudah jauh berbeda.

### A4. Upload
Bila Higgsfield MCP tersedia: panggil `media_upload_widget` **sebagai satu-satunya tool di giliran itu**
(`type: "image"`; Soul → `min_files: 5, max_files: 20`; Element → `min_files: 1, max_files: 1`;
Keduanya → `min_files: 5, max_files: 20`). Jangan membaca file lokal/lampiran chat. Lanjutkan setelah
widget mengembalikan `media_id`.

### A5. Kunci identitas
- **Soul:** `show_characters({ action: "train", name: "<ID_KARAKTER>", images: [media_ids], type: "soul_2" })`.
  Training ±10 menit, non-blocking; sambil menunggu, kerjakan A6. Cek dengan `action: "status"`.
- **Element:** `show_reference_elements` (action `create`) dengan foto terpilih; simpan ID element-nya.
- **Keduanya:** jalankan dua-duanya; Element dari foto terbaik.

### A6. Checkpoint 1: Character Bible
Isi Bible (format `prompt-templates.md §1`). Untuk wajah: **deskripsikan apa yang terlihat di foto
secara jujur**, jangan dipercantik (bentuk wajah, mata, alis, rambut, tanda unik, warna kulit).
Tambahkan outfit, 3 anchor features, dan Style Formula. Tandai isian tebakan dengan `[default]`.
Minta persetujuan. **Jangan generate sheet sebelum disetujui.**

### A7. Checkpoint 2: Sheet
- Tunjukkan model, jumlah varian (2–4), aspect ratio (16:9), dan perkiraan kredit; tunggu persetujuan.
  `use_unlim` hanya bila user memintanya.
- **Soul:** `generate_image` dengan `model: "soul_2"` (atau `soul_cinematic`) + `soul_id`; prompt sheet
  memakai **identitas yang ringkas** (Soul yang membawa wajah, jangan deskripsikan ulang wajah secara detail);
  fokus prompt pada komposisi sheet, outfit, anchor features, cahaya.
- **Element / gaya non-photoreal:** Nano Banana Pro (default) atau model lain yang mendukung element,
  dengan element/foto sebagai referensi + prompt sheet + modul render gaya.
- Urutan: split-screen dulu → pilih → turnaround/expression dengan split-screen terpilih sebagai referensi.
- Tampilkan hasil dengan `show_generation_by_ids`.

### A8. Checkpoint 3–4: QC & Asset Pack
Pakai checklist QC sheet dari `new-character.md` **plus satu cek wajib**: bandingkan wajah di sheet
dengan **foto asli user**, bukan hanya antar panel. Sheet yang "mirip tapi bukan orangnya" (lookalike)
= gagal; perbaiki dengan menempel ulang referensi/element, meringkas deskripsi wajah di prompt, atau
pindah ke jalur Soul. Setelah dipilih, serahkan Asset Pack (format `new-character.md`) dengan tambahan
`SOUL_ID` / `ELEMENT_ID` dan daftar `media_id` foto sumber.

---

## Cabang B: Claude generate dari nol

### B1. Tanyakan detail karakter
Kirim formulir ringkas ini (user boleh mengisi sebagian; sisanya diisi `[default]`):

```
WAJIB
1. Tujuan/peran karakter      :
2. Gaya visual                : photoreal / 3D stylized / anime 2D / lainnya
3. Gender, usia, etnis/kulit  :
4. Vibe/kepribadian (3 kata)  :

OPSIONAL (kosongkan = saya pilihkan)
5. Wajah (bentuk, mata, hidung, bibir) :
6. Rambut (warna, panjang, gaya)       :
7. Tipe tubuh / tinggi                 :
8. Outfit utama                        :
9. Ciri khas / aksesori / tanda unik   :
10. Warna brand / hal yang dihindari   :
11. Platform & aspect ratio video      : (default 9:16)
12. Sheet tambahan                     : turnaround / expression / outfit kedua
13. Gambar moodboard (hanya untuk gaya):
```

Kalau user belum punya ide: tawarkan **3 konsep mini** (nama kerja, peran, gaya, vibe, 1 ciri khas),
dengan gaya yang berbeda-beda, lalu minta user memilih/menggabungkan. Karakter harus orisinal: nama
selebriti/IP hanya boleh sebagai "vibe", tidak disalin wajah/desainnya.

### B2. Checkpoint 1: Character Bible
Bible lengkap + Style Formula + 3 anchor features + rencana sheet (jenis, aspect ratio, model).
Minta persetujuan sebelum generate.

### B3. Checkpoint 2: Sheet
Ikuti `new-character.md` Checkpoint 2: rakit prompt dari template (field Bible **verbatim**), tunjukkan
model + varian + perkiraan kredit, tunggu persetujuan, generate split-screen dulu, lalu turnaround/expression
dengan split-screen terpilih sebagai referensi. Tanpa tool generate → prompt copy-paste + Panduan Manual.

### B4. Checkpoint 3–4: QC & Asset Pack
Ikuti `new-character.md` Checkpoint 3–4. Opsional: tawarkan melatih Soul dari 5–20 gambar konsisten
hasil sheet/keyframe bila karakter photoreal akan dipakai jangka panjang.

---

## Aturan umum

- Satu pertanyaan pembuka dulu, lalu satu putaran pertanyaan lanjutan. Jangan menginterogasi.
- Selalu ada persetujuan user sebelum setiap generate/training yang memakai kredit.
- Perbaikan terarah: ubah hanya yang diminta, tulis ulang field lain persis sama.
- Akhiri dengan Asset Pack dan tawaran langkah berikutnya: "Mau lanjut bikin keyframe/video dengan
  karakter ini?" → `consistent-character-video` Fase 4.
