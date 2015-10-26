###########################
Sekilas Tentang CodeIgniter
###########################

CodeIgniter itu Sebuah Aplikasi Framework
=========================================

CodeIgniter adalah sebuah Application Development Framework (toolkit)
bagi orang-orang yang ingin membangun website menggunakan PHP.
Tujuannya adalah untuk memungkinkan Anda mengembangkan proyek-proyek
lebih cepat daripada Anda menulis kode dari awal, tersedia banyak libary
untuk tugas-tugas yang biasa diperlukan, serta antarmuka dan struktur logis
yang sederhana untuk mengakses library ini. CodeIgniter memungkinkan Anda fokus
pada proyek Anda dengan meminimalkan jumlah kode yang dibutuhkan untuk tugas yang diberikan.

CodeIgniter itu Gratis
======================

CodeIgniter dilisensikan di bawah lisensi MIT sehingga Anda dapat menggunakannya sesuka hati Anda.
Untuk informasi lebih lanjut silahkan baca :doc:`license agreement <../license>`.

CodeIgniter itu Ringan
======================

Benar-benar ringan. Sistem inti hanya memerlukan beberapa *library* yang sangat kecil.
Hal ini kontras dengan banyak *framework* yang membutuhkan lebih banyak sumber daya secara signifikan.
*Library* tambahan dimuat secara dinamis atau sesuai permintaan, berdasarkan kebutuhan Anda untuk proses tertentu, sehingga
sistem dasar sangat ramping dan cukup cepat.

CodeIgniter itu Cepat
=====================

Sangat cepat. Kami menantang Anda untuk menemukan *framework* yang memiliki kinerja
lebih baik dari CodeIgniter.

CodeIgniter Menggunakan M-V-C
=============================

CodeIgniter menggunakan pendekatan *Model-View-Controller*, yang memungkinkan pemisahan
antara logika dan presentasi. Ini sangat baik untuk proyek yang dimana desainer bekerja dengan
file template Anda, sehingga kode di file ini menjadi minimal. Kami menjelaskan MVC lebih
detail pada halamannya sendiri.

CodeIgniter Menghasilkan URL yang Bersih
========================================

URL yang dihasilkan oleh CodeIgniter bersih dan *search-engine friendly*.
Daripada menggunakan standar "query string" pendekatan ke URL yang
identik dengan sistem dinamis, CodeIgniter menggunakan pendekatan *segment-based*::

	example.com/news/article/345

Catatan: Secara default file ``index.php`` disertakan dalam URL tetapi bisa
dihapus menggunakan file ``.htaccess`` yang sederhana.

CodeIgniter Packs a Punch
=========================

CodeIgniter dilengkapi dengan *library* yang lengkap yang umumnya paling
diperlukan untuk tugas pengembangan web, seperti mengakses database,
mengirim email, memvalidasi data *form*, menjaga *session*, memanipulasi
gambar, bekerja dengan XML-RPC data dan masih banyak lagi.

CodeIgniter itu Extensible
==========================

Sistem ini dapat dengan mudah diperluas dengan menggunakan *library* Anda sendiri,
*helper*, atau melalui *class extensions* atau *system hooks*.

CodeIgniter Tidak Membutuhkan Template Engine
=============================================

Meskipun CodeIgniter mempunyai template parser sederhana yang bisa
digunakan secara opsional, ia tidak memaksa Anda untuk menggunakannya.
*Template engine* tidak bisa menyamai kinerja *native* PHP, dan sintaks yang
harus dipelajari untuk menggunakan *template engine* biasanya hanya sedikit
lebih mudah daripada belajar dasar-dasar PHP. Pertimbangkan blok kode PHP berikut::

	<ul>
	<?php foreach ($addressbook as $name):?>
		<li><?=$name?></li>
	<?php endforeach; ?>
	</ul>

Kontras ini dengan *pseudo-code* yang digunakan oleh *template engine*::

	<ul>
	{foreach from=$addressbook item="name"}
		<li>{$name}</li>
	{/foreach}
	</ul>

Ya, contoh *template engine* diatas sedikit lebih bersih, tapi harus ditukar dengan performa,
karena pseudo-code harus diubah kembali ke PHP untuk dijalankan.
Karena salah satu tujuan kami adalah **performa maksimal**, kami memilih untuk tidak
memerlukan penggunaan *template engine*.

CodeIgniter didokumentasikan Secara Menyeluruh
==============================================

Programmer suka kode dan membenci menulis dokumentasi. Kami tidak berbeda,
tentu saja, tapi karena dokumentasi **sama pentingnya** sebagai
kode itu sendiri, maka kami berkomitmen untuk melakukannya. *Source code* kami sangat
bersih dan mempunyai komentar yang baik juga.

CodeIgniter memiliki Komunitas Pengguna yang Ramah
==================================================

Komunitas pengguna yang berkembang dapat dilihat secara aktif yang berpartisipasi dalam
`Community Forums <http://forum.codeigniter.com/>`_ kami.
