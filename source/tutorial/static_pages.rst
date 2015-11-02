##############
Halaman Statis
##############

**Catatan:** Tutorial ini mengasumsikan Anda sudah download CodeIgniter dan
*:doc:`telah terinstall <../installation/index>` di *development environment*
Anda.

Hal pertama yang akan Anda lakukan adalah membuat **controller** untuk menangani
halaman statis. Sebuah controller hanyalah sebuah *class* yang membantu delegasi
pekerjaan. Ini adalah perekat aplikasi web Anda.

Sebagai contoh, ketika panggilan dilakukan ke:

	http://example.com/news/latest/10

Kita dapat membayangkan bahwa ada *controller* bernama "*news*". *Method* yang
dipanggil dalam controller* "*news*" adalah "*latest*". Pekerjaan *method*
"*latest*" pada *controller* "*news*" ini bisa untuk mengambil 10 item berita,
dan memuat mereka ke halaman. Sangat sering di MVC, Anda akan melihat pola URL
seperti:

	http://example.com/[controller-class]/[controller-method]/[arguments]

Saat skema URL menjadi lebih komples, hal ini dapat berubah. Tapi untuk saat
ini, skema ini yang kita perlu tahu.

Buat file pada ``application/controllers/Pages.php`` dengan kode seperti ini.

::

	<?php

	class Pages extends CI_Controller
	{

		public function view($page = 'home')
		{

	 	}

	}

Anda telah membuat sebuah *class* bernama ``Pages``, dengan *method* bernama
``view`` yang menerima satu argumen bernama ``$page``. *Class* ``Pages``
memperpanjang *class* ``CI_Controller``. Ini berarti bahwa *class* ``Pages``
dapat mengakses metode dan variabel yang didefinisikan dalam *class*
``CI_Controller`` (*system/core/Controller.php*).

**Controller** adalah apa yang akan menjadi pusat untuk setiap permintaan di
aplikasi web Anda. Dalam diskusi CodeIgniter yang sangat teknis, hal itu
mungkin disebut sebagai *super object*. Seperti *class* php, Anda lihat itu
dalam controller Anda sebagai ``$this``. Mengacu kepada ``$this`` adalah
bagaimana Anda akan memuat *library*, *view*, dan memerintah *framework* secara
keseluruhan.

Sekarang Anda telah membuat *method* pertama Anda, saatnya untuk membuat
*template* beberapa halaman dasar. Kita akan membuat dua "*view*" (*template*
halaman) yang bertindak sebagai footer dan header halaman kita.

Buat header di ``application/views/templates/header.php`` dan tambahkan kode
berikut:

::

	<html>
		<head>
			<title>CodeIgniter Tutorial</title>
		</head>
		<body>
			<h1><?php echo $title; ?></h1>

Header berisi kode HTML dasar yang akan Anda ingin tampilkan sebelum memuat
view* utama, bersama-sama dengan heading. Ini juga akan menampilkan variabel
``$title``, yang akan kita tentukan kemudian di controller. Sekarang, buat
footer di ``application/views/templates/footer.php`` yang berisi kode berikut:

::

			<em>&copy; 2015</em>
		</body>
	</html>

Menambahkan logika ke dalam controller
--------------------------------------

Sebelumnya Anda mengatur controller dengan *method* ``view()``. *Method* ini
menerima satu parameter, yang merupakan nama dari halaman yang akan dimuat.
Template* halaman statis akan ditempatkan di direktori
``application/views/pages/``.

Dalam direktori tersebut, buat dua file bernama ``home.php`` dan ``about.php``.
Dalam file-file tersebut, ketik beberapa teks - apapun yang Anda inginkan - dan
simpan mereka. Jika Anda ingin menjadi sangat *un-original*, coba "Hello
World!".

Untuk memuat halaman tersebut, Anda harus memeriksa apakah halaman yang diminta
benar-benar ada:

::

	public function view($page = 'home')
	{
	 	if ( ! file_exists(APPPATH.'/views/pages/'.$page.'.php')) {
			// Whoops, we don't have a page for that!
			show_404();
		}

		$data['title'] = ucfirst($page); // Capitalize the first letter

		$this->load->view('templates/header', $data);
		$this->load->view('pages/'.$page, $data);
		$this->load->view('templates/footer', $data);
	}

Sekarang, ketika halaman tidak ada, itu dimuat, termasuk header dan footer, dan
ditampilkan kepada pengguna. Jika halaman tidak ada, halaman "404 Page not
found" akan ditampilkan.

Baris pertama dalam *method* ini memeriksa apakah halaman benar-benar ada.
Fungsi asli PHP ``file_exists()`` digunakan untuk memeriksa apakah file tersebut
ada. ``show_404()`` adalah fungsi *built-in* CodeIgniter yang merender halaman
default *error*.

Dalam *template* header, variabel ``$title`` digunakan untukmenyesuaikan judul
halaman. Nilai ``$title`` didefinisikan dalam *method* ini, tapi bukannya
*assign* nilai ke variabel, itu *assign* untuk elemen *title* di *array*
``$data``.

Hal terakhir yang harus dilakukan adalah memuat *view* sesuai dengan yang
seharusnya ditampilkan. Parameter kedua dalam *method* ``view()`` digunakan
untuk mengoper (*pass*) nilai-nilai ke *view*. Setiap nilai dalam *array*
``$data`` di *assign* ke variabel yang sesuai dengan *key* dari *array* ``$data``.
Jadi nilai ``$data['title']`` di controller setara dengan ``$title`` dalam
*view*.

Routing
-------

*Controller* sekarang berfungsi! Arahkan browser Anda ke
``[your-site-url]/index.php/pages/view`` untuk melihat halaman Anda. Ketika
Anda mengunjungi ``index.php/pages/view/about`` Anda akan melihat halaman
*about*, termasuk *header* dan *footer*.

Menggunakan *rule* *routing* kustom, Anda memiliki kekuatan untuk
memetakan setiap URI ke *controller* apapun dan *method*, dan bebas dari
konvensi yang normal:
``http://example.com/[controller-class]/[controller-method]/[arguments]``

Mari kita melakukan itu. Buka file *routing* yang terletak di
``application/config/routes.php`` dan tambahkan dua baris berikut. Hapus semua
kode lain yang mengatur setiap elemen di *array* ``$route``.

::

	$route['default_controller'] = 'pages/view';
	$route['(:any)'] = 'pages/view/$1';

CodeIgniter membaca *rule* *routing* dari atas ke bawah dan mengarahkan *request*
ke *rule* pertama yang cocok. Setiap *rule* adalah *regular expression* (sisi
kiri) dipetakan ke *controller* dan nama *method* dipisahkan oleh garis miring
(sisi kanan). Ketika permintaan datang, CodeIgniter mencari *rule* yang cocok
pertama kali, dan memanggil *controller* dan *method* yang sesuai, memungkinkan
dengan argumen.

Informasi lebih lanjut tentang *routing* dapat ditemukan dalam dokumentasi
:doc:`URI Routing <../general/routing>`.

Di sini, aturan kedua dalam *array* ``$routes`` cocok dengan **semua**
*request* dengan menggunakan *wildcard string* ``(:any)`` dan mengoper
(*pass*) parameter ke *method* ``view()`` di *class* ``Pages``.

Sekarang kunjungi ``index.php/about``. Apakah itu disalurkan dengan
benar ke *method* ``view()`` di *controller* ``Pages``? Bagus!
