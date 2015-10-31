#####################
Model-View-Controller
#####################

CodeIgniter didasarkan pada pola pengembangan **Model-View-Controller**.
MVC adalah pendekatan perangkat lunak yang memisahkan logika aplikasi dari
presentasi. Dalam prakteknya, itu memungkinkan halaman web Anda memiliki
*scripting* yang minimal karena presentasi terpisah dari *scripting* PHP.

-  **Model** mewakili struktur data Anda. Biasanya *class* model Anda akan berisi fungsi yang
   membantu Anda mengambil, menyimpan, dan memperbarui informasi dalam database Anda.
-  **View** adalah informasi yang disajikan kepada pengguna. *View* yang biasanya akan menjadi halaman web,
   tetapi dalam CodeIgniter, *view* juga bisa menjadi bagian dari sebuah halaman seperti header atau footer.
   Hal ini juga dapat menjadi halaman *RSS*, atau jenis-jenis lain dari "halaman".
-  **Controller** berfungsi sebagai perantara antara *Model*, *View*, dan *resource* lain yang diperlukan
   untuk memproses *HTTP request* dan menghasilkan halaman web.

CodeIgniter memiliki pendekatan yang cukup longgar untuk MVC karena *Model* tidak
selalu diperlukan. Jika Anda tidak perlu menambahkan pemisahan, atau menemukan bahwa
mempertahankan sebuah *model* memerlukan kompleksitas lebih dari yang Anda inginkan, Anda bisa
mengabaikan mereka dan membangun aplikasi Anda dengan minimal menggunakan *Controller* dan
*View*. CodeIgniter juga memungkinkan Anda untuk memasukkan *script* Anda sendiri,
atau bahkan mengembangkan *library* inti untuk sistem, memungkinkan Anda untuk
bekerja dengan cara yang paling masuk akal bagi Anda.
