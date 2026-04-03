# 🎭 Naskah Role-Play: "Membangun Karoseri AME dengan SDLC Spiral"

**[INTRO]**
*(Project Manager maju ke depan, menyapa audiens)*

**Project Manager:** "Halo semuanya! Hari ini tim kami akan mendemonstrasikan bagaimana kami membangun Sistem Manajemen Produksi untuk PT. Alfa Mega Engineering (Karoseri Famega). 

Semuanya bermula dari keluhan Business Owner bengkel tersebut. Beliau bilang: *"Sasis truk yang masuk ke bengkel pencatatannya masih manual. Sering ketukar, dan saya mau semuanya terpantau dari HP!"* Kalau pakai metode *Waterfall*, kita bakal bikin dokumen tebal di awal, ngoding berbulan-bulan, dan kalau klien nggak suka, hancur semua. Makanya, kami pakai **SDLC Spiral**. Kami memutar siklus pengembangan menjadi 4 iterasi kecil, di mana setiap iterasinya melewati 4 kuadran: *Planning*, *Risk Analysis*, *Engineering*, dan *Evaluation*. Mari kita mulai dari putaran pertama!"

---

## 🔄 ITERASI 0: Pondasi & Kelayakan (Target: LCO)

**Project Manager (Kuadran 1 - Planning):** "Di Iterasi 0, tujuannya menyiapkan fondasi. Sebagai PM, saya mendefinisikan *scope* awal dan membuat dokumen hidup pertama kita: `01_PRD.md`. Kami sepakat pakai Next.js 16, Drizzle ORM, dan PostgreSQL."

**Risk Analyst (Kuadran 2 - Risk Analysis):** "Tunggu dulu. Sebelum koding dimulai, saya harus menganalisis risiko teknisnya. Framework Next.js 16 itu masih sangat baru, dan NextAuth v5 masih berstatus *beta*. Secara teknis, ini bahaya kalau ada API yang tiba-tiba berubah dan bikin *error* di tengah jalan. Saya catat ini di `03_Spiral_Risk_Log.md`. Mitigasinya: kita hanya akan pakai fitur *core* (seperti JWT) dan menghindari eksperimen fitur *beta*."

**System Architect (Kuadran 3 - Engineering/Design):** "Karena risiko teknis sudah dimitigasi, saya mulai menggambar kerangka sistem. Saya menyusun diagram arsitektur klien-server dan draf awal tabel *database* di `02_ERD_Architecture.md`."

**Lead Engineer (Kuadran 3 - Engineering/Code):** "Gua yang eksekusi kerangka itu. Bikin *project* Next.js dan *setup* Tailwind selesai. Tapi praktiknya nggak semudah teori. Pas gua mau dorong kodingan ke GitHub pakai `git push`, terminal langsung teriak *Authentication Failed*! Ternyata GitHub udah nggak bisa pakai *password* biasa. Gua harus bolak-balik bikin *Personal Access Token* (PAT) dan benerin URL *remote* di terminal. Baru deh kodingan awal kita selamat!"

**Project Manager (Kuadran 4 - Evaluation):** "Banyak drama, tapi *setup* akhirnya aman. Kami resmi mencapai *Milestone* LCO (*Life Cycle Objectives*). Mari putar spiralnya ke Iterasi 1!"

---

## 🔄 ITERASI 1: MVP Inti (Target: Fitur Dasar)

**Project Manager (Kuadran 1 - Planning):** "Iterasi 1 dimulai. Target di PRD saya perbarui: Admin harus bisa Login, input data sasis truk, dan datanya harus muncul di Kanban Board secara visual."

**Risk Analyst (Kuadran 2 - Risk Analysis):** "Dari segi teknis, integrasi NextAuth v5 di *Edge Runtime* bentrok dengan *database* Postgres. Ini *technical risk* tingkat tinggi (R1-2). Selain itu, bikin *library* drag-and-drop untuk Kanban terlalu berat untuk MVP. Mitigasinya: pisahkan file *config* auth, dan tunda drag-and-drop, ganti pakai *dropdown* statis saja untuk pindah status."

**System Architect (Kuadran 3 - Engineering/Design):** "Sesuai mitigasi, saya finalisasi skema Drizzle di ERD untuk tabel `users` dan `antrian`."

