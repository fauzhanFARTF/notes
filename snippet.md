# Tutorial Membuat Snippet di VS Code (Markdown, PHP, JavaScript)

Panduan ini menjelaskan cara membuat snippet di VS Code agar penulisan dan coding menjadi lebih cepat dan efisien.

---

## 1. Membuka Pengaturan Snippet

Langkah pertama adalah membuka konfigurasi snippet:

- Tekan

```bash
Ctrl + Shift + P
```

- Ketik

```bash
Snippets: Configure User Snippets
```

- Pilih sesuai kebutuhan:
  - `markdown.json`
  - `php.json`
  - `javascript.json`

> **Catatan:** Pastikan Anda memilih file snippet sesuai bahasa.

---

## 2. Menambahkan Snippet

Tambahkan kode berikut ke dalam file `markdown.json`:

```json

// Image Markdown
{
  "Insert Markdown Image": {
    "prefix": "img",
    "body": ["![${1:Image}](${2:url})"],
    "description": "Insert image markdown"
  }
}

/*
prefix: kata kunci untuk memanggil snippet (img)
${1:Image}: posisi pertama kursor (alt text)
${2:url}: posisi kedua kursor (link gambar)
*/


// Catatan (Blockquote)
{
  "Catatan Blockquote": {
    "prefix": "note",
    "body": ["> **Catatan:** ${1:isi catatan}"]
  }
}

// Catatan Multiline
{
  "Catatan Multiline": {
    "prefix": "note2",
    "body": ["> **Catatan:** ${1:judul}", "> ", "> ${2:penjelasan}"]
  }
}

// Video

{
  "Markdown Video ": {
    "prefix": "vid",
    "body": [
    "[![${1:Judul Video}](https://img.youtube.com/vi/${2:VIDEO_ID}/0.jpg)](https://www.youtube.com/watch?v=${2:VIDEO_ID})"
    ],
    "description": "Insert YouTube video thumbnail markdown"
  }
}
```

## 3.Cara Menggunakan Snippet

- Buka file dengan ekstensi:

```bash
.md
```

- Ketik:

```bash
img
# atau
note

```

- Tekan:

```bash
TAB
```

- Hasil:

```bash
![Image](url)
```

> **Catatan:** Gunakan tombol Tab untuk berpindah antar bagian input.

Tambahkan kode berikut ke dalam file `php.json`:

```json
// 1. Echo
{
  "PHP Echo": {
    "prefix": "pe",
    "body": [
      "echo \"${1:text}\";"
    ]
  }
}
// 2. Print_r (Debug)
{
  "PHP Print_r": {
    "prefix": "pr",
    "body": [
      "echo '<pre>';",
      "print_r(${1:$data});",
      "echo '</pre>';"
    ]
  }
}
// 3. Function
{
  "PHP Function": {
    "prefix": "pf",
    "body": [
      "function ${1:namaFunction}(${2:$param}) {",
      "    ${3:// code}",
      "}"
    ]
  }
}
// 4. If
{
  "PHP If": {
    "prefix": "pif",
    "body": [
      "if (${1:condition}) {",
      "    ${2:// code}",
      "}"
    ]
  }
}
// 5. Foreach
{
  "PHP Foreach": {
    "prefix": "pfe",
    "body": [
      "foreach (${1:$array} as ${2:$item}) {",
      "    ${3:// code}",
      "}"
    ]
  }
}
// 6. PDO Query
{
  "PHP PDO Query": {
    "prefix": "pdo",
    "body": [
      "$stmt = $pdo->prepare(\"${1:SELECT * FROM table WHERE id = :id}\");",
      "$stmt->execute(['id' => ${2:$id}]);",
      "$result = $stmt->fetchAll();"
    ]
  }
}
```

Tambahkan kode berikut ke dalam file `javascript.json`:

