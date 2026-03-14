## <p align="center">MINI PROJECT PEMOGRAMAN APLIKASI BERGERAK (2) "RESERVASI SALON"</p>

## <p align="center">BEAUTI-FY SALON</p>

<img width="1200" height="400" alt="beauti-fysalon img" src="https://github.com/user-attachments/assets/cfa42b6d-4117-47af-a00c-5bc3ce3750c5" />


### <p align="center">Disusun Oleh:</p> 

<p align="center">Aliyah Azzah Sekedang</p> 

<p align="center">(2409116021)</p>



---

## 🗂 DESKRIPSI APLIKASI
**Beauti-Fy Salon** adalah aplikasi mobile berbasis Flutter untuk mengelola reservasi layanan salon secara digital. Aplikasi ini memungkinkan pengguna melakukan pencatatan dan pengelolaan data booking secara terstruktur melalui sistem CRUD (Create, Read, Update, Delete).

Pengguna dapat melakukan login dan register menggunakan ***Supabase Authentication***, kemudian menambahkan, melihat, mengedit, dan menghapus data reservasi yang tersimpan pada database Supabase. Aplikasi ini dirancang dengan navigasi multi-halaman serta antarmuka modern untuk memberikan pengalaman penggunaan yang lebih efisien dan interaktif.

---

## 🗂 STRUKTUR FOLDER

***1. main.dart***

File utama aplikasi. Berfungsi untuk inisialisasi Supabase, mengatur routing awal, dan menjalankan aplikasi.

