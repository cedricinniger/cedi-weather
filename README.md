<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aktiver Tiefpass und Hochpass mit Mehrfachgegenkopplung</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        .container {
            max-width: 600px;
            margin: auto;
        }
        .input-group {
            margin-bottom: 15px;
        }
        .input-group label {
            display: block;
            margin-bottom: 5px;
        }
        .input-group input {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
        }
        .result {
            margin-top: 20px;
            padding: 10px;
            background-color: #f4f4f4;
            border: 1px solid #ddd;
        }
        h1 {
            margin-top: 30px;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Tiefpass-Filter -->
        <h1>Aktiver Tiefpass mit Mehrfachgegenkopplung</h1>
        <div class="input-group">
            <label for="C5">C5</label>
            <input type="number" id="C5" placeholder="C5 eingeben">
        </div>
        <div class="input-group">
            <label for="Qp">Qp</label>
            <input type="number" id="Qp" placeholder="Qp eingeben">
        </div>
        <div class="input-group">
            <label for="V0">V0</label>
            <input type="number" id="V0" placeholder="V0 eingeben">
        </div>
        <div class="input-group">
            <label for="fcTP">fc (Grenzfrequenz in Hz)</label>
            <input type="number" id="fcTP" placeholder="fc eingeben">
        </div>
        <div class="input-group">
            <label for="OmegaP">Ωp (Polfrequenz)</label>
            <input type="number" id="OmegaP" placeholder="Ωp eingeben">
        </div>
        <button onclick="calculateTiefpass()">Berechnen (Tiefpass)</button>
        <div class="result" id="tiefpassResult"></div>

        <!-- Hochpass-Filter -->
        <h1>Aktiver Hochpass mit Mehrfachgegenkopplung</h1>
        <div class="input-group">
            <label for="C">C (C1 = C2 = C4)</label>
            <input type="number" id="C" placeholder="C eingeben">
        </div>
        <div class="input-group">
            <label for="QpHochpass">Qp</label>
            <input type="number" id="QpHochpass" placeholder="Qp eingeben">
        </div>
        <div class="input-group">
            <label for="fcHP">fc (Grenzfrequenz in Hz)</label>
            <input type="number" id="fcHP" placeholder="fc eingeben">
        </div>
        <button onclick="calculateHochpass()">Berechnen (Hochpass)</button>
        <div class="result" id="hochpassResult"></div>
    </div>

    <script>
        // Tiefpass-Berechnung
        function calculateTiefpass() {
            const C5 = parseFloat(document.getElementById('C5').value);
            const Qp = parseFloat(document.getElementById('Qp').value);
            const V0 = parseFloat(document.getElementById('V0').value);
            const fcTP = parseFloat(document.getElementById('fcTP').value);
            const OmegaP = parseFloat(document.getElementById('OmegaP').value);

            // Umrechnung von fc (Hz) in ωc (rad/s)
            const omegaC = 2 * Math.PI * fcTP;

            // Berechnung von C3 basierend auf Qp, V0 und C5
            const C3 = 4 * Qp * Qp * (1 + Math.abs(V0)) * C5;

            // Berechnung der Widerstände für den Tiefpass
            const R2 = (C3 + Math.sqrt(C3 * C3 - 4 * C3 * C5 * Qp * Qp * (1 + Math.abs(V0)))) / (2 * C3 * C5 * Qp * OmegaP * omegaC);
            const R1 = R2 / Math.abs(V0);
            const R4 = 1 / (R2 * C3 * C5 * OmegaP * omegaC * omegaC);

            // Anzeige der Ergebnisse
            document.getElementById('tiefpassResult').innerHTML = `
                <p>R1: ${R1.toFixed(4)} Ohm</p>
                <p>R2: ${R2.toFixed(4)} Ohm</p>
                <p>R4: ${R4.toFixed(4)} Ohm</p>
            `;
        }

        // Hochpass-Berechnung
        function calculateHochpass() {
            const C = parseFloat(document.getElementById('C').value);
            const Qp = parseFloat(document.getElementById('QpHochpass').value);
            const fcHP = parseFloat(document.getElementById('fcHP').value);

            // Umrechnung von fc (Hz) in ωc (rad/s)
            const omegaC = 2 * Math.PI * fcHP;

            // Berechnung der Widerstände für den Hochpass
            const R3 = 1 / (3 * Qp * C * omegaC);
            const R5 = (3 * Qp) / (C * omegaC);

            // Anzeige der Ergebnisse
            document.getElementById('hochpassResult').innerHTML = `
                <p>R3: ${R3.toFixed(4)} Ohm</p>
                <p>R5: ${R5.toFixed(4)} Ohm</p>
            `;
        }
    </script>
</body>
</html>
