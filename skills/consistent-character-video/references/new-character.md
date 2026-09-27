# Mode Karakter Baru — Intake, Deliverable, dan Panduan

Dipakai saat user minta **membuat karakter baru dari nol** (belum ada sheet, belum ada Soul ID).
Tujuan akhir mode ini: **satu karakter terkunci** (Character Bible + character sheet terpilih)
yang siap dipakai untuk keyframe dan video. Mode ini **tidak** membuat video — itu fase berikutnya.

---

## 1. Intake — apa yang dibutuhkan dari user

### Cara bertanya
- Jangan lempar formulir panjang. Kalau user sudah memberi brief singkat, **isi sendiri
  sisanya dengan default yang masuk akal**, tandai `[default]`, dan minta konfirmasi di
  Checkpoint 1. Tanyakan hanya yang benar-benar tidak bisa ditebak (maks. 2–3 pertanyaan).
- Kalau user belum punya ide sama sekali: tawarkan **3 konsep mini** (nama kerja, peran,
  gaya, vibe, 1 ciri khas) dan minta user memilih/menggabungkan.
- Kalau user minta formulir, berikan formulir di bawah (bagian Wajib + Opsional).

### Wajib (tidak boleh ditebak kalau brief tidak memberi petunjuk)
| # | Data | Kenapa perlu | Contoh |
|---|---|---|---|
| 1 | **Tujuan & peran karakter** | Menentukan outfit, ekspresi, dan jenis sheet | "Host konten kuliner TikTok", "maskot brand kopi", "tokoh utama series horor" |
| 2 | **Gaya visual** | Menentukan model & modul render | photoreal / anime-2D / 3D stylized (Pixar-like) / game concept / lainnya |
| 3 | **Gender, rentang usia, etnis/warna kulit** | Inti identitas | "Perempuan Indonesia akhir 20-an, kulit sawo matang" |
| 4 | **Kepribadian/vibe (3 kata)** | Ekspresi default, postur, pilihan outfit | "ceria, penasaran, membumi" |

### Opsional (diisi default bila kosong)
| Data | Default bila kosong |
|---|---|
| Detail wajah (bentuk, mata, hidung, bibir) | Disusun agar cocok dengan etnis & vibe; wajah dewasa (tidak babyface) untuk karakter dewasa |
| Rambut | Satu gaya yang mudah dikenali dari siluet |
| Outfit utama | Satu outfit "signature" sesuai peran, dengan 1 warna mencolok |
| 3 anchor features | Diusulkan: 1 item outfit berwarna khas + 1 aksesori asimetris + 1 tanda wajah |
| Tanda unik (tahi lalat, freckles) | Satu tanda kecil yang aman dipertahankan |
| Tipe tubuh & tinggi | Rata-rata, proporsi natural |
| Platform & aspect ratio video nanti | 9:16 (TikTok/Reels) |
| Jumlah outfit/state | 1 (DEFAULT) |
| Jenis sheet | Split-screen + turnaround; expression sheet bila karakter akan berakting/bicara |
| Warna brand / larangan budaya / hal yang dihindari | Tidak ada |
| Gambar moodboard | Tidak ada. Bila ada: hanya untuk **style & mood**, bukan menyalin wajah |
| Jalur identitas | Reference sheet (Jalur B). Soul ID hanya bila photoreal jangka panjang atau wajah user sendiri |
| Suara | Ditentukan nanti di fase video (cukup catat karakter suaranya) |

### Tolak / arahkan ulang
- Kemiripan orang nyata tanpa izin atau karakter ber-hak cipta → buat karakter orisinal yang
  hanya "terinspirasi vibe"-nya.
- Wajah user sendiri → boleh, dengan foto milik user (untuk Soul ID ±20+ foto).
- Karakter anak-anak → hanya konteks aman (cerita anak, edukasi), outfit & pose wajar.

---

## 2. Deliverable & Checkpoint (urutan wajib)

### Checkpoint 1 — Character Bible (teks)
Serahkan:
- Character Bible lengkap (format `prompt-templates.md §1`), field default ditandai `[default]`.
- Style Formula satu kalimat.
- 3 anchor features + alasan singkat (kenapa mudah dikenali di video).
- Rencana sheet (jenis apa saja, aspect ratio, model yang disarankan).

Tanya: **"Ada yang mau diubah sebelum saya buat sheet-nya?"** Jangan generate sebelum user
menyetujui atau bilang "lanjut".

### Checkpoint 2 — Prompt sheet (+ generate bila memungkinkan)
Rakit prompt sheet dari template `prompt-templates.md §2` (isi field Bible **verbatim**).

