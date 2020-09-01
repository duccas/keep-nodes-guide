# Konfigurasi dan menjalankan Random Beacon dan ECDSA Nodes

### 1. **Persiapan**

Jalankan terminal untuk server kita pada alamat dimana kita membuat server atau program special yang dijelaskan pada sesi:

{% page-ref page="../../getting-started/technical-requirements.md" %}

### 2. **Konfigurasi Ubuntu**

Update packages pada server ke versi terakhir:

```text
sudo apt update
```

Install the git package jika tidak terpasang pada server:

```text
sudo apt install git
```

Install Docker:

```text
sudo apt install docker.io curl -y
```

Activate Docker:

```text
sudo systemctl start docker
sudo systemctl enable docker
```

### 3. **Konfigurasi Firewall**

Buka ports 22, 3919 and 3920 dan jalankan Firewall:

```text
sudo ufw allow 22 && sudo ufw allow 3919 && sudo ufw allow 3920 && sudo ufw enable
```

Setelah menjalankan perintah, tekan "y" dan Enter untuk konfirmasi pengaktifan firewall.

Cek status ports terbuka dengan perintah:

```text
sudo ufw status
```

### 4. **Konfigurasi nodes**

Pertama, unduh repository pada github server dengan semua folders dan configs untuk menjalankan 2 nodes dengan menggunakan perintah:

```text
git clone https://github.com/icohigh/keep-nodes.git
```

1. Pada perintah dibawah, ganti "YOUR ETH ADDRESS" dengan alamat dompet ETH anda.
2. "YOUR PASSWORD" untuk password dari dompet ETH anda.
3. "CONTENT OF FILE UTC--2020-08-24T16-27-57" untuk contents dokumen terunduh pada saat membuat dompet ETH.
4. Enter semua perintah.

```text
echo 'YOUR ETH ADDRESS' >> $HOME/keep-nodes/data/eth-address.txt
echo 'YOUR PASSWORD' >> $HOME/keep-nodes/data/eth-address-pass.txt
echo 'CONTENT OF FILE UTC--2020-08-24T16-27-57' >> $HOME/keep-nodes/data/keep_wallet.json
```

Seharusnya terlihat seperti ini:

{% code title="\#EXAMPLE" %}
```text
echo '0x208E233b930aacC7E17768F02106b6429B822133' >> $HOME/keep-nodes/data/eth-address.txt
echo 'qwerty123' >> $HOME/keep-nodes/data/eth-address-pass.txt
echo '{"version":3,"id":"d01c210a-1206-4754-9202-9f3g87472afe","address":"0x208E233b930aacC7E17768F02106b6429B822133","crypto":{"ciphertext":"85b53ab95e6fbea53f123123b5p234ujdce2122b08f6a73310f2d131e700","cipherparams":{"iv":"13d3efdead3523501ae8ede4328duwh4158"},"cipher":"aes-128-ctr","kdf":"scrypt","kdfparams":{"dklen":32,"salt":"ffad567d42eb5b3f1907e91023478fhs234r720234fs21a0a324cffc9e6c119137","n":131072,"r":8,"p":1},"mac":"c3b300aa4db1531add1c7c78d73d88f75a387485627g46539f1027999c66517"}}' >> $HOME/keep-nodes/data/keep_wallet.json
```
{% endcode %}

   5. Tulis export data of your Password and server IP ke dokumen .profile dengan menjalankan perintah:

```text
echo 'export ETH_PASSWORD=$(cat $HOME/keep-nodes/data/eth-address-pass.txt)' >> $HOME/.profile
echo 'export SERVER_IP=$(curl ifconfig.co)' >> $HOME/.profile
```

   6. Sekarang kita butuh untuk menambahkan dokumen konfigurasi INFURA ID dari akun yang anda buat sebelumnya[ https://infura.io/](https://infura.io/). Sisipkan pada "YOUR\_INFURA\_ID\_BEACON\_NODE" dan "YOUR\_INFURA\_ID\_ECDSA\_NODE", masing-masing, the ID of the Beacon and ECDSA nodes.

```text
grep -rl INFURA_BEACON_ID $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/INFURA_BEACON_ID/YOUR_INFURA_ID_BEACON_NODE/g'
grep -rl INFURA_ECDSA_ID $HOME/keep-nodes/ecdsa/config* | xargs perl -p -i -e 's/INFURA_ECDSA_ID/YOUR_INFURA_ID_ECDSA_NODE/g'
```

Seharusnya terlihat seperti ini:

{% code title="\#EXAMPLE" %}
```text
grep -rl INFURA_BEACON_ID $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/INFURA_BEACON_ID/6e6a4ed128a5f7s82bcc470710fb0/g'
grep -rl INFURA_ECDSA_ID $HOME/keep-nodes/ecdsa/config* | xargs perl -p -i -e 's/INFURA_ECDSA_ID/a888cf7gy6e888b0d21ee96b4201e0/g'
```
{% endcode %}

    7. Sekarang export the password dengan perintah:

```text
export ETH_PASSWORD=$(cat $HOME/keep-nodes/data/eth-address-pass.txt)
```

   8. Semua sudah siap untuk lanjut!

### 5. **Menjalankan Beacon node**

Jalankan Beacon node dengan perintah dibawah:

```text
sudo docker run -d \
--entrypoint keep-client \
--restart always \
--volume $HOME/keep-nodes/data:/mnt/data \
--volume $HOME/keep-nodes/beacon/config:/mnt/beacon/config \
--volume $HOME/keep-nodes/beacon/persistence:/mnt/beacon/persistence \
--env KEEP_ETHEREUM_PASSWORD=$ETH_PASSWORD \
--env LOG_LEVEL=debug \
--name keep-client \
-p 3919:3919 \
keepnetwork/keep-client:v1.3.0-rc --config /mnt/beacon/config/config.toml start
```

### 6. **Menjalankan ECDSA node**

Jalankan the ECDSA node dengan perintah berikut:

```text
sudo docker run -d \
--entrypoint keep-ecdsa \
--restart always \
--volume $HOME/keep-nodes/data:/mnt/data \
--volume $HOME/keep-nodes/ecdsa/config:/mnt/ecdsa/config \
--volume $HOME/keep-nodes/ecdsa/persistence:/mnt/ecdsa/persistence \
--env KEEP_ETHEREUM_PASSWORD=$ETH_PASSWORD \
--env LOG_LEVEL=debug \
--name keep-ecdsa \
-p 3920:3919 \
keepnetwork/keep-ecdsa-client:v1.2.0-rc --config /mnt/ecdsa/config/config.toml start
```

### 7. **Stop dan delete**

The container dapat diberhentikan dan dihapus dengan menggunakan perintah:

```text
sudo docker stop keep-client && sudo docker rm keep-client
sudo docker stop keep-ecdsa && sudo docker rm keep-ecdsa
```

### 8. Penting!

{% page-ref page="../memperbarui-node.md" %}

