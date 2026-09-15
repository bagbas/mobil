<?php

// Menentukan apakah hasil sudah dihitung
$hasil = false;

// Jika tombol Hitung ditekan
if ($_POST) {

    // Mengambil data dari form
    $harga = $_POST["harga"];
    $dpPersen = $_POST["dp"];
    $tenorTahun = $_POST["tenor"];

    // Menghitung bunga 20%
    $bunga = $harga * 20 / 100;

    // Menghitung DP
    $dp = $harga * $dpPersen / 100;

    // Mengubah tahun menjadi bulan
    $tenorBulan = $tenorTahun * 12;

    // Menghitung angsuran per bulan
    $angsuran = ($harga + $bunga - $dp) / $tenorBulan;

    // Menandakan bahwa hasil sudah tersedia
    $hasil = true;
}

// Fungsi untuk membuat angka menjadi format Rupiah
function rupiah($angka)
{
    return "Rp " . number_format($angka, 0, ",", ".");
}

?>

<!DOCTYPE html>
<html lang="id">

<head>
    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>CalCar - Kredit Mobil</title>

    <!-- Bootstrap -->
    <link
        href="css/bootstrap.min.css"
        rel="stylesheet">
</head>

<body>

    <!-- ==================== NAVBAR ==================== -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">

        <div class="container">

            <a class="navbar-brand fw-bold" href="#">
                🚗 CalCar
            </a>

            <button
                class="navbar-toggler"
                type="button"
                data-bs-toggle="collapse"
                data-bs-target="#menu">

                <span class="navbar-toggler-icon"></span>

            </button>

            <div class="collapse navbar-collapse" id="menu">

                <ul class="navbar-nav ms-auto">

                    <li class="nav-item">
                        <a class="nav-link" href="#beranda">
                            Beranda
                        </a>
                    </li>

                    <li class="nav-item">
                        <a class="nav-link" href="#tentang">
                            Tentang
                        </a>
                    </li>

                    <li class="nav-item">
                        <a class="nav-link" href="#kalkulator">
                            Kalkulator
                        </a>
                    </li>

                    <li class="nav-item">
                        <a class="nav-link" href="#kontak">
                            Kontak
                        </a>
                    </li>

                </ul>

            </div>

        </div>

    </nav>


    <!-- ==================== SLIDER ==================== -->
    <section id="beranda">

        <div
            id="slider"
            class="carousel slide"
            data-bs-ride="carousel">

            <!-- Indikator slider -->
            <div class="carousel-indicators">

                <button
                    type="button"
                    data-bs-target="#slider"
                    data-bs-slide-to="0"
                    class="active">
                </button>

                <button
                    type="button"
                    data-bs-target="#slider"
                    data-bs-slide-to="1">
                </button>

                <button
                    type="button"
                    data-bs-target="#slider"
                    data-bs-slide-to="2">
                </button>

            </div>


            <!-- Isi slider -->
            <div class="carousel-inner">

                <!-- Slide 1 -->
                <div class="carousel-item active">

                    <img
                        src="https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=1600&q=80"
                        class="d-block w-100"
                        style="height:450px; object-fit:cover;">

                    <div class="carousel-caption">

                        <h1>
                            Mobil Impianmu
                        </h1>

                        <p>
                            Hitung estimasi kredit dengan mudah.
                        </p>

                        <a
                            href="#kalkulator"
                            class="btn btn-primary">

                            Mulai Hitung

                        </a>

                    </div>

                </div>


                <!-- Slide 2 -->
                <div class="carousel-item">

                    <img
                        src="https://images.unsplash.com/photo-1492144534655-ae79c964c9d7?auto=format&fit=crop&w=1600&q=80"
                        class="d-block w-100"
                        style="height:450px; object-fit:cover;">

                    <div class="carousel-caption">

                        <h1>
                            Kredit Lebih Mudah
                        </h1>

                        <p>
                            Tentukan DP dan tenor sesuai kebutuhan.
                        </p>

                    </div>

                </div>


                <!-- Slide 3 -->
                <div class="carousel-item">

                    <img
                        src="https://images.unsplash.com/photo-1553440569-bcc63803a83d?auto=format&fit=crop&w=1600&q=80"
                        class="d-block w-100"
                        style="height:450px; object-fit:cover;">

                    <div class="carousel-caption">

                        <h1>
                            Hitung Cicilanmu
                        </h1>

                        <p>
                            Cepat, sederhana, dan mudah digunakan.
                        </p>

                    </div>

                </div>

            </div>


            <!-- Tombol sebelumnya -->
            <button
                class="carousel-control-prev"
                type="button"
                data-bs-target="#slider"
                data-bs-slide="prev">

                <span class="carousel-control-prev-icon"></span>

            </button>


            <!-- Tombol berikutnya -->
            <button
                class="carousel-control-next"
                type="button"
                data-bs-target="#slider"
                data-bs-slide="next">

                <span class="carousel-control-next-icon"></span>

            </button>

        </div>

    </section>


    <!-- ==================== TENTANG ==================== -->
    <section id="tentang" class="py-5">

        <div class="container">

            <div class="row align-items-center g-4">

                <!-- Teks -->
                <div class="col-md-6">

                    <h2 class="fw-bold">
                        Tentang CalCar
                    </h2>

                    <p>
                        CalCar merupakan website sederhana yang
                        membantu pengguna menghitung estimasi
                        kredit mobil.
                    </p>

                    <p>
                        Pengguna cukup memasukkan harga mobil,
                        memilih DP, dan menentukan lama tenor kredit.
                    </p>

                    <p>
                        Sistem kemudian menghitung bunga, DP,
                        tenor, dan estimasi angsuran setiap bulan.
                    </p>

                </div>


                <!-- Gambar -->
                <div class="col-md-6">

                    <img
                        src="https://images.unsplash.com/photo-1542282088-fe8426682b8f?auto=format&fit=crop&w=1000&q=80"
                        class="img-fluid rounded"
                        alt="Mobil">

                </div>

            </div>

        </div>

    </section>


    <!-- ==================== KALKULATOR ==================== -->
    <section id="kalkulator" class="py-5 bg-light">

        <div class="container">

            <div class="text-center mb-4">

                <h2 class="fw-bold">
                    Kalkulator Kredit Mobil
                </h2>

                <p class="text-muted">
                    Masukkan data untuk menghitung cicilan.
                </p>

            </div>


            <div class="row justify-content-center">

                <div class="col-md-7">

                    <div class="card shadow-sm">

                        <div class="card-body p-4">

                            <!-- Form -->
                            <form method="POST">

                                <!-- Harga Mobil -->
                                <div class="mb-3">

                                    <label class="form-label fw-bold">
                                        Harga Mobil
                                    </label>

                                    <input
                                        type="number"
                                        name="harga"
                                        class="form-control"
                                        placeholder="Contoh: 200000000"
                                        required
                                        min="1">

                                </div>


                                <!-- DP -->
                                <div class="mb-3">

                                    <label class="form-label fw-bold">
                                        DP
                                    </label>

                                    <select
                                        name="dp"
                                        class="form-select"
                                        required>

                                        <option value="">
                                            Pilih DP
                                        </option>

                                        <option value="10">
                                            10%
                                        </option>

                                        <option value="20">
                                            20%
                                        </option>

                                        <option value="30">
                                            30%
                                        </option>

                                        <option value="40">
                                            40%
                                        </option>

                                        <option value="50">
                                            50%
                                        </option>

                                        <option value="60">
                                            60%
                                        </option>

                                    </select>

                                </div>


                                <!-- Tenor -->
                                <div class="mb-3">

                                    <label class="form-label fw-bold">
                                        Tenor
                                    </label>


                                    <div class="d-flex gap-2 flex-wrap">

                                        <?php for ($i = 1; $i <= 5; $i++): ?>

                                            <input
                                                type="radio"
                                                class="btn-check"
                                                name="tenor"
                                                id="tahun<?= $i ?>"
                                                value="<?= $i ?>"
                                                required>

                                            <label
                                                class="btn btn-outline-primary"
                                                for="tahun<?= $i ?>">

                                                <?= $i ?> Tahun

                                            </label>

                                        <?php endfor; ?>

                                    </div>

                                </div>


                                <!-- Informasi bunga -->
                                <div class="alert alert-info">

                                    Bunga kredit:
                                    <strong>20%</strong>
                                    dari harga mobil.

                                </div>


                                <!-- Tombol -->
                                <button
                                    type="submit"
                                    class="btn btn-primary w-100">

                                    Hitung Angsuran

                                </button>

                            </form>

                        </div>

                    </div>

                </div>

            </div>

        </div>

    </section>


    <!-- ==================== HASIL ==================== -->

    <?php if ($hasil): ?>

        <section class="py-5">

            <div class="container">

                <div class="row justify-content-center">

                    <div class="col-md-7">

                        <div class="card shadow-sm">

                            <div class="card-body p-4">

                                <h3 class="text-center fw-bold mb-4">
                                    Hasil Perhitungan
                                </h3>


                                <!-- Harga -->
                                <div class="row mb-2">

                                    <div class="col-6">
                                        Harga Mobil
                                    </div>

                                    <div class="col-6 text-end fw-bold">

                                        <?= rupiah($harga) ?>

                                    </div>

                                </div>


                                <!-- Bunga -->
                                <div class="row mb-2">

                                    <div class="col-6">
                                        Bunga 20%
                                    </div>

                                    <div class="col-6 text-end fw-bold">

                                        <?= rupiah($bunga) ?>

                                    </div>

                                </div>


                                <!-- DP -->
                                <div class="row mb-2">

                                    <div class="col-6">
                                        DP <?= $dpPersen ?>%
                                    </div>

                                    <div class="col-6 text-end fw-bold">

                                        <?= rupiah($dp) ?>

                                    </div>

                                </div>


                                <!-- Tenor -->
                                <div class="row mb-3">

                                    <div class="col-6">
                                        Tenor
                                    </div>

                                    <div class="col-6 text-end fw-bold">

                                        <?= $tenorTahun ?> Tahun
                                        (<?= $tenorBulan ?> Bulan)

                                    </div>

                                </div>


                                <hr>


                                <!-- Angsuran -->
                                <div class="text-center">

                                    <p class="text-muted mb-1">
                                        Angsuran Per Bulan
                                    </p>

                                    <h2 class="text-primary fw-bold">

                                        <?= rupiah($angsuran) ?>

                                    </h2>

                                </div>

                            </div>

                        </div>

                    </div>

                </div>

            </div>

        </section>

    <?php endif; ?>


    <!-- ==================== FOOTER ==================== -->

    <footer
        id="kontak"
        class="bg-dark text-white py-4">

        <div class="container text-center">

            <h5>
                🚗 CalCar
            </h5>

            <p class="mb-1">
                Kalkulator Kredit Mobil Sederhana
            </p>

            <small class="text-secondary">

                &copy; <?= date("Y") ?> CalCar

            </small>

        </div>

    </footer>


    <!-- Bootstrap JavaScript -->
    <script
        src="js/bootstrap.bundle.min.js">
    </script>

</body>

</html>
