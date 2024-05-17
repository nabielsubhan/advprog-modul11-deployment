## Nama   : Muhammad Nabiel Subhan
## NPM    : 2206081553
## Kelas  : AdPro B

###  Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?

<p align="center">
  <img src="images\before-exposed.png" />
</p>
<p align="center">
  <img src="images\after-exposed.png" />
</p>

Dapat dilihat bahwa terdapat perbedaan pada kedua gambar tersebut. Gambar pertama menunjukkan keadaan log ketika belum meng-*exposed* sebagai service, sedangkan gambar kedua menunjukkan keadaan log ketika sudah meng-*exposed* sebagai service. Log tersebut berisi aktivitas yang terjadi dari aplikasi yang berjalan di container, yaitu adanya server HTTP yang telah dimulai pada port tertentu dan diterimanya permintaan GET pada endpoint "/" beberapa kali. Jumlah log juga akan terus bertambah seiring banyaknya kita mencoba mengakses aplikasi tersebut. Hal tersebut dapat dilihat dari log permintaan GET yang terus bertambah.

### Notice that there are two versions of `kubectl get` invocation during this tutorial section.The first does not have any option, while the latter has `-n` option with value set to `kube-system`.  What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?

Penggunaan `-n` berfungsi untuk menspesifikasikan `namespace` yang akan dijadikan target. Pada versi yang pertama (tanpa `-n`), perintah tersebut akan mengembalikan pods dan services dari semua `namespace` yang ada di kluster Kubernetes, sedangkan versi yang kedua (dengan `-n`) akan mengembalikan pods dan services dari `namespace` yang telah dispesifikasikan (dalam kasus ini "kube-system") saja.

### What is the difference between Rolling Update and Recreate deployment strategy?
Rolling update mmerupakan strategi default deployment. Cara kerjanya adalah dengan tidak langsung meng-*update* pods semuanya secara bersamaan, tetapi meng-*update* pods satu-satu atau beberapa terlebih dahulu sehingga pods yang lama masih masih tetap berjalan dan menjaga agar aplikasi tetap berjalan. Di sisi lain, strategi Recreate langsung menghapus semua pods yang ada, lalu menciptakan pods yang baru. Dengan demikian, hal tersebut akan menciptakan kondisi dimana tidak ada sama sekali pods yang berjalan.

### Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt.
* Membuat spring-petclinic-rest baru dengan versi 3.0.2, melakukan expose dan scale
<p align="center">
  <img src="images\new_deployment.png" />
</p>

* Mengubah yaml untuk mengganti strategi deployment menjadi Recreate
<p align="center">
  <img src="images\edit.png" />
</p>

* Hasil pengubahan
<p align="center">
  <img src="images\edit_result.png" />
</p>

* Menghapus pods yang ada
<p align="center">
  <img src="images\delete_pods.png" />
</p>
Dapat dilihat bahwa pods baru langsung dibuat setelah pods yang sebelumnya dihapus.

* Mencoba menjalankan dan mengakses service
<p align="center">
  <img src="images\try_run.png" />
</p>

* Service berhasil di akses
<p align="center">
  <img src="images\run_succeed.png" />
</p>

### Prepare different manifest files for executing Recreate deployment strategy.
<p align="center">
  <img src="images\prepare_new_yaml.png" />
</p>

###  What do you think are the benefits of using Kubernetes manifest files? Recall your experience in deploying the app manually and compare it to your experience when deploying the same app by applying the manifest files (i.e., invoking `kubectl apply-f` command) to the cluster.

Menggunakan Kubernetes manifest files memungkinkan adanya `declarative configuration` yang berarti bahwa state aplikasi kita dapat disimpan dalam format yang terstruktur, seperti yaml. Dengan adanya format yang terstruktur tersebut memungkinkan terjadinya konsistensi state aplikasi ketika ingin menjalankan deployment di berbagai lingkungan (dev, production, staging) dengan menggunakan format yang sama. Selain itu, men-*deploy* menggunakan perintah `kubectl apply-f` memungkinkan terjadinya automasi pada CI/CD pipelines sehingga proses deployment dapat dilakukan secara otomatis.