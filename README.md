# Tugas-2-Pemrograman-Berbasis-Perangkat-Bergerak
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Data Cuaca Jakarta</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f6f8;
      color: #333;
      padding: 20px;
    }
    h1 {
      text-align: center;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
      background: white;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 8px;
      text-align: center;
    }
    th {
      background: #0078d7;
      color: white;
    }
  </style>
</head>
<body>
  <h1>Prakiraan Cuaca Jakarta (Open-Meteo API)</h1>
  <table id="weatherTable">
    <thead>
      <tr>
        <th>Waktu</th>
        <th>Suhu (°C)</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>

  <script>
    async function getWeather() {
      const url = 'https://api.open-meteo.com/v1/forecast?latitude=-6.2&longitude=106.8&hourly=temperature_2m';
      const response = await fetch(url);
      const data = await response.json();

      const times = data.hourly.time;
      const temps = data.hourly.temperature_2m;

      const tbody = document.querySelector('#weatherTable tbody');
      tbody.innerHTML = '';

      for (let i = 0; i < times.length; i++) {
        const row = document.createElement('tr');
        const timeCell = document.createElement('td');
        const tempCell = document.createElement('td');

        timeCell.textContent = new Date(times[i]).toLocaleString('id-ID');
        tempCell.textContent = temps[i];

        row.appendChild(timeCell);
        row.appendChild(tempCell);
        tbody.appendChild(row);
      }
    }

    getWeather();
  </script>
</body>
</html>
