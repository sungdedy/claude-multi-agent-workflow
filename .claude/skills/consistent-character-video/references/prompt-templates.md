# Prompt Templates — Consistent Character Video

Prompt untuk model ditulis dalam **bahasa Inggris** (model image/video paling patuh pada
bahasa Inggris). Penjelasan dalam bahasa Indonesia.

Urutan kata penting: model memberi bobot lebih besar pada token di awal. Taruh komposisi dan
identitas di depan, detail kualitas di belakang.

---

## 1. Character Bible (isi sekali, copy-paste identik)

```
CHARACTER ID: <KODE_PENDEK, mis. RARA_V1>
ROLE: <peran dalam cerita>
AGE & HERITAGE: <mis. Indonesian woman in her late twenties, warm medium-tan skin with golden undertone>
FACE: <bentuk wajah, rahang, tulang pipi, hidung, bibir + finish>
EYES: <bentuk, warna> with naturally muted catchlights
EYEBROWS: <bentuk, ketebalan, warna>
HAIR: <warna + undertone>, <panjang>, <tekstur/style>, <finish>, <belahan>
UNIQUE MARKS: <tahi lalat, freckles, bekas luka, posisi persis kiri/kanan>
BODY: <tinggi relatif, tipe tubuh, postur>
OUTFIT (state: <nama state, mis. DEFAULT>): <top> , <layer> , <bawahan> , <sabuk> , <sepatu> , <perhiasan> , <tas atau "no bag">
ANCHOR FEATURES (harus selalu terlihat): 1) ... 2) ... 3) ...
VOICE: <voice_id terkunci> — <karakter suara: hangat, tempo sedang, dll>
DO NOT CHANGE: face, hair, marks, anchor features (kecuali ada state baru)
```

### Contoh terisi

```
CHARACTER ID: RARA_V1
ROLE: street-food vlogger, cheerful, curious
AGE & HERITAGE: Indonesian woman in her late twenties, warm medium-tan skin with golden undertone
FACE: soft oval face with a defined adult jawline, high rounded cheekbones, small straight nose, full lips with natural rosy-brown tint and satin finish
EYES: almond-shaped dark brown eyes, slight upward tilt, naturally muted catchlights
EYEBROWS: medium-thick straight brows, natural dark brown
HAIR: jet black with cool undertone, shoulder-length, soft layered waves, natural matte finish, middle part with thin wispy curtain bangs
UNIQUE MARKS: small mole under the left eye, faint freckles across the nose bridge
BODY: average height, slim-athletic build, relaxed confident posture
OUTFIT (state: DEFAULT): mustard-yellow cropped utility jacket with brass snap buttons over a plain white crew-neck tee, high-waisted straight-leg light-wash jeans, thin brown leather belt, white canvas low-top sneakers, small silver hoop earring on the left ear only, no bag
ANCHOR FEATURES: 1) mustard-yellow utility jacket 2) single silver hoop on left ear 3) mole under left eye
VOICE: <voice_id> — warm, upbeat, medium tempo, light Jakarta accent
```

### Style Formula (satu kalimat, identik di semua prompt)

```
STYLE: <medium>, <lensa/kamera>, <karakter cahaya>, <grading/palet>, <tekstur>
```
Contoh photoreal: `cinematic photoreal, 35mm lens look, soft natural daylight with gentle contrast, warm teal-and-amber grade, fine film grain, unretouched natural skin texture`
Contoh 3D: `stylized 3D animation render, appealing proportions, soft global illumination, pastel warm palette, clean subsurface skin`
Contoh anime: `clean 2D anime key visual, crisp lineart, cel shading with soft gradients, vivid but balanced palette`

---

## 2. Character Sheet Prompts

### 2a. Split-screen (default)

```
Split-screen character sheet composition, left side a full-body shot of the character standing upright in a neutral straight pose facing the camera, arms relaxed at the sides, full head-to-toe framing with both feet visible, right side a tight chest-up close-up portrait of the same character, identical original character on both sides, single subject only, pure light-grey seamless studio background, professional character sheet presentation,
<AGE & HERITAGE>, <FACE>, <EYES>, <EYEBROWS>, <HAIR>, <UNIQUE MARKS>,
visible fine skin texture with natural pores and subtle asymmetry, no digital smoothing, no beauty filter, matte-to-natural complexion,
<BODY>, wearing <OUTFIT>,
soft even diffused studio lighting without harsh shadows, <STYLE>,
no text, no watermark, no logos, no frame borders, exactly one person, no props, no furniture, left panel standing full-body not cropped not sitting, right panel close-up not full body
```
Aspect ratio: 16:9. Untuk gaya anime/3D, buang klausa pori-pori kulit dan ganti dengan render module gaya tersebut.

### 2b. Turnaround

```
Character turnaround model sheet, four consistent full-body views of the identical original character in a row — front view, three-quarter view, side profile, back view — evenly spaced, same scale, neutral standing pose, pure light-grey seamless background, even flat studio lighting,
<CHARACTER BIBLE fields>, <STYLE>,
no text, no watermark, exactly one character repeated in four views, no other people
```

