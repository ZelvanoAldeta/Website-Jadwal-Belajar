<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Jadwal Whibie Aldyansyah S.</title>
    <style>
        :root {
            --primary: #2c3e50;
            --accent: #3498db;
            --success: #27ae60;
            --danger: #e74c3c;
        }
        body {
            font-family: 'Segoe UI', sans-serif;
            background-color: #f4f7f6;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .container {
            width: 100%;
            max-width: 1000px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            overflow: hidden;
        }
        .header {
            background: var(--primary);
            color: white;
            padding: 30px;
            text-align: center;
        }
        .header h1 { margin: 0; font-size: 24px; }
        .header p { margin: 5px 0 0; opacity: 0.8; }

        /* Form Input Section */
        .admin-panel {
            padding: 20px;
            background: #ecf0f1;
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            border-bottom: 2px solid #ddd;
        }
        input, select {
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            color: white;
            transition: 0.3s;
        }
        .btn-add { background: var(--success); }
        .btn-add:hover { background: #219150; }
        .btn-clear { background: var(--danger); }

        /* Table Style */
        .table-section { padding: 20px; overflow-x: auto; }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 15px;
            text-align: center;
        }
        th { background: var(--accent); color: white; }
        tr:nth-child(even) { background: #f9f9f9; }
        .delete-row {
            color: var(--danger);
            cursor: pointer;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <h1>Jadwal Belajar Whibie Aldyansyah S.</h1>
        <p>Kelas: 11 TJKT | Manajemen Jadwal Mandiri</p>
    </div>

    <div class="admin-panel">
        <select id="inputHari">
            <option value="Senin">Senin</option>
            <option value="Selasa">Selasa</option>
            <option value="Rabu">Rabu</option>
            <option value="Kamis">Kamis</option>
            <option value="Jumat">Jumat</option>
        </select>
        <input type="text" id="inputJam" placeholder="Contoh: 07:30 - 09:00">
        <input type="text" id="inputMapel" placeholder="Nama Mata Pelajaran">
        <button class="btn btn-add" onclick="tambahJadwal()">Tambah Jadwal</button>
        <button class="btn btn-clear" onclick="resetJadwal()">Reset Semua</button>
    </div>

    <div class="table-section">
        <table id="tabelJadwal">
            <thead>
                <tr>
                    <th>Hari</th>
                    <th>Waktu</th>
                    <th>Mata Pelajaran</th>
                    <th>Aksi</th>
                </tr>
            </thead>
            <tbody id="bodyJadwal">
                </tbody>
        </table>
    </div>
</div>

<script>
    // Load data saat halaman dibuka
    document.addEventListener('DOMContentLoaded', TampilkanJadwal);

    function tambahJadwal() {
        const hari = document.getElementById('inputHari').value;
        const jam = document.getElementById('inputJam').value;
        const mapel = document.getElementById('inputMapel').value;

        if (jam === "" || mapel === "") {
            alert("Harap isi jam dan mata pelajaran!");
            return;
        }

        const jadwalBaru = { hari, jam, mapel };
        
        // Ambil data lama dari LocalStorage
        let listJadwal = JSON.parse(localStorage.getItem('jadwalWhibie')) || [];
        listJadwal.push(jadwalBaru);
        
        // Simpan kembali
        localStorage.setItem('jadwalWhibie', JSON.stringify(listJadwal));
        
        // Reset form dan refresh tabel
        document.getElementById('inputJam').value = "";
        document.getElementById('inputMapel').value = "";
        tampilkanJadwal();
    }

    function tampilkanJadwal() {
        const tbody = document.getElementById('bodyJadwal');
        tbody.innerHTML = "";
        
        let listJadwal = JSON.parse(localStorage.getItem('jadwalWhibie')) || [];

        // Urutkan berdasarkan hari (opsional)
        const urutanHari = ["Senin", "Selasa", "Rabu", "Kamis", "Jumat"];
        listJadwal.sort((a, b) => urutanHari.indexOf(a.hari) - urutanHari.indexOf(b.hari));

        listJadwal.forEach((item, index) => {
            let row = `<tr>
                <td>${item.hari}</td>
                <td>${item.jam}</td>
                <td>${item.mapel}</td>
                <td class="delete-row" onclick="hapusBaris(${index})">Hapus</td>
            </tr>`;
            tbody.innerHTML += row;
        });
    }

    function hapusBaris(index) {
        let listJadwal = JSON.parse(localStorage.getItem('jadwalWhibie'));
        listJadwal.splice(index, 1);
        localStorage.setItem('jadwalWhibie', JSON.stringify(listJadwal));
        tampilkanJadwal();
    }

    function resetJadwal() {
        if (confirm("Apakah Anda yakin ingin menghapus SEMUA jadwal?")) {
            localStorage.removeItem('jadwalWhibie');
            tampilkanJadwal();
        }
    }
</script>

</body>
</html>
