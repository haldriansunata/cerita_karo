# 🎭 Naskah Role-Play: "Membangun Karoseri AME dengan SDLC Spiral"

**[INTRO]**
*(Project Manager maju ke depan, menyapa audiens)*

**Project Manager:** "Halo semuanya! Hari ini tim kami akan mendemonstrasikan bagaimana kami membangun Sistem Manajemen Produksi untuk PT. Alfa Mega Engineering (Karoseri Famega). 

Semuanya bermula dari keluhan Business Owner bengkel tersebut. Beliau bilang: *"Sasis truk yang masuk ke bengkel pencatatannya masih manual. Sering ketukar, dan saya mau semuanya terpantau dari HP!"* Kalau pakai metode *Waterfall*, kita bakal bikin dokumen tebal di awal, ngoding berbulan-bulan, dan kalau klien nggak suka, hancur semua. Makanya, kami pakai **SDLC Spiral**. Kami memutar siklus pengembangan menjadi 4 iterasi kecil, di mana setiap iterasinya melewati 4 kuadran: *Planning*, *Risk Analysis*, *Engineering*, dan *Evaluation*. Mari kita mulai dari putaran pertama!"

---

## 🔄 ITERASI 0: Pondasi & Kelayakan (Target: LCO)

**Project Manager (Kuadran 1 - Planning):** "Di Iterasi 0, tujuannya menyiapkan fondasi. Sebagai PM, saya mendefinisikan *scope* awal dan membuat dokumen hidup pertama kita: `01_PRD.md`. Kami sepakat pakai Next.js 16, Drizzle ORM, dan PostgreSQL."

**Risk Analyst (Kuadran 2 - Risk Analysis):** "Tunggu dulu. Sebelum koding dimulai, saya harus menganalisis risikonya. Dari segi *user*, orang bengkel itu kerjanya pakai sarung tangan, kadang layar HP kotor. Kalau UI-nya ribet, mereka pasti malas pakai sistem ini. Dari segi teknis, Next.js 16 dan NextAuth v5 itu masih sangat baru dan rawan *bug*. Saya catat ini di `03_Spiral_Risk_Log.md`. Mitigasinya: UI harus berukuran besar dan gampang di-klik, dan kita hanya akan pakai fungsi dasar dari *framework* agar tidak *error*."

**System Architect (Kuadran 3 - Engineering/Design):** "Karena risiko sudah dimitigasi, saya mulai menggambar kerangka sistem. Saya menyusun diagram arsitektur klien-server dan draf awal tabel *database* di `02_ERD_Architecture.md`."

**Lead Engineer (Kuadran 3 - Engineering/Code):** "Gua yang eksekusi kerangka itu. Bikin *project* Next.js dan *setup* Tailwind selesai. Tapi praktiknya nggak semudah teori. Pas gua mau dorong kodingan ke GitHub pakai `git push`, terminal langsung teriak *Authentication Failed*! Ternyata GitHub udah nggak bisa pakai *password* biasa. Gua harus bolak-balik bikin *Personal Access Token* (PAT) dan benerin URL *remote* di terminal. Baru deh kodingan awal kita selamat!"

**Project Manager (Kuadran 4 - Evaluation):** "Banyak drama, tapi *setup* akhirnya aman. Kami resmi mencapai *Milestone* LCO (*Life Cycle Objectives*). Mari putar spiralnya ke Iterasi 1!"

---

## 🔄 ITERASI 1: MVP Inti (Target: Fitur Dasar)

**Project Manager (Kuadran 1 - Planning):** "Iterasi 1 dimulai. Target di PRD saya perbarui: Admin harus bisa Login, input data sasis truk, dan datanya harus muncul di Kanban Board secara visual."

**Risk Analyst (Kuadran 2 - Risk Analysis):** "Ada risiko operasional besar di sini. Kalau kita pakai fitur Kanban *drag-and-drop* di layar HP, rawan banget kepencet sama staf bengkel, tahu-tahu status sasis pindah sendiri! Selain itu, secara teknis integrasi *database* di sistem *Edge Runtime* itu rentan bentrok. Mitigasinya: Kita buang rencana *drag-and-drop*, ganti dengan *dropdown* klik biasa agar *user* tidak salah input. Untuk teknis, kita pisahkan *file config auth*."

**System Architect (Kuadran 3 - Engineering/Design):** "Sesuai mitigasi, saya finalisasi skema Drizzle di ERD untuk tabel `users` dan `antrian`."

