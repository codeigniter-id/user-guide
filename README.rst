######################################
Panduan Pengguna Codeigniter Indonesia
######################################

.. image:: https://img.shields.io/travis/codeigniter-id/user-guide/master.svg?style=flat-square
    :target: https://travis-ci.org/codeigniter-id/user-guide
.. image:: https://img.shields.io/badge/GITTER-join%20chat-green.svg?style=flat-square
    :target: https://gitter.im/codeigniter-id

******************
Panduan Persiapan
******************

Panduan penggunaan Codeigniter menggunakan Sphinx untuk mengelola dokumentasi dan
menghasilkan ke berbagai macam format. Setiap halaman ditulis dalam
`ReStructured Text <http://sphinx.pocoo.org/rest.html>`_ *human-readable* format.

*********
Prasyarat
*********

Sphinx membutuhkan Python, yang sudah terinstall jika Anda menggunakan OS X.
Anda dapat mengkonfirmasi di *terminal window* dengan menjalankan perintah ``python``
tanpa parameter apapun. Jika Python telah terinstall, maka akan muncul versi Python
yang Anda gunakan di `Terminal window`. Jika versi Python Anda bukan 2.7+, maka kunjungi
http://python.org/download/releases/2.7.2/ dan install versi 2.7.2

********************
Instalasi (opsional)
********************

1. Install `python pip <https://pip.pypa.io/en/latest/installing/>`_
2. Masuk ke direktori tempat anda meng-*clone* repositori ini ``cd ci-user-guide-id``
3. Jalankan perintah ``pip install --upgrade pip`` untuk update ke versi ``pip`` terbaru (opsional)
4. Lalu, Jalankan perintah ``pip install -r requirements.txt`` untuk menginstall semua dependensi yang dibutuhkan
5. Install CI Lexer untuk PHP, HTML, CSS, and JavaScript *syntax highlighting* di contoh (lihat di ``cilexer/README``) atau agar lebih mudah jalankan perintah ``easy_install cilexer``
6. Terakhir, jalankan perintah ``make html``

**Catatan:** Anda tidak harus meng-*install* semua kebutuhan diatas jika anda hanya ingin berkontribusi alih bahasa saja,
kecuali jika anda juga ingin melihat hasil html dari *compile*.

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
Jika Anda ingin *reset* file HTML Anda, cukup hapus folder ``build`` atau dapat anda lakukan dengan
menjalankan perintah ``make clean`` dan *generate* ulang seperti proses sebelumnya.

***************
Panduan Styling
***************

Silahkan lihat ``source/documentation/index.rst`` untuk panduan umum tentang
menggunakan Sphinx untuk dokumentasi Codeigniter.
