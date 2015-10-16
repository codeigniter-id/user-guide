#################
Panduan Instalasi
#################

CodeIgniter diinstal dalam empat langkah:

#. Unzip paket.
#. Upload folder CodeIgniter dan file ke server Anda. Biasanya file ``index.php`` berada di *root folder* Anda.
#. Buka ``application/config/config.php`` dengan teks editor dan atur URL dasar Anda. Jika Anda berniat untuk menggunakan *encryption* atau *session*, atur *encryption key* Anda.
#. Jika Anda berniat untuk menggunakan database, buka file ``application/config/database.php`` dengan teks editor dan atur konfigurasi database Anda.

Jika Anda ingin meningkatkan keamanan aplikasi Anda dengan menyembunyikan lokasi
file CodeIgniter Anda, Anda dapat mengubah nama sistem dan folder aplikasi menjadi
sesuatu yang lebih pribadi. Jika Anda ingin mengubah namanya, Anda harus membuka
file index.php di *root folder* dan mengatur variabel ``$system_path`` dan variabel ``$application_folder``
dengan nama baru yang Anda sukai.

Untuk keamanan yang terbaik, baik sistem dan folder aplikasi
harus ditempatkan di atas *web root* sehingga mereka tidak langsung dapat diakses
melalui browser. Secara default, file .htaccess telah disertakan dalam setiap folder
untuk membantu mencegah akses langsung, tapi yang terbaik adalah dengan menghapus mereka dari akses publik
sepenuhnya dalam hal perubahan konfigurasi web server atau tidak mematuhi .htaccess.

Jika Anda ingin *views* Anda dapat diakses secara publik, Anda dapat memindahkan folder *views* dari folder aplikasi Anda.

Setelah memindah folder *views* Anda, buka file ``index.php`` utama Anda dan atur
variable ``$system_path``, ``$application_folder`` dan ``$view_folder``,
sebaiknya dengan path lengkap, misalnya ``'/www/MyUser/system'``.

Satu tambahan untuk lingkungan produksi adalah dengan menonaktifkan
*PHP error reporting* dan setiap fungsi *development-only* lainnya. Di
CodeIgniter, ini dapat dilakukan dengan menetapkan konstan ``ENVIRONMENT``, yang
lebih lengkap dijelaskan di :doc:`halaman Keamanan <../general/security>`.

That's it!

Jika Anda baru untuk CodeIgniter, silakan baca bagian :doc:`Memulai dengan Codeigniter <../overview/getting_started>`
dari Panduan Pengguna untuk mulai belajar bagaimana membangun aplikasi PHP yang dinamis. Selamat menikmati!

.. toctree::
	:hidden:
	:titlesonly:

	downloads
	self
	upgrading
	troubleshooting

