---
name: character-sheet
description: Membuat prompt character sheet (lembar referensi karakter) untuk AI image generator. Gunakan setiap kali user meminta "character sheet", "turnaround", "lembar karakter", atau referensi karakter dari foto/deskripsi. Layout wajib 3 tampilan full body (depan, samping, belakang) + 3 tampilan kepala (depan, samping, 3/4).
---

# Character Sheet

Skill ini dipakai untuk menulis prompt character sheet yang siap dipakai di image generator
(Nano Banana, Flux, GPT Image, Seedream, Midjourney, Stable Diffusion).

## Layout wajib

Setiap character sheet SELALU berisi 6 panel ini, tidak lebih dan tidak kurang
(kecuali user minta tambahan):

**Baris atas: 3 tampilan full body, dari kepala sampai kaki, skala dan tinggi sama**
1. Full body depan (front view)
2. Full body samping (side view / profile)
3. Full body belakang (back view)

**Baris bawah: 3 close-up kepala yang memperlihatkan detail rambut dan wajah**
4. Kepala depan (front)
5. Kepala samping (side profile)
6. Kepala 3/4 samping (three-quarter view)

Aturan layout:
- Semua full body dalam pose netral (A-pose atau berdiri tegak santai), tidak terpotong di kaki atau kepala.
- Close-up kepala dengan ekspresi netral, sama di ketiga panel, supaya fokus ke detail
  rambut (gaya, arah sisiran, garis rambut, tekstur) dan wajah.
- Background abu-abu muda netral, pencahayaan studio rata, proporsi dan detail
  kostum konsisten di semua panel.

## Langkah kerja

1. **Pelajari referensi.** Kalau user memberi foto wajah, tulis ciri yang terlihat secara
   netral: perkiraan usia, warna kulit, bentuk wajah, alis, mata, hidung, bibir, rambut
   wajah, gaya rambut dan garis rambut. Kalau ada foto kostum atau armor, uraikan material,
   warna, ornamen dan aksesorinya.
2. **Masukkan permintaan tambahan user** (misalnya jubah, tanpa helm, material metal) ke
   bagian karakter atau kostum.
3. **Tulis prompt** memakai template di bawah, dalam bahasa Inggris (image model lebih akurat
   dengan bahasa Inggris). Penjelasan ke user tetap mengikuti bahasa user.
4. **Sertakan** negative prompt, versi pendek untuk Midjourney/Flux, dan tips menjaga
   kemiripan wajah.

## Template prompt

```
Professional character design reference sheet, hyper-realistic, highly detailed, 8K.
Use the attached photos as identity reference and keep the exact facial likeness.

CHARACTER:
[usia, etnis/warna kulit, bentuk wajah, alis, mata, hidung, bibir, rambut wajah]
HAIR: [warna, panjang, gaya, arah sisiran, garis rambut, sisi samping]
EXPRESSION: neutral, calm

OUTFIT:
[kostum/armor: material, warna, ornamen, aksesori, senjata, jubah, dll.]

SHEET LAYOUT (exactly 6 panels):
Top row - three full body views, head to toe, same scale, neutral standing pose:
  1. full body front view
  2. full body side view (profile)
  3. full body back view
Bottom row - three head close-ups showing hair and face detail, same neutral expression:
  4. head front view
  5. head side profile view
  6. head three-quarter view

Clean neutral light grey studio background, soft even lighting, consistent proportions
and outfit details across all panels, thin divider lines between panels.
```

## Negative prompt default

```
cropped body, cut off feet, cut off head, inconsistent outfit between views, different face,
altered facial features, extra panels, missing panels, extra characters, deformed hands,
extra fingers, cartoon, low detail, blurry, busy background, text artifacts, watermark
```

Tambahkan item sesuai konteks (misalnya `helmet, visor, covered face` kalau user minta wajah terlihat).

## Versi pendek (Midjourney / Flux)

```
character design sheet, top row full body front view, side view, back view, bottom row head
close-ups front, side profile, three-quarter view showing hair and face detail, [ringkasan
karakter], [ringkasan kostum], neutral grey background, consistent design, hyper-realistic
--ar 16:9 --style raw
```

## Tips untuk user

- Unggah foto wajah tampak depan sebagai face reference utama, lalu foto samping dan 3/4
  sebagai tambahan supaya panel kepala samping dan 3/4 lebih mirip.
- Midjourney: `--cref [url foto] --cw 100`. Stable Diffusion: IP-Adapter FaceID atau InstantID.
- Referensi kostum dipakai sebagai style/image reference dengan kekuatan sedang supaya
  background referensi tidak ikut tersalin.
