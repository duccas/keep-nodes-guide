# Memperbarui Node

Anda tidak perlu mengganti apapun pada dokumen config node untuk perbarui. Setelah pengumuman resmi dari kontrak baru atau rekan, mereka akan segera ditambahkan ke my github repository.

### **Perintah untuk update cepat**

1. Hentikan kontainer:

```text
sudo docker stop keep-client && sudo docker rm keep-client
sudo docker stop keep-ecdsa && sudo docker rm keep-ecdsa
```

   2. Kami memasukkan perintah berikut untuk memperbarui alamat kontrak:

```text
grep -rl 0xf417b31104631280adF9F6828ee19985BC299fdC $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/0xf417b31104631280adF9F6828ee19985BC299fdC/0xC8337a94a50d16191513dEF4D1e61A6886BF410f/g'
grep -rl 0x8117632eC1D514550b3880Bc68F9AC1A76c9C67B $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/0x8117632eC1D514550b3880Bc68F9AC1A76c9C67B/0x234d2182B29c6a64ce3ab6940037b5C8FdAB608e/g'
grep -rl 0xd83248e311DC2Ba0d2A051e86f0678d8857f6ADD $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/0xd83248e311DC2Ba0d2A051e86f0678d8857f6ADD/0x6c04499B595efdc28CdbEd3f9ed2E83d7dCCC717/g'
grep -rl 0xb37c8696cD023c11357B37b5b12A9884c9C83784 $HOME/keep-nodes/ecdsa/config* | xargs perl -p -i -e 's/0xb37c8696cD023c11357B37b5b12A9884c9C83784/0x9EcCf03dFBDa6A5E50d7aBA14e0c60c2F6c575E6/g'
grep -rl 0x9F3B3bCED0AFfe862D436CB8FF462a454040Af80 $HOME/keep-nodes/ecdsa/config* | xargs perl -p -i -e 's/0x9F3B3bCED0AFfe862D436CB8FF462a454040Af80/0xc3f96306eDabACEa249D2D22Ec65697f38c6Da69/g'
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

