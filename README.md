Logo Lapisan Eigen
Dokumen EigenLayer
Mencari
ctrl
K
Panduan OperatorInstalasi

Di halaman ini
Instalasi
 Operator Node
 Perangkat Lunak
Docker: Pastikan Docker diinstal pada sistem Anda. Untuk mengunduh Docker, ikuti instruksi yang tercantum di sini .
Docker Compose: Pastikan Docker Compose juga diinstal dan dikonfigurasi dengan benar. Untuk mengunduh Docker Compose, ikuti instruksi yang tercantum di sini .
Lingkungan Linux: EigenLayer hanya didukung di Linux. Pastikan Anda memiliki lingkungan Linux, seperti Docker, untuk instalasi.
Jika Anda memilih untuk menginstal eigenlayer-cli menggunakan bahasa pemrograman Go, pastikan Anda telah menginstal Go, versi 1.21 atau lebih tinggi. Anda dapat menemukan panduan instalasi di sini .
Memeriksa 
Pada sistem Linux asli, Anda dapat menggunakan perintah lsb_release -a untuk mendapatkan informasi tentang distribusi Linux Anda.

Periksa Docker Jika Anda tidak menggunakan sistem Linux asli dan ingin menggunakan EigenLayer, Anda dapat memeriksa apakah Docker sudah diinstal:

Buka terminal atau prompt perintah.
Jalankan perintah berikut untuk memeriksa apakah Docker diinstal dan dijalankan:css
docker --version

Jika Docker diinstal dan dijalankan, EigenLayer dapat digunakan dalam container Docker, yang menyediakan lingkungan Linux.

Dengan mengikuti langkah-langkah ini, Anda dapat menentukan apakah Anda memiliki lingkungan Linux yang sesuai untuk instalasi EigenLayer.

Instal CLI menggunakan 
Untuk mengunduh biner untuk rilis terbaru, jalankan:

curl -sSfL https://raw.githubusercontent.com/layr-labs/eigenlayer-cli/master/scripts/install.sh | sh -s


Biner akan dipasang di dalam ~/bindirektori.

Untuk menambahkan biner ke jalur Anda, jalankan:

export PATH=$PATH:~/bin

Menginstal di 
Untuk mengunduh biner di lokasi khusus, jalankan:

curl -sSfL https://raw.githubusercontent.com/layr-labs/eigenlayer-cli/master/scripts/install.sh | sh -s -- -b <custom_location>


Instal CLI menggunakan 
Sekarang kita akan menginstal eigenlayer-CLI menggunakan Go. Perintah berikut akan menginstal executable eigenlayer bersama dengan perpustakaan dan dependensinya di sistem Anda.

go install github.com/Layr-Labs/eigenlayer-cli/cmd/eigenlayer@latest

Untuk memeriksa apakah GOBIN tidak ada di PATH Anda, Anda dapat mengeksekusi echo $GOBINdari Terminal. Jika tidak mencetak apa pun, maka itu tidak ada di PATH Anda. Untuk menambahkan GOBIN ke PATH Anda, tambahkan baris berikut ke $HOME/.profile Anda:

export GOBIN=$GOPATH/bin
export PATH=$GOBIN:$PATH

Perubahan yang dilakukan pada file profil mungkin tidak berlaku hingga Anda masuk lagi ke komputer Anda. Untuk segera menerapkan perubahan, jalankan perintah shell secara langsung atau jalankan dari profil menggunakan perintah seperti source $HOME/.profile.

Instal CLI dari 
Untuk melakukan metode instalasi ini Anda harus memiliki Go. Harap pastikan bahwa Anda menginstal Go dengan versi minimum 1.21 di sini .

Dengan metode ini, Anda menghasilkan biner secara manual, mengunduh dan mengkompilasi kode sumber.

git clone https://github.com/Layr-Labs/eigenlayer-cli.git
cd eigenlayer-cli
mkdir -p build
go build -o build/eigenlayer cmd/eigenlayer/main.go

atau jika Anda sudah menginstal :

git clone https://github.com/Layr-Labs/eigenlayer-cli.git
cd eigenlayer
make build

Eksekusinya akan ada di folder build.

Jika Anda menginginkan biner di PATH Anda (atau jika Anda menggunakan metode Go dan tidak memiliki $GOBIN di PATH Anda), silakan salin biner tersebut ke /usr/local/bin:

Buat dan Daftar 
Pasangan kunci ECDSA sesuai dengan alamat operator Ethereum dan kunci untuk berinteraksi dengan Eigenlayer. Kunci BLS digunakan untuk tujuan pengesahan dalam protokol EigenLayer. Hanya 1 kunci BLS yang dapat didaftarkan per entitas Operator di EigenLayer. Hanya 1 kunci BLS yang boleh dipasangkan dengan 1 kunci ECDSA saja dan sebaliknya.

Ada hubungan tetap 1 banding 1 antara kunci ECDSA dan kunci BLS. Anda tidak dapat menggunakan kembali kunci apa pun dengan jenis kunci lainnya. Setelah terdaftar, Anda tidak dapat mengubah kunci BLS yang terkait dengan kunci ECDSA.

