Saya ingin melakukan redesign dan implementasi bertahap pada scene 3D Assetrack yang sedang ada.

PENTING:
- Jangan membuat ulang konsep scene dari nol secara sembarangan.
- Pertahankan Three.js, sistem scroll-driven camera, dan struktur program yang sudah ada selama masih relevan.
- Tetapi layout environment boleh diubah cukup besar karena kita memang sedang memperbaiki desain scene.
- Fokus implementasi kali ini hanya sampai:
  1. Asset Management
  2. Asset Borrowing / QR Scanning
- Jangan mengerjakan detail Depreciation, Monitoring, atau Maintenance terlebih dahulu selain menyediakan ruangnya.
- Jangan menghapus fitur scroll yang sudah ada.
- Prioritaskan ketepatan spatial layout dan camera composition daripada dekorasi berlebihan.

==================================================
1. WORLD COORDINATE DAN ARAH KAMERA
==================================================

Tetapkan sistem koordinat dunia secara konsisten:

+X = EAST
-X = WEST
-Z = NORTH
+Z = SOUTH

Arah kamera awal website adalah:
WEST (-X)

Artinya pada opening scene kamera melihat ke arah barat.

Posisi feature utama di dalam ruang besar:

1. Asset Management
   = SOUTH-EAST
   = (+X, +Z)

2. Maintenance / Service
   = NORTH-EAST
   = (+X, -Z)

3. Depreciation
   = SOUTH-WEST
   = (-X, +Z)

4. Monitoring
   = NORTH-WEST
   = (-X, -Z)

Jangan mengubah hubungan geografis ini.

Gunakan sistem koordinat tersebut sebagai dasar semua camera waypoint dan object placement berikutnya.

==================================================
2. PERBESAR ENVIRONMENT
==================================================

Ruangan saat ini masih terasa terlalu kecil untuk camera choreography.

Perbesar ruangan lagi.

Targetnya bukan memperbesar semua object secara tidak proporsional, tetapi memberikan ruang antar-feature sehingga kamera dapat bergerak dengan nyaman.

Gunakan konsep:

- large modern office / asset management office
- open-plan office
- cukup luas untuk beberapa feature station
- terdapat area kosong untuk camera movement
- feature station tidak saling bertumpuk
- setiap feature memiliki ruang visual sendiri

Jika ukuran room sebelumnya sekitar 22 x 16, boleh diperbesar lagi sekitar 1.3x–1.5x jika diperlukan.

Jangan terpaku pada angka tersebut.
Prioritaskan:
- camera distance
- camera turning radius
- object visibility
- clear separation antar feature

==================================================
3. BUAT ENVIRONMENT JAUH LEBIH DETAIL
==================================================

Scene jangan lagi terasa seperti kumpulan object yang diletakkan di ruang kosong.

Buat environment seperti kantor sungguhan.

Tambahkan secara procedural dengan Three.js:

FLOOR:
- lantai kantor
- material tile / concrete / vinyl yang sederhana
- pattern atau panel lantai halus
- jangan terlalu noisy

WALL:
- dinding
- baseboard
- beberapa panel dekoratif
- material berbeda antara dinding dan lantai

CEILING:
- ceiling slab / ceiling panel
- lampu kantor
- beberapa ceiling light
- jangan membuat ceiling terlalu gelap

OFFICE ELEMENTS:
- meja kerja
- kursi
- lemari
- rak
- storage cabinet
- beberapa tanaman indoor
- beberapa monitor
- kabel sederhana
- lampu
- whiteboard / wall panel bila diperlukan

Gunakan low-poly / stylized realistic geometry.

Jangan membuat terlalu banyak detail kecil yang tidak terlihat kamera.

Prioritas:
1. silhouette
2. material
3. lighting
4. spatial depth
5. detail kecil

Scene harus terlihat seperti satu kantor yang benar-benar memiliki ruang, bukan sekumpulan demo object.

==================================================
4. KONSEP ASSET MANAGEMENT AREA
==================================================

Area Asset Management berada di:

SOUTH-EAST
(+X, +Z)

Buat area ini berbeda dari area kantor biasa.

Konsepnya adalah:

"OPEN ASSET STORAGE / ASSET MANAGEMENT AREA"

Bayangkan ruang penyimpanan aset perusahaan yang terbuka.

Di area tersebut terdapat beberapa aset fisik:
- laptop
- projector
- monitor
- beberapa perangkat elektronik kantor
- box / equipment
- storage rack bila diperlukan

Jangan menaruh semua aset secara acak.

Buat komposisi seperti area inventory/showroom kecil.

