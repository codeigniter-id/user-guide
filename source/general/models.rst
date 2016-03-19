#####
Model
#####

Models merupakan suatu *opsi* yang tersedia untuk siapa saja yang ingin menggunakan pendekatan tradisional yang lebih pada MVC.

.. daftar isi:: Konten Halaman

Apa itu model?
==============

Model merupakan class PHP yang didesain untuk hal-hal yang terkait dengan informasi basis data.
Sebagai contoh, katakanlah Anda menggunakan CodeIgniter untuk mengolah sebuah blog.
Anda mesti memiliki sebuah class model yang berisi beberapa fungsi (metode) untuk menambah, mengedit, atau menampilkan data blog Anda.
Berikut ini sebuah contoh seperti apa yang dimaksud dengan class model::

	class Blog_model extends CI_Model {

		public $judul;
		public $konten;
		public $waktu;

		public function __construct()
		{
			// Memanggil konstruktor CI_Model
			parent::__construct();
		}

		public function data_sepuluh_artikel_terakhir()
		{
			$query = $this->db->get('artikel', 10);
			return $query->result();
		}

		public function tambahkan_item()
		{
			$this->judul	= $_POST['judul']; // lihat catatan di bawah
			$this->konten	= $_POST['konten'];
			$this->waktu	= time();

			$this->db->insert('artikel', $this);
		}

		public function sunting_artikel()
		{
			$this->judul	= $_POST['judul'];
			$this->konten	= $_POST['konten'];
			$this->waktu	= time();

			$this->db->update('artikel', $this, array('id' => $_POST['id']));
		}

	}

.. catatan:: Beberapa metode atau fungsi pada contoh di atas menggunakan metode basis data yang dinamakan :doc:`Query Builder
	<../database/query_builder>`.

.. catatan:: Untuk contoh sederhana di sini menggunakan ``$_POST`` secara langsung.
	Umumnya ini praktek yang buruk untuk dilakukan, mengingat akan timbulnya masalah celah keamanan.
	Untuk pendekatan yang lebih baik, sebaiknya menggunakan :doc:`Input Library <../libraries/input>`
	``$this->input->post('judul')`` dan sebagainya.

Susunan sebuah Model
====================

Berkas atau class model berada di direktori **application/models/**.
Model dapat dikelompokkan di dalam sub-direktori bila model yang Anda inginkan menjadi lebih terorganisir.

Bentuk dasar sebuah model digambarkan seperti berikut ini::

	class Nama_model extends CI_Model {

		public function __construct()
		{
			parent::__construct();
		}

	}

Dimana **Nama_model** adalah nama class dari class model yang Anda buat.
Penamaan class **harus** dimulai dengan huruf besar (kapital) pada karakter huruf pertama.
Pastikan model class Anda merupakan turunan dari base Model (class **CI_Model** atau **MY_Model**). 

Antara nama berkas dan nama class harus sama. Sebagai contoh, jika Anda menggunakan model class berikut::

	class User_model extends CI_Model {

		public function __construct()
		{
			parent::__construct();
		}

	}

Maka, nama berkasnya harus seperti ini::

	application/models/User_model.php

Menghubungkan sebuah Model
==========================

Model pada dasarnya akan dimuat dan dipanggil dari metode atau fungsi yang ada pada
:doc:`controller <controllers>`. Untuk menghubungkan model, Anda harus menggunakan metode berikut ini::

	$this->load->model('nama_model');

Jika model yang Anda buat terletak di dalam sebuah sub-direktori, sertakan alamat relatif (*relative path*) dari model yang Anda buat.
Sebagai contoh, jika model yang Anda miliki berlokasi di 
*application/models/blog/Queries.php* Anda akan menghubungkannya dengan cara::

	$this->load->model('blog/queries');

Ketika terhubung, Anda dapat mengakses metode-metode yang ada pada model menggunakan sebuah objek
dengan nama yang sama dengan nama model class yang Anda buat sebelumnya::

	$this->load->model('nama_model');

	$this->nama_model->metode();

Jika Anda ingin menggunakan objek yang berbeda untuk sebuah model, Anda bisa menggunakan penamaan (alias) di parameter kedua::

	$this->load->model('nama_model', 'foobar');

	$this->foobar->metode();

Berikut adalah contoh sebuah controller yang terhubung dengan sebuah model
dan menampilkan data hasil olahan model ke view::

	class Blog_controller extends CI_Controller {

		public function blog()
		{
			$this->load->model('blog');

			$data['query'] = $this->blog->data_sepuluh_artikel_terakhir();

			$this->load->view('blog', $data);
		}
	}
	

*Auto-loading* Model
====================

Auto-loading (menghubungkan secara otomatis) model tertentu secara global bisa Anda lakukan dengan
menggunakan pengaturan yang ada pada berkas **application/config/autoload.php**. Tambahkan model yang
ingin Anda hubungkan secara otomatis selama sistem berjalan::

	$autoload['model'] = array('nama_model');

Koneksi ke Basis Data (Database)
================================

Ketika sebuah model sudah terhubung namun tidak dapat terkoneksi ke basis data secara otomatis,
beberapa opsi yang bisa digunakan untuk mengatasi masalah ini:

-  Anda dapat meng-koneksikan dengan menggunakan standar metode database (:doc:`penjelasan di sini <../database/connecting>`),
   antara class Controller atau class Model.
-  Anda dapat mengatur sebuah model melakukan *auto-connect* dengan menambahkan nilai TRUE (boolean) di parameter ketiga.
   Atau mengatur konektivitas sebagaimana yang telah didefinisikan di dalam berkas **application/config/database.php**::

	$this->load->model('nama_model', '', TRUE);

-  Anda dapat mengatur koneksi secara manual dengan menambahkan item-item berupa array pada parameter ketiga seperti contoh berikut::

	$config['hostname'] = 'localhost';
	$config['username'] = 'namapengguna';
	$config['password'] = 'katasandi';
	$config['database'] = 'nama_database';
	$config['dbdriver'] = 'mysqli';
	$config['dbprefix'] = '';
	$config['pconnect'] = FALSE;
	$config['db_debug'] = TRUE;

	$this->load->model('nama_model', '', $config);
