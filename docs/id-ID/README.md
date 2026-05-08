**Bahasa:** [English](../../README.md) | [Português (Brasil)](../pt-BR/README.md) | [简体中文](../../README.zh-CN.md) | [繁體中文](../zh-TW/README.md) | [日本語](../ja-JP/README.md) | [한국어](../ko-KR/README.md) | [Türkçe](../tr/README.md) | Bahasa Indonesia

# Everything Claude Code

![Everything Claude Code — the performance system for AI agent harnesses](../../assets/hero.png)

> **140K+ stars** | **21K+ forks** | **170+ contributors** | **12+ ekosistem bahasa** | **Pemenang Anthropic Hackathon**

---

<div align="center">

**Language / 语言 / 語言 / Dil / Bahasa**

[English](../../README.md) | [Português (Brasil)](../pt-BR/README.md) | [简体中文](../../README.zh-CN.md) | [繁體中文](../zh-TW/README.md) | [日本語](../ja-JP/README.md) | [한국어](../ko-KR/README.md) | [Türkçe](../tr/README.md) | **Bahasa Indonesia**

</div>

---

**Sistem optimasi performa untuk antarmuka agen AI. Dari pemenang hackathon Anthropic.**

Bukan sekadar kumpulan konfigurasi. Ini adalah sistem yang lengkap: *skills* (keterampilan), *instincts* (insting), optimasi memori, pembelajaran berkelanjutan, pemindaian keamanan, dan pengembangan berbasis riset. Agen yang siap masuk tahap produksi, hooks, aturan, konfigurasi MCP, dan shims perintah lama yang berevolusi lebih dari 10 bulan penggunaan harian secara intensif untuk membangun produk nyata.

Bekerja dengan lancar di berbagai platform seperti **Claude Code**, **Codex**, **Cursor**, **OpenCode**, **Gemini**, dan antarmuka (harness) agen AI lainnya.

---

## Panduan Utama

Repositori ini hanya berisi kode mentah. Panduan berikut menjelaskan semuanya.

| Topik | Apa yang Akan Anda Pelajari |
|-------|-------------------|
| Optimasi Token | Pemilihan model, perampingan sistem prompt, proses latar belakang |
| Persistensi Memori | Hooks yang menyimpan/memuat konteks antar sesi secara otomatis |
| Pembelajaran Berkelanjutan | Ekstraksi pola otomatis dari sesi menjadi *skills* yang dapat digunakan kembali |
| Loop Verifikasi | Checkpoint vs evaluasi berkelanjutan, tipe *grader*, metrik pass@k |
| Paralelisasi | Git worktrees, metode kaskade, kapan harus meningkatkan skala instans |
| Orkestrasi Sub-agen | Masalah konteks, pola pencarian iteratif |

---

## Apa yang Baru

### v2.0.0-rc.1 — Pembaruan Antarmuka, Alur Kerja Operator, dan ECC 2.0 Alpha (Apr 2026)
- **Dashboard GUI** — Aplikasi desktop baru berbasis Tkinter (`ecc_dashboard.py` atau `npm run dashboard`).
- **Pembaruan antarmuka publik yang disinkronkan dengan repositori live** — 48 agen, 182 skills, dan 68 shims perintah lama.
- **Eksploitasi alat media** — Termasuk pembuatan video berbasis AI.
- **Alpha ECC 2.0 sudah tersedia** — Prototipe di `ecc2/` sudah dapat dibangun secara lokal.

*(Lihat Changelog lengkap di rilis GitHub kami).*

---

## Mulai Cepat (Quick Start)

Mulai menggunakan dalam waktu kurang dari 2 menit:

### Langkah 1: Instal Plugin (Direkomendasikan)

Untuk pengguna Claude Code:
```bash
# Tambahkan marketplace
/plugin marketplace add https://github.com/affaan-m/everything-claude-code

# Instal plugin
/plugin install everything-claude-code@everything-claude-code
```

### Langkah 2: Instal Aturan (Wajib)

> **Penting:** Plugin Claude Code tidak dapat mendistribusikan `rules` secara otomatis. Anda harus menyalin direktori aturan yang relevan secara manual.

```bash
# Kloning repositori terlebih dahulu
git clone https://github.com/affaan-m/everything-claude-code.git
cd everything-claude-code

# Instal dependensi (pilih package manager Anda)
npm install        # atau: pnpm install | yarn install | bun install

# Salin direktori aturan (rules) ke dalam namespace khusus ECC
mkdir -p ~/.claude/rules/ecc
cp -R rules/common ~/.claude/rules/ecc/
cp -R rules/typescript ~/.claude/rules/ecc/  # Ganti dengan bahasa yang Anda gunakan
```

Atau instalasi manual tanpa plugin:
```bash
./install.sh --profile full
```

### Langkah 3: Mulai Gunakan