***2. models/***

Berisi struktur model data yang digunakan dalam aplikasi.

- ***reservation.dart***

  Model data yang mendefinisikan struktur reservasi yang terdiri dari beberapa field seperti id, name, contact, service, date, notes, dan price. Model ini digunakan untuk mempermudah pengelolaan dan pengiriman data antara form, halaman, dan service yang terhubung dengan Supabase.

***3. services/***

Berisi file yang menangani proses komunikasi antara aplikasi dengan database Supabase.

- ***reservation_service.dart***

  Bertanggung jawab untuk mengelola seluruh operasi CRUD (Create, Read, Update, Delete) ke database Supabase, yaitu:
  - Create : Menambahkan data reservasi baru ke tabel reservations
  - Read : Mengambil dan menampilkan seluruh data reservasi dari database
  - Update : Memperbarui data reservasi berdasarkan id
  - Delete : Menghapus data reservasi berdasarkan id
    
  File ini memisahkan logic database dari tampilan (UI) sehingga struktur kode menjadi lebih terorganisir dan mudah dikembangkan.

***4. pages/***

Berisi seluruh halaman (screen) dalam aplikasi.

- ***login_page.dart***

  Halaman autentikasi pengguna untuk masuk ke dalam aplikasi menggunakan email dan password melalui Supabase Auth. Dilengkapi dengan validasi input, fitur show/hide password, notifikasi login berhasil/gagal, serta navigasi ke halaman register.

- ***register_page.dart***

  Halaman pendaftaran akun baru menggunakan email dan password melalui Supabase Auth. Terdapat validasi minimal password dan notifikasi apabila registrasi berhasil atau gagal. Setelah berhasil, pengguna diarahkan kembali ke halaman login.

- ***home_page.dart***
  
  Menampilkan daftar reservasi dan mengelola state data reservasi serta fitur-fitur yaitu Tambah data, Edit data dan Hapus data. Data ditampilkan langsung dari database Supabase.
  
- ***add_page.dart***
  
  Berisi form untuk menambahkan data reservasi baru menggunakan TextField, DropdownButtonFormField, dan showDatePicker. Data yang disimpan akan dikirim ke Supabase.
  
- ***edit_page.dart***
  
  Berfungsi untuk mengubah data reservasi yang sudah ada. Data lama akan otomatis terisi dan dapat diperbarui.


## 🗂 FITUR APLIKASI

**Aplikasi Beauti-Fy Salon** memiliki beberapa fitur utama yang terbagi ke dalam LoginPage, RegisterPage, HomePage, AddPage, dan EditPage. Pada bagian ini dijelaskan fitur-fotur yang tersedia serta bagaimana fitur tersebut diimplementasikan di dalam kode program dan integrasinya dengan Supabase.

**1. LoginPage**

LoginPage merupakan halaman awal aplikasi yang berfungsi sebagai sistem autentikasi pengguna sebelum dapat mengakses fitur utama aplikasi. Halaman ini menggunakan StatefulWidget karena terdapat perubahan state seperti loading indicator dan toggle visibility password.

Controller yang digunakan:

~~~ Javascript
final TextEditingController emailController = TextEditingController();
final TextEditingController passwordController = TextEditingController();
~~~

Proses login dilakukan menggunakan Supabase Auth:

~~~ Javascript
await Supabase.instance.client.auth.signInWithPassword(
  email: emailController.text.trim(),
  password: passwordController.text.trim(),
);
~~~

State loading dikontrol menggunakan:

~~~ Javascript
setState(() {
  isLoading = true;
});
~~~

Jika login berhasil:
- Menampilkan SnackBar: "Login successful"
- Navigasi ke HomePage menggunakan Navigator.pushReplacement

Jika gagal:
- Menampilkan pesan error menggunakan SnackBar

---

## 🗂 WIDGET YANG DIGUNAKAN
Berikut widget utama yang digunakan dalam aplikasi:

**1. Layout & Structure**
   - Scaffold
   - Stack
   - Container
   - Column
   - Row
   - Center
   - Align
   - Positioned
   - SizedBox

2. Input & Form
- TextField
- TextEditingController
- InputDecoration
- IconButton

3. Button
- ElevatedButton
- TextButton
- GestureDetector

4. Visual & UI Effects
- AnimatedContainer
- FadeTransition
- ScaleTransition
- BackdropFilter
- ClipRRect
- BoxDecoration
- LinearGradient
- BoxShadow
- CircularProgressIndicator

5. Navigation
- Navigator.push
- Navigator.pushReplacement
- Navigator.pop

6. Backend Integration
- Supabase.instance.client.auth.signUp
- Supabase.instance.client.auth.signInWithPassword

---

## 🗂 TAMPILAN APLIKASI

**1. Halaman Login**
- Background image dengan overlay gradient
- Glassmorphism login card
- Input email & password
- Toggle show/hide password
- Dark mode button
- Tombol Sign Up

- ***Tampilan Light Mode***
  
  <img width="1919" height="912" alt="image" src="https://github.com/user-attachments/assets/9c097f79-7680-4e2f-ba4b-c4b1b2d2e892" />

- ***Tampilan Dark Mode***
  
  <img width="1919" height="904" alt="image" src="https://github.com/user-attachments/assets/808be766-461f-4f77-8c72-c9f230f40a68" />

<br>

**2. Halaman Register**

- ***Tampilan Light Mode***

  <img width="1919" height="909" alt="image" src="https://github.com/user-attachments/assets/57adebfd-af3e-488a-acd3-c6cbbfcc697c" />

- ***Tampilan Dark Mode***

  <img width="1919" height="902" alt="image" src="https://github.com/user-attachments/assets/7abafb04-c4a5-4066-87ac-c33decc0301a" />

**3. Halaman **

## 🗂 LANGKAH - LANGKAH PENGGUNAAN APLIKASI 

**1. Apabila belum memiliki akun, pengguna dapat langsung klik "Sign Up".**

**2. Kemudian, pengguna akan diarahkan ke halaman register untuk membuat akun sebagai pengguna baru. Pengguna diminta untuk mengisi kolom berupa _textfield_ yaitu email, password, dan confirm password, kolom password juga dilengkapi dengan fitur show/hide password. Setelah pengguna selesai mengisi data, tekan tombol "REGISTER" untuk menyimpan data.**

<img width="1442" height="869" alt="image" src="https://github.com/user-attachments/assets/018a8adc-0d65-45e7-8e74-6eef0c9a0b33" />
