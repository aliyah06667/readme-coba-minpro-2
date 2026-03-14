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

### *1. main.dart*

File utama aplikasi. Berfungsi untuk inisialisasi Supabase, mengatur routing awal, dan menjalankan aplikasi.

### *2. models/*

Berisi struktur model data yang digunakan dalam aplikasi.

- #### *reservation.dart*

  Model data yang mendefinisikan struktur reservasi yang terdiri dari beberapa field seperti id, name, contact, service, date, notes, dan price. Model ini digunakan untuk mempermudah pengelolaan dan pengiriman data antara form, halaman, dan service yang terhubung dengan Supabase.

### *3. services/*

Berisi file yang menangani proses komunikasi antara aplikasi dengan database Supabase.

- #### *reservation_service.dart*

  Bertanggung jawab untuk mengelola seluruh operasi CRUD (Create, Read, Update, Delete) ke database Supabase, yaitu:
  - Create : Menambahkan data reservasi baru ke tabel reservations
  - Read : Mengambil dan menampilkan seluruh data reservasi dari database
  - Update : Memperbarui data reservasi berdasarkan id
  - Delete : Menghapus data reservasi berdasarkan id
    
  File ini memisahkan logic database dari tampilan (UI) sehingga struktur kode menjadi lebih terorganisir dan mudah dikembangkan.

### *4. pages/*

Berisi seluruh halaman (screen) dalam aplikasi.

- #### *login_page.dart*

  Halaman autentikasi pengguna untuk masuk ke dalam aplikasi menggunakan email dan password melalui Supabase Auth. Dilengkapi dengan validasi input, fitur show/hide password, notifikasi login berhasil/gagal, serta navigasi ke halaman register.

- #### *register_page.dart*

  Halaman pendaftaran akun baru menggunakan email dan password melalui Supabase Auth. Terdapat validasi minimal password dan notifikasi apabila registrasi berhasil atau gagal. Setelah berhasil, pengguna diarahkan kembali ke halaman login.

- #### *home_page.dart*
  
  Menampilkan daftar reservasi dan mengelola state data reservasi serta fitur-fitur yaitu Tambah data, Edit data dan Hapus data. Data ditampilkan langsung dari database Supabase.
  
- #### *add_page.dart*
  
  Berisi form untuk menambahkan data reservasi baru menggunakan TextField, DropdownButtonFormField, dan showDatePicker. Data yang disimpan akan dikirim ke Supabase.
  
- #### *edit_page.dart*
  
  Berfungsi untuk mengubah data reservasi yang sudah ada. Data lama akan otomatis terisi dan dapat diperbarui.

---

## 🗂 FITUR APLIKASI

**Beauti-Fy Salon** memiliki beberapa fitur utama yang terbagi ke dalam *LoginPage*, *RegisterPage*, *HomePage*, *AddPage*, *EditPage*, serta sistem pendukung seperti *Theme Management*, *Loading State*, dan *Error Handling*. Pada bagian ini dijelaskan fitur-fitur yang tersedia serta bagaimana fitur tersebut diimplementasikan di dalam kode program dan integrasinya dengan Supabase.

### 1. LoginPage

*LoginPage* merupakan halaman awal aplikasi yang berfungsi sebagai sistem autentikasi pengguna sebelum dapat mengakses fitur utama aplikasi. Halaman ini menggunakan **StatefulWidget** karena terdapat perubahan state seperti loading indicator dan toggle visibility password.

🔹 Fitur:
- Input email dan password
- Validasi form (tidak boleh kosong)
- Show / Hide password
- Login menggunakan Supabase Auth
- Loading indicator saat proses login
- Notifikasi berhasil / gagal
- Navigasi ke RegisterPage

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

### 2. RegisterPage

RegisterPage digunakan untuk membuat akun baru menggunakan Supabase Authentication. Halaman ini juga menggunakan StatefulWidget karena membutuhkan validasi input dan loading state.

🔹 Fitur:
- Input email dan password
- Validasi form (tidak boleh kosong)
- Show / Hide password
- Register menggunakan Supabase Auth
- Loading indicator saat proses regist
- Notifikasi berhasil / gagal
- Navigasi ke LoginPage
  
Proses registrasi dilakukan menggunakan:

~~~ Javascript
await Supabase.instance.client.auth.signUp(
  email: emailController.text.trim(),
  password: passwordController.text.trim(),
);
~~~