```bash
# Skills adalah permukaan alur kerja utama.
/everything-claude-code:plan "Add user authentication"

# Cek perintah yang tersedia
/plugin list everything-claude-code@everything-claude-code
```

**Selesai!** Sekarang Anda memiliki akses ke 48 agen, 182 skills, dan 68 perintah bawaan.

### Dashboard GUI

Buka dashboard desktop untuk menelusuri komponen ECC secara visual:

```bash
npm run dashboard
# atau
python3 ./ecc_dashboard.py
```

---

## Konsep Utama

### Agen (Agents)
Sub-agen menangani tugas yang didelegasikan dengan ruang lingkup terbatas.
Contoh (`code-reviewer.md`): Agen ini dikhususkan untuk mengulas kualitas, keamanan, dan pemeliharaan kode.

### Skills (Keterampilan)
Skills adalah alur kerja utama yang dapat dipanggil langsung, disarankan secara otomatis, dan digunakan ulang oleh agen. Contohnya `tdd-workflow` yang menegakkan disiplin penulisan antarmuka terlebih dahulu sebelum kode.

### Hooks
Hooks akan dipicu pada event eksekusi tertentu, seperti mengingatkan Anda untuk menghapus `console.log` setelah mengedit file.

### Rules (Aturan)
Panduan yang harus selalu diikuti. Terdiri dari aturan `common/` (lintas-bahasa) dan folder spesifik bahasa pemrogramannya.

---

## Agen Mana yang Harus Saya Gunakan?

| Saya ingin... | Gunakan fitur ini | Agen yang bekerja |
|--------------|-----------------|------------|
| Merencanakan fitur baru | `/everything-claude-code:plan "Fitur"` | planner |
| Mendesain arsitektur sistem | `/everything-claude-code:plan` + agen architect | architect |
| Menulis kode TDD | skill `tdd-workflow` | tdd-guide |
| Mengulas kode | `/code-review` | code-reviewer |
| Memperbaiki masalah build | `/build-fix` | build-error-resolver |
| Melakukan tes end-to-end | skill `e2e-testing` | e2e-runner |
| Mencari kerentanan keamanan | `/security-scan` | security-reviewer |
| Menghapus *dead code* | `/refactor-clean` | refactor-cleaner |
| Memperbarui dokumentasi | `/update-docs` | doc-updater |

---

## Alat Ekosistem (Ecosystem Tools)

### Skill Creator
Terdapat dua cara untuk menghasilkan skill secara otomatis dari repositori Anda:
- Menggunakan perintah `/skill-create` secara lokal.
- Menggunakan [Aplikasi GitHub Skill Creator](https://github.com/apps/skill-creator) untuk repositori yang besar.

### AgentShield — Auditor Keamanan
Gunakan `npx ecc-agentshield scan` untuk memindai konfigurasi Claude Code Anda guna mendeteksi kerentanan, miskonfigurasi, dan risiko injeksi.

### Pembelajaran Berkelanjutan v2
Sistem ini mempelajari pola pengkodean Anda secara otomatis:
- `/instinct-status`: Lihat insting yang dipelajari.
- `/evolve`: Gabungkan insting yang berelasi menjadi skills.

---

## Dukungan Lintas Perangkat (Cross-Tool Parity)

ECC sepenuhnya mendukung lintas platform:
- **Claude Code**: Native (target utama)
- **Cursor IDE**: Terdapat pre-translated configs di `.cursor/`.
- **OpenCode**: Dukungan plugin penuh di `.opencode/`.
- **Codex**: Dukungan untuk CLI & Aplikasi macOS.
- **Antigravity**: Integrasi alur kerja dalam direktori `.agent/`.

---

## Optimasi Token

Menggunakan Claude Code dapat memakan biaya mahal jika Anda tidak mengatur konsumsi token. Pengaturan berikut ini sangat mengurangi biaya tanpa mengorbankan kualitas.

Tambahkan ini di `~/.claude/settings.json`:
```json
{
  "model": "sonnet",
  "env": {
    "MAX_THINKING_TOKENS": "10000",
    "CLAUDE_AUTOCOMPACT_PCT_OVERRIDE": "50"
  }
}
```

- Gunakan `/model sonnet` sebagai standar, dan hanya ubah ke `opus` ketika membutuhkan pemikiran arsitektural mendalam.
- Gunakan `/clear` di antara tugas-tugas yang tidak berhubungan.
- Gunakan `/compact` pada titik perhentian logis (seperti setelah riset atau menyelesaikan sebuah target).

---

## Berkontribusi

Kami mengundang Anda untuk ikut berkontribusi! Baik Anda memiliki tambahan sub-agen, skills untuk kerangka kerja (framework) tertentu, atau perbaikan pada dokumentasi. Silakan baca `CONTRIBUTING.md` untuk pedoman selengkapnya.

---

**Beri bintang (Star) pada repositori ini jika bermanfaat bagi Anda!**
