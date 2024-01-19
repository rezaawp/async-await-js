# Pembahasan 1
## Konsep Asynchronous
Memahami asynchronus adalah salah satu hal penting dalam dunia Javascript. Topik ini sering dilewatkan ketika masih di tahap belajar fundamental mungkin karena konsepnya terlalu ribet dijelaskan atau alasan lain. Bahkan banyak yang sudah bertahun-tahun menggunakan javascript ternyata masih banyak yang masih kurang paham dengan konsep asynchronous. Walaupun secara praktek mungkin sudah sering digunakan.

## Synchronous vs Asynchronous
- Dalam dunia programming kedua istilah ini digunakan untuk membedakan tentang cara urutan eksekusi perintah-perintah yang ada dalam kode anda.
- Synchronous adalah yang paling umum dan mudah di mengerti. Setiap perintah di eksekusi satu persatu sesuai urutan kode yang anda tuliskan. Contoh :
```javascript
console.log('Hello')
console.log('Javascript')
console.log('Coder')

/*
Output :
Hello!
Javascipt
Coder
*/
```

- Output dari kode diatas dijamin akan sesuai urutan, karena setiap perintah harus menunggu perintah sebelumnya selesai. Proses seperti ini disebut ‘blocking’.

- Dalam dunia nyata ini mirip seperti antrian di BANK. Jika anda berada antrian nomor 4, maka anda akan dilayani setelah antrian 1–3 sampai selesai.

- Sedangkan Asynchronous hasil eksekusi atau output tidak selalu berdasarkan urutan kode, tetapi berdasarkan waktu proses. Eksekusi dengan asynchronous tidak akan membloking atau menunggu suatu perintah sampai selesai. Daripada menunggu, asynchronous akan mengeksekusi perintah selanjutnya. Wait, sampai disini mungkin tidak masuk akal. Contoh :

```javascript
  console.log('Hello');
setTimeout(() => { console.log('Javascript')},100) // tunda selama 100 miliseconds
console.log('Coder');

/* ----------
Output :
Hello!
Coder
Javascipt
------------*/
```

- Mari kita lihat performancenya, Sebagai contoh ada 3 perintah dengan waktu proses masing-masing.

![alt text](https://miro.medium.com/v2/resize:fit:720/format:webp/1*-x526WMVTAKM2tVtP42PZA.png)
![image sync](https://miro.medium.com/v2/resize:fit:720/format:webp/0*jTvg1V81fvA6Stm1.png)
![image async](https://miro.medium.com/v2/resize:fit:720/format:webp/0*FZAS49wNTj9X-ySD.png)

- Dari contoh simulasi diatas model eksekusi asynchronous lebih effisien. Tapi ada yang menjadi pertimbangan yang disebut race condition. Race Condition terjadi ketika ada satu perintah yang bergantung pada output eksekusi asynchronous sebelumnya.Dengan kata lain kejar-kejaran. Contoh :
```javascript
console.log('hello')
let user = requestAjax() // di eksekusi secara asynchronous
displayUser(user)
```

- Dari contoh kode diatas besar kemungkinan displayUser menampilkan data kosong, karena belum tentu output dari ekskusi requestAjax sudah selesai.

- [pertanyaan](https://telegra.ph/pertanyaan-1-01-19)