Validasi dilakukan sebelum proses register:
- Email tidak boleh kosong
- Password minimal 6 karakter

Jika registrasi berhasil:
- Menampilkan SnackBar "Account successfully created"
- Kembali ke *LoginPage*

### 3. HomePage

*HomePage* merupakan halaman utama setelah pengguna berhasil login. Halaman ini menampilkan seluruh data reservasi yang diambil dari database Supabase. Halaman ini menggunakan StatefulWidget karena data bersifat dinamis dan berubah setelah operasi CRUD.

🔹 Fitur:
- Menampilkan seluruh data reservasi dari Supabase
- Loading indicator saat mengambil data
- Error handling jika gagal load data
- Tombol tambah data
- Tombol edit data
- Tombol delete data
- Logout
- Menampilkan harga layanan
- Refresh otomatis setelah melakukan CRUD

Data tidak disimpan dalam List lokal statis, tetapi diambil dari Supabase menggunakan:

~~~ Javascript
final data = await supabase.from('reservations').select();
~~~

Data kemudian ditampilkan menggunakan ListView.builder.

Setiap item reservasi menampilkan atribut:
- name
- contact
- service
- date
- notes
- price

Perubahan data diperbarui menggunakan setState() agar tampilan otomatis refresh setelah create, update, atau delete.

 #### a. Menampilkan Data (Read)

Data diambil melalui ReservationService:

~~~ Javascript
Future<List> getReservations() async {
  final data = await supabase.from('reservations').select();
  return data;
}
~~~

Loading state ditampilkan menggunakan CircularProgressIndicator saat data sedang dimuat.

#### b. Tombol Tambah Data

Pada bagian bawah halaman terdapat tombol FloatingActionButton untuk menambahkan reservasi baru.

~~~ Javascript
FloatingActionButton(
  onPressed: () {
    Navigator.push(...);
  },
)
~~~

Tombol ini mengarahkan pengguna ke *AddPage*.

#### c. Tombol Edit

Setiap item memiliki tombol edit yang akan mengirimkan data lama ke EditPage melalui parameter constructor.

Navigasi dilakukan menggunakan:

~~~ Javascript
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (_) => EditPage(reservation: selectedData),
  ),
);
~~~

#### d. Tombol Delete

Penghapusan data dilakukan menggunakan method delete pada service:

~~~ Javascript
await supabase.from('reservations').delete().eq('id', id);
~~~

Setelah berhasil:
- Data di-refresh
- Menampilkan SnackBar "Data successfully deleted"

#### e. Logout

Logout dilakukan menggunakan:

~~~ Javascript
await Supabase.instance.client.auth.signOut();
~~~

Setelah logout:
- Kembali ke *LoginPage*

### 4. AddPage (Create Reservation)

*AddPage* digunakan untuk menambahkan data reservasi baru ke database Supabase.

Komponen form yang digunakan:
- `TextField` untuk name, contact, notes
- `DropdownButtonFormField` untuk memilih service
- `showDatePicker()` untuk memilih tanggal

Contoh implementasi DatePicker:

~~~ Javascript
final pickedDate = await showDatePicker(
  context: context,
  initialDate: DateTime.now(),
  firstDate: DateTime(2023),
  lastDate: DateTime(2100),
);
~~~

Harga layanan otomatis ditentukan berdasarkan pilihan service.

Data dikirim ke Supabase melalui:

~~~ Javascript
await supabase.from('reservations').insert({
  'name': name,
  'contact': contact,
  'service': service,
  'date': date,
  'notes': notes,
  'price': price,
});
~~~

Jika berhasil:
- Menampilkan "Data successfully created"
- Kembali ke *HomePage*

### 5. EditPage (Update Reservation)

EditPage digunakan untuk memperbarui data reservasi yang sudah ada.

Data lama dikirim dari HomePage dan diinisialisasi ke dalam controller:

~~~ Javascript
nameController.text = widget.reservation['name'];
~~~

Proses update dilakukan menggunakan:

~~~ Javascript
await supabase
  .from('reservations')
  .update({
    'name': name,
    'contact': contact,
    'service': service,
    'date': date,
    'notes': notes,
    'price': price,
  })
  .eq('id', id);
~~~

Jika berhasil:
- Menampilkan "Data successfully updated"
- Kembali ke *HomePage*
- Data otomatis diperbarui

