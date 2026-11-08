# STELK CLASS MONITOR — X TJKT 5

Aplikasi web monitoring kelas dengan React, TypeScript, Vite, dan Tailwind CSS. Antarmuka menyediakan dashboard, daftar siswa, pencatatan salat, jadwal piket, kas, eviden, analisis, laporan, dan pengaturan.

## Jalankan lokal

```bash
npm install
npm run dev
```

Buka alamat lokal yang ditampilkan Vite. Build produksi: `npm run build` (hasil di `dist/`).

## Catatan

Versi awal ini adalah **mode pratinjau UI** dengan data contoh siswa; perubahan tidak tersimpan ke database dan halaman login/backend belum diaktifkan. Sebelum digunakan dengan data nyata, hubungkan Supabase Auth, tabel, Storage, dan Row Level Security sesuai rancangan skema aplikasi. Jangan pernah menaruh service-role key di browser atau mengunggah data pribadi siswa ke repositori.
