######################################
Panduan Pengguna Codeigniter Indonesia
######################################

.. image:: https://travis-ci.org/codeigniter-id/user-guide.svg?branch=master
    :target: https://travis-ci.org/codeigniter-id/user-guide

******************
Panduan Persiapan
******************

Panduan penggunaan Codeigniter menggunakan Sphinx untuk mengelola dokumentasi dan
menghasilkan ke berbagai macam format. Setiap halaman ditulis dalam
`ReStructured Text <http://sphinx.pocoo.org/rest.html>`_ *human-readable* format.

*************
Prasyarat
*************
Sphinx membutuhkan Python, yang sudah terinstall jika Anda menggunakan OS X.
Anda dapat mengkonfirmasi di *terminal window* dengan menjalankan perintah ``python``
tanpa parameter apapun. Jika Python telah terinstall, maka akan muncul versi Phython
yang Anda gunakan di `Terminal window`. Jika versi Python Anda bukan 2.7+, maka kunjungi
http://python.org/download/releases/2.7.2/ dan install versi 2.7.2

************
Instalasi
************

1. Install `easy_install <http://peak.telecommunity.com/DevCenter/EasyInstall#installing-easy-install>`_
2. Jalankan perintah ``easy_install "sphinx==1.2.3"``
3. Lalu, jalankan perintah ``easy_install sphinxcontrib-phpdomain``
4. Install CI Lexer untuk PHP, HTML, CSS, and JavaScript *syntax highlighting* di contoh (lihat di ``cilexer/README``)
5. Jalankan perintah ``cd user_guide_src``
6. Terakhir, jalankan perintah ``make html``

********************************
Mengubah dan Membuat Dokumentasi
********************************

Semua sumber file berada di dalam folder ``source/`` dan di folder itulah Anda akan menambahkan
dokumentasi baru atau memodifikasi dokumentasi yang ada. Sama seperti dengan mengubah kode,
kami sarankan Anda bekerja dari branch ``feature`` dan membuat ``pull request`` ke repository ini.

*******************
Dimanakah HTML nya?
*******************

*Generate* file HTML sangat simple. Dari *root directory* repository ini, Anda cukup
menjalankan perintah::

    make html

Anda akan melihat proses *compile* yang nanti akan otomatis membuat folder
``build/html`` dan menyimpan file-file HTML ke folder tersebut. Jika file HTML telah dibuat
dan jika Anda ingin *generate* file HTML yang baru, setiap kali proses *generate* berhasil
hanya *generate* ulang file yang diubah untuk menghemat waktu.
Jika Anda ingin *reset* file HTML Anda, cukup hapus folder ``build`` dan *generate* ulang seperti proses sebelumnya.

***************
Panduan Styling
***************

Silahkan lihat ``source/documentation/index.rst`` untuk panduan umum tentang
menggunakan Sphinx untuk dokumentasi Codeigniter.