### 6. Delete Reservation

Delete Reservation digunakan untuk menghapus data reservasi yang sudah ada dari database Supabase. Sebelum data benar-benar dihapus, sistem akan menampilkan dialog konfirmasi untuk memastikan pengguna tidak menghapus data secara tidak sengaja.

Dialog konfirmasi ditampilkan menggunakan:

~~~ Javascript
showDialog(
context: context,
builder: (context) => AlertDialog(
title: Text("Delete Confirmation"),
content: Text("Are you sure you want to delete this reservation?"),
actions: [
TextButton(
onPressed: () => Navigator.pop(context),
child: Text("Cancel"),
),
TextButton(
onPressed: () async {
await supabase.from('reservations').delete().eq('id', id);
Navigator.pop(context);
},
child: Text("Delete"),
),
],
),
);
~~~

Jika pengguna memilih Cancel:
- Proses penghapusan dibatalkan
- Dialog ditutup

Jika pengguna memilih Delete:
- Data dihapus menggunakan:
  ~~~ Javascript
  await supabase
  .from('reservations')
  .delete()
  .eq('id', id);
  ~~~

- Jika berhasil:
  - Menampilkan "Data successfully deleted"
  - Dialog tertutup
  - Kembali ke *HomePage*
  - Data otomatis diperbarui

### 7. Dark Mode & Light Mode

Aplikasi mendukung perubahan tema tampilan.

🔹 Fitur:
- Toggle Light Mode
- Toggle Dark Mode
- Tampilan berubah secara real-time

Implementasi menggunakan ThemeMode pada MaterialApp:

~~~ Javascript
themeMode: isDarkMode ? ThemeMode.dark : ThemeMode.light,
~~~

State theme dikontrol menggunakan setState().

### 8. Loading State & Error Handling

Setiap proses asynchronous dibungkus dalam try-catch:

~~~ Javascript
try {
  ...
} catch (e) {
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(content: Text(e.toString())),
  );
}
~~~

Loading indicator menggunakan:

~~~ Javascript
if (isLoading)
  CircularProgressIndicator()
~~~

Hal ini memastikan aplikasi tetap responsif dan informatif saat terjadi proses atau kesalahan.

### 9. Database Supabase

Seluruh data:
- Disimpan di database Supabase
- Tidak menggunakan List lokal
- Menggunakan tabel `reservations`
- Dikelola melalui `ReservationService`

Struktur ini menerapkan konsep separation of concerns dengan memisahkan UI dan database logic.

---

## 🗂 WIDGET & KOMPONEN YANG DIGUNAKAN
Berikut widget utama yang digunakan dalam aplikasi:

| WIDGET / KOMPONEN | KETERANGAN |
|-------------------|------------|
| MaterialApp | Root widget aplikasi yang mengatur tema, navigasi, dan konfigurasi global aplikasi. |
| ThemeData | Mengatur tampilan Light Mode dan Dark Mode. |
| ThemeMode | Mengontrol perubahan tema secara dinamis. |
| Scaffold | Struktur dasar setiap halaman seperti AppBar, body, dan FloatingActionButton. |
| AppBar | Menampilkan judul halaman serta tombol aksi seperti logout dan toggle theme. |
| SafeArea | Menyesuaikan tampilan agar tidak tertutup sistem UI perangkat. |
| Column | Menyusun widget secara vertikal. |
| Row | Menyusun widget secara horizontal. |
| Container | Membungkus widget dan mengatur styling seperti warna dan margin. |
| Padding | Memberikan jarak antar widget agar tampilan lebih rapi. |
| SizedBox | Memberikan jarak atau ukuran tetap antar komponen. |
| Center | Memposisikan widget di tengah layar. |
| Expanded | Membuat widget menyesuaikan ruang yang tersedia. |
| Text | Menampilkan informasi seperti nama, layanan, tanggal, dan harga. |
| Icon | Menampilkan ikon pada field atau tombol aksi. |
| TextField | Digunakan untuk input data seperti nama, kontak, email, password, dan catatan. |
| TextEditingController | Mengontrol dan mengambil nilai dari TextField. |
| DropdownButtonFormField | Digunakan untuk memilih jenis layanan salon. |
| InputDecoration | Mengatur tampilan TextField seperti label, hint, icon, dan border. |
| showDatePicker | Digunakan untuk memilih tanggal reservasi. |
| Navigator.push | Berpindah ke halaman baru seperti AddPage dan EditPage. |
| Navigator.pushReplacement | Mengganti halaman, misalnya setelah login berhasil. |
| Navigator.pop | Kembali ke halaman sebelumnya atau menutup dialog. |
| MaterialPageRoute | Mengatur transisi antar halaman. |
| ListView.builder | Menampilkan daftar reservasi secara dinamis dari database Supabase. |
| Card | Menampilkan data reservasi dalam bentuk kartu agar lebih terstruktur. |
| ListTile | Menyusun informasi reservasi dalam satu baris rapi (jika digunakan). |
| IconButton | Tombol aksi seperti edit dan delete. |
| FloatingActionButton | Tombol untuk menambahkan reservasi baru. |
| SnackBar | Menampilkan notifikasi seperti "Data successfully created", "updated", atau "deleted". |
| ScaffoldMessenger | Mengontrol dan menampilkan SnackBar. |
| AlertDialog | Menampilkan konfirmasi sebelum menghapus data. |
| TextButton | Tombol pada dialog seperti Cancel dan Delete. |
| CircularProgressIndicator | Menampilkan loading indicator saat proses async berjalan (login, register, CRUD, fetch data). |
| StatefulWidget | Digunakan pada halaman dengan perubahan data dinamis seperti HomePage, AddPage, EditPage, LoginPage, dan RegisterPage. |
| StatelessWidget | Digunakan pada halaman yang tidak memiliki perubahan state. |
| setState() | Digunakan untuk memperbarui tampilan setelah terjadi perubahan data. |

