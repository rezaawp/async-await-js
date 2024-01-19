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

# Pembahasan 2 (AJAX)
![diagram ajax](https://qph.cf2.quoracdn.net/main-qimg-aec92b9065dfc46a8ccc43bc35ce2816-lq)
- Intinya AJAX itu seperti cara untuk pengambilan data dari client ke server tanpa mengubah fungsi lainnya, khususnya fungsi tampilan client/user.
- Jadi ketika anda perlu data baru tetapi tampilan web yang sama, maka dengan memakai ajax anda bisa menghemat data karena tidak memerlukan mengambil data tampilan lagi secara berulang-ulang.
- Contohnya seperti yang biasa digunakan pada kolom pencarian website,
![searching ajax](https://qph.cf2.quoracdn.net/main-qimg-f1e57b8f3069313f6754cbab16c38c69)
- Kalau didibaratkan sih metode pengambilan data memakai ajax itu ibarat asisten kerja, misalnya anda sedang bekerja lalu ingin membuat kopi, maka anda harus berhenti bekerja dahulu, jalan ke dapur dan membuat kopi lalu kembali lagi dan melanjutkan bekerja, sedangkan jika menggunakan asisten yang ibarat ajax, anda tinggal menyuruh asisten untuk membuatkan kopi sedangkan anda masih dapat bekerja tanpa diganggu.

# Pembahasan 3 (Callback)
- Callback sebenarnya adalah function bedanya dengan function pada umumnya adalah di cara eksekusinya. Jika function pada umumnya di eksekusi berurutan dari atas ke bawah maka callback di eksekusi pada point tertentu, itu sebabnya di sebut callback.
- Callback disebut juga dengan high-order function. Callback sebenarnya adalah function, bedanya dengan function pada umumnya adalah di cara eksekusinya. Jika function pada umumnya di eksekusi secara langsung sedangkan callback di eksekusi dalam function lain melalui parameter.
- Contoh :
```javascript

function main(param1,param2,callBack){ 
  console.log(param1, param2) 
  callBack()  
}

function myCallback(){ 
  console.log ('hello callback')
}

main(1,2,myCallback)

/* ===================
Output :
 1 2
 hello callback
 */
```

## Kenapa function bisa di jadikan sebagai parameter ?
- Function dalam javascript adalah object atau sering disebut first-class object, yang artinya :
  - Function bisa di jadikan parameter
  - Function dapat disimpan ke dalam variabel
  - Seperti object pada umumnya, function bisa memiliki property dan method
  - Function dapat mengembalikan value dalam bentuk function

## Kapan Callback digunakan ?
- Callback dapat digunakan untuk proses synchronous maupun asynchronous. Beberapa contoh implementasi callback adalah :
  - Injeksi atau modifikasi hasil eksekusi sebuah function
  - Event listener
  - Menangani proses asynchronous

### Callback sebagai injeksi
```javascript
function calculate(x,y){
  result = x + y
  return result
}
calculate(3,2) // 5
```
- Kode diatas cukup sederhana yaitu untuk melakukan operasi penjumlahan. Berikut tantangannya :
  - Buatlah function diatas agar bisa melakukan operasi matematika yg lain seperti kurang, bagi, kali dan lain sebagainya.
  - Output dari function di atas harus bisa di format ke dalam mata uang
- Dengan cara umum kita bisa menyelesaikanya dengan bantuan if atau switch untuk menguji operatornya. Tapi ini akan membuat code lebih panjang dan kurang dinamis. Dengan callback kita dapat membuat function diatas menjadi lebih dinamis
```javascript
function calculate(param1,param2,callback){
  //default operation
  result = param1 + param2
  
  // callback is function ?
  if (typeof callback == 'function'){
   result= callback(param1,param2)
  }
  
  return result
}

//execute
a=calculate(2000,4000, function(x,y){return "$ " + (x + y) }) 
b=calculate(7000,2000, function(x,y){return "Rp " + (x * y) }) 
console.log(a) // $ 6000
console.log(b) // Rp 14000
```

### Callback sebagai Event Listener 
- Event Listener adalah function yang di eksekusi karena suatu event contoh ketika berinteraksi dengan DOM seperti event click, focus, keydown,keypress dan lain sebagainya.

- Contoh pada Native Javascript
```javascript
document.getElementById("my_button").addEventListener("click",function(){
   alert('Ouhh aku di klik!') 
})
```

- Contoh ketika menggunakan jquery
```javascript
$('#my_button').on('click', function(e) {
  console.log('Ouhh aku di klik!');
})
```

### Callback Pada Asynchronous
- Proses asynchronous identik dengan delay, dimana hasil dari proses tersebut membutuhkan selang waktu tertentu untuk menghasilkan output. Kita akan menemukan proses asynchronous pada proses Ajax, komunikasi HTTP, Operasi file, timer, dsb.
- Pada synchronous output di prosess berdasarkan urutan kode.
```javascript
function p1() {
  console.log('p1 done')
}
function p2() {
  console.log('p2 done')
}
function p3() {
  console.log('p3 done')
}
p1()
p2()
p3()

/* Output :
p1 done
p2 done
p3 done
*/
```
- Tetapi pada proses asynchronous output dari kode yang tuliskan tidak selalu berurutan. Hasilnya tergantung yang mana yang lebih dulu selesai. Perhatikan contoh berikut :
```javascript
function p1() {
  console.log('p1 done')
}
function p2() {
  //setTimeout or delay for asynchronous simulation 
  setTimeout(
      function() {
        console.log('p2 done')
      },100
  )
}
function p3() {
  console.log('p3 done')
}
p1()
p2()
p3()

/* Output :
p1 done
p3 done
p2 done
*/
```

- Catatan : setTimeout digunakan untuk simulasi asynchronous. Karena sebenarnya kita tidak bisa membuat proses asynchronous murni.
- Perhatikan output dari kode diatas tidak lagi berurutan. Kerena javascript mengerjakan mana yang lebih dulu selesai. Mungkin pada contoh diatas tidak terlalu masalah tapi pada kasus tertentu ini menjadi problem, Contohnya kita ingin menampilkan data yang harus di request terlebih dahulu dengan proses ajax.

```javascript
data=requestAjax() // asynchronous process
showResult(data) //undefined
```
- Kemungkinan besar hasilnya undefined. Karena belum tentu data sudah tersedia ketika function showResult( ) di eksekusi. Teknik callback dapat kita gunakan untuk problem ini.
- Baik sebelum membahas ajax lebih , kita akan coba memperbaiki challange asynchronus di atas dengan memastikan output p1,p2,p3 sesuai urutan.
- Solusinya adalah dengan membuat p3 menjadi callback bagi p2.

```javascript
function p1() {
 console.log('p1 done')
}

function p2(callback) {
 setTimeout(
  function() {
   console.log('p2 done')
    callback()
  },100
  )
}

function p3() {
  console.log('p3 done')
}
p1()
p2(p3)
```
