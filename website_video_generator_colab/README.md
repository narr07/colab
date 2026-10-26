# Website Video Generator — Google Colab MVP

Notebook untuk membuat video showcase dari website publik menggunakan Playwright, storyboard berbasis aturan, Gradio, dan FFmpeg. HyperFrames bersifat opsional; renderer fallback berbasis FFmpeg tetap digunakan jika HyperFrames tidak tersedia.

## Cara menjalankan
1. Pilih Runtime → Change runtime type → GPU bila tersedia. CPU tetap didukung.
2. Jalankan semua cell dari atas ke bawah.
3. Pastikan cell setup menampilkan status `Chromium install status: OK` dan `browser-check OK` sebelum lanjut.
4. Isi URL website publik pada UI Gradio.
5. Gunakan Preview terlebih dahulu, lalu Render Video.

## Catatan startup Gradio
- Pesan `Mengimpor Gradio...` hanya proses import package, bukan proses render UI.
- Notebook sekarang memakai `share=False` sebagai default untuk mengurangi kesan hang saat startup lokal.
- Jika butuh link publik, ubah `demo.launch(..., share=False, ...)` menjadi `share=True`.
- Startup menampilkan log `Gradio sedang memulai server lokal...` agar jelas proses masih berjalan.

## Troubleshooting Chromium (`libatk-1.0.so.0`)
Jika Generate gagal dan log berisi `BrowserType.launch` atau `libatk-1.0.so.0: cannot open shared object file`:
1. Jalankan ulang cell setup (sudah mencoba `playwright install --with-deps chromium` lebih dulu).
2. Jika runtime gagal memasang dependency otomatis, jalankan manual:
   - `!apt-get update && apt-get install -y libatk1.0-0 libatk-bridge2.0-0 libcups2 libdrm2 libxkbcommon0 libxcomposite1 libxdamage1 libxfixes3 libxrandr2 libgbm1 libasound2 libnss3 libnspr4 libgtk-3-0`
   - `!python -m playwright install chromium`
3. Jalankan ulang browser preflight sampai status `browser-check OK`, lalu coba Generate lagi.

## Troubleshooting FFmpeg (`exit status 187`)
- Notebook sekarang menyimpan stderr FFmpeg pada detail error (JSON di panel `Detail storyboard / status`), termasuk command yang dijalankan dan fallback codec.
- Jika `libx264` gagal, renderer otomatis mencoba fallback `mpeg4` untuk kompatibilitas MP4.
- Jika tetap gagal:
  1. Cek RAM dan disk Colab (cell runtime info). Render 1080p portrait 30fps lebih berat.
  2. Coba dulu `720p` + `Slow/Medium` FPS untuk verifikasi pipeline.
  3. Jalankan `Generate Preview` dulu; mode ini hanya menghasilkan PNG (tidak merender MP4).
  4. Pastikan output folder `/content/website_video_generator/output` masih punya ruang kosong.

## Batasan MVP
- Capture berbasis screenshot pada beberapa posisi scroll, bukan perekaman scroll kontinu.
- Website login, CAPTCHA, bot protection, atau asset yang memerlukan autentikasi mungkin tidak dapat diproses.
- File runtime Colab dapat hilang ketika sesi berakhir; unduh hasil MP4 setelah selesai.
- GPU membantu encoding jika FFmpeg build mendukungnya, tetapi Playwright dan sebagian besar komposisi tetap memakai CPU.

## Struktur notebook
- Instalasi dan pemeriksaan runtime
- Validasi dan capture website
- Analisis sederhana dan storyboard
- Komposisi preview
- Renderer MP4 fallback FFmpeg
- UI Gradio

Roadmap berikutnya: capture scroll kontinu, audio/logo, editor storyboard, dan integrasi HyperFrames yang lebih mendalam.