==================================================
5. MEJA MELINGKAR / CURVED TABLE ARRANGEMENT
==================================================

Area asset management dikelilingi meja yang membentuk susunan melingkar / curved arrangement.

Bukan satu meja lurus biasa.

Buat beberapa meja modular yang jika dilihat dari atas membentuk:
- lingkaran
atau
- oval / U-shaped curved arrangement

Tujuannya agar area tengah dapat menjadi open storage/display area.

Contoh konsep:

                 TABLE
            ╭──────────╮
         ╭──╯          ╰──╮
       TABLE              TABLE
       │                    │
       │   ASSET STORAGE    │
       │                    │
       TABLE              TABLE
         ╰──╮          ╭──╯
            ╰──────────╯

Tidak harus benar-benar berupa lingkaran sempurna.

Yang penting terlihat sebagai satu area asset management.

==================================================
6. CAMERA SHOT — ASSET MANAGEMENT
==================================================

Camera awal website:

menghadap WEST.

Saat scroll bergerak menuju bagian Asset Management:

kamera bergerak menuju sisi WEST dari area Asset Management.

PENTING:
Kamera jangan berhenti di tengah area.

Target akhir camera shot pertama adalah:

MEJA BAGIAN WEST dari area Asset Management.

Di atas meja tersebut terdapat:

PROJECTOR
+
QR CODE

Projector menggantikan laptop QR yang digunakan pada versi scene sebelumnya.

Komposisi akhir:

- projector menjadi focal point
- QR terlihat jelas
- meja terlihat cukup untuk memberikan konteks
- area asset storage masih sedikit terlihat sebagai background
- jangan terlalu close-up
- jangan sampai projector memenuhi seluruh layar
- sisakan ruang untuk floating application preview

Dari POV kamera:

PROJECTOR / QR harus menjadi primary visual.

==================================================
7. PROJECTOR + QR
==================================================

Buat projector kantor yang cukup realistis tetapi tetap stylized.

Projector:
- body
- lens
- beberapa tombol/detail
- ukuran masuk akal terhadap meja

Tambahkan QR code pada bagian projector yang mudah terlihat dari kamera.

QR harus benar-benar terlihat sebagai QR.

Tidak perlu QR terlalu besar.

QR adalah identifier aset.

==================================================
8. FLOATING APPLICATION PREVIEW
==================================================

Saat camera sudah mencapai Asset Management shot:

munculkan floating screen di sekitar projector.

Floating screen harus terasa seperti holographic / floating UI panel.

Jangan langsung muncul sejak opening.

Timeline:

camera masih jauh
→ floating screen invisible

camera mendekati Asset Management
→ floating screen mulai fade in

camera mencapai final Asset Management shot
→ floating screen fully visible

camera mulai meninggalkan Asset Management
→ floating screen fade out

PENTING:
floating screen harus reusable karena nanti akan digunakan juga pada feature lain.

Buat komponen/function reusable seperti:

createFloatingScreen()
showFloatingScreen()
hideFloatingScreen()
updateFloatingScreen()

Jangan membuat logic floating screen terpisah dan hardcoded untuk setiap feature.

==================================================
9. FLOATING SCREEN CONTENT
==================================================

Floating screen pertama menampilkan preview aplikasi Assetrack.

Referensi visual:

Saya memberikan dua gambar sebagai referensi.

Gambar pertama:
adalah tampilan floating screen yang saat ini sudah ada di scene.

Gambar kedua:
adalah tampilan aplikasi "Detail Aset" yang ingin direpresentasikan.

Gunakan gambar kedua sebagai REFERENSI VISUAL, bukan sebagai image yang harus langsung ditempel sebagai texture.

Jangan sekadar memasukkan screenshot penuh sebagai texture jika tidak diperlukan.

Lebih baik buat ulang UI secara sederhana menggunakan:

THREE.CanvasTexture

atau sistem 2D texture ringan yang cocok dengan Three.js.

Tujuannya:
- lebih ringan
- resolusi dapat dikontrol
- tidak bergantung pada file screenshot
- dapat dianimasikan
- nantinya dapat digunakan kembali untuk screen lain

Gunakan resolusi texture yang wajar, misalnya:
512 x 768
atau resolusi lain yang cukup untuk keterbacaan.

Jangan menggunakan resolusi 2K/4K untuk UI kecil.

==================================================
10. DETAIL FLOATING UI ASSET MANAGEMENT
==================================================

Floating screen harus merepresentasikan aplikasi Detail Asset.

Tidak perlu menyalin seluruh screenshot secara pixel-perfect.