**Bila Higgsfield MCP tersedia:**
1. `get_workflow_instructions({ workflow: "character-sheet" })` dan ikuti arsitektur slot-nya.
2. Pilih model (`models_explore` recommend/get bila ragu). Default: photoreal → Nano Banana Pro
   atau Soul 2.0; anime/3D/stylized → Nano Banana Pro atau Seedream.
3. Tampilkan ke user: model, aspect ratio (16:9 untuk sheet multi-panel), jumlah varian (2–4),
   dan perkiraan kredit. Tunggu persetujuan. `use_unlim` hanya bila user memintanya.
4. Generate split-screen dulu. Turnaround/expression dibuat **setelah** split-screen dipilih,
   dengan split-screen terpilih ditempel sebagai referensi (bukan dari teks saja).
5. Tampilkan hasil dengan `show_generation_by_ids`.

**Bila tidak ada tool generate:** serahkan prompt siap copy-paste + **Panduan Manual** (§3).

### Checkpoint 3 — QC & pilih
- Nilai setiap varian dengan checklist di bawah; rekomendasikan satu dan jelaskan alasannya.
- User memilih. Perbaikan dilakukan **terarah** (mis. "rambut kurang panjang", "jaket harus
  mustard bukan oranye"): ubah hanya yang diminta, tulis ulang field lain persis sama.
- Maksimal ±3 putaran perbaikan per sheet; lebih dari itu, revisi Bible-nya dulu.

QC khusus sheet:
- [ ] Hanya satu karakter, tidak ada orang/figur tambahan.
- [ ] Panel full body benar-benar kepala sampai kaki, berdiri, tidak terpotong.
- [ ] Wajah di semua panel adalah orang yang sama.
- [ ] Semua field Bible terlihat benar (rambut, outfit, anchor features, tanda unik, sisi kiri/kanan).
- [ ] Background polos, cahaya rata, tanpa teks/watermark.
- [ ] Anatomi benar (tangan, jari, proporsi); tidak "plastik" untuk photoreal.

### Checkpoint 4 — Kunci & Asset Pack
Serahkan **Asset Pack** final:
```
CHARACTER: <ID>  (status: LOCKED)
BIBLE: <Character Bible final, verbatim>
STYLE FORMULA: <...>
SHEETS:
  - split-screen: <job id / URL / nama file>  ← referensi utama
  - turnaround:   <...>
  - expression:   <...>
MODEL YANG DIPAKAI: <model + setting>
STATE: DEFAULT (state lain: belum ada)
CATATAN DRIFT: <hal yang cenderung melenceng di model ini, mis. "anting sering pindah ke kanan">
```
Plus **Langkah Berikutnya** singkat untuk user:
1. Simpan sheet dengan nama file = ID karakter (mis. `RARA_V1_sheet_split.png`).
2. Jangan re-generate / "rapikan" sheet yang sudah dikunci; perubahan = state baru.
3. (Opsional, photoreal jangka panjang) Latih Soul ID: buat 20+ gambar konsisten dari sheet
   (berbagai sudut & ekspresi, cahaya rata) lalu latih di Higgsfield.
4. Lanjut ke Fase 4 skill ini: shot list + keyframe.

---

## 3. Panduan Manual (tanpa tool generate)

Berikan ke user dalam bentuk langkah bernomor:
1. Buka tool image di Higgsfield (atau tool lain).
2. Pilih model yang disarankan di Checkpoint 1.
3. Atur **aspect ratio 16:9** (sheet multi-panel) dan resolusi 2K bila tersedia.
4. Tempel prompt split-screen persis apa adanya — jangan diedit sebagian.
5. Generate 2–4 varian. Pilih yang paling cocok dengan checklist QC.
6. Untuk turnaround/expression: **unggah split-screen terpilih sebagai gambar referensi**, lalu
   tempel prompt turnaround/expression.
7. Unduh dan beri nama file sesuai ID karakter.
8. Kirim hasilnya kembali ke Claude untuk QC dan penguncian (Checkpoint 3–4).

Catatan: nama menu di UI Higgsfield bisa berubah; yang penting adalah model, aspect ratio,
prompt verbatim, dan referensi gambar.

---

## 4. Contoh percakapan singkat

> **User:** Pakai skill ini, buatkan karakter cewek Indonesia buat konten kuliner, realistis.
>
> **Claude:** Gaya (photoreal), gender & etnis, dan peran sudah jelas. Satu pertanyaan saja:
> vibe-nya mau seperti apa, misalnya "ceria, penasaran, membumi" atau "elegan, kalem, food
> critic"? Sisanya saya isi default dan saya tunjukkan dulu Character Bible-nya untuk Anda cek.
>
> *(user menjawab → Claude mengirim Checkpoint 1 → user setuju → Checkpoint 2 dst.)*
