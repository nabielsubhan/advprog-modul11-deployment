## Nama   : Muhammad Nabiel Subhan
## NPM    : 2206081553
## Kelas  : AdPro B

###  Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?

<p align="center">
  <img src="images\before_exposed.png" />
</p>
<p align="center">
  <img src="images\after_exposed.png" />
</p>

Dapat dilihat bahwa terdapat perbedaan pada kedua gambar tersebut. Gambar pertama menunjukkan keadaan log ketika belum meng-*exposed* sebagai service, sedangkan gambar kedua menunjukkan keadaan log ketika sudah meng-*exposed* sebagai service. Log tersebut berisi aktivitas yang terjadi dari aplikasi yang berjalan di container, yaitu adanya server HTTP yang telah dimulai pada port tertentu dan diterimanya permintaan GET pada endpoint "/" beberapa kali. Jumlah log juga akan terus bertambah seiring banyaknya kita mencoba mengakses aplikasi tersebut. Hal tersebut dapat dilihat dari log permintaan GET yang terus bertambah.

### Notice that there are two versions of `kubectl get` invocation during this tutorial section.The first does not have any option, while the latter has `-n` option with value set to `kube-system`.  What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?

Penggunaan `-n` berfungsi untuk menspesifikasikan `namespace` yang akan dijadikan target. Pada versi yang pertama (tanpa `-n`), perintah tersebut akan mengembalikan pods dan services dari semua `namespace` yang ada di kluster Kubernetes, sedangkan versi yang kedua (dengan `-n`) akan mengembalikan pods dan services dari `namespace` yang telah dispesifikasikan (dalam kasus ini "kube-system") saja.