Yang penting visual hierarchy-nya jelas:

Header:
"Detail Aset"

Asset:
"Lenovo terbaru"

Status:
"Perawatan"

Section:
"Informasi Aset"

Beberapa card informasi:

- Tanggal Pembelian
- Harga
- Lokasi
- Serial Number
- Jadwal Maintenance
- Ekspektasi Umur Aset
- Kategori Detail
- Nilai Saat Ini

Kemudian:
Asset Tag
AST-93

dan bagian QR di bawahnya.

Gunakan layout yang mirip referensi tetapi sederhanakan jika diperlukan.

Text harus tetap terbaca ketika floating screen dilihat dari camera.

==================================================
11. FLOATING SCREEN SCALE DAN POSITION
==================================================

Floating screen tidak boleh menutupi projector.

Komposisi:

              FLOATING SCREEN
             ┌──────────────┐
             │ Detail Asset │
             │              │
             │ Asset info   │
             │              │
             └──────────────┘

                 PROJECTOR
              ┌────────────┐
              │    QR      │
              └────────────┘

Floating screen sedikit berada:
- di atas
- atau di belakang/samping projector

Tetapi tetap terlihat sebagai satu visual group.

Gunakan sedikit tilt/perspective supaya terasa berada di dunia 3D.

Jangan membuat screen selalu menghadap kamera secara billboard jika itu membuatnya terasa seperti UI 2D yang ditempel di layar.

Lebih baik memiliki orientation 3D yang konsisten dengan environment.

==================================================
12. ASSET MANAGEMENT EXIT
==================================================

Saat scroll bergerak menjauh dari Asset Management:

floating screen harus hilang.

Urutannya:

Asset Management final shot
→ camera mulai bergerak menjauh
→ floating screen fade out
→ screen invisible
→ camera melanjutkan perjalanan ke Asset Borrowing

Jangan membuat floating screen tetap berada di scene setelah camera meninggalkan area.

Ini adalah aturan GLOBAL:

SETIAP FLOATING APPLICATION SCREEN DI MASA DEPAN HARUS:
- muncul ketika camera mencapai feature
- tetap terlihat selama feature shot
- menghilang ketika camera meninggalkan feature

Buat mekanismenya reusable.

==================================================
13. ASSET BORROWING AREA
==================================================

Asset Borrowing berada di area:

SOUTH-EAST juga,
tetapi berada di bagian yang berbeda dari Asset Management.

Jangan meletakkan borrowing di tengah ruangan besar seperti scene lama.

Buat sebagai bagian lain dari curved asset-management workspace.

Pada meja bagian NORTH dari area Asset Management:

letakkan:

LAPTOP
+
QR CODE

Laptop harus berada di atas meja dan QR terlihat jelas.

==================================================
14. EMPLOYEE + TABLET
==================================================

Di dekat laptop terdapat seorang employee.

Employee:
- berdiri / sedikit membungkuk ke arah laptop
- tangan kanan memegang tablet
- tablet menghadap ke arah camera
- tangan kiri natural

PENTING:
tablet harus berada di TANGAN KANAN.

Jangan membuat tablet berada di tangan kiri.

Posisi tubuh harus natural dan tidak menutupi laptop.

Komposisi yang diinginkan:

              TABLET
             ┌───────┐
             │ SCAN  │
             └───────┘
                  \
                   \ employee
                    \
                  LAPTOP
                 ┌──────┐
                 │  QR  │
                 └──────┘

Camera berada sedikit di belakang/samping employee sehingga:
- tablet terlihat
- laptop terlihat
- QR laptop terlihat
- employee tidak memenuhi foreground

==================================================
15. CAMERA SHOT — ASSET BORROWING
==================================================

Setelah Asset Management:

camera meninggalkan projector/floating screen.

Floating screen Asset Management fade out.

Camera bergerak menuju:

NORTH TABLE
di area Asset Management / Asset Borrowing.

Camera tidak perlu melakukan vertical rotation ekstrem.

Gerakan harus terasa natural sebagai perpindahan camera di dalam kantor.

Final composition:

TABLET
+
LAPTOP QR
+
EMPLOYEE

ketiganya harus terlihat.

Jangan terlalu dekat sampai kepala employee memenuhi layar.

==================================================
16. ANIMASI SCANNING PADA TABLET
==================================================

Ketika camera belum mencapai Asset Borrowing:

tablet berada dalam state normal.

Ketika camera mencapai threshold feature:

mulai animasi scanning.

State:

IDLE
→ SCANNING
→ BORROW FORM

Buat state machine sederhana.

Contoh:

