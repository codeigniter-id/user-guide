###################
Membuat Item Berita
###################

Anda sekarang tahu bagaimana Anda dapat membaca data dari *database* menggunakan
CodeIgniter, tapi Anda masih belum menulis informasi ke *database*. Di bagian
ini Anda akan memperluas *controller* ``news`` dan *model* yang dibuat
sebelumnya untuk memasukkan fungsi ini.

Membuat Form
------------

Untuk memasukkan data ke dalam *database* yang Anda butuhkan untuk membuat
*form* di mana Anda dapat masukan informasi yang akan disimpan. Ini berarti Anda
akan membutuhkan *form* dengan dua *field*, satu untuk judul dan satu untuk teks.
Anda akan mendapatkan *slug* dari judul kita di dalam *model*. Buat *view* baru
di ``application/views/news/create.php``.

::

    <h2><?php echo $title; ?></h2>

    <?php echo validation_errors(); ?>

    <?php echo form_open('news/create'); ?>

        <label for="title">Title</label>
        <input type="input" name="title" /><br />

        <label for="text">Text</label>
        <textarea name="text"></textarea><br />

        <input type="submit" name="submit" value="Create news item" />

    </form>

Hanya ada dua hal di sini yang mungkin terlihat asing bagi Anda:
fungsi ``form_open()`` dan fungsi ``validation_errors()``.

Fungsi yang pertama disediakan oleh :doc:`form helper <../helpers/form_helper>`
dan membuat elemen *form* dan menambahkan fungsi tambahan, seperti menambahkan
:doc:`field pencegahan CSRF <../libraries/security>` yang tersembunyi. Fungsi
yang terakhir digunakan untuk melaporkan kesalahan terkait dalam validasi
*form*.

Kembali ke *controller* ``news`` Anda. Anda akan melakukan dua hal di sini,
memeriksa apakah *form* tersebut di *submit* dan apakah data yang di *submit*
melewati aturan validasi. Anda akan menggunakan *library* :doc:`validasi form
<../libraries/form_validation>` untuk melakukan hal ini.

::

    public function create()
    {
        $this->load->helper('form');
        $this->load->library('form_validation');

        $data['title'] = 'Create a news item';

        $this->form_validation->set_rules('title', 'Title', 'required');
        $this->form_validation->set_rules('text', 'Text', 'required');

        if ($this->form_validation->run() === FALSE) {
            $this->load->view('templates/header', $data);
            $this->load->view('news/create');
            $this->load->view('templates/footer');

        } else {
            $this->news_model->set_news();
            $this->load->view('news/success');
        }
    }

Kode di atas menambahkan banyak fungsionalitas. Beberapa baris pertama memuat
*form helper* dan *library* validasi *form*. Setelah itu, aturan untuk validasi
*form* ditetapkan. *Method* ``set_rules()`` mengambil tiga argumen; nama
*field* input, nama yang akan digunakan dalam pesan kesalahan, dan peraturan.
Dalam hal ini *field* judul dan teks yang diharuskan.

CodeIgniter memiliki *library* validasi *form* yang kuat seperti yang
ditunjukkan di atas. Anda dapat membaca :doc:`lebih lanjut tentang library ini
disini <../libraries/form_validation>`.

Terus turun, Anda dapat melihat kondisi yang memeriksa apakah validasi *form*
berhasil. Jika tidak, *form* yang ditampilkan, jika di *submit* **dan** berhasil
melewati semua aturan, *model* ini dipanggil. Setelah itu, *view* dimuat untuk
menampilkan pesan sukses. Buat *view* di ``application/views/news/success.php``
dan tulis pesan sukses.

Model
-----

Satu-satunya hal yang tersisa adalah menulis sebuah *method* yang menulis
data ke database. Anda akan menggunakan *class* **Query Builder** untuk
memasukkan informasi dan menggunakan *library* **Input** untuk mendapatkan data
yang diposting. Buka *model* yang dibuat sebelumnya dan tambahkan berikut ini:

::

    public function set_news()
    {
        $this->load->helper('url');

        $slug = url_title($this->input->post('title'), 'dash', TRUE);

        $data = array(
            'title' => $this->input->post('title'),
            'slug' => $slug,
            'text' => $this->input->post('text')
        );

        return $this->db->insert('news', $data);
    }

*Method* baru ini mengurus memasukkan berita ke dalam database. Baris ketiga
berisi fungsi baru, ``url_title()``. Fungsi ini - disediakan oleh :doc:`URL
helper <../helpers/url_helper>` - menghapus string yang Anda oper, mengganti
semua spasi dengan tanda hubung (-) dan memastikan semuanya dalam huruf kecil.
Hal ini membuat Anda mendapatkan *slug* yang bagus, sempurna untuk menciptakan
URI.

Mari kita lanjutkan dengan menyiapkan *record* yang akan dimasukkan
kemudian, dalam *array* ``$data``. Setiap elemen sesuai dengan kolom dalam
tabel database yang dibuat sebelumnya. Anda mungkin melihat *method* baru di
sini, yaitu *method* ``post()`` :doc:`library Input <../libraries/input>`.
*Method* ini memastikan data sudah dibersihkan, melindungi Anda dari serangan
jahat dari orang lain. *Library* **Input** dimuat secara *default*. Akhirnya,
Anda memasukkan *array* ``$data`` kita ke dalam database kita.

Routing
-------

Sebelum Anda dapat mulai menambahkan item berita ke dalam aplikasi CodeIgniter
Anda, Anda harus menambahkan aturan tambahan di file ``config/routes.php``.
Pastikan file Anda berisi seperti berikut ini. Hal ini akan memastikan
CodeIgniter melihat '*create*' sebagai *method* bukan sebagai *slug* berita ini.

::

    $route['news/create'] = 'news/create';
    $route['news/(:any)'] = 'news/view/$1';
    $route['news'] = 'news';
    $route['(:any)'] = 'pages/view/$1';
    $route['default_controller'] = 'pages/view';

Sekarang arahkan browser Anda ke *development environment* lokal Anda di mana
Anda menginstall CodeIgniter dan tambahkan ``index.php/news/create`` ke URL.
Selamat, Anda baru saja membuat aplikasi CodeIgniter pertama Anda!
Tambahkan beberapa berita dan periksa halaman yang berbeda yang Anda buat.
