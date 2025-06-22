# Markethac Monthly Product Sales Report

1. WITH report_monthly_orders_product_agg AS: Membuat CTE (Common Table Expression) atau semacam temporary table bernama 'report_monthly_orders_product_agg/ untuk menyimpan hasil agregasi sebelum digunakan di query utama.
2. SELECT FORMAT_TIMESTAMP('%Y-%m', o.created_at) AS month: Mengubah 'created_at' dari tabel orders menjadi format 'YYYY-MM' agar bisa dikelompokkan per bulan.
3.   p.id AS product_id,
    p.name AS product_name : Mengambil ID dan nama produk dari tabel 'products'.
4. SUM(oi.sale_price) AS total_sales: Menjumlahkan total 'sale_price' dari setiap baris di 'order_items', sebagai total penjualan produk.
5. COUNT(oi.id) AS total_quantity: Menghitung jumlah baris (item) dari tabel 'order_items' untuk setiap produk.
6. COUNT(DISTINCT o.order_id) AS total_orders: Menghitung berapa pesanan unik yang menyertakan produk tersebut dalam 1 bulan.
7. 