```json
// 1. Console Log
{
  "Console Log": {
    "prefix": "clg",
    "body": [
      "console.log(${1:data});"
    ]
  }
}
// 2. Arrow Function
{
  "Arrow Function": {
    "prefix": "fn",
    "body": [
      "const ${1:nama} = (${2:params}) => {",
      "  ${3:// code}",
      "};"
    ]
  }
}
// 3. Fetch API
{
  "Fetch API": {
    "prefix": "fetch",
    "body": [
      "fetch('${1:url}')",
      "  .then(res => res.json())",
      "  .then(data => {",
      "    console.log(data);",
      "  })",
      "  .catch(err => console.error(err));"
    ]
  }
}
// 4. If
{
  "JS If": {
    "prefix": "if",
    "body": [
      "if (${1:condition}) {",
      "  ${2:// code}",
      "}"
    ]
  }
}
// 5. For Loop
{
  "JS For Loop": {
    "prefix": "for",
    "body": [
      "for (let i = 0; i < ${1:length}; i++) {",
      "  ${2:// code}",
      "}"
    ]
  }
}
// 6. Async Await
{
  "Async Function": {
    "prefix": "async",
    "body": [
      "const ${1:getData} = async () => {",
      "  try {",
      "    const res = await fetch('${2:url}');",
      "    const data = await res.json();",
      "    console.log(data);",
      "  } catch (err) {",
      "    console.error(err);",
      "  }",
      "};"
    ]
  }
}
```

## 4.Jika Snippet Tidak Muncul

Berikut beberapa penyebab umum dan solusinya:

### 4.1 File bukan Markdown

Pastikan file yang digunakan berekstensi:

```bash
.md
```

Catatan: Snippet Markdown tidak akan muncul di file .js, .txt, dll.

### 4.2 Tidak muncul suggestion

- Tekan:

```bash
Ctrl + Space
```

> **Catatan:** isi catatan Ini akan memunculkan suggestion secara manual.

### 4.3 Setting snippet belum aktif

Cara mengaktifkan snippet suggestion:

- Tekan:

```bash
Ctrl + ,
```

- Cari:

```bash
snippetSuggestions
```

- Ubah menjadi:

```bash
top
```

Atau via JSON:

- Tekan:

```bash
Ctrl + Shift + P
```

Pilih:

```bash
Preferences: Open Settings (JSON)
```

Tambahkan:

```json
"editor.snippetSuggestions": "top"
```

### 4.4 Aktifkan Tab Completion

Tambahkan juga:

```bash
"editor.tabCompletion": "on"
```

> **Catatan:** Ini memungkinkan snippet langsung expand dengan tombol Tab.

### 4.5 JSON Error

Pastikan struktur JSON benar:

Tidak ada koma berlebih
Kurung {} lengkap
Format valid

> **Catatan:** isi catatan JSON error akan membuat snippet tidak terbaca.

## 5.Testing Snippet

Untuk memastikan snippet berjalan, coba tambahkan:

```json
{
  "Test Snippet": {
    "prefix": "test",
    "body": ["INI BERHASIL"]
  }
}
```

Lalu ketik:

```bash
test
```

Jika berhasil muncul → konfigurasi sudah benar.

## 6.Tips Tambahan

- Gunakan prefix unik (contoh: mdimg)
- Restart VS Code setelah edit snippet
- Gunakan Ctrl + Space jika snippet tidak muncul
- Simpan snippet sesuai bahasa (Markdown → markdown.json) 7. Contoh Snippet Tambahan (Opsional)
- Image dengan Title

```json
{
  "Insert Markdown Image with Title": {
    "prefix": "imgt",
    "body": ["![${1:alt}](${2:url} \"${3:title}\")"]
  }
}
```

Hasil:

```bash
![alt](url 'title')
```

## Penutup

Dengan snippet, penulisan Markdown jadi jauh lebih cepat dan efisien.
Fitur ini sangat berguna untuk dokumentasi, catatan belajar, maupun proyek development.

> **Catatan:** isi catatan Jika masih tidak berhasil, periksa kembali file .md, konfigurasi snippet, dan setting VS Code.