---

## 🗂 TAMPILAN APLIKASI

### 1. Halaman LoginPage

#### *Tampilan Light Mode*
  
<p align="center"><img width="1919" height="912" alt="image" src="https://github.com/user-attachments/assets/9c097f79-7680-4e2f-ba4b-c4b1b2d2e892" /></p>  

#### *Tampilan Dark Mode*
  
<p align="center"><img width="1919" height="904" alt="image" src="https://github.com/user-attachments/assets/808be766-461f-4f77-8c72-c9f230f40a68" /></p> 

<br>

### 2. Halaman RegisterPage

#### *Tampilan Light Mode*

<p align="center">
   <img src="[https://github.com/user-attachments/assets/a8c87877-1100-405e-b830-b1ce89698a2c](https://github.com/user-attachments/assets/57adebfd-af3e-488a-acd3-c6cbbfcc697c)" width="100" style="border:2px solid #ddd; border-radius:10px;">
</p>

#### *Tampilan Dark Mode*

<p align="center"><img width="1919" height="902" alt="image" src="https://github.com/user-attachments/assets/7abafb04-c4a5-4066-87ac-c33decc0301a" /></p>

### 3. Halaman HomePage

#### *Tampilan Light Mode*

<p align="center"><img width="1919" height="907" alt="Image" src="https://github.com/user-attachments/assets/41aaec33-7a63-43e4-a2df-34bf2d154a8a" /></p>

#### *Tampilan Dark Mode*

<p align="center"><img width="1919" height="908" alt="Image" src="https://github.com/user-attachments/assets/7d16de9a-b5c8-49aa-9a59-c4f4ce9998a7" /></p>

### 4. Add Reservation Page

#### *Tampilan Light Mode*

<p align="center"><img width="1919" height="903" alt="Image" src="https://github.com/user-attachments/assets/82c6ad67-3c3c-4f0d-9efa-4b13967bf456" /></p>

#### *Tampilan Dark Mode*

<p align="center"><img width="1919" height="904" alt="Image" src="https://github.com/user-attachments/assets/0ab2ded1-9531-4255-9c86-57d719b54582" /></p>

### 4. Edit Reservation Page

#### *Tampilan Light Mode*

<p align="center"><img width="1919" height="905" alt="Image" src="https://github.com/user-attachments/assets/d3e0822a-3772-4e66-8717-6116a992b489" /></p>

#### *Tampilan Dark Mode*

<p align="center"><img width="1919" height="905" alt="Image" src="https://github.com/user-attachments/assets/b5b1f910-ae73-4a50-878e-2d2d19d1cd9e" /></p>

---

## 🗂 LANGKAH - LANGKAH PENGGUNAAN APLIKASI 

### 1. Masuk Halaman Login

