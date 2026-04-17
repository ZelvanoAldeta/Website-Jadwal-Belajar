<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jadwal Belajar Whibie Aldyansyah S.</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f0f2f5;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            color: #333;
        }
        
        .header-card {
            background: #2c3e50;
            color: white;
            width: 100%;
            max-width: 900px;
            text-align: center;
            padding: 20px;
            border-radius: 15px 15px 0 0;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .header-card h1 { margin: 0; font-size: 24px; }
        .header-card p { margin: 5px 0 0; opacity: 0.9; font-size: 18px; }

        /* Gaya Tabel */
        .table-container {
            width: 100%;
            max-width: 900px;
            background: white;
            padding: 20px;
            border-radius: 0 0 15px 15px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            min-width: 600px;
        }

        th, td {
            border: 1px solid #e0e0e0;
            padding: 15px;
            text-align: center;
        }

        th {
            background-color: #3498db;
            color: white;
            text-transform: uppercase;
            font-size: 14px;
        }

        tr:nth-child(even) { background-color: #f8f9fa; }
        tr:hover { background-color: #ebf5fb; transition: 0.3s; }

        .jam { font-weight: bold; color: #2c3e50; background: #f1f1f1; }

        /* Gaya Pencarian Interaktif */
        .search-box {
            margin-top: 30px;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            text-align: center;
            width: 100%;
            max-width: 400px;
        }

        input {
            padding: 10px;
            width: 70%;
            border: 2px solid #ddd;
            border-radius: 5px;
            outline: none;
        }

        button {
            padding: 10px 20px;
            background-color: #27ae60;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }

        button:hover { background-color: #219150; }

        #hasilPencarian {
            margin-top: 15px;
            font-weight: bold;
            color: #2980b9;
        }
    </style>
</head>
<body>

    <div class="header-card">
        <h1>Jadwal Belajar Whibie Aldyansyah S.</h1>
        <p>Kelas: 11 TJKT</p>
    </div>

    <div class="table-container">
        <table>
            <thead>
                <tr>
                    <th>Waktu</th>
                    <th>Senin</th>
                    <th>Selasa</th>
                    <th>Rabu</th>
                    <th>Kamis</th>
                    <th>Jumat</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td class="jam">07:30 - 09:00</td>
                    <td>AIJ (Infrastruktur)</td>
                    <td>ASJ (Sistem)</td>
                    <td>Matematika</td>
                    <td>Bahasa Inggris</td>
                    <td>TLJ (Layanan)</td>
                </tr>
                <tr>
                    <td class="jam">09:15 - 10:45</td>
                    <td>Keamanan Jaringan</td>
                    <td>WAN (Jaringan Luas)</td>
                    <td>Bahasa Indonesia</td>
                    <td>Pendidikan Agama</td>
                    <td>PKK (Produk Kreatif)</td>
                </tr>
            </tbody>
        </table>
    </div>

    <div class="search-box">
        <h3>Cek Mapel Hari Ini</h3>
        <input type="text" id="hariInput" placeholder="Ketik hari (ex: Senin)">
        <button onclick="cariJadwal()">Cek</button>
        <div id="hasilPencarian"></div>
    </div>

    <script>
        const jadwalData = {
            "Senin": "AIJ (Infrastruktur) & Keamanan Jaringan",
            "Selasa": "ASJ (Sistem) & WAN (Jaringan Luas)",
            "Rabu": "Matematika & Bahasa Indonesia",
            "Kamis": "Bahasa Inggris & Pendidikan Agama",
            "Jumat": "TLJ (Layanan) & PKK (Produk Kreatif)"
        };

        function cariJadwal() {
            const input = document.getElementById('hariInput').value.trim();
            const hasil = document.getElementById('hasilPencarian');
            
            // Ubah input jadi huruf depan besar
            const formatHari = input.charAt(0).toUpperCase() + input.slice(1).toLowerCase();

            if (jadwalData[formatHari]) {
                hasil.innerHTML = `Mata Pelajaran: ${jadwalData[formatHari]}`;
                hasil.style.color = "#2980b9";
            } else {
                hasil.innerHTML = "Hari tidak ditemukan!";
                hasil.style.color = "#e74c3c";
            }
        }
    </script>

</body>
</html># Website-Jadwal-Belajar
Web Whibie Aldyansyah S.
