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
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- Bootstrap Icons -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">

    <style>
        body {
            background: #fff;
            color: #222;
        }

        .navbar {
            border-bottom: 1px solid #ddd;
        }

        .brand-box {
            width: 48px;
            height: 48px;
            border: 1px solid #ccc;
            border-radius: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: #fff;
        }

        .brand-box img {
            width: 32px;
            height: 32px;
            object-fit: contain;
        }

        .brand-text small {
            display: block;
            font-size: 11px;
            color: #555;
        }

        .nav-link {
            color: #333 !important;
            font-size: 14px;
            padding: 18px 14px !important;
        }

        .nav-link.active {
            border-bottom: 2px solid #222;
            font-weight: 600;
        }

        .hero {
            min-height: 315px;
            background: linear-gradient(90deg, #fff 0%, #f8f8f8 45%, #e9e9e9 100%);
            position: relative;
            overflow: hidden;
        }

        .hero::after {
            content: "";
            position: absolute;
            right: 5%;
            bottom: -30px;
            width: 48%;
            height: 75%;
            background: url("https://images.unsplash.com/photo-1542282088-fe8426682b8f?auto=format&fit=crop&w=1000&q=80") center/cover no-repeat;
            opacity: .18;
            filter: grayscale(1);
        }

        .hero-content {
            position: relative;
            z-index: 2;
            padding: 65px 0 55px;
        }

        .hero h1 {
            font-weight: 700;
            font-size: 34px;
            line-height: 1.15;
        }

        .hero p {
            color: #555;
            max-width: 380px;
        }

        .hero-car {
            width: 100%;
            max-width: 520px;
            height: 250px;
            object-fit: contain;
            filter: grayscale(1);
            mix-blend-mode: multiply;
        }

        .arrow-btn {
            width: 40px;
            height: 40px;
            border: 1px solid #bbb;
            border-radius: 50%;
            background: #fff;
            color: #222;
            display: flex;
            align-items: center;
            justify-content: center;
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            z-index: 3;
        }

        .arrow-left { left: 18px; }
        .arrow-right { right: 18px; }

        .dots {
            position: absolute;
            bottom: 12px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 3;
        }

        .dots span {
            display: inline-block;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: #ccc;
            margin: 0 4px;
        }

        .dots span.active { background: #333; }

        .calculator-section {
            padding: 14px 0 35px;
            background: #fff;
        }

        .main-card {
            border: 1px solid #ccc;
            border-radius: 5px;
            background: #fff;
            height: 100%;
        }

        .card-title {
            font-size: 19px;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 22px;
        }

        .card-title i {
            font-size: 25px;
        }

        .form-label {
            font-weight: 600;
            margin-bottom: 7px;
        }

        .input-group-text {
            background: #fff;
        }

        .choice-row {
            display: flex;
            gap: 5px;
            flex-wrap: wrap;
            margin-top: 8px;
        }

        .choice-row .btn {
            flex: 1;
            min-width: 48px;
            font-size: 13px;
            padding: 7px 5px;
        }

        .result-total {
            background: #f4f4f4;
            border: 1px solid #ccc;
            border-radius: 5px;
            padding: 13px;
            text-align: center;
            margin-bottom: 12px;
        }

        .result-total small {
            display: block;
            font-size: 14px;
        }

        .result-total strong {
            display: block;
            font-size: 28px;
            line-height: 1.2;
        }

        .result-list {
            border: 1px solid #ccc;
            border-radius: 5px;
            overflow: hidden;
        }

        .result-item {
            display: grid;
            grid-template-columns: 42px 1fr 1fr;
            min-height: 48px;
            border-bottom: 1px solid #ddd;
            align-items: center;
        }

        .result-item:last-child { border-bottom: 0; }

        .result-icon {
            text-align: center;
            font-size: 18px;
        }

        .result-label,
        .result-value {
            padding: 8px 10px;
            font-size: 13px;
        }

        .result-value {
            border-left: 1px solid #ddd;
        }

        .result-item.final {
            font-weight: 700;
        }

        .result-item.final .result-value {
            font-size: 16px;
        }

        .footer-top {
            border-top: 1px solid #ccc;
            padding: 25px 0;
        }

        .footer-column {
            border-right: 1px solid #ccc;
            min-height: 125px;
        }

        .footer-column:last-child { border-right: 0; }

        .footer-title {
            font-weight: 700;
            margin-bottom: 10px;
        }

        .footer-text,
        .footer-contact {
            font-size: 13px;
            color: #555;
            line-height: 1.7;
        }

        .footer-bottom {
            border-top: 1px solid #ddd;
            padding: 8px 0;
            text-align: center;
            font-size: 12px;
            color: #555;
        }

        @media (max-width: 767px) {
            .nav-link.active { border-bottom: 0; }
            .hero { min-height: 430px; }
            .hero-content { padding: 45px 30px; }
            .hero h1 { font-size: 28px; }
            .hero-car { height: 190px; }
            .arrow-left { left: 8px; }
            .arrow-right { right: 8px; }
            .footer-column {
                border-right: 0;
                border-bottom: 1px solid #ddd;
                padding-bottom: 18px;
                margin-bottom: 18px;
            }
        }
    </style>
</head>

<body>

    <!-- ==================== NAVBAR ==================== -->
    <nav class="navbar navbar-expand-lg navbar-light bg-white">
        <div class="container">

            <a class="navbar-brand d-flex align-items-center gap-2" href="#beranda">
                <div class="brand-box">
                    <img src="https://static.vecteezy.com/system/resources/previews/013/923/543/original/blue-car-logo-png.png" alt="Logo CalCar">
                </div>
                <div class="brand-text">
                    <strong>AUTO KREDIT</strong>
                    <small>Solusi Kredit Mobil Anda</small>
                </div>
            </a>

            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#menu">
                <span class="navbar-toggler-icon"></span>
            </button>

            <div class="collapse navbar-collapse" id="menu">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <a class="nav-link active" href="#beranda"><i class="bi bi-house-fill me-1"></i> Beranda</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#tentang"><i class="bi bi-buildings me-1"></i> Tentang Perusahaan</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#kontak"><i class="bi bi-telephone-fill me-1"></i> Kontak Perusahaan</a>
                    </li>
                </ul>
            </div>

        </div>
    </nav>


    <!-- ==================== HERO ==================== -->
    <section id="beranda" class="hero">
        <button class="arrow-btn arrow-left" type="button"><i class="bi bi-chevron-left"></i></button>

        <div class="container hero-content">
            <div class="row align-items-center">
                <div class="col-md-6">
                    <h1>Dapatkan Mobil<br>Impian Anda</h1>
                    <p>Hitung cicilan kredit mobil dengan mudah, cepat dan transparan.</p>
                    <a href="#kalkulator" class="btn btn-outline-dark px-4 py-2">Hitung Sekarang</a>
                </div>
                <div class="col-md-6 text-center">
                    <img class="hero-car" src="https://images.unsplash.com/photo-1542282088-fe8426682b8f?auto=format&fit=crop&w=1000&q=80" alt="Mobil">
                </div>
            </div>
        </div>

        <button class="arrow-btn arrow-right" type="button"><i class="bi bi-chevron-right"></i></button>

        <div class="dots">
            <span class="active"></span>
            <span></span>
            <span></span>
        </div>
    </section>


    <!-- ==================== KALKULATOR + HASIL ==================== -->
    <section id="kalkulator" class="calculator-section">
        <div class="container">
            <div class="row g-3">

                <!-- Kalkulator -->
                <div class="col-lg-5">
                    <div class="main-card p-4">
                        <div class="card-title">
                            <i class="bi bi-calculator"></i>
                            <span>Hitung Kredit Mobil</span>
                        </div>

                        <form method="POST">

                            <!-- Harga Mobil -->
                            <div class="mb-3">
                                <label class="form-label">1. Harga Mobil (Rp)</label>
                                <div class="input-group">
                                    <input type="number" name="harga" class="form-control" placeholder="Masukkan harga mobil" required min="1">
                                    <span class="input-group-text">Rp</span>
                                </div>
                            </div>

                            <!-- DP -->
                            <div class="mb-3">
                                <label class="form-label">2. DP (Persen)</label>
                                <select name="dp" class="form-select" required>
                                    <option value="">Pilih DP</option>
                                    <option value="10">10%</option>
                                    <option value="20">20%</option>
                                    <option value="30">30%</option>
                                    <option value="40">40%</option>
                                    <option value="50">50%</option>
                                    <option value="60">60%</option>
                                </select>

                                <div class="choice-row">
                                    <button type="button" class="btn btn-outline-secondary" onclick="pilihDP(10)">10%</button>
                                    <button type="button" class="btn btn-outline-secondary" onclick="pilihDP(20)">20%</button>
                                    <button type="button" class="btn btn-outline-secondary" onclick="pilihDP(30)">30%</button>
                                    <button type="button" class="btn btn-outline-secondary" onclick="pilihDP(40)">40%</button>
                                    <button type="button" class="btn btn-outline-secondary" onclick="pilihDP(50)">50%</button>
                                    <button type="button" class="btn btn-outline-secondary" onclick="pilihDP(60)">60%</button>
                                </div>
                            </div>

                            <!-- Tenor -->
                            <div class="mb-3">
                                <label class="form-label">3. Tenor (Tahun)</label>
                                <select name="tenor" class="form-select" id="tenor" required>
                                    <option value="">Pilih Tenor</option>
                                    <?php for ($i = 1; $i <= 5; $i++): ?>
                                        <option value="<?= $i ?>"><?= $i ?> Tahun</option>
                                    <?php endfor; ?>
                                </select>

                                <div class="choice-row">
                                    <?php for ($i = 1; $i <= 5; $i++): ?>
                                        <button type="button" class="btn btn-outline-secondary" onclick="pilihTenor(<?= $i ?>)"><?= $i ?> Tahun</button>
                                    <?php endfor; ?>
                                </div>
                            </div>

                            <div class="alert alert-light border mb-3">
                                <i class="bi bi-info-circle-fill me-2"></i>
                                Bunga tetap <strong>20%</strong> dari harga mobil
                            </div>

                            <button type="submit" class="btn btn-dark w-100 py-2">
                                Hitung Angsuran
                            </button>
                        </form>
                    </div>
                </div>


                <!-- Hasil -->
                <div class="col-lg-7">
                    <div class="main-card p-4" id="hasil-perhitungan">
                        <div class="card-title">
                            <i class="bi bi-pie-chart-fill"></i>
                            <span>Hasil Perhitungan</span>
                        </div>

                        <?php if ($hasil): ?>

                            <div class="result-total">
                                <small>Angsuran Per Bulan</small>
                                <strong><?= rupiah($angsuran) ?></strong>
                            </div>

                            <div class="result-list">
                                <div class="result-item">
                                    <div class="result-icon"><i class="bi bi-car-front-fill"></i></div>
                                    <div class="result-label">Harga Mobil</div>
                                    <div class="result-value"><?= rupiah($harga) ?></div>
                                </div>

                                <div class="result-item">
                                    <div class="result-icon"><i class="bi bi-percent"></i></div>
                                    <div class="result-label">DP (Persen)</div>
                                    <div class="result-value"><?= $dpPersen ?>%</div>
                                </div>

                                <div class="result-item">
                                    <div class="result-icon"><i class="bi bi-cash-stack"></i></div>
                                    <div class="result-label">Nominal DP</div>
                                    <div class="result-value"><?= rupiah($dp) ?></div>
                                </div>

                                <div class="result-item">
                                    <div class="result-icon"><i class="bi bi-cash-stack"></i></div>
                                    <div class="result-label">Bunga (20% dari harga mobil)</div>
                                    <div class="result-value"><?= rupiah($bunga) ?></div>
                                </div>

                                <div class="result-item">
                                    <div class="result-icon"><i class="bi bi-pie-chart-fill"></i></div>
                                    <div class="result-label">Total Harga + Bunga</div>
                                    <div class="result-value"><?= rupiah($harga + $bunga) ?></div>
                                </div>

                                <div class="result-item">
                                    <div class="result-icon"><i class="bi bi-calculator-fill"></i></div>
                                    <div class="result-label">Jumlah Pinjaman<br>(Total - DP)</div>
                                    <div class="result-value"><?= rupiah($harga + $bunga - $dp) ?></div>
                                </div>

                                <div class="result-item">
                                    <div class="result-icon"><i class="bi bi-calendar3"></i></div>
                                    <div class="result-label">Tenor (Tahun)</div>
                                    <div class="result-value"><?= $tenorTahun ?> Tahun</div>
                                </div>

                                <div class="result-item">
                                    <div class="result-icon"><i class="bi bi-calendar3"></i></div>
                                    <div class="result-label">Jumlah Bulan<br>(Tenor x 12)</div>
                                    <div class="result-value"><?= $tenorBulan ?> Bulan</div>
                                </div>

                                <div class="result-item final">
                                    <div class="result-icon"><i class="bi bi-credit-card-fill"></i></div>
                                    <div class="result-label">Angsuran Per Bulan</div>
                                    <div class="result-value"><?= rupiah($angsuran) ?></div>
                                </div>
                            </div>

                        <?php else: ?>

                            <div class="result-total py-5">
                                <i class="bi bi-calculator fs-1 d-block mb-3"></i>
                                <small>Hasil perhitungan akan muncul di sini.</small>
                                <span class="text-muted">Silakan isi data kredit terlebih dahulu.</span>
                            </div>

                        <?php endif; ?>
                    </div>
                </div>

            </div>
        </div>
    </section>


    <!-- ==================== TENTANG ==================== -->
    <section id="tentang" class="footer-top">
        <div class="container">
            <div class="row g-4">

                <div class="col-md-4 footer-column pe-md-4">
                    <div class="d-flex align-items-center gap-2 mb-2">
                        <div class="brand-box">
                            <img src="https://static.vecteezy.com/system/resources/previews/013/923/543/original/blue-car-logo-png.png" alt="Logo CalCar">
                        </div>
                        <div>
                            <strong>AUTO KREDIT</strong>
                            <small class="d-block text-muted">Solusi Kredit Mobil Anda</small>
                        </div>
                    </div>
                    <p class="footer-text mb-0">
                        Kami membantu Anda mewujudkan mobil impian dengan cicilan yang ringan dan proses mudah.
                    </p>
                </div>

                <div class="col-md-4 footer-column px-md-4">
                    <div class="footer-title">Tentang Perusahaan</div>
                    <p class="footer-text mb-0">
                        CalCar merupakan website sederhana yang membantu pengguna menghitung estimasi kredit mobil dengan mudah dan transparan.
                    </p>
                </div>

                <div class="col-md-4 footer-column ps-md-4" id="kontak">
                    <div class="footer-title">Kontak Perusahaan</div>
                    <div class="footer-contact">
                        <div><i class="bi bi-geo-alt-fill me-2"></i>Jl. Merdeka No. 123, Jakarta, Indonesia</div>
                        <div><i class="bi bi-telephone-fill me-2"></i>(021) 1234 5678</div>
                        <div><i class="bi bi-envelope-fill me-2"></i>info@autokredit.co.id</div>
                        <div><i class="bi bi-globe me-2"></i>www.autokredit.co.id</div>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <!-- ==================== FOOTER ==================== -->
    <footer>
        <div class="footer-bottom">
            &copy; <?= date("Y") ?> CalCar. All rights reserved.
        </div>
    </footer>


    <!-- Bootstrap JavaScript -->
    <script src="js/bootstrap.bundle.min.js"></script>

    <script>
        function pilihDP(nilai) {
            document.querySelector('select[name="dp"]').value = nilai;
        }

        function pilihTenor(nilai) {
            document.querySelector('select[name="tenor"]').value = nilai;
        }
    </script>

</body>
</html>
