#############
Bagian Berita
#############

Pada bagian terakhir, kita mempelajari beberapa konsep dasar dari *framework*
dengan menulis sebuah *class* yang meliputi halaman statis. Kita membersihkan
URI dengan menambahkan *rule* routing kustom. Sekarang saatnya untuk mengenal
konten dinamis dan mulai menggunakan database.

Menyiapkan Model Anda
---------------------

Alih-alih menulis operasi *database* di controller, query seharusnya ditempatkan
dalam model, sehingga mereka dapat dengan mudah digunakan kembali nanti. *Model*
adalah tempat di mana Anda mengambil, menambahkan, dan memperbarui informasi
Anda di *database* atau menyimpan data lainnya. Mereka mewakili data Anda.

Buka direktori ``application/models/`` dan buat file baru yang bernama
``News_model.php`` dan tambahkan kode berikut. Pastikan Anda sudah
menkonfigurasi *database* Anda dengan benar seperti yang dijelaskan
:doc:`disini <../database/configuration>`.

::

	<?php
	class News_model extends CI_Model
	{

		public function __construct()
		{
			$this->load->database();
		}
	}

Kode ini terlihat mirip dengan kode controller yang digunakan sebelumnya. Kode
diatas menciptakan model baru dengan memperluas ``CI_Model`` dan memuat
*library database*. Ini akan membuat *class database* yang tersedia melalui 
objek ``$this->db``.

Sebelum melakukan *query* ke *database*, skema *database* harus dibuat terlebih
dahulu. Hubungkan ke *database* Anda dan jalankan perintah SQL di bawah ini
(MySQL). Yang juga akan menambahkan beberapa *record*.

::

	CREATE TABLE news (
		id int(11) NOT NULL AUTO_INCREMENT,
		title varchar(128) NOT NULL,
		slug varchar(128) NOT NULL,
		text text NOT NULL,
		PRIMARY KEY (id),
		KEY slug (slug)
	);

Sekarang *database* dan *model* telah diatur, Anda akan memerlukan *method*
untuk mendapatkan semua *posting* kita dari database. Untuk melakukan hal ini,
*database abstraction layer* yang disertakan dengan CodeIgniter - :doc:`Query
Builder <../database/query_builder>` - digunakan. Hal ini memungkinkan Anda
untuk menulis '*query*' sekali dan membuat mereka bekerja pada :doc:`semua
sistem database didukung <../general/requirements>`. Tambahkan kode berikut
untuk *model* Anda.

::

	public function get_news($slug = FALSE)
	{
		if ($slug === FALSE) {
			$query = $this->db->get('news');
			return $query->result_array();
		}

		$query = $this->db->get_where('news', array('slug' => $slug));
		return $query->row_array();
	}

Dengan kode ini Anda dapat melakukan dua *query* yang berbeda. Anda bisa
mendapatkan semua *record* berita, atau mendapatkan sebuah berita dengan `slug
<#>`_. Anda mungkin melihat bahwa variabel ``$slug`` tidak dibersihkan sebelum
menjalankan *query*. :doc:`Query Builder <../database/query_builder>`
melakukannya untuk anda.

Menampilkan Berita
------------------

Sekarang *query* sudah ditulis, *model* harus terikat dengan *view*
yang akan menampilkan berita kepada pengguna. Hal ini dapat dilakukan
di *controller* ``Pages`` yang kita buat sebelumnya, tapi demi kejelasan,
*controller* ``News`` baru telah didefinisikan. Buat *controller* baru di
``application/controllers/News.php``.

::

	<?php
	class News extends CI_Controller
	{

		public function __construct()
		{
			parent::__construct();
			$this->load->model('news_model');
			$this->load->helper('url_helper');
		}

		public function index()
		{
			$data['news'] = $this->news_model->get_news();
		}

		public function view($slug = NULL)
		{
			$data['news_item'] = $this->news_model->get_news($slug);
		}
	}

Melihat kode diatas, Anda dapat melihat beberapa kesamaan dengan file yang kita
buat sebelumnya. Pertama, *method* ``__construct()``: itu memanggil konstruktor
*class* induknya (``CI_Controller``) dan memuat *model*, sehingga dapat
digunakan di semua *method* di dalam *controller* ini. Hal ini juga memuat
*collection* dari fungsi :doc:`URL Helper <../helpers/url_helper>`, karena kita
akan menggunakan salah satu dari mereka dalam *view* nanti.