Buat 
Hasilkan kunci ECDSA dan BLS terenkripsi menggunakan CLI:

eigenlayer operator keys create --key-type ecdsa [keyname]
eigenlayer operator keys create --key-type bls [keyname]

[keyname]- Ini akan menjadi nama file kunci yang dibuat. Itu akan disimpan sebagai <keyname>.ecdsa.key.jsonatau <keyname>.bls.key.json.
Ini akan meminta kata sandi yang dapat Anda gunakan untuk mengenkripsi kunci. Kunci akan disimpan di disk lokal dan akan ditampilkan setelah kunci dibuat. Ini juga akan menampilkan kunci pribadi hanya sekali, sehingga Anda dapat mencadangkannya jika Anda kehilangan kata sandi atau file kunci.

 Masukan
eigenlayer operator keys create --key-type ecdsa test

Alat ini meminta kata sandi untuk mengenkripsi kunci pribadi ECDSA untuk tujuan keamanan. Input kata sandi disembunyikan untuk alasan keamanan.

? Enter password to encrypt the ecdsa private key:
ECDSA Private Key (Hex):  b3eba201405d5b5f7aaa9adf6bb734dc6c0f448ef64dd39df80ca2d92fca6d7b
Please backup the above private key hex in safe place.

Key location: /home/ubuntu/.eigenlayer/operator_keys/test.ecdsa.key.json
Public Key hex:  f87ee475109c2943038b3c006b8a004ee17bebf3357d10d8f63ef202c5c28723906533dccfda5d76c1da0a9f05cc6d32085ca1af8aaab5a28171474b1ad0aa68
Ethereum Address 0x6a8c0D554a694899041E52a91B4EC3Ff23d8aBD5



Impor 
Anda dapat mengimpor kunci ECDSA dan BLS yang ada menggunakan CLI, yang diperlukan untuk pendaftaran operator dan operasi on-chain lainnya. Ini berguna jika Anda sudah memiliki alamat yang ingin Anda gunakan sebagai operator.

Untuk mengimpor kunci ECDSA, gunakan perintah: eigenlayer operator keys import --key-type ecdsa [keyname] [privatekey].

Untuk mengimpor kunci BLS, gunakan perintah: eigenlayer operator keys import --key-type bls [keyname] [privatekey].

[keyname]adalah nama file kunci yang diimpor, dan akan disimpan sebagai <keyname>.ecdsa.key.jsonatau <keyname>.bls.key.json.
privatekeyadalah kunci pribadi dari kunci yang ingin Anda impor.
Untuk kunci BLS, jumlahnya harus besar.
Untuk kunci ECDSA, harus dalam format hex.
 Masukan
Bagian dari perintah ini memberi tahu alat EigenLayer bahwa Anda ingin mengimpor kunci.

eigenlayer operator keys import --key-type ecdsa test 6842fb8f5fa574d0482818b8a825a15c4d68f542693197f2c2497e3562f335f6


Ini adalah permintaan yang meminta Anda memasukkan kata sandi untuk mengenkripsi kunci pribadi ECDSA.

? Enter password to encrypt the ecdsa private key: *******
ECDSA Private Key (Hex):  6842fb8f5fa574d0482818b8a825a15c4d68f542693197f2c2497e3562f335f6
Please backup the above private key hex in safe place.

Key location: /home/ubuntu/.eigenlayer/operator_keys/test.ecdsa.key.json
Public Key hex:  a30264c19cd7292d5153da9c9df58f81aced417e8587dd339021c45ee61f20d55f4c3d374d6f472d3a2c4382e2a9770db395d60756d3b3ea97e8c1f9013eb1bb
Ethereum Address 0x9F664973BF656d6077E66973c474cB58eD5E97E1



Ini akan memulai permintaan kata sandi yang dapat Anda gunakan untuk mengenkripsi kunci. Kunci akan disimpan di disk lokal Anda dan akan ditampilkan setelah dibuat.

Kunci pribadi juga hanya akan ditampilkan satu kali, sehingga Anda dapat membuat cadangan jika Anda lupa kata sandi atau kehilangan file kunci.

Daftar 
Ini adalah perintah yang dapat Anda gunakan untuk mengambil daftar kunci yang telah Anda buat dengan alat cli EigenLayer.

eigenlayer operator keys list

Saat Anda menjalankan perintah daftar kunci operator Eigenlayer, ini akan menampilkan daftar semua kunci yang dihasilkan menggunakan perintah khusus ini, bersama dengan kunci publik terkait.

Informasi ini dapat berguna untuk mengelola dan mengidentifikasi kunci yang Anda buat. Kunci publik biasanya digunakan untuk enkripsi, otentikasi, dan verifikasi tanda tangan digital.

Ekspor 
Jika Anda ingin melihat kunci pribadi dari kunci yang ada, Anda dapat menggunakan perintah di bawah ini. Ini hanya akan berfungsi jika kunci Anda berada di lokasi default ( ~/.eigenlayer/operator_keys)

