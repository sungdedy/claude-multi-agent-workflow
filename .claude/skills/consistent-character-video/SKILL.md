---
name: consistent-character-video
description: Bikin karakter AI baru yang konsisten (wajah, rambut, outfit, gaya) lengkap dengan character sheet, lalu hidupkan jadi video multi-shot di Higgsfield atau tool sejenis (Soul ID, Nano Banana Pro, Seedance, Kling, Wan, MiniMax). Pakai saat user minta buat karakter baru, character sheet, karakter yang sama di banyak gambar/klip, series/short film/iklan/konten AI influencer, atau mengeluh "wajahnya berubah-ubah tiap shot".
---

# Consistent Character → Video

Skill ini mengubah ide karakter menjadi **aset identitas yang terkunci**, lalu memakainya untuk
menghasilkan **video multi-shot** yang karakternya tidak berubah dari shot ke shot.

Prinsip intinya satu: **identitas dibuat SEKALI, lalu hanya DIREFERENSIKAN — tidak pernah
dideskripsikan ulang dengan kata-kata berbeda.** Hampir semua masalah "karakternya berubah"
datang dari melanggar prinsip ini.

Detail pendukung ada di folder `references/`:
- `references/new-character.md` — **Mode Karakter Baru**: data yang diminta dari user, default, checkpoint, deliverable, panduan manual.
- `references/prompt-templates.md` — template Character Bible, character sheet, keyframe, dan prompt video.
- `references/model-guide.md` — model mana untuk tahap mana (image, video, audio) dan parameter pentingnya.
- `references/troubleshooting.md` — diagnosis drift (wajah berubah, outfit berubah, style bergeser) dan cara memperbaikinya.

---

## Kapan dipakai

- User ingin karakter yang sama muncul di beberapa gambar atau beberapa klip video.
- User minta character sheet / model sheet / turnaround / expression sheet.
- User bikin series, short film, iklan dengan "brand ambassador" AI, konten AI influencer, atau video cerita/anak.
- User bilang wajah, outfit, atau gaya karakter berubah-ubah antar generasi.

Tidak perlu skill ini untuk satu gambar atau satu klip lepas tanpa kebutuhan kontinuitas.

---

## Aturan emas (jangan dilanggar)

1. **Character Bible dulu, generate belakangan.** Tulis identitas karakter sebagai teks tetap
   (lihat template). Teks ini di-copy **persis sama (byte-identik)** ke setiap prompt gambar yang
   butuh deskripsi karakter. Jangan parafrase — "rambut hitam sebahu" dan "rambut gelap medium"
   bagi model adalah dua orang berbeda.
2. **Referensi gambar mengalahkan teks.** Setelah character sheet disetujui, sheet itulah
   sumber kebenaran. Setiap generasi berikutnya WAJIB menempelkan sheet (atau Soul ID) sebagai
   referensi. Teks hanya pelengkap.
3. **Pisahkan Identitas vs Gerakan.** Di prompt video, JANGAN deskripsikan ulang wajah/rambut
   (itu tugas referensi). Prompt video hanya berisi: aksi, ekspresi, kamera, lingkungan, cahaya.
   Menulis ulang fitur wajah justru mengundang model "menggambar ulang" wajahnya.
4. **Keyframe dulu, baru video.** Jangan text-to-video untuk karakter penting. Buat still frame
   per shot (image-to-image dari sheet) → cek → baru animasikan (image-to-video, `start_image`).
   Gambar murah untuk diulang; video mahal.
5. **Satu state = satu aset.** Ganti outfit, luka, basah, umur lebih tua, dsb. = buat sheet
   baru yang MEREFERENSIKAN sheet pertama ("orang yang SAMA dengan referensi, sekarang ...").
   Jangan berharap prompt teks saja bisa mengganti outfit tanpa menggeser wajah.
6. **Kunci semua variabel lain juga.** Style, palet warna, lensa, grading, dan lokasi dibuat
   sebagai aset/formula tetap. Konsistensi karakter ikut rusak kalau style tiap shot berbeda.
7. **QC setiap klip terhadap sheet.** Bandingkan karakter per karakter. Shot pertama paling
   sering drift. Perbaiki di tahap gambar sebelum lanjut ke suara & editing.
8. **Karakter orisinal / dengan izin.** Jangan membuat kemiripan orang nyata tanpa izin atau
   karakter ber-hak cipta. Untuk wajah orang nyata (misal diri sendiri) pakai foto milik sendiri
   atau dengan persetujuan orangnya.

---

## Mode Karakter Baru (baca ini dulu bila user minta karakter baru)

Kalau user minta **membuat karakter baru** (belum ada sheet/Soul ID), **pakai skill
`character-build`** (`../character-build/SKILL.md`). Skill itu selalu dimulai dengan pertanyaan
"foto referensi sendiri atau di-generate dari nol?", lalu menjalankan alur di bawah ini
(detail di `references/new-character.md`). Ringkasannya:

