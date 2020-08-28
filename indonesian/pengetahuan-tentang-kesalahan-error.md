# Pengetahuan tentang kesalahan/error

### **Kesalahan** 1

Jika anda mendapat kesalahan, seperti tampilan dibawah, kemudian langkah pertama yang harus anda cek adalah memastikan jika kontrak terotorisasi pada KEEP dashboard -[ https://dashboard.test.keep.network/applications/random-beacon](https://dashboard.test.keep.network/applications/random-beacon). 

Jika semua terotorisasi, kemudian masalah biasanya pada Infura account.

![](../.gitbook/assets/image%20%2824%29.png)

1. Anda butuh untuk masuk ke akun Infura anda
2. Pilih proyek BEACON NODE \(anda dapat menamai sesuka anda\)

![](../.gitbook/assets/image%20%2820%29.png)

   3. Pergi ke project settings

![](../.gitbook/assets/image%20%2823%29.png)

   4. Dan pada kolom ALLOWLIST CONTRACT ADDRESSES, masukan alamat ETH anda dan klik ADD

![](../.gitbook/assets/image%20%2819%29.png)

   5. Lakukan hal yang sama untuk ECDSA node project.  
   6. Selesai.

### **Kesalahan** 2

Jika setelah menjalankan, kita melihat beberapa kata yang terlihat sama pada logs, kemudian kita punya kesalahan pada password.

> FATAL keep-main error reading config file: password is required; set in the config file, set environment variable KEEP\_ETHEREUM\_PASSWORD to the password, or set the same environment variable to 'prompt' to be prompted for the password at startup

![](../.gitbook/assets/image%20%2826%29.png)

1.  Let's re-export the password dengan perintah:

```text
export ETH_PASSWORD=$(cat $HOME/keep-nodes/data/eth-address-pass.txt)
```

   2. Jika itu tidak membantu, kemudian anda butuh untuk menulis password anda langsung pada perintah launch seperti tampilan dibawah ini pada $ETH\_PASSWORD:

![Ganti $ETH\_PASSWORD dengan kata sandi dompet Anda](../.gitbook/assets/image%20%2825%29.png)

   3. Anda dapat menjalankan nodes anda.

