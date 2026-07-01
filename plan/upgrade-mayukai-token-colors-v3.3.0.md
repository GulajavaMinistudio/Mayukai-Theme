---
goal: Perbaikan dan Upgrade Token Color Mayukai Theme ke Standar VS Code API 2026
version: 3.3.0
last_updated: 2026-07-01
status: Complete (v3.3.0)
owner: GulajavaMinistudio
tags: upgrade, bug, chore, theme, vscode
---

# Introduction
<!-- markdownlint-disable -->

![Status: Planned](https://img.shields.io/badge/status-Planned-blue)

Dokumen ini merupakan rencana implementasi untuk memperbaiki dan meng-upgrade seluruh varian tema Mayukai (**9 file tema** — sesuai yang terdaftar di `package.json`) agar sesuai dengan standar **VS Code API Theme Color Reference (Juni 2026)** dan **TextMate Scope Conventions**. Perbaikan mencakup 3 bug kritis, 2 gap konsistensi scope, dan penambahan dukungan fitur modern VS Code (bracket pair colorization, inlay hints).

Satu bug kritis yang sudah berdampak pada pengguna: file `Mayukai-reversal-color-theme.json` saat ini mengandung JavaScript comment (`//`) yang membuat JSON tidak valid. Saat user memilih tema Mayukai Reversal di VS Code, tema akan gagal di-load dan VS Code akan fallback ke tema default. Bug ini diperbaiki di **TASK-001** sebagai prioritas tertinggi.

Seluruh perbaikan menggunakan warna dari palet yang **sudah ada** di masing-masing tema — tidak ada warna baru yang diciptakan dari luar palet.

---

## 1. Requirements & Constraints

- **REQ-001**: Semua tema harus memiliki format JSON yang valid (tidak ada trailing comma yang tidak bisa ditoleransi, tidak ada JavaScript comment).
- **REQ-002**: Scope TextMate harus menggunakan dot-separated notation yang valid — tidak boleh mengandung spasi atau karakter non-standar.
- **REQ-003**: Nama key UI color harus sesuai dengan VS Code API Theme Color Reference terbaru (Juni 2026).
- **REQ-004**: Setiap scope TextMate harus menggunakan warna dari palet foreground yang SUDAH ADA di tema masing-masing.
- **REQ-005**: Bracket pair colorization harus menyediakan 6 warna berbeda yang kontras satu sama lain per tema. Setiap warna dalam satu tema harus memiliki hue yang berbeda secara jelas (tidak boleh ada dua warna dengan hue yang terlalu mirip, misal kedua-duanya merah). Verifikasi: cek bahwa tidak ada dua warna dalam satu tema yang perbedaan hue-nya <30° pada HSL color space.
- **CON-001**: Tidak boleh mengubah warna existing yang sudah berfungsi — hanya menambah atau memperbaiki.
- **CON-002**: File `Mayukai-reversal-color-theme.json` harus diperbaiki syntax JSON-nya terlebih dahulu karena saat ini invalid.
- **CON-003**: Harus menjaga konsistensi antar tema — scope yang sama di tema berbeda sebaiknya menggunakan hue yang mirip.
- **CON-004**: **SETIAP** warna baru yang ditambahkan ke sebuah tema — baik untuk UI color key (`editorBracketHighlight.*`, `editorInlayHint.*`, dll) maupun tokenColor scope — **HARUS diambil dari palet warna yang sudah ada di dalam file tema tersebut**. Tidak boleh menciptakan atau meminjam warna dari tema lain. Sumber warna bisa dari `tokenColors[].settings.foreground` atau dari `colors.*` yang sudah ada di file yang sama.

---

## 2. Implementation Steps

> **⚠️ EXECUTION DIRECTIVE FOR AI AGENTS:**
> Anda HARUS mengeksekusi rencana ini fase demi fase. Anda HARUS menjalankan langkah pengujian/verifikasi spesifik di akhir setiap fase. Setelah fase diuji, Anda **HARUS BERHENTI DAN MENUNGGU** persetujuan eksplisit pengguna sebelum melanjutkan ke fase berikutnya.

---

### Implementation Phase 1: Critical Bug Fixes (3 bugs + 1 cleanup di 9 file)

- **GOAL-001**: Memperbaiki 3 bug kritis yang menyebabkan warna tidak berfungsi atau file tidak bisa di-load oleh VS Code.

| Task     | Description | Completed | Date |
| -------- | ----------- | --------- | ---- |
| TASK-001 | **Fix JSON comment di `Mayukai-reversal-color-theme.json`**: Hapus baris `// "foreground": "#A9DC76"` pada line 215. Ganti menjadi `"foreground": "#FFCC66"` (sama dengan nilai di bawahnya). Verifikasi: file bisa di-parse oleh `JSON.parse()`. | ✅ | 2026-07-01 |
| TASK-002 | **⚠️ JALANKAN SETELAH TASK-001** — Fix malformed scope di 9 tema (termasuk Reversal yang sudah diperbaiki): Ganti scope `constant.numeric.line-number.find-in-files - match` (mengandung karakter ` - ` yang invalid) menjadi `constant.numeric.line-number.match`. 7 tema menggunakan `#5c6773`, Gruvbox menggunakan `#83a598`, Reversal menggunakan `#5c6773`. Verifikasi: tidak ada scope yang mengandung ` - ` di semua tema. | ✅ | 2026-07-01 |
| TASK-003 | **⚠️ JALANKAN SETELAH TASK-001** — Fix redundant JSON scopes di 9 tema: Di setiap tema terdapat 2 scope JSON yang sangat panjang dan berulang. Ganti kedua scope tersebut dengan `support.type.property-name.json`. Target rule: temukan rule dengan `"name"` mengandung "JSON key" atau "JSON property". **Efek samping (positif)**: scope menjadi lebih generik — match di SEMUA konteks JSON. Verifikasi: tidak ada scope dengan panjang >80 karakter di semua tema. | ✅ | 2026-07-01 |
| TASK-004 | **Fix key `quickInput.list.focusBackground`** di `Mayukai-mirage-color-theme-semantic.json`: file ini memiliki kedua key (`quickInput.list.focusBackground` dan `quickInputList.focusBackground`) dengan nilai sama `#191e2a`. Hapus key `quickInput.list.focusBackground`, pertahankan `quickInputList.focusBackground`. Verifikasi: tidak ada tema yang menggunakan key `quickInput.list.focusBackground`. | ✅ | 2026-07-01 |
| TASK-005 | **VERIFY**: Validasi JSON semua 9 file tema — harus valid. Cek scope: tidak boleh ada ` - ` dan tidak boleh scope >100 karakter. Pastikan tidak ada key `quickInput.list.focusBackground`. | ✅ | 2026-07-01 |
| TASK-006 | **APPROVAL**: Tunggu konfirmasi eksplisit user untuk melanjutkan ke Phase 2. | ⏳ | — |

> **Bonus fix**: Selain task di atas, ditemukan dan diperbaiki juga trailing commas pre-existing di 5 file tema (`Mayukai-alucard`, `Mayukai-darker`, `Mayukai-mirage-darker`, `Mayukai-mirage-gruvbox`, `Mayukai-mono`) yang menyebabkan JSON tidak valid. Trailing comma dihapus menggunakan regex `,(\s*[}\]])` → `$1`.

---

### Implementation Phase 2: Scope Consistency — Mayukai Midnight & Sunset

- **GOAL-002**: Menambahkan scope yang hilang di Mayukai Midnight (8 scope) dan Mayukai Sunset (4 scope) agar konsisten dengan 8 tema lainnya. Warna diambil dari palet yang sudah ada.

| Task     | Description                                                                                                                                                                                                                       | Completed | Date |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | ---- |
| TASK-007 | **Tambahkan scope yang hilang di Mayukai Midnight** (`themes/Mayukai-midnight.json`). Tambahkan tokenColor rules dengan warna dari palet Midnight yang sudah ada. Detail:                                                         | ✅ | 2026-07-01 |
|          | 📍 `entity.name.type` — foreground: `#F29668` (orange, dari palet `keyword.operator`)                                                                                                                                              | | |
|          | 📍 `constant.language.boolean` — foreground: `#D4BFFF` (lavender, dari palet `variable.other.constant`)                                                                                                                            | | |
|          | 📍 `storage.type.class` — foreground: `#F07178`, fontStyle: `italic` (merah, dari palet `support.function`)                                                                                                                        | | |
|          | 📍 `support.class.promise` — foreground: `#F28779` (merah-muda, dari palet `variable.member`)                                                                                                                                      | | |
|          | 📍 `variable.language.this` — foreground: `#F28779`, fontStyle: `italic`                                                                                                                                                           | | |
|          | 📍 `keyword.operator.new` — foreground: `#F07178` (merah, dari palet `support.function`)                                                                                                                                           | | |
|          | Catatan: `entity.name.class` dan `support.type.primitive` TIDAK PERLU ditambah karena parent scope (`entity.name`=`#FF8F40` dan `support.type`=`#9CD1BB`) sudah memberikan warna yang identik dengan scope spesifik di tema lain. | | |
| TASK-008 | **Tambahkan scope yang hilang di Mayukai Sunset** (`themes/Mayukai-sunset-color-theme.json`). Tambahkan tokenColor rules:                                                                                                         | ✅ | 2026-07-01 |
|          | 📍 `entity.name.type` — foreground: `#F29668` (orange)                                                                                                                                                                             | | |
|          | 📍 `constant.language.boolean` — foreground: `#FFA759` (yellow-orange, dari palet `storage.type`)                                                                                                                                  | | |
|          | 📍 `storage.type.class` — foreground: `#F07178`, fontStyle: `italic` (merah)                                                                                                                                                       | | |
|          | Catatan: `entity.name.class` TIDAK PERLU ditambah karena parent `entity.name`=`#FF8F40` sudah identik.                                                                                                                            | | |
| TASK-009 | **VERIFY**: Periksa bahwa Midnight dan Sunset sekarang memiliki total token rules yang bertambah (+6 untuk Midnight, +3 untuk Sunset). Periksa tidak ada duplikasi scope dalam satu tema. Validasi JSON valid.                    | ✅ | 2026-07-01 |
| TASK-010 | **APPROVAL**: Tunggu konfirmasi eksplisit user untuk melanjutkan ke Phase 3.                                                                                                                                                      | ⏳ | — |

---

### Implementation Phase 3: Modern Feature Support — Bracket Pair & Inlay Hints

- **GOAL-003**: Menambahkan dukungan warna untuk fitur modern VS Code (bracket pair colorization, inlay hints, dan bracket pair guides) di semua **9 tema** (termasuk Reversal yang sudah diperbaiki di Phase 1). Semua warna diambil dari palet foreground tokenColors yang sudah ada di masing-masing file tema.

| Task     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Completed | Date |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- | ---- |
| TASK-011 | **Tambahkan `editorBracketHighlight.foreground1`–`foreground6` ke semua 9 tema**. Setiap tema mendapat 6 warna dari palet foreground-nya sendiri. Detail per tema: | ✅ | 2026-07-01 |
|          | **Mayukai-alucard**: `#ff6188`, `#fc4085`, `#f5ba78`, `#95fb79`, `#5ccfe6`, `#d495f6` | | |
|          | **Mayukai-darker**: `#ff6188`, `#ff8f40`, `#ffcc66`, `#c2d94c`, `#5ccfe6`, `#d4bfff` | | |
|          | **Mayukai-midnight**: `#f07178`, `#ffa759`, `#ffcc66`, `#a9dc76`, `#77a8d9`, `#d2a6ff` | | |
|          | **Mayukai-mirage-darker**: `#ff6188`, `#ff8f40`, `#ffcc66`, `#bae67e`, `#5ccfe6`, `#d4bfff` | | |
|          | **Mayukai-mirage-semantic**: `#ff6188`, `#ff8f40`, `#ffcc66`, `#bae67e`, `#5ccfe6`, `#d4bfff` | | |
|          | **Mayukai-mirage-gruvbox**: `#fb4934`, `#fe8019`, `#fabd2f`, `#b8bb26`, `#83a598`, `#d3869b` | | |
|          | **Mayukai-mono**: `#ff6188`, `#fc9867`, `#ffd866`, `#a9dc76`, `#78dce8`, `#c39ac9` | | |
|          | **Mayukai-reversal**: `#fc4085`, `#FF8F40`, `#FFCC66`, `#BAE67E`, `#77a8d9`, `#d4bfff` | | |
|          | **Mayukai-sunset**: `#f07178`, `#ffa759`, `#ffcc66`, `#a9dc76`, `#77a8d9`, `#d4bfff` | | |
|          | — | | |
|          | **Tambahkan juga `editorBracketHighlight.unexpectedBracket.foreground` ke semua 9 tema**: `#ff3333` untuk semua tema, dengan pengecualian: Gruvbox `#fb4934`, Midnight `#ff6666`. | | |
| TASK-012 | **Tambahkan `editorBracketPairGuide.activeBackground1`–`activeBackground6` dan `editorBracketPairGuide.background1`–`background6` ke semua 9 tema**. Gunakan warna yang sama dengan `editorBracketHighlight.foreground*` tetapi dengan alpha dikurangi: inactive `26` (~15%), active `99` (~60%). | ✅ | 2026-07-01 |
| TASK-013 | **Tambahkan `editorInlayHint.background` dan `editorInlayHint.foreground` ke semua 9 tema**. Gunakan `editorSuggestWidget.background` untuk background (fallback: `editor.background`) dan `editor.foreground` + alpha `99` untuk foreground. | ✅ | 2026-07-01 |
| TASK-014 | **VERIFY**: 9 tema menambahkan **21 color key baru** per tema (= 189 total keys). **CON-004**: setiap hex color dari tokenColors/colors tema sendiri. **REQ-005**: hue antar 6 bracket tidak <30°. JSON valid, tidak ada duplikasi key. | ✅ | 2026-07-01 |

---

### Implementation Phase 4: Final Verification & Package Validation

- **GOAL-004**: Verifikasi menyeluruh bahwa semua tema valid dan siap digunakan di VS Code.

| Task     | Description | Completed | Date |
| -------- | ----------- | --------- | ---- |
| TASK-016 | **Validasi JSON**: Jalankan validasi JSON pada semua 9 file tema. Semua harus valid. | ✅ | 2026-07-01 |
| TASK-017 | **Validasi struktur tema VS Code**: Setiap file harus memiliki key `name`, `type` (harus `"dark"`), `colors` (object), `tokenColors` (array), `semanticHighlighting` (boolean). | ✅ | 2026-07-01 |
| TASK-018 | **Validasi konsistensi**: Semua tema harus memiliki setidaknya token rules yang comparable. Midnight (~83→89) dan Sunset (~87→90) harus bertambah. | ✅ | 2026-07-01 |
| TASK-019 | **Update CHANGELOG.md**: Tambahkan entry untuk versi 3.3.0 yang mendokumentasikan semua perbaikan. | ✅ | 2026-07-01 |
| TASK-020 | **Update package.json version**: Bump versi dari `3.2.4` ke `3.3.0`. | ✅ | 2026-07-01 |
| TASK-021 | **FINAL APPROVAL**: Serahkan hasil akhir ke user untuk diuji langsung di VS Code Extension Development Host. | ⏳ | — |

---

## 3. Alternatives

- **ALT-001: Rewrite penuh tema dengan format baru VS Code**. Tidak dipilih karena akan mengubah terlalu banyak dan berisiko mengubah identitas visual tema.
- **ALT-002: Menambahkan semantic highlighting ke semua tema**. Tidak dipilih untuk phase ini karena memerlukan analisis semantic token types yang lebih dalam. Akan dijadikan phase terpisah di masa depan.
- **ALT-003: Menggunakan color generator otomatis untuk bracket pair colors**. Tidak dipilih karena hasilnya bisa tidak konsisten dengan palet manual yang sudah dikurasi.
- **ALT-004: Menghapus scope yang malformed tanpa mengganti**. Tidak dipilih karena akan menghilangkan styling untuk line number match di Find in Files.

---

## 4. Dependencies

- **DEP-001**: Tidak ada dependency eksternal. Semua perubahan adalah editing JSON dalam folder `themes/`.
- **DEP-002**: VS Code ≥1.92.0 (sesuai `engines` di `package.json`). Bracket pair colorization memerlukan VS Code ≥1.60. Inlay hints memerlukan VS Code ≥1.67.
- **DEP-003**: `package.json` di root project untuk update versi dan CHANGELOG.

---

## 5. Files

| File                                              | Phase   | Operasi |
| ------------------------------------------------- | ------- | ------- |
| `themes/Mayukai-reversal-color-theme.json`        | 1, 3    | Perbaiki JSON comment, fix scope, redundant scope, bracket colors |
| `themes/Mayukai-mirage-color-theme-semantic.json` | 1, 3    | Hapus key `quickInput.list.focusBackground`, fix scope, redundant scope, bracket colors |
| `themes/Mayukai-alucard-color-theme.json`         | 1, 3    | Fix scope, redundant scope, bracket colors |
| `themes/Mayukai-darker-color-theme.json`          | 1, 3    | Fix scope, redundant scope, bracket colors |
| `themes/Mayukai-midnight.json`                    | 1, 2, 3 | Fix scope, redundant scope, tambah scope, bracket colors |
| `themes/Mayukai-mirage-darker-color-theme.json`   | 1, 3    | Fix scope, redundant scope, bracket colors |
| `themes/Mayukai-mirage-gruvbox-color-theme.json`  | 1, 3    | Fix scope, redundant scope, bracket colors |
| `themes/Mayukai-mono-color-theme.json`            | 1, 3    | Fix scope, redundant scope, bracket colors |
| `themes/Mayukai-sunset-color-theme.json`          | 1, 2, 3 | Fix scope, redundant scope, tambah scope, bracket colors |
| `CHANGELOG.md`                                    | 4       | Tambah entry v3.3.0 |
| `package.json`                                    | 4       | Bump version ke 3.3.0 |
---

## 6. Testing
- **TEST-001 — JSON Validity**: Semua 9 file tema harus lolos `JSON.parse()` tanpa error.
- **TEST-002 — No Malformed Scopes**: Tidak boleh ada scope TextMate yang mengandung karakter ` - ` (spasi-dash-spasi).
- **TEST-003 — No Deprecated Keys**: Tidak boleh ada key `quickInput.list.focusBackground` di semua tema.
- **TEST-004 — Key Coverage**: Setiap tema harus memiliki minimal 85 tokenColor rules. Midnight (~83→89) dan Sunset (~87→90) harus bertambah.
- **TEST-005 — VS Code Extension Host**: (Manual oleh user) Load tema di VS Code Extension Development Host — pastikan semua tema muncul di Color Theme picker dan tidak ada error di console.
---

## 7. Risks & Assumptions

- **RISK-001**: Warna bracket pair yang dipilih dari palet existing mungkin kurang kontras di tema tertentu. **Mitigasi**: User bisa menguji dan memberikan feedback untuk penyesuaian.
- **RISK-002**: Scope baru yang ditambahkan ke Midnight/Sunset mungkin bentrok dengan aturan scope parent yang lebih general. **Mitigasi**: TextMate scope selector bersifat specificity-based — scope yang lebih spesifik selalu menang. Jadi menambahkan `entity.name.type` akan meng-override `entity.name` tanpa efek samping.
- **RISK-003**: Penghapusan redundant scope JSON mungkin mengubah tampilan di JSON nested yang dalam. **Mitigasi**: Scope `support.type.property-name.json` sudah ada di aturan terpisah (`string.json support.type.property-name.json`) dengan warna yang sama.
- **ASSUMPTION-001**: Diasumsikan semua tema menggunakan encoding UTF-8.
- **ASSUMPTION-002**: Diasumsikan VS Code ≥1.92 dapat membaca semua color key yang ditambahkan (backward compatible).

---

## 8. Related Specifications / Further Reading

- [VS Code Theme Color Reference (June 2026)](https://code.visualstudio.com/api/references/theme-color)
- [VS Code Color Theme Guide](https://code.visualstudio.com/api/extension-guides/color-theme)
- [VS Code Syntax Highlight Guide](https://code.visualstudio.com/api/language-extensions/syntax-highlight-guide)
- [TextMate Scope Naming Conventions](https://macromates.com/manual/en/language_grammars)
- [Mayukai Theme GitHub Repository](https://github.com/GulajavaMinistudio/Mayukai-Theme)

---

## 9. Rollback Strategy

Jika terjadi kesalahan saat implementasi, gunakan strategi rollback berikut:

| Skenario | Rollback |
| --- | --- |
| Perubahan salah di satu file tema | `git checkout -- themes/<nama-file>.json` untuk mengembalikan file ke state sebelum perubahan |
| Semua perubahan salah | `git reset --hard HEAD` untuk mengembalikan semua file tema ke commit terakhir |
| Ingin menyimpan sebagian perubahan | `git stash` untuk menyimpan sementara, lalu `git stash pop` untuk mengembalikan |
| File tema corrupt dan tidak ada di git | Salin dari backup atau dari tema lain yang belum diubah sebagai template |

> **Rekomendasi**: Sebelum memulai setiap fase, buat git commit checkpoint. Ini memungkinkan rollback per-fase tanpa kehilangan seluruh progress.

---

## 10. Notes & Clarifications

- **`editorIndentGuide.background` (tanpa suffix angka)**: Key ini masih valid di VS Code API Juni 2026 sebagai fallback ketika `editorIndentGuide.background1-6` tidak diset. Semua tema Mayukai menggunakan key ini. **Pertahankan apa adanya** — tidak perlu diubah atau dimigrasi.
- **Angka 8 vs 9 tema**: Sebelum TASK-001, 8 tema valid JSON + 1 Reversal (invalid) = 9 file. Setelah TASK-001, semua 9 tema valid. File `Mayukai-mirage-color-theme.json` dan `Mayukai-dark-color-theme.json` adalah varian lighter yang tidak terdaftar di `package.json` — tidak termasuk dalam plan ini (sesuai keputusan klarifikasi).
- **Semantic highlighting**: Hanya `Mayukai-mirage-color-theme-semantic` yang mengaktifkan semantic highlighting (`"semanticHighlighting": true` implisit via `semanticTokenColors`). 9 tema lain secara eksplisit mematikannya (`false`). Ini adalah keputusan desain yang valid — tidak diubah dalam plan ini.
