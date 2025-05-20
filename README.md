# advprog-modul10-timer

Nama: Muhammad Naufal Ramadhan <br>
NPM: 2306241700 <br>
Kelas: B
<hr>

## Experiment 1.2: Understanding how it works.
![experiment 1.2](/images/exp1.2.png)
Bisa dilihat pada gambar, urutan outputnya adalah `Hey Hey`, `Howdy`, dan 'Done'. Karena program menggunakan konsep asynchronous, urutan eksekusi kodenya menjadi berbeda dengan program synchronous biasa. Pertama, program akan mengeksekusi `println!("Naufal's Komputer: hey hey")` yang berada di main thread terlebih dahulu. Setelah itu, executor mulai menjalankan task async yang berisi perintah untuk mencetak `howdy!`, kemudian menunggu timer selama 2 detik (menggunakan `Duration::new(2, 0)`), dan terakhir mencetak `done!`. Timer yang diset selama 2 detik ini menyebabkan output `done!` muncul paling terakhir setelah delay.

## Experiment 1.3: Multiple Spawn and removing drop.
### With Drop
![experiment 1.3_withDrop](/images/exp1.3(with_drop).png)
Dengan adanya spawner bisa terlihat bahwa program menjalankan multiple tasks secara asynchronous. Output menunjukkan urutan eksekusi dimulai dengan "hey hey", diikuti oleh "howdy!", "howdy2!", dan "howdy3!" yang dijalankan secara berurutan. Setelah delay 2 detik, muncul "done!", "done3!", "done2!" dengan urutan yang tidak selalu sama. Urutan yang berbeda pada output "done" ini terjadi karena meskipun timer diset sama, ketika multiple tasks async selesai secara bersamaan, urutan eksekusinya tidak deterministik dan tergantung pada bagaimana executor menjadwalkan task-task tersebut dan dapat selalu berubah. Pemanggilan `drop(spawner)` di sini penting untuk memberitahu executor bahwa tidak akan ada task baru yang ditambahkan, sehingga program bisa selesai setelah semua task tereksekusi.

### Without Drop
![experiment 1.3_withoutDrop](/images/exp1.3(without_drop).png)
Dengan dihilangkannya Drop dari program, bisa terlihat bahwa program tidak menyelesaikan eksekusinya dengan sempurna. Hal ini terjadi karena executor tidak mendapat sinyal bahwa tidak ada lagi task yang akan ditambahkan ke dalam queue. Tanpa `drop(spawner)`, executor terus menunggu task baru yang mungkin ditambahkan, menyebabkan program tidak pernah selesai dan tetap berjalan tanpa batas.