Berikutnya, ada dua *method* untuk melihat semua berita dan satu berita untuk
berita tertentu. Anda dapat melihat bahwa variabel ``$slug`` dilewatkan ke
*method* *model* dalam *method* kedua. *Model* ini menggunakan *slug* untuk
mengidentifikasi berita yang dikembalikan.

Sekarang data tersebut diambil oleh *controller* melalui *model* kami, tapi
belum ada yang ditampilkan. Hal berikutnya yang harus dilakukan adalah
mengoper (*passing*) data ini ke *view*.

::

	public function index()
	{
		$data['news'] = $this->news_model->get_news();
		$data['title'] = 'News archive';

		$this->load->view('templates/header', $data);
		$this->load->view('news/index', $data);
		$this->load->view('templates/footer');
	}

Kode di atas berfungsi untuk mendapat semua *record* berita dari *model* dan
*assign* ke sebuah variabel. Nilai untuk judul juga di-*assign* ke elemen
``$data['title']`` dan semua data akan dioper ke *view*. Anda sekarang perlu
untuk membuat *view* untuk memuat berita. Buat
``application/views/news/index.php`` dan tambahkan potongan kode berikut.

::

	<h2><?php echo $title; ?></h2>
	
	<?php foreach ($news as $news_item): ?>

		<h3><?php echo $news_item['title']; ?></h3>
		<div class="main">
			<?php echo $news_item['text']; ?>
		</div>
		<p><a href="<?php echo site_url('news/'.$news_item['slug']); ?>">View article</a></p>

	<?php endforeach; ?>

Di sini, setiap item berita diulang dan ditampilkan kepada pengguna. Anda dapat
melihat kita menulis *template* kita di PHP yang dicampur dengan HTML. Jika
Anda memilih untuk menggunakan *template language*, Anda dapat menggunakan
CodeIgniter *class* :doc:`Template Parser <../libraries/parser>` atau
*parser* pihak ketiga.

Halaman ikhtisar berita sekarang selesai, tetapi halaman untuk menampilkan
berita individu masih belum. *Model* yang dibuat sebelumnya dibuat sedemikian
rupa agar mudah digunakan untuk fungsi ini. Anda hanya perlu menambahkan
beberapa kode untuk *controller* dan membuat *view* baru. Kembali ke
*controller* ``News`` dan perbaiki *method* ``view()`` seperti berikut:

::

	public function view($slug = NULL)
	{
		$data['news_item'] = $this->news_model->get_news($slug);

		if (empty($data['news_item']))
		{
			show_404();
		}

		$data['title'] = $data['news_item']['title'];

		$this->load->view('templates/header', $data);
		$this->load->view('news/view', $data);
		$this->load->view('templates/footer');
	}

Alih-alih memanggil *method* ``get_news()`` tanpa parameter, variabel ``$slug``
dioper, sehingga akan mengembalikan *item* berita tertentu. Satu-satunya hal
yang tersisa untuk dilakukan adalah membuat *view* yang sesuai di
``application/views/news/view.php``. Masukan kode berikut dalam file ini.

::

	<?php
	echo '<h2>'.$news_item['title'].'</h2>';
	echo $news_item['text'];

Routing
-------

Karena *rule routing wildcard* yang kita buat sebelumnya, Anda perlu *route*
ekstra untuk melihat *controller* yang baru saja Anda buat. Modifikasi file
*routing* (``application/config/routes.php``) sehingga terlihat sebagai berikut.
Hal ini untuk memastikan permintaan mencapai *controller* ``News`` bukannya
langsung ke *controller* ``Pages``. *Route* URI baris pertama dengan *slug* ke
*method* ``view()`` dalam *controller* ``News``.

::

	$route['news/(:any)'] = 'news/view/$1';
	$route['news'] = 'news';
	$route['(:any)'] = 'pages/view/$1';
	$route['default_controller'] = 'pages/view';

Arahkan browser Anda ke *root* dokumen Anda, diikuti dengan ``index.php/news``
dan lihat halaman berita Anda.