tabletState = "idle"

ketika cameraProgress masuk area Asset Borrowing:
tabletState = "scanning"

setelah animation selesai:
tabletState = "borrow-form"

Jangan menjalankan animasi scanning terus-menerus sejak page load.

Animasi hanya aktif ketika feature sudah dicapai.

==================================================
17. TAMPILAN SCAN PADA TABLET
==================================================

Tablet awalnya menampilkan UI scanning.

Buat UI menggunakan CanvasTexture seperti floating screen.

Contoh:

┌─────────────────────┐
│     Scan Asset      │
│                     │
│       ┌─────┐       │
│       │ QR  │       │
│       │     │       │
│       └─────┘       │
│                     │
│   Scanning...       │
│       ───────       │
└─────────────────────┘

Tambahkan scanning animation:

horizontal scanning line
atau
animated scanner frame.

Animasi harus sederhana dan ringan.

Tidak perlu video.

==================================================
18. SETELAH SCAN BERHASIL
==================================================

Setelah beberapa detik scanning:

tablet UI berubah menjadi:

BORROW ASSET FORM

Transisi:

SCANNING
    ↓
QR detected
    ↓
short transition
    ↓
BORROW FORM

Contoh UI:

┌─────────────────────┐
│   Pinjam Aset       │
│                     │
│ Asset               │
│ Lenovo ThinkPad     │
│                     │
│ Asset ID            │
│ AST-001             │
│                     │
│ Peminjam            │
│ Rizal               │
│                     │
│ Tanggal              │
│ 27/09/2026          │
│                     │
│ [ Ajukan Peminjaman ]│
└─────────────────────┘

Tidak perlu benar-benar mengirim form.

Ini adalah visual demonstration.

==================================================
19. TABLET SCREEN IMPLEMENTATION
==================================================

Jangan menggunakan screenshot aplikasi penuh.

Gunakan CanvasTexture sederhana seperti floating screen.

Buat satu reusable system:

createDeviceScreen()
setDeviceScreenState()

State:

"idle"
"scanning"
"borrow-form"

Dengan demikian nanti kita bisa menambahkan state lain dengan mudah.

==================================================
20. SCROLL CONTROL
==================================================

Pastikan scroll menjadi sumber utama camera progression.

Jangan menggunakan auto camera movement.

Konsep:

scroll progress
      ↓
camera path
      ↓
feature threshold
      ↓
floating screen state
      ↓
tablet animation state

Buat threshold yang jelas.

Contoh konseptual:

0.00–0.20
Overview

0.20–0.38
Approach Asset Management

0.38–0.52
Asset Management final shot
→ floating screen visible

0.52–0.65
Leave Asset Management
→ floating screen fade out

0.65–0.80
Approach Asset Borrowing

0.80–0.95
Asset Borrowing final shot
→ tablet scan animation
→ borrow form

Angka tersebut hanya contoh.
Sesuaikan dengan panjang scroll dan camera path yang sudah ada.

==================================================
21. CAMERA COMPOSITION RULE
==================================================

Ini sangat penting.

Jangan menentukan endpoint hanya berdasarkan:

camera x/y/z.

Setiap feature harus dievaluasi berdasarkan apa yang terlihat di layar.

Asset Management final shot:
- projector = primary
- QR = visible
- floating screen = secondary
- storage area = background

Asset Borrowing final shot:
- tablet = primary
- laptop QR = secondary
- employee = supporting object
- tidak ada kepala/tubuh yang memenuhi foreground

Jangan membuat camera terlalu dekat dengan object.

Sisakan ruang visual.

==================================================
22. JANGAN MEMBUAT FLOATING SCREEN BILLBOARD SECARA SEMBARANGAN
==================================================

Floating screen harus terasa sebagai bagian dari 3D environment.

Jika menggunakan lookAt(camera), gunakan dengan hati-hati.

Prioritaskan:
- consistent perspective
- correct scale
- slight rotation
- depth
- shadow/glow yang ringan

Jangan sampai terlihat seperti HTML overlay 2D yang ditempel di viewport.

==================================================
23. PERFORMANCE
==================================================

Karena scene akan semakin besar:

- gunakan geometry sederhana
- reuse geometry/material jika memungkinkan
- gunakan instancing untuk object berulang
- jangan membuat texture resolusi besar
- CanvasTexture UI maksimal sekitar 512–768 px untuk screen kecil
- jangan load screenshot besar sebagai texture jika tidak diperlukan
- jangan menambah library baru jika tidak diperlukan

Floating screen dan tablet screen harus menggunakan reusable CanvasTexture system.

