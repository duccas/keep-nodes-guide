# Melihat logs dan perintah lainnya

### Cara melihat logs

Disini terdapat beberapa pilihan untuk melihat logs.

1. Lihat kontainer yang sedang berjalan:

```text
docker ps -a
```

![](../.gitbook/assets/image%20%2818%29.png)

   2. Semua logs of Beacon and ECDSA nodes:

```text
sudo docker logs keep-client -f --since 1m
sudo docker logs keep-ecdsa -f --since 1m
```

   3. Hasil atau keluaran dari peers yang terhubung \(number of connected peers\):

{% code title="\#FOR BEACON NODE" %}
```text
sudo docker logs -f keep-client --tail 1000 2>&1 | grep "number of connected peers:"
```
{% endcode %}

{% code title="\#FOR ECDSA NODE" %}
```text
sudo docker logs -f keep-ecdsa --tail 1000 2>&1 | grep "number of connected peers:"
```
{% endcode %}

![](../.gitbook/assets/image%20%2821%29.png)

### Perintah tambahan

1. Menghentikan dan menghapus container:

```text
sudo docker stop keep-client && sudo docker rm keep-client
sudo docker stop keep-ecdsa && sudo docker rm keep-ecdsa
```

### Simpan log ke file 

Menyimpan log kontainer ke file selama 30 menit terakhir:

```text
sudo docker logs keep-ecdsa --since 30m >& ecdsa.log
```