1. **Intake singkat:** 4 data wajib (tujuan/peran, gaya visual, gender-usia-etnis, vibe 3 kata);
   sisanya diisi default bertanda `[default]`. Maks. 2–3 pertanyaan; belum punya ide → tawarkan 3 konsep mini.
2. **Checkpoint 1 — Character Bible:** kirim Bible + Style Formula + 3 anchor features + rencana
   sheet. **Jangan generate sebelum user setuju.**
3. **Checkpoint 2 — Sheet:** rakit prompt dari template; bila Higgsfield MCP tersedia, tampilkan
   model + jumlah varian + perkiraan kredit, tunggu persetujuan, lalu generate split-screen dulu,
   baru turnaround/expression dengan split-screen terpilih sebagai referensi. Tanpa tool →
   prompt copy-paste + Panduan Manual.
4. **Checkpoint 3 — QC & pilih:** nilai varian, rekomendasikan satu, perbaikan terarah (maks. ±3 putaran).
5. **Checkpoint 4 — Asset Pack:** Bible final, ID/URL sheet, model & setting, catatan drift,
   langkah berikutnya. Karakter berstatus LOCKED.

Mode ini berhenti di karakter terkunci. Video baru dikerjakan bila user meminta (Fase 4–7).

---

## Workflow (7 fase)

### Fase 0 — Brief (tanya maksimal 2–3 hal yang benar-benar menghalangi)
Kumpulkan: tujuan video (iklan/series/konten), durasi & aspect ratio (9:16 untuk TikTok/Reels,
16:9 untuk YouTube), gaya visual (photoreal, anime, 3D Pixar-like, dll), jumlah karakter,
apakah karakter berbicara di kamera (butuh lip-sync) atau pakai narator.

### Fase 1 — Character Bible (teks terkunci)
Isi template **Character Bible** di `references/prompt-templates.md`:
nama/kode karakter, usia, etnis & warna kulit, bentuk wajah, mata, alis, hidung, bibir,
rambut (warna + panjang + tekstur + finish + belahan), tanda unik (tahi lalat, bekas luka,
freckles), tipe tubuh, outfit dari atas ke bawah (top → layer → bawahan → sabuk → sepatu →
perhiasan → tas), dan **3 "anchor features"** — ciri paling khas yang harus selalu terlihat
(mis. jaket kuning mustard, anting perak kecil di telinga kiri, poni tipis).

Tulis juga **Style Formula** satu kalimat (medium, lensa, cahaya, grading) yang akan dipakai
identik di semua prompt.

### Fase 2 — Identity Anchor (pilih satu jalur)
| Jalur | Kapan | Cara |
|---|---|---|
| **A. Soul ID (Higgsfield)** | Karakter photoreal yang akan dipakai lama (series, AI influencer) atau wajah Anda sendiri | Latih Soul ID dari 5–20 foto orang yang sama (idealnya mendekati 20) (pencahayaan rata, banyak sudut, tanpa kacamata hitam/filter). Setelah itu generate lewat **Soul 2.0** dengan `soul_id`. Kalau karakternya fiktif, generate dulu 5–20 gambar konsisten dari character sheet, lalu latih Soul ID dari situ. |
| **B. Reference sheet** | Paling fleksibel, semua gaya (anime, 3D, photoreal) | Buat character sheet (Fase 3) dengan model image yang kuat (Nano Banana Pro, GPT Image, Seedream, Soul 2.0), lalu jadikan referensi di setiap generasi. |
| **C. Keduanya** | Proyek serius | Soul ID untuk wajah + sheet untuk outfit/prop/pose. |

### Fase 3 — Character Sheet (sumber kebenaran visual)
Generate sheet dalam **satu gambar** (identitas lebih terkunci daripada merakit banyak gambar):
- **Split-screen** (full body berdiri kiri + close-up wajah kanan) — default, paling serbaguna.
- **Turnaround** (depan, 3/4, samping, belakang) — penting untuk shot dari berbagai sudut.
- **Expression sheet** (netral, senyum, serius, kaget) — penting kalau karakter berakting.
- **Outfit sheet** — satu per state/outfit.

Aturan sheet: background polos netral (putih/abu-abu), cahaya rata tanpa bayangan keras,
satu karakter saja, full body benar-benar dari kepala sampai kaki, ekspresi netral, tanpa
teks/watermark. Aspect 16:9 untuk sheet multi-panel. Generate 2–4 varian, pilih satu,
**lalu kunci**. Sheet terpilih tidak boleh di-"rapikan" lagi lewat model (setiap re-generate
menggeser wajah sedikit) — perubahan berikutnya jadi aset baru.

### Fase 4 — Shot List + Keyframes
1. Pecah cerita menjadi shot 3–10 detik. Untuk tiap shot tulis: nomor, ukuran shot
   (wide/medium/close-up/ECU), sudut kamera, aksi, ekspresi, lokasi, cahaya, durasi,
   dialog/VO. Variasikan ukuran & sudut antar shot supaya tidak monoton.
