# Markethac Monthly Product Sales Report (Penjelasan dari masing-masing kode)

1. WITH report_monthly_orders_product_agg AS: Membuat CTE (Common Table Expression) atau semacam temporary table bernama 'report_monthly_orders_product_agg/ untuk menyimpan hasil agregasi sebelum digunakan di query utama.
2. SELECT FORMAT_TIMESTAMP('%Y-%m', o.created_at) AS month: Mengubah 'created_at' dari tabel orders menjadi format 'YYYY-MM' agar bisa dikelompokkan per bulan.
3.   p.id AS product_id, p.name AS product_name : Mengambil ID dan nama produk dari tabel 'products'.
4. SUM(oi.sale_price) AS total_sales: Menjumlahkan total 'sale_price' dari setiap baris di 'order_items', sebagai total penjualan produk.
5. COUNT(oi.id) AS total_quantity: Menghitung jumlah baris (item) dari tabel 'order_items' untuk setiap produk.
6. COUNT(DISTINCT o.order_id) AS total_orders: Menghitung berapa pesanan unik yang menyertakan produk tersebut dalam 1 bulan.
7. FROM `bigquery-public-data.thelook_ecommerce.orders` o: Mengambil data dari tabel 'orders' dan memberi alias 'o'.
8. JOIN `bigquery-public-data.thelook_ecommerce.order_items` oi ON o.order_id = oi.order_id: Inner join ke tabel 'order_items' (alias oi), berdasarkan 'order_id'.
9. JOIN `bigquery-public-data.thelook_ecommerce.products` p ON oi.product_id = p.id: Menggabungkan lagi dengan tabel products (alias p) berdasarkan product_id.
10. WHERE o.status = 'Complete': Hanya mengambil transaksi yang sudah selesai.
11. GROUP BY month, p.id, p.name: Mengelompokkan hasil berdasarkan:
    - 'month': Bulan Pesanan
    - 'p.id': ID Produk
    - 'p.name': Nama Produk
12. SELECT * FROM report_monthly_orders_product_agg: Mengambil semua kolom data dari temporary tabel 'report_monthly_orders_product_agg', yang berisi hasil GROUP BY dari tabel 'orders', 'order_items', dan 'products'.
13. ORDER BY month, total_sales DESC: Mengurutkan hasil berdasarkan:
    - 'month' secara naik (default ascending), agar laporan tersusun per bulan.
    - 'total_sales DESC' yaitu produk dengan total penjualan tertinggi di urutan atas setiap bulannya.
