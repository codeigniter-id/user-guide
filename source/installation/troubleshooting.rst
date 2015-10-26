####################
Penyelesaian Masalah
####################

Jika Anda menemukan bahwa tidak peduli apa yang Anda masukkan ke dalam URL Anda hanya
default halaman Anda yang sedang di *load*, mungkin server Anda tidak mendukung
variabel REQUEST_URI yang dibutuhkan untuk melayani URL *search-engine friendly*. Sebagai
langkah pertama, buka file ``application/config/config.php`` Anda dan cari
informasi *URI Protocol*. Ini akan menyarankan Anda mencoba beberapa
pengaturan alternatif. Jika masih tidak bekerja setelah Anda sudah mencoba ini,
Anda harus memaksa CodeIgniter untuk menambahkan tanda tanya ke URL Anda. Untuk
melakukan hal ini, buka file **application/config/config.php** Anda dan ubah bagian ini::

	$config['index_page'] = "index.php";

Menjadi ini::

	$config['index_page'] = "index.php?";