### 2c. Expression sheet

```
Character expression sheet, a grid of six head-and-shoulders portraits of the identical original character showing: neutral, warm smile, laughing, serious focus, surprised, sad, same lighting and camera distance in every panel, pure light-grey background,
<AGE & HERITAGE>, <FACE>, <EYES>, <HAIR>, <UNIQUE MARKS>, <OUTFIT top only>, <STYLE>,
no text, no watermark
```

### 2d. State baru (outfit/umur/kondisi berubah)
Lampirkan sheet DEFAULT sebagai referensi, lalu:
```
The SAME person as in the reference image — identical face, hair, skin tone and marks — now wearing <OUTFIT BARU>. <composition sheet yang sama>. Keep everything else unchanged.
```
Beri kode baru: `RARA_V1_RAINCOAT`, `RARA_V1_OLDER`, dst.

---

## 3. Keyframe Prompt (image-to-image, per shot)

Referensi: lokasi → sheet karakter / Soul ID → prop.

```
[SHOT <nomor>] <shot size> <camera angle> shot, the same character as in the character reference image (<CHARACTER ID>), <aksi/pose saat frame pertama>, <ekspresi>, in <lokasi dari referensi lokasi>, <waktu & cahaya>, <posisi di frame: left third / center>, <STYLE>,
keep face, hair, outfit and anchor features identical to the reference: <ANCHOR FEATURES>
```

Contoh:
```
[SHOT 03] Medium close-up, slightly low angle, the same character as in the character reference image (RARA_V1), holding a paper plate of satay close to the camera, eyes wide with delight, at a busy night food stall from the location reference, warm string lights and smoky backlight, character on the right third, cinematic photoreal, 35mm lens look, warm teal-and-amber grade, fine film grain,
keep face, hair, outfit and anchor features identical to the reference: mustard-yellow utility jacket, single silver hoop on left ear, mole under left eye
```

---

## 4. Video (Motion) Prompt — image-to-video

**Jangan deskripsikan wajah lagi.** Struktur:

```
<Subjek singkat> <satu aksi utama dengan kata kerja jelas>, <ekspresi mikro>, <gerakan sekunder: rambut/kain/asap>, camera <jenis gerakan + kecepatan>, <atmosfer/cahaya yang berubah bila ada>. Keep the character's face, hair and outfit identical to the reference. <audio/dialog bila ada>
```

Contoh:
```
The woman lifts a satay skewer, takes a bite and closes her eyes in delight, then laughs softly toward the camera; smoke drifts across the frame and string lights flicker in the background; camera slow push-in from medium to close-up. Keep the character's face, hair and outfit identical to the reference. She says: "Ini juara banget!"
```

Kosakata kamera yang aman: `static locked-off`, `slow push-in`, `slow pull-out`, `pan left/right`, `tilt up/down`, `handheld subtle shake`, `orbit 90 degrees around the subject`, `tracking shot following from behind`, `crane up`, `dolly zoom`.

Tips:
- Satu klip = satu aksi utama. Dua–tiga aksi berurutan boleh kalau durasi ≥8 detik, tulis
  berurutan dengan "then".
- Karakter tidak bicara? Tulis: `the character does not speak, only gestures and emotes`.
- Hindari kata yang memicu redesign: "beautiful", "different look", "stylish new", nama
  selebriti.

---

## 5. Last-frame chaining (kontinuitas antar klip)

Ambil frame terakhir klip sebagai `start_image` klip berikutnya:

```bash
ffmpeg -sseof -0.1 -i clip03.mp4 -frames:v 1 -q:v 2 clip03_last.jpg
```

Bila frame terakhir blur (gerakan cepat), mundur sedikit:

```bash
ffmpeg -sseof -0.5 -i clip03.mp4 -frames:v 1 -q:v 2 clip03_last.jpg
```

Catatan: chaining berulang-ulang menumpuk drift kecil. Setiap 2–3 klip, "reset" dengan
membuat keyframe baru dari sheet asli.

---

## 6. Shot List Template

| # | Durasi | Shot size | Angle | Aksi | Ekspresi | Lokasi | Cahaya | Dialog/VO | Start frame | End frame |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 5s | Wide | Eye level | Rara berjalan masuk ke pasar malam | Penasaran | LOC_PASAR | Malam, lampu kuning | VO: "Malam ini kita..." | kf01.jpg | – |
| 2 | 4s | Medium | Low | Rara menunjuk gerobak sate | Excited | LOC_PASAR_ALT | Sama | "Itu dia!" | kf02.jpg | kf02_end.jpg |
| 3 | 6s | MCU | Slightly low | Menggigit sate, tertawa | Senang | LOC_SATE | Asap backlight | "Ini juara banget!" | kf03.jpg | – |

Aturan variasi: ukuran dan sudut shot bersebelahan harus berbeda; maksimal ~2 shot berturut-turut
di sudut lokasi yang sama sebelum pindah.