==================================================
24. LIGHTING
==================================================

Buat pencahayaan kantor yang lebih baik:

- ambient light
- directional light / area-like lighting
- ceiling lights
- sedikit accent lighting pada feature station

Pastikan:
- laptop tidak terlalu gelap
- projector dan QR terlihat
- tablet screen terlihat
- floating screen memiliki sedikit glow
- tetapi jangan sampai glow terlalu kuat

==================================================
25. IMPLEMENTASI BERTAHAP
==================================================

Kerjakan dalam urutan berikut:

STEP 1
Perbesar room dan perbaiki environment dasar.

STEP 2
Buat floor, wall, ceiling, ceiling lights, meja, kursi, storage, dan office props.

STEP 3
Buat Asset Management area di SOUTH-EAST.

STEP 4
Buat curved/circular table arrangement.

STEP 5
Buat asset storage/display area.

STEP 6
Buat projector + QR di WEST table.

STEP 7
Buat floating application screen system.

STEP 8
Implementasikan Detail Asset UI pada floating screen.

STEP 9
Implementasikan appearance/disappearance floating screen berdasarkan scroll.

STEP 10
Buat laptop + QR pada NORTH table.

STEP 11
Buat employee dengan tablet di tangan kanan.

STEP 12
Buat tablet CanvasTexture.

STEP 13
Implementasikan:
idle → scanning → borrow-form.

STEP 14
Atur camera endpoint Asset Management.

STEP 15
Atur camera endpoint Asset Borrowing.

STEP 16
Test scroll dari:
Overview
→ Asset Management
→ keluar Asset Management
→ Asset Borrowing.

==================================================
26. JANGAN DULU
==================================================

Untuk tahap ini JANGAN:

- menyelesaikan Maintenance
- menyelesaikan Depreciation
- menyelesaikan Monitoring
- menyelesaikan Audit Trail
- menambah terlalu banyak karakter
- menambah animasi karakter kompleks
- menambah physics
- menambah particle berlebihan

Sisakan ruang untuk feature tersebut.

==================================================
27. HASIL AKHIR YANG DIHARAPKAN
==================================================

Saat user membuka website:

kamera menghadap WEST.

Terlihat:
- kantor besar
- area kerja
- beberapa feature station
- Asset Management di SOUTH-EAST
- Maintenance di NORTH-EAST
- Depreciation di SOUTH-WEST
- Monitoring di NORTH-WEST

Ketika scroll:

OVERVIEW
↓
camera bergerak menuju SOUTH-EAST
↓
masuk Asset Management
↓
camera mendekati WEST table
↓
terlihat projector + QR
↓
floating Detail Asset UI muncul
↓
user melihat preview aplikasi
↓
scroll dilanjutkan
↓
floating UI menghilang
↓
camera bergerak menuju NORTH table
↓
terlihat laptop + QR
↓
employee dengan tablet tangan kanan terlihat
↓
camera berhenti pada composition yang memperlihatkan tablet + laptop
↓
tablet mulai scanning
↓
QR detected
↓
tablet berubah menjadi Borrow Asset Form

HASIL YANG DIINGINKAN BUKAN SEKADAR:
"semua object ada."

Tetapi:
"camera storytelling menjelaskan fitur Assetrack."

==================================================
28. VALIDASI SETELAH IMPLEMENTASI
==================================================

Setelah selesai:

1. Jalankan website.
2. Test scroll dari awal sampai Asset Management.
3. Pastikan camera awal benar-benar menghadap WEST.
4. Pastikan Asset Management berada di SOUTH-EAST.
5. Pastikan projector berada di WEST table.
6. Pastikan QR terlihat.
7. Pastikan floating screen muncul hanya ketika mendekati/berada di Asset Management.
8. Pastikan floating screen menghilang ketika meninggalkan area.
9. Pastikan laptop + QR berada di NORTH table.
10. Pastikan tablet berada di tangan kanan.
11. Pastikan tablet dapat menampilkan scanning animation.
12. Pastikan scanning berubah menjadi Borrow Form.
13. Pastikan camera tidak terlalu dekat dengan manusia.
14. Pastikan tidak ada vertical camera rotation yang tidak diinginkan.
15. Pastikan tidak ada object yang keluar dari framing secara tiba-tiba.

Jika ada masalah, prioritaskan perbaikan:
CAMERA COMPOSITION > OBJECT PLACEMENT > ANIMATION > DECORATION.

Jangan hanya melaporkan bahwa implementasi selesai.
Lakukan pengecekan hasil render/browser dan perbaiki masalah visual yang ditemukan.