# advprog-modul10-timer

Nama: Muhammad Naufal Ramadhan <br>
NPM: 2306241700 <br>
Kelas: B
<hr>

## Experiment 1.2: Understanding how it works.
![experiment 1.2](/images/exp1.2.png)
Bisa dilihat pada gambar, urutan outputnya adalah `Hey Hey`, `Howdy`, dan 'Done'. Karena program menggunakan konsep asynchronous, urutan eksekusi kodenya menjadi berbeda dengan program synchronous biasa. Pertama, program akan mengeksekusi `println!("Naufal's Komputer: hey hey")` yang berada di main thread terlebih dahulu. Setelah itu, executor mulai menjalankan task async yang berisi perintah untuk mencetak `howdy!`, kemudian menunggu timer selama 2 detik (menggunakan `Duration::new(2, 0)`), dan terakhir mencetak `done!`. Timer yang diset selama 2 detik ini menyebabkan output `done!` muncul paling terakhir setelah delay.