**Lead Engineer (Kuadran 3 - Engineering/Code):** "Gua langsung sikat kodingannya. Kredensial aman pakai *hashing* bcrypt. Form input sasis sukses nyimpen data ke Postgres, dan kartu antriannya muncul di Kanban Board dengan tombol *dropdown* yang aman."

**Project Manager (Kuadran 4 - Evaluation):** "Kita uji coba. Sasis berhasil masuk sistem, Kanban berjalan lancar tanpa takut salah geser. MVP Inti selesai!"

---

## 🔄 ITERASI 2: Otomatisasi Dokumen (Target: LCA)

**Project Manager (Kuadran 1 - Planning):** "Business Owner puas, tapi menuntut fitur baru: *Sistem harus bisa mencetak SPK dan Tanda Terima dalam bentuk PDF.* PRD kembali saya *update*."

**Risk Analyst (Kuadran 2 - Risk Analysis):** "Ada risiko dari segi bisnis (R2-2). Kalau format PDF SPK yang kita *generate* beda jauh dari kertas yang biasa dibaca tukang las, mereka bisa salah potong sasis truk! Risiko teknisnya: me-render PDF di sisi klien itu sangat berat dan bikin *browser crash*. Mitigasinya: Kita pastikan *field* SPK dikonfirmasi langsung ke klien, dan kita lempar proses pembuatan PDF-nya ke *server* *backend*."

**System Architect (Kuadran 3 - Engineering/Design):** "Saya tambahkan relasi *one-to-one* di ERD. Satu antrian sasis, punya satu tabel `spk`, dan satu tabel `tanda_terima`."

**Lead Engineer (Kuadran 3 - Engineering/Code):** "Kodingan *generate* PDF sukses! Tapi ada drama lagi pas narik data. Tanggal dari *database* keluar dengan format aneh kayak `2026-04-02T...`. Klien pasti bingung bacanya. Gua terpaksa bikin *utility function* `formatTanggal` biar PDF-nya rapi."

**Project Manager (Kuadran 4 - Evaluation):** "Dokumen PDF bisa diunduh dan formatnya sesuai kebutuhan lapangan. Kita resmi mencapai *Milestone* LCA (*Life Cycle Architecture*)."

---

## 🔄 ITERASI 3: Finalisasi & Deployment (Target: IOC)

**Project Manager (Kuadran 1 - Planning):** "Putaran terakhir! Target fitur: Surat Jalan, Upload Foto Bukti Sasis, dan *Deployment* agar sistem ini *online*."

**Risk Analyst (Kuadran 2 - Risk Analysis):** "Risiko *User Error* paling fatal ada di sini (US-3.0). Gimana kalau Kepala Produksi iseng atau nggak sengaja klik tombol 'Selesai' padahal truk belum beres? Mitigasinya: Harus ada pembatasan Hak Akses. Kepala Produksi cuma boleh *update* sampai tahap 'Finishing'. Yang berhak menyatakan 'Selesai' dan bikin Surat Jalan cuma Admin."

**System Architect (Kuadran 3 - Engineering/Design):** "Sistem hak akses itu saya atur logika transisinya. Dan untuk urusan teknis, karena kita mau *deploy* ke Vercel, driver *database* lokal harus saya rombak menjadi `@neondatabase/serverless` agar server tidak mati mendadak."

**Lead Engineer (Kuadran 3 - Engineering/Code):** "Ini *boss battle* kita. Gua pasang batas akses *role*-nya. Buat *upload* foto, gua pakai Cloudinary biar gampang. Terus pas mau *deploy* ke Neon DB, terminal teriak *"No database connection string"*. Ternyata Node.js nggak baca file `.env.local` otomatis. Gua harus akalin pakai *flag* khusus `--env-file` di terminal. Setelah sukses, gua masukin kunci rahasia `AUTH_SECRET` ke Vercel, klik Deploy, dan BOOM! Web kita *live*!"

**Project Manager (Kuadran 4 - Evaluation & Penutup):** "Aplikasi Karoseri Famega resmi beroperasi. Business Owner sekarang bisa memantau sasis masuk dan keluar langsung dari HP, dan mekanik tidak lagi dipusingkan dengan kertas yang hilang. Kami mencapai *Milestone* akhir: IOC (*Initial Operational Capability*).

Inilah inti dari SDLC Spiral. Dokumen kami (`PRD`, `ERD`, `Risk Log`) bukan sekadar pajangan awal. Mereka adalah 'Dokumen Hidup' yang terus berubah bersamaan dengan kodingan, di mana setiap fitur selalu diuji kelayakannya dari sisi teknis maupun dari sisi *user*. Terima kasih!"

**[OUTRO / SELESAI]**