2. Buat aset lokasi (tanpa orang) dan prop penting sebagai referensi terpisah.
3. Generate **keyframe (still pertama)** tiap shot: image-to-image dengan referensi urutan
   **lokasi → karakter (sheet/Soul ID) → prop**, prompt berisi komposisi shot + "the same
   character as the reference image". Untuk storyboard cepat bisa pakai multi-output
   (mis. Popcorn / batch) agar lighting & komposisi seragam.
4. QC tiap keyframe vs sheet (lihat checklist). Ulang yang drift SEKARANG.
5. Opsional: buat **end frame** juga untuk shot yang butuh posisi akhir tertentu
   (model yang mendukung `end_image`: Seedance, Kling 3.0, Wan 2.7, MiniMax H3).

### Fase 5 — Animasi (image-to-video)
- Masukkan keyframe sebagai `start_image` (+ `end_image` bila ada). Pada model yang menerima
  `image_references` (Seedance 2.0/2.5, MiniMax H3, Grok Video), sertakan juga sheet karakter
  sebagai referensi identitas.
- Prompt video = **hanya gerakan**: subjek + aksi (satu aksi utama per klip) + ekspresi mikro +
  gerakan kamera + atmosfer. Contoh ada di template. Tambahkan "keep the character's face,
  hair and outfit identical to the reference".
- Durasi pendek (4–6 detik) lebih stabil daripada panjang. Untuk adegan kontinu yang panjang,
  pakai **last-frame chaining**: ambil frame terakhir klip N (lihat perintah `ffmpeg` di
  `references/prompt-templates.md`) sebagai `start_image` klip N+1, atau pakai mode
  `video_extension` (Seedance 2.5).
- Draft dulu di resolusi/mode murah (480p–720p, mode `fast`/`std`), final di 1080p/`pro`/4K
  setelah gerakan disetujui.
- Gerakan spesifik dari video referensi (tarian, gerakan tangan): pakai motion control
  (Genjutsu / Kling Motion Control) dengan gambar karakter sebagai subjek.

### Fase 6 — Suara & Lip-sync
- Satu karakter = **satu voice_id** yang dikunci; pakai yang sama di semua klip.
- Karakter bicara di kamera: generate dengan audio native (Seedance/Kling/Wan dengan audio on)
  atau lip-sync setelahnya. Kalau pakai narator, tulis di prompt "character does not speak,
  only gestures and emotes" agar mulut tidak bergerak acak.

### Fase 7 — Editing, QC akhir, Upscale
- Susun klip, samakan color grade, tambahkan musik/SFX/subtitle.
- Upscale video final kalau perlu (Upscale Studio / upscale_video).
- Jalankan **Checklist QC** di bawah sebelum publish.

---

## Checklist QC (per keyframe dan per klip)

- [ ] Bentuk wajah, mata, alis, hidung, bibir sama dengan sheet.
- [ ] Warna, panjang, tekstur, dan belahan rambut sama.
- [ ] 3 anchor features terlihat dan benar.
- [ ] Outfit lengkap dan sama (warna, bahan, detail, aksesori, sisi kiri/kanan).
- [ ] Warna kulit & tanda unik (tahi lalat/freckles) konsisten.
- [ ] Proporsi tubuh & tinggi relatif antar karakter konsisten.
- [ ] Style, palet, grading sama dengan shot lain.
- [ ] Tidak ada tangan/jari rusak, wajah "plastik", atau orang tambahan yang tidak diminta.
- [ ] Suara karakter sama di semua klip.

Gagal satu poin → perbaiki di tahap paling awal yang murah (keyframe), bukan di video.
Lihat `references/troubleshooting.md`.

---

## Jika dijalankan lewat Higgsfield MCP (agent mode)

Urutan tool yang disarankan:
1. `get_workflow_instructions({ workflow: "character-sheet" })` → rakit prompt sheet.
2. `models_explore({ action: "recommend", ... })` bila ragu model → `generate_image`
   (sheet; 16:9) → `show_generation_by_ids`.
3. Keyframe: `generate_image_batch` dengan sheet sebagai media referensi → `jobs_wait`.
4. Video: `generate_video_batch` (keyframe sebagai `start_image`, sheet sebagai
   `image_references` bila model mendukung, `aspect_ratio` eksplisit) → `jobs_wait`.
5. Selalu tunjukkan estimasi biaya kredit dan minta persetujuan sebelum batch besar.
   Jangan menyalakan `use_unlim` kecuali user memintanya.

Untuk orkestrasi end-to-end dengan satu chat, Higgsfield juga punya **Supercomputer**
(agent yang merencanakan langkah, memilih model, menampilkan biaya, lalu otomatis meneruskan
gambar karakter dari langkah 1 sebagai referensi langkah 2). Prinsip di skill ini tetap berlaku
di sana — terutama Character Bible dan QC.
