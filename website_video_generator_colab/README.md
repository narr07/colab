# Website Video Generator — Google Colab MVP

Notebook untuk membuat video showcase dari website publik menggunakan Playwright, storyboard berbasis aturan, Gradio, dan FFmpeg. HyperFrames bersifat opsional; renderer fallback berbasis FFmpeg tetap digunakan jika HyperFrames tidak tersedia.

## Cara menjalankan
1. Pilih Runtime → Change runtime type → GPU bila tersedia. CPU tetap didukung.
2. Jalankan semua cell dari atas ke bawah.
3. Isi URL website publik pada UI Gradio.
4. Gunakan Preview terlebih dahulu, lalu Render Video.

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