Pada saat pertama kali membuka aplikasi **Beauti-Fy Salon**, pengguna akan langsung diarahkan ke halaman login. Di sini, pengguna dapat memasukkan email dan password mereka untuk masuk.

<p align="center"><img width="1919" height="907" alt="Image" src="https://github.com/user-attachments/assets/19f69132-7938-4824-9595-c12c35543fef" /></p>

Jika belum memiliki akun, pengguna cukup menekan tombol “Sign Up” dan akan diarahkan ke halaman pendaftaran akun baru. Terdapat fitur show/hide password sehingga pengguna bisa memastikan kata sandi yang diketik sudah benar.

<p align="center"><img width="1919" height="907" alt="Image" src="https://github.com/user-attachments/assets/37f08454-b302-465a-93f6-2e28461550c6" /></p>/>

### 2. Mendaftar di Halaman Register

Setelah menekan “Sign Up”, pengguna akan masuk ke halaman register. Di halaman ini, pengguna diminta untuk mengisi beberapa kolom berupa email, password, dan konfirmasi password. 

Setelah semua data diisi, pengguna menekan tombol “REGISTER”. Jika registrasi berhasil, aplikasi akan menampilkan pesan “Account successfully created” dan otomatis membawa pengguna kembali ke halaman login untuk masuk menggunakan akun baru mereka.

### 3. Menjelajahi HomePage

Begitu berhasil login, pengguna akan tiba di halaman utama atau *HomePage*. Tampilan pertama akan menampilkan teks "No Reservation Yet." karena pengguna belum membuat suatu reservasi.

<p align="center"><img width="1919" height="907" alt="Image" src="https://github.com/user-attachments/assets/41aaec33-7a63-43e4-a2df-34bf2d154a8a" /></p>

Di sini, semua reservasi yang pernah dibuat ditampilkan dalam bentuk daftar. Setiap kartu reservasi menampilkan nama pelanggan, kontak, layanan, tanggal, catatan, dan harga layanan. Pengguna bisa melihat seluruh reservasi dengan mudah dan rapi.

Di HomePage, terdapat beberapa tombol aksi:
- Tombol + untuk menambahkan reservasi baru
- Tombol edit untuk memperbarui data reservasi
- Tombol delete untuk menghapus reservasi
- Tombol logout untuk keluar dari akun

### 4. Menambahkan Reservasi Baru
Saat pengguna menekan tombol +, mereka akan diarahkan ke halaman *AddPage*. Di sini, pengguna dapat mengisi form reservasi baru: nama pelanggan, kontak, layanan yang dipilih melalui dropdown, tanggal melalui DatePicker, catatan tambahan, dan harga layanan otomatis sesuai pilihan layanan. 

Setelah semua data diisi, pengguna menekan tombol "BOOK APPOINTMENT". Jika berhasil, aplikasi akan menampilkan pesan “Reservation successfully created” dan kembali ke HomePage dengan daftar yang sudah diperbarui.

### 5. Mengubah Reservasi yang Sudah Ada
Jika ada data reservasi yang perlu diperbarui, pengguna cukup menekan tombol edit pada kartu reservasi yang bersangkutan. Aplikasi akan menampilkan form yang sudah terisi dengan data lama. Pengguna bisa mengubah informasi yang diperlukan dan menekan tombol UPDATE. Setelah berhasil, pesan “Data successfully updated” akan muncul, dan HomePage akan menampilkan data yang sudah diperbarui.

### 6. Menghapus Reservasi
Untuk menghapus reservasi, pengguna menekan tombol delete pada kartu reservasi. Aplikasi akan menampilkan dialog konfirmasi: jika pengguna menekan Cancel, proses penghapusan dibatalkan. Jika menekan Delete, data akan dihapus dari database, muncul pesan “Data successfully deleted”, dan daftar reservasi otomatis diperbarui.

### 7. Mengubah Tema Tampilan
Beauti-Fy Salon mendukung Light Mode dan Dark Mode. Pengguna dapat mengubah tema melalui tombol toggle di AppBar. Saat diganti, tampilan aplikasi akan berubah secara real-time sesuai pilihan pengguna.

### 8. Logout
Jika pengguna selesai menggunakan aplikasi, mereka dapat menekan tombol Logout di HomePage. Setelah itu, session Supabase akan dihapus dan pengguna akan kembali ke halaman login.
