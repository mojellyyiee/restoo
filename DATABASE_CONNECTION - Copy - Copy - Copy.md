# Koneksi Database db_resto

Aplikasi ini sudah dikonfigurasi untuk terhubung ke database `db_resto` melalui backend API.

## Konfigurasi

### 1. Setup Environment Variable

Buat file `.env` di root project (copy dari `.env.example`):

```env
VITE_API_BASE_URL=http://localhost:8000/api
```

Sesuaikan URL dengan backend API Anda.

### 2. Struktur Database

Aplikasi ini menggunakan database `db_resto` dengan tabel-tabel berikut:

- **menu** - Data menu makanan/minuman
- **menu_harian** - Menu spesial harian
- **meja** - Data meja restoran
- **pesanan** - Data pesanan pelanggan
- **detail_pesanan** - Detail item pesanan
- **stok** - Data stok harian (opsional, bisa menggunakan kolom stok di tabel menu)

### 3. Service Layer

Service layer sudah dibuat di folder `src/services/`:

- `menu.service.ts` - Service untuk menu
- `menu-harian.service.ts` - Service untuk menu harian
- `meja.service.ts` - Service untuk meja
- `pesanan.service.ts` - Service untuk pesanan
- `stok.service.ts` - Service untuk stok

### 4. Endpoint API yang Diperlukan

Backend API harus menyediakan endpoint berikut:

#### Menu
- `GET /api/menu` - Ambil semua menu
- `GET /api/menu/:id` - Ambil menu by ID
- `GET /api/menu?kategori=makanan` - Ambil menu by kategori

#### Menu Harian
- `GET /api/menu-harian` - Ambil semua menu harian
- `GET /api/menu-harian/date/:date` - Ambil menu harian by tanggal

#### Meja
- `GET /api/meja` - Ambil semua meja
- `GET /api/meja/:id` - Ambil meja by ID
- `PUT /api/meja/:id/status` - Update status meja

#### Pesanan
- `GET /api/pesanan` - Ambil semua pesanan
- `GET /api/pesanan/:id` - Ambil pesanan by ID
- `POST /api/pesanan` - Buat pesanan baru
- `PUT /api/pesanan/:id` - Update pesanan (termasuk status)

#### Stok
- `GET /api/stok` - Ambil semua stok
- `GET /api/stok/date/:date` - Ambil stok by tanggal
- `PUT /api/stok/:id` - Update stok

### 5. Format Response API

Semua endpoint harus mengembalikan response dalam format:

```json
{
  "success": true,
  "data": [...],
  "message": "Optional message"
}
```

Atau untuk error:

```json
{
  "success": false,
  "message": "Error message"
}
```

### 6. Fallback ke Mock Data

Jika API belum tersedia atau terjadi error, aplikasi akan otomatis menggunakan mock data sebagai fallback. Ini memungkinkan development frontend tanpa backend terlebih dahulu.

### 7. Testing

Untuk testing koneksi database:

1. Pastikan backend API sudah running
2. Pastikan database `db_resto` sudah dibuat
3. Pastikan tabel-tabel sudah dibuat
4. Set `VITE_API_BASE_URL` di file `.env`
5. Restart development server
6. Buka aplikasi dan coba akses halaman yang menggunakan service

### 8. Troubleshooting

**Error: Failed to fetch**
- Pastikan backend API sudah running
- Pastikan URL di `.env` benar
- Cek CORS settings di backend

**Data tidak muncul**
- Cek console browser untuk error
- Pastikan format response API sesuai
- Pastikan database dan tabel sudah ada

**Mock data masih muncul**
- Hapus mock data di service file
- Atau pastikan API mengembalikan `success: true`