**Lead Engineer (Kuadran 3 - Engineering/Code):** "Gua langsung sikat kodingannya. Kredensial aman pakai *hashing* bcrypt. Form input sasis sukses nyimpen data ke Postgres, dan kartu antriannya muncul di Kanban Board."

**Project Manager (Kuadran 4 - Evaluation):** "Kita uji coba. Sasis berhasil masuk sistem, Kanban berjalan lancar. MVP Inti selesai!"

---

## 🔄 ITERASI 2: Otomatisasi Dokumen (Target: LCA)

**Project Manager (Kuadran 1 - Planning):** "Business Owner puas, tapi menuntut fitur baru: *Sistem harus bisa mencetak SPK dan Tanda Terima dalam bentuk PDF.* PRD kembali saya *update*."

**Risk Analyst (Kuadran 2 - Risk Analysis):** "Saya deteksi risiko performa (R2-1). Me-render PDF langsung di komponen *frontend* Next.js App Router itu sangat berat dan rentan bikin *browser crash*. Mitigasi teknisnya: Kita proses PDF-nya menggunakan `@react-pdf/renderer` murni di API Routes *backend*, biar *server* yang kerja keras, bukan laptop *user*."

**System Architect (Kuadran 3 - Engineering/Design):** "Saya tambahkan relasi *one-to-one* di ERD. Satu antrian sasis, punya satu tabel `spk`, dan satu tabel `tanda_terima`."

**Lead Engineer (Kuadran 3 - Engineering/Code):** "Kodingan *generate* PDF sukses! Tapi ada drama lagi pas narik data Drizzle. Tanggal yang keluar formatnya berantakan kayak `2026-04-02T...`. Gua terpaksa bikin *utility function* `formatTanggal` biar PDF-nya rapi dan enak dibaca."

**Project Manager (Kuadran 4 - Evaluation):** "Dokumen PDF bisa diunduh. Kita resmi mencapai *Milestone* LCA (*Life Cycle Architecture*)."

---

## 🔄 ITERASI 3: Finalisasi & Deployment (Target: IOC)

**Project Manager (Kuadran 1 - Planning):** "Putaran terakhir! Target fitur: Surat Jalan, Upload Foto Bukti Sasis, dan *Deployment* agar sistem ini *online*."

**Risk Analyst (Kuadran 2 - Risk Analysis):** "Risiko teknis terbesar di proyek ini ada di proses *upload* foto (R3-1). Kalau foto dilempar ke *database* atau *server* Next.js kita, *bandwidth* akan habis dan *server timeout*. Mitigasi mutlak: Kita pakai Cloudinary dengan mode *Unsigned Upload*. Foto dikirim langsung dari *browser* ke Cloudinary, *server* kita hanya menyimpan *link* URL-nya saja."

**System Architect (Kuadran 3 - Engineering/Design):** "Setuju. Dan karena kita mau *deploy* ke lingkungan Serverless (Vercel), driver *database* lokal `pg` harus saya rombak menjadi `@neondatabase/serverless` agar koneksi tidak terputus-putus."

**Lead Engineer (Kuadran 3 - Engineering/Code):** "Ini *boss battle* kita. Pas kodingan udah jalan dan mau dorong skema ke Neon DB pakai script *seed*, terminal teriak *"No database connection string"*. Ternyata Node.js nggak baca file `.env.local` otomatis. Gua harus akalin pakai *flag* khusus `--env-file` di terminal. Setelah itu sukses, gua pindahin 4 kunci rahasia termasuk `AUTH_SECRET` ke *dashboard* Vercel, klik Deploy, tunggu *confetti* turun, dan BOOM! Web kita *live*!"

**Project Manager (Kuadran 4 - Evaluation & Penutup):** "Aplikasi Karoseri Famega resmi beroperasi. Business Owner sekarang bisa memantau sasis masuk dan keluar langsung dari HP. Kami mencapai *Milestone* akhir: IOC (*Initial Operational Capability*).

Inilah inti dari SDLC Spiral. Dokumen kami (`PRD`, `ERD`, `Risk Log`) bukan sekadar pajangan awal. Mereka adalah 'Dokumen Hidup' yang terus berubah bersamaan dengan kodingan, di mana setiap kode yang ditulis selalu didahului oleh mitigasi risiko teknis. Terima kasih!"

**[OUTRO / SELESAI]**
