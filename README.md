# HepiBite

## Aturan Kolaborasi

1. **Diskusi & Persetujuan**: Sebelum melakukan perubahan besar, diskusikan terlebih dahulu di issue atau pull request.
2. **Code Review**: Setiap perubahan harus melalui proses review sebelum di-merge ke branch utama.
3. **Commit Message**: Gunakan pesan commit yang jelas dan deskriptif.
4. **Base Branch**: Semua pengembangan fitur/bugfix baru HARUS bercabang (branch) dari branch `development` (bukan langsung dari `main`).

## Alur Kontribusi (Fork & Development Branch)

Ikuti langkah berikut saat ingin berkontribusi:

1. Fork repository ini di GitHub (Fork otomatis menyertakan semua branch yang ada).
2. Clone fork Anda:
   ```bash
   git clone https://github.com/<username-anda>/HepiBite.git
   cd HepiBite
   ```
3. Tambahkan remote upstream untuk sinkronisasi dengan repo utama:
   ```bash
   git remote add upstream https://github.com/migraine-developer/HepiBite.git
   git fetch upstream --all
   ```
4. Pastikan branch `development` terbaru tersedia lokal:
   ```bash
   git checkout development || git checkout -b development upstream/development
   git pull upstream development
   ```
5. Buat branch baru dari `development` sesuai format penamaan (lihat bagian Penamaan Branch):
   ```bash
   git checkout development
   git pull upstream development
   git checkout -b feat/nama-fitur
   ```
6. Lakukan perubahan & commit terstruktur:
   ```bash
   git add .
   git commit -m "feat: deskripsi singkat fitur"
   ```
7. Push ke fork Anda:
   ```bash
   git push -u origin feat/nama-fitur
   ```
8. Buat Pull Request ke branch `development` pada repository utama.
9. Setelah review & merge ke `development`, maintainer yang akan mengatur proses rilis (merge ke `main`).

### Menyinkronkan Fork Anda

Sebelum mulai pekerjaan baru atau jika branch Anda tertinggal:

```bash
git checkout development
git fetch upstream
git pull upstream development
git push origin development
```

Jika ingin memperbarui feature branch Anda dengan perubahan terbaru dari `development`:

```bash
git checkout feat/nama-fitur
git fetch upstream
git merge upstream/development
# atau gunakan rebase (opsional, jika terbiasa):
# git rebase upstream/development
```

Hindari langsung commit ke `main` atau membuat PR dari `main`. Gunakan `development` sebagai sumber kebenaran untuk pekerjaan berjalan.

## Proses Pull Request & Review

Setelah pekerjaan pada branch fitur/bugfix selesai:

1. Pastikan branch Anda sudah di-update dengan `development` terbaru.
   ```bash
   git checkout feat/nama-fitur
   git fetch upstream
   git merge upstream/development
   # (opsional) rebase: git rebase upstream/development
   ```
2. Pastikan tidak ada error build / lint (jalankan `npm run dev` lokal & perbaiki peringatan penting).
3. Push perubahan terakhir ke origin (fork Anda):
   ```bash
   git push origin feat/nama-fitur
   ```
4. Buat Pull Request ke branch `development` (bukan `main`).
5. Isi deskripsi PR dengan format disarankan:
   - Ringkasan singkat tujuan perubahan
   - Perubahan utama (bullet list)
   - Issue terkait (jika ada) contoh: `Closes #12`
   - Langkah uji (Steps to Test)
   - Catatan tambahan / breaking changes (jika ada)
6. Tambahkan label sesuai tipe (feat, fix, chore, docs, refactor) jika tersedia.
7. Jangan self-merge. PR akan di-review oleh author/maintainer. Reviewer dapat meminta revisi sebelum merge.
8. Setelah approved, author akan melakukan merge ke `development` dan mengelola integrasi lebih lanjut ke `main` saat rilis.
9. Setelah merge, hapus branch fitur di fork Anda (opsional tapi direkomendasikan) untuk menjaga kebersihan.

> Catatan: Jika pipeline CI ditambahkan di masa depan, pastikan semua check (build/test/lint) lulus sebelum meminta review.

## Penamaan Branch

Gunakan format berikut untuk penamaan branch:

- `feat/nama-fitur` — Untuk penambahan fitur baru (feature)
- `fix/nama-perbaikan` — Untuk perbaikan bug
- `chore/nama-tugas` — Untuk tugas non-fungsional (misal: update dependensi)
- `docs/nama-dokumentasi` — Untuk perubahan dokumentasi
- `refactor/nama-refactor` — Untuk refaktor kode

Contoh:

```
feat/auth-login
fix/navbar-overlap
chore/update-eslint
```

## Panduan Menjalankan Project (Development)

1. **Install Dependencies**
   Jalankan perintah berikut:

   ```bash
   npm install
   ```

2. **Migrasi Database (Prisma)**
   Jalankan migrasi agar database sesuai dengan schema:

   ```bash
   npx prisma migrate dev --name init
   ```

3. **Menjalankan Project**
   Jalankan server development:

   ```bash
   npm run dev
   ```

4. **(Opsional) Generate Prisma Client**
   Jika ada perubahan pada schema:

   ```bash
   npx prisma generate
   ```

5. **Testing**
   (Tambahkan instruksi testing jika sudah tersedia)

---

Silakan update bagian ini jika ada perubahan workflow atau tools.
