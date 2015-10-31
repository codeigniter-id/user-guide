#############
Alur Aplikasi
#############

Grafik berikut menggambarkan bagaimana alur data melewati sistem:

|Alur aplikasi Codeigniter|

#. File ``index.php`` berfungsi sebagai *front controller*, menginisialisasi *resource* utama yang dibutuhkan untuk menjalankan CodeIgniter.
#. *Router* memeriksa *HTTP request* untuk menentukan apa yang harus dilakukan dengan itu.
#. Jika file *cache* ada, dikirim langsung ke browser, melewati eksekusi sistem normal.
#. Keamanan. Sebelum *controller* aplikasi dimuat, *HTTP request* dan setiap data pengguna yang di *submit* disaring terlebih dahulu untuk keamanan.
#. *Controller* memuat *model*, *library* utama, *helper*, dan setiap *resource* lainnya yang diperlukan untuk memproses permintaan khusus.
#. *View* di *render* kemudian dikirim ke web browser agar dapat dilihat. Jika *caching* diaktifkan, *view* di *cache* terlebih dahulu sehingga pada permintaan berikutnya dapat dilayani.

.. |Alur aplikasi Codeigniter| image:: ../images/appflowchart.gif