eigenlayer operator keys export --key-type ecdsa [keyname]

Ini juga akan meminta kata sandi yang digunakan untuk mengenkripsi kunci.

Jika kunci Anda tidak berada di lokasi default, Anda dapat memberikan jalur lengkap ke file kunci menggunakan tanda --key-path. Anda tidak perlu memberikan nama kunci dalam hal ini.

eigenlayer operator keys export --key-type ecdsa --key-path [path]

Dana 
Langkah 1: Ikuti instruksi di Mendapatkan Testnet ETH untuk mendanai dompet web3 dengan Goerli ETH.

Langkah 2: Kirim setidaknya 1 Goerli ETH ke kolom “alamat” yang direferensikan di file operator-config.yaml Anda. ETH ini akan digunakan untuk menutupi biaya bahan bakar untuk pendaftaran operator pada langkah selanjutnya.

 Operator
 Konfigurasi
Anda dapat membuat file konfigurasi yang diperlukan untuk registrasi operator menggunakan perintah di bawah ini:

eigenlayer operator config create

Saat dimintai alamat operator, pastikan alamat operator Anda sama dengan alamat kunci ecdsa yang Anda buat/impor pada langkah pembuatan kunci.

Ini akan membuat dua file: operator.yamldan metadata.jsonSetelah mengisi detailnya metadata.json, harap unggah ini ke lokasi yang dapat diakses publik dan isi url itu di operator.yaml. Url metadata yang valid diperlukan agar pendaftaran berhasil. Contoh file operator.yaml disediakan untuk referensi Anda di sini: operator.yaml .

Url metadata publik diperlukan untuk mendaftarkan operator. Setelah memperbarui metadata.jsonfile, Anda harus mengunggahnya ke lokasi yang dapat diakses publik dan menambahkan url publik tersebut ke operator.yamlfile Anda. Anda juga diharuskan mengunggah gambar operator ke lokasi yang dapat diakses publik dan memberikan url di file metadata. Registrasi operator hanya mendukung .pnggambar untuk saat ini.

PERINGATAN
Harap pastikan bahwa metadata.jsonfile dihosting di lokasi yang dapat diakses publik. Parameter metadata_url dalam konfigurasi operator harus dapat diakses publik agar pendaftaran berhasil. Saat menggunakan Github untuk menghosting file ini, pastikan Anda menautkan ke file mentah ( contoh ), bukan URL repo github ( contoh ).

CLI EigenLayer memerlukan akses ke node Ethereum RPC untuk memposting pendaftaran. Harap rencanakan untuk memanfaatkan penyedia node RPC atau jalankan node RPC lokal Anda sendiri untuk referensi di operator-config.yaml.

Contoh daftar penyedia tersedia di sini untuk referensi Anda. Anda dapat menemukannya menggunakan Chainlist Goerli .

 kontrak Goerli Smart
Untuk pendaftaran operator di lingkungan Goerli, Anda perlu mengatur kontrak ringkasan kunci publik Slasher dan BLS sebagai berikut.
Operator CLI memerlukan dua set kunci (ECDSA dan BLS) untuk dua tujuan berbeda. Untuk ECDSA, ini adalah alamat Operator Ethereum dan kunci untuk berinteraksi dengan Eigenlayer. Untuk kunci BLS, ini adalah kunci yang digunakan untuk pengesahan pada EigenLayer.

Alamat Kontrak Pemotong:0xD11d60b669Ecf7bE10329726043B3ac07B380C22

Alamat Kontrak Kompendium Kunci Publik BLS:0xc81d3963087Fe09316cd1E032457989C7aC91b19

# EigenLayer Slasher contract address
# This will be provided by EigenLayer team
el_slasher_address: 0xD11d60b669Ecf7bE10329726043B3ac07B380C22

# Address of BLS Public Key Compendium contract
# This will be provided by EigenLayer team
bls_public_key_compendium_address: 0xc81d3963087Fe09316cd1E032457989C7aC91b19

 registrasi
Ini adalah perintah yang dapat Anda gunakan untuk mendaftarkan operator Anda.

Catatan: Kunci ECDSA dan BLS diperlukan untuk registrasi operator. Anda dapat memilih untuk membuat kumpulan kunci Anda sendiri menggunakan EigenLayer CLI (disarankan untuk pengguna pertama kali) atau mengimpor kunci yang ada (disarankan untuk pengguna tingkat lanjut yang sudah membuat kunci) seperti dijelaskan di bagian sebelumnya.

eigenlayer operator register operator.yaml

Memeriksa Status 
Ini adalah perintah yang dapat Anda gunakan untuk menanyakan status pendaftaran operator Anda.

eigenlayer operator status operator.yaml

 Metadata
Ini adalah perintah yang dapat Anda gunakan untuk melakukan perubahan atau pembaruan pada metadata operator Anda.

eigenlayer operator update operator.yaml
