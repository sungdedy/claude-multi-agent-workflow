# Brief: "Learn 98% of Higgsfield AI in 18 Minutes" (V1cho)

- Video: https://youtu.be/-vqocuhO1YE (dipublikasikan 24 Juli 2026)
- Skill turunan: [`skills/consistent-character-video/`](../skills/consistent-character-video/SKILL.md)

## Catatan sumber (penting)

YouTube tidak bisa diakses langsung dari lingkungan kerja ini, jadi video dianalisis lewat
fitur *video analysis* Higgsfield. Analisis itu hanya menghasilkan **30 detik pertama**
(bagian intro). Isi di bawah dibagi dua:
- **Dari video (terverifikasi):** apa yang benar-benar terlihat/terdengar di intro.
- **Dilengkapi dari sumber lain:** fitur Higgsfield yang dijanjikan video untuk dibahas,
  diambil dari dokumentasi/workflow resmi Higgsfield, katalog model, dan artikel publik.

---

## 1. Dari video (00:00–00:30)

- **Pembuka:** kreator sudah berbulan-bulan membuat video di Higgsfield dan menyebut platform
  ini bisa menangani **seluruh workflow kreatif di satu tempat** — bukan hanya tool image &
  video yang biasa dipakai orang.
- **Janji video:** satu *run-through* penuh seluruh platform, "setiap fitur dan setiap
  setting".
- **Yang ditampilkan:** workspace gambar dengan banyak shot sinematik, timeline editing video
  dengan audio waveform, menu fitur seperti **Create Video, Edit Video, Upscale Studio**.
- **Highlight:** "satu chat yang bisa menjalankan seluruh platform untuk Anda" — ini adalah
  **Higgsfield Supercomputer**.
- **CTA:** seluruh workflow beserta semua prompt yang dipakai dibagikan gratis di deskripsi
  video.
- **Teknik produksi video itu sendiri** (layak ditiru): hook langsung ke manfaat dalam 3 detik,
  talking head dengan rim light hangat-dingin (kayu hangat di kiri, hijau dingin di kanan),
  B-roll layar dengan zoom halus, inset wajah kreator bulat di pojok, lower-third "LINK IN THE
  DESCRIPTION". Konsisten secara visual: background & lighting tidak berubah di semua shot
  talking head.

## 2. Peta platform Higgsfield (konteks untuk fitur yang dibahas)

| Area | Fungsi | Relevansi ke karakter konsisten |
|---|---|---|
| **Supercomputer** | Agent chat: jelaskan hasil yang diinginkan, agent memecah langkah, memilih model & preset, menampilkan biaya kredit, lalu mengeksekusi. Output langkah 1 (mis. gambar karakter) otomatis jadi referensi langkah 2. | Menghilangkan download/upload ulang yang sering jadi sumber drift. |
| **Soul 2.0 + Soul ID** | Model foto photoreal; Soul ID = identitas terlatih dari 5–20 foto orang yang sama (training ±10 menit; hanya untuk Soul 2.0 / Soul Cinema). | Cara paling kuat mengunci wajah photoreal. |
| **Image models** (Nano Banana Pro, GPT Image, Seedream) | Gambar dari teks/referensi. | Character sheet & keyframe multi-referensi. |
| **Popcorn / storyboard** | Beberapa gambar sekaligus dengan karakter, cahaya, komposisi seragam. | Storyboard cepat yang konsisten. |
| **Cinema Studio** | Pembuatan shot sinematik: kontrol kamera, lensa, karakter sebagai elemen yang dikunci. | Identitas di elemen/karakter, gerakan di prompt. |
| **Video models** (Seedance 2.0/2.5, Kling 3.0, Wan 2.7, MiniMax H3, dll) | Image-to-video, start/end frame, referensi, audio native. | Menghidupkan keyframe tanpa mengubah karakter. |
| **Motion control / Genjutsu** | Transfer gerakan dari video referensi ke karakter. | Gerakan presisi tanpa redesign karakter. |
| **Edit Video / Upscale Studio** | Editing timeline, upscale. | Finishing. |
| **Audio / voice** | TTS, voice custom, lip-sync, dubbing. | Suara karakter yang konsisten. |

## 3. Pelajaran utama untuk karakter konsisten

1. **Identitas dibuat sekali, lalu hanya direferensikan.** Character Bible teks + character
   sheet gambar = sumber kebenaran.
2. **Referensi gambar > deskripsi teks.** Setiap generasi menempelkan sheet/Soul ID.
3. **Pisahkan identitas dan gerakan.** Prompt video hanya aksi, kamera, suasana — jangan
   tulis ulang wajah.
4. **Keyframe dulu, video belakangan.** Iterasi di gambar (murah), baru animasi (mahal).
5. **Start/end frame dan last-frame chaining** untuk kontinuitas antar klip.
6. **Satu state = satu aset** (outfit/umur/kondisi baru = sheet baru yang mereferensikan
   sheet pertama).
7. **Kunci juga style, lokasi, suara** — konsistensi karakter ikut rusak kalau variabel lain
   bergeser.
8. **QC setiap klip vs sheet**, terutama shot pertama.
9. **Draft murah, final mahal:** resolusi rendah untuk eksplorasi, naikkan setelah disetujui.
10. **Agent (Supercomputer) mempercepat**, tapi prinsip di atas tetap harus dipegang.

## 4. Latihan untuk memperdalam

1. **Latihan 1 — Character Bible:** tulis bible satu karakter orisinal, tetapkan 3 anchor
   features.
2. **Latihan 2 — Sheet:** generate split-screen + turnaround di 2 model, pilih dan kunci satu.
3. **Latihan 3 — 6 keyframe:** 6 shot dengan ukuran & sudut berbeda di 2 lokasi, QC semuanya.
4. **Latihan 4 — Animasi:** animasikan 3 keyframe (4–5 detik), pakai sheet sebagai referensi.
5. **Latihan 5 — Kontinuitas:** satu adegan 15 detik dari 3 klip dengan last-frame chaining.
6. **Latihan 6 — Suara:** tambahkan dialog dengan satu voice terkunci, edit jadi video 20–30
   detik.

## Sumber

- Video: https://www.youtube.com/watch?v=-vqocuhO1YE
- Higgsfield Supercomputer guide: https://higgsfield.ai/blog/higgsfield-supercomputer-guide
- Soul ID: https://higgsfield.ai/blog/Soul-ID-AI-Character-Consistency
- Soul ID help center: https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-create-and-use-a-soul-id-character
- Popcorn review: https://www.glbgpt.com/hub/higgsfield-popcorn-review
- Nano Banana Pro guide: https://higgsfield.ai/blog/Nano-Banana-Pro-is-Here-Full-Review-and-Guide
- Referensi komunitas (MIT): https://github.com/OSideMedia/higgsfield-ai-prompt-skill
- Workflow resmi Higgsfield MCP: `character-sheet`, `faceless-video`
