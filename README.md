# STELK CLASS MONITOR — X TJKT 5

Aplikasi monitoring kelas berbasis React, TypeScript, Vite, dan Supabase. Tersedia dashboard, data siswa, monitoring salat, jadwal piket, kas, eviden, analisis/laporan, dan pengaturan agama.

## Menghubungkan ke Supabase

1. Buat atau buka proyek Supabase. Pada **Project Settings → API** salin Project URL dan **publishable key** (atau legacy anon key). Jangan pernah menggunakan `service_role` di browser.
2. Salin `.env.example` menjadi `.env.local`, lalu isi nilainya:

   ```env
   VITE_SUPABASE_URL=https://PROJECT_REF.supabase.co
   VITE_SUPABASE_ANON_KEY=sb_publishable_... 
   ```

   Di Vercel/Netlify, masukkan dua variabel yang sama pada pengaturan environment variables lalu redeploy.
3. Buka **SQL Editor** pada proyek Supabase dan jalankan seluruh isi `supabase/migrations/001_supabase_setup.sql` satu kali. Ini membuat tabel, RLS, bucket eviden privat, fungsi pembantu, dan data awal 30 siswa.
4. Di **Authentication → Users**, buat pengguna admin (auto-confirm email). Salin UUID pengguna, lalu jalankan SQL berikut dengan UUID dan nama yang benar:

   ```sql
   insert into public.user_profiles(user_id, display_name, role)
   values ('UUID_AUTH_USER', 'Nama Administrator', 'administrator');
   ```

   Buat akun lain melalui Authentication, lalu buat profil `pengurus`, `orang_tua`, atau `siswa` di `user_profiles`; akun orang tua/siswa harus memiliki `student_id` yang sesuai. Jabatan bendahara: `Bendahara` atau `Wakil Bendahara`.
5. Jalankan `npm install`, `npm run dev`. Build produksi: `npm run build`.

## Akses & keamanan

Login menggunakan Supabase Auth. RLS membatasi data siswa, aktivitas, kas, dan eviden sesuai profil; orang tua/siswa hanya mengakses siswa yang ditautkan, sedangkan transaksi kas hanya dapat diakses administrator/bendahara. Storage eviden privat. Data agama dan kewajiban salat hanya untuk administrator. Pastikan uji menggunakan akun dengan peran berbeda sebelum dipakai dengan data nyata.

Jika kredensial proyek pernah dibagikan secara publik, rotate key dari dashboard Supabase. Publishable/anon key boleh digunakan di browser dengan RLS yang benar; `service_role` dan password tidak boleh dimasukkan ke frontend atau Git.
