# Memperbarui Node

Anda tidak perlu mengganti apapun pada dokumen config node untuk perbarui. Setelah pengumuman resmi dari kontrak baru atau rekan, mereka akan segera ditambahkan ke my github repository.

### **Perintah untuk update cepat**

1. Hentikan kontainer:

```text
sudo docker stop keep-client && sudo docker rm keep-client
sudo docker stop keep-ecdsa && sudo docker rm keep-ecdsa
```

   2. Masukan perintah berikut untuk mengunduh versi dokumen terakhir dari github:

```text
cd keep-nodes && git pull && cd
```

Semuanya, setelah itu, nodes anda akan sepenuhnya siap untuk dijalankan.

Selanjutnya, pergi ke bagian Konfigurasi dan menjalankan Random Beacon dan ECDSA Nodes dan jalankan langkah 5 and 6.

{% page-ref page="panduan-pemasangan/konfigurasi-dan-menjalankan-random-beacon-dan-ecdsa-nodes.md" %}

### **Masalah pada saat memperbarui**

Jika terdapat beberapa alasan anda tidak dapat memperbarui dengan perintah diatas, kemudian jalankan perintah yang menghapus semua direkotori node pada server anda:

```text
rm -R keep-nodes
```

Kemudian pergi ke Konfigurasi dan menjalankan Random Beacon dan ECDSA Nodes dan kembali jalankan dari langkah nomor 4.

{% page-ref page="panduan-pemasangan/konfigurasi-dan-menjalankan-random-beacon-dan-ecdsa-nodes.md" %}

