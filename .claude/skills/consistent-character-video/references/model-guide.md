# Model Guide — mana dipakai untuk apa

Snapshot katalog model Higgsfield per **September 2026** (dicek lewat `models_explore`).
Katalog berubah cepat — sebelum produksi, cek ulang dengan
`models_explore({ action: "get", model_id })` untuk parameter & batas terbaru.

## Tahap gambar (identitas, sheet, keyframe)

| Model | Kekuatan | Kapan dipakai | Catatan parameter |
|---|---|---|---|
| **Soul 2.0** (`soul_2`) | Photoreal, UGC, fashion editorial, karakter | Karakter photoreal jangka panjang; wajib bila pakai **Soul ID** | `soul_id` untuk identitas terlatih; `quality` 1.5k/2k; 1 gambar referensi |
| **Nano Banana Pro** (`nano_banana_pro`) | Kualitas & ketajaman tinggi, patuh prompt, bisa banyak referensi (hingga ~5 karakter & ~14 objek per workflow menurut Higgsfield) | Character sheet, keyframe dengan beberapa referensi (lokasi + karakter + prop), storyboard | `image_references`; resolusi 1k/2k/4k; banyak aspect ratio |
| **GPT Image 2.5** (`gpt_image_2_5`) | Editing presisi, teks, referensi | Edit kecil pada keyframe (ganti prop, perbaiki tangan) tanpa merusak wajah | `quality` low→max; `background` transparent untuk aset prop |
| **Seedream** (v4.5 / v5 Pro) | Rentang style luas, konsisten dengan style anchor | Aset non-photoreal (kartun, 3D, storybook), roster karakter+lokasi+prop | Tempel style key sebagai referensi di semua aset |
| **Nano Banana** (`nano_banana`) | Murah | Draft/eksplorasi awal | – |

Tips: jalankan prompt sheet yang sama di 2–3 model, bandingkan, baru kunci satu.

## Tahap video (animasi)

| Model | Kekuatan | Kapan dipakai | Media yang diterima | Durasi |
|---|---|---|---|---|
| **Seedance 2.0** (`seedance_2_0`) | Referensi identitas kuat, start+end frame, audio native, genre hint | Default untuk karakter konsisten: keyframe sebagai start + sheet sebagai referensi | start, end, image/video/audio references | 4–15 s; hingga 4K (`mode: std`) |
| **Seedance 2.5** (`seedance_2_5`) | `omni_reference`, `video_edit`, `video_extension` | Klip panjang (hingga 30 s), memperpanjang klip tanpa ganti karakter, edit video yang sudah ada | start, end, image/video/audio references | 4–30 s |
| **Kling 3.0** (`kling3_0`) | Multi-shot, sinkron audio, motion transfer, sinematik | Adegan dengan beberapa shot/aksi dramatis, 4K | start, end | 3–15 s; `mode` std/pro/4k |
| **Wan 2.7** (`wan2_7`) | Video karakter konsisten dengan audio sinkron | Karakter bicara, dialog pendek | start, end, audio reference | 2–15 s |
| **MiniMax H3** (`minimax_h3`) | Keyframe + referensi multimodal, 2K, batch hingga 4 | Kontrol keyframe ketat, butuh beberapa varian sekaligus | start, end, image/video/audio references | 4–15 s |
| **Grok Video 1.5** (`grok_video_v15`) | Start image + referensi gambar & audio, fisika | Alternatif image-to-video dengan referensi | start, image & audio references | 2–15 s |
| **Genjutsu** (`hf_mult_motion_control`) | Transfer gerakan dari video referensi | Karakter harus meniru gerakan persis (dance, gestur) | image refs (karakter) + video ref (gerakan) | ikut video ref |

Aturan praktis:
- Butuh **identitas paling kuat** → model yang menerima `image_references` (Seedance, MiniMax,
  Grok) + keyframe sebagai `start_image`.
- Butuh **posisi akhir tertentu** → model dengan `end_image`.
- Butuh **gerakan yang ditiru** → Genjutsu / motion control.
- Butuh **klip lebih panjang** → Seedance 2.5 `video_extension` atau last-frame chaining.
- Selalu set `aspect_ratio` secara eksplisit di setiap panggilan video.

## Tahap audio

- Kunci satu `voice_id` per karakter (`list_voices` / `create_voice`), pakai di semua klip.
- Audio native dari model video (Seedance/Kling/Wan) praktis untuk dialog pendek; untuk
  narasi panjang lebih stabil pakai TTS terpisah lalu digabung saat editing.

## Hemat kredit

1. Eksplorasi di gambar, bukan video.
2. Video draft: 480p–720p, mode `fast`/`std`, `sound: off` bila belum perlu audio.
3. Final: naikkan resolusi/mode hanya untuk klip yang sudah disetujui.
4. Batch beberapa generasi independen sekaligus lalu tunggu bersama (lebih cepat).
5. Cek biaya sebelum menjalankan batch besar.
