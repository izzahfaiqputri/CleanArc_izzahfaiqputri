Dalam refaktorisasi proyek ini dari arsitektur Model-View-Controller (MVC) ke Clean Architecture, terdapat beberapa perubahan utama yang dilakukan untuk meningkatkan modularitas, skalabilitas, dan pemisahan concerns. Berikut adalah perubahan yang diterapkan:

1. Pemisahan Domain dan Entitas
Pada MVC, model database langsung digunakan di dalam controller.
Dalam Clean Architecture, model database dipisahkan ke dalam Domain Layer sebagai UserEntity di domain/user.py. Ini membuat entitas lebih fleksibel dan tidak bergantung pada ORM tertentu.

2. Pengenalan Repository Layer
MVC langsung menggunakan SQLAlchemy dalam controller.
Dalam Clean Architecture, dibuat Repository Interface (repository/user_repository.py) sebagai abstraksi untuk data storage.
Implementasi konkret UserRepositoryImpl (repository/user_repository_impl.py) menangani interaksi dengan database.

3. Pemindahan Business Logic ke Use Case Layer
Pada MVC, logika bisnis ada di dalam controller.
Dalam Clean Architecture, dibuat Use Case Layer (usecase/user_usecase.py) untuk menangani logika bisnis sebelum mengakses repository.

4. Refaktorisasi Controller
Pada MVC, controller berisi langsung query database dan logika bisnis.
Dalam Clean Architecture, controller hanya bertindak sebagai perantara antara HTTP request dan Use Case Layer.

5. Struktur Folder

MVC :
``` backend_architecture/
├── models/
├── controllers/
├── routes/
├── database/
├── app.py
```
Clean Architecture :
``` backend_architecture/
├── domain/          # Entitas bisnis
├── repository/      # Abstraksi & implementasi data storage
├── usecase/         # Logika bisnis utama
├── models/          # Model database
├── controllers/     # Endpoint handler
├── routes/          # Routing
├── database/        # Konfigurasi database
├── app.py
```
7. Kelebihan Clean Architecture
- Kode lebih rapi karena sudah dipisah sesuai fungsi masing-masing.
- Lebih fleksibel, misalnya kalau mau ganti database atau framework, tidak perlu banyak perubahan.
- Mudah untuk dites, karena setiap bagian berdiri sendiri dan bisa diuji secara terpisah.

Tambahan : Clean Architecture lebih cocok untuk proyek besar karena pattern ini lebih mudah ketika testing.
