<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Filterberechnung</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        .container { max-width: 600px; margin: auto; }
        label, input, button { display: block; margin-top: 10px; }
        input { padding: 5px; width: 100%; }
    </style>
</head>
<body>
    <div class="container">
        <h2>Aktiver Tiefpass</h2>
        <label for="C3">C3 (F):</label>
        <input type="number" id="C3" step="any">
        <label for="C5">C5 (F):</label>
        <input type="number" id="C5" step="any">
        <label for="Qp">Qp:</label>
        <input type="number" id="Qp" step="any">
        <label for="Vo">Vo:</label>
        <input type="number" id="Vo" step="any">
        <label for="wc">ωc (rad/s):</label>
        <input type="number" id="wc" step="any">
        <button onclick="berechneTiefpass()">Berechnen</button>
        <p id="ergebnisTiefpass"></p>
        
        <h2>Aktiver Hochpass</h2>
        <label for="C">C (F):</label>
        <input type="number" id="C" step="any">
        <label for="QpHP">Qp (HP):</label>
        <input type="number" id="QpHP" step="any">
        <label for="OmegaHP">Ωp (HP):</label>
        <input type="number" id="OmegaHP" step="any">
        <button onclick="berechneHochpass()">Berechnen</button>
        <p id="ergebnisHochpass"></p>
    </div>

    <script>
        function berechneTiefpass() {
            let C3 = parseFloat(document.getElementById('C3').value);
            let C5 = parseFloat(document.getElementById('C5').value);
            let Qp = parseFloat(document.getElementById('Qp').value);
            let Vo = parseFloat(document.getElementById('Vo').value);
            let wc = parseFloat(document.getElementById('wc').value);
            
            let R2 = C3 / (2 * C3 * C5 * Qp * wc);
            let R1 = R2 / Math.abs(Vo);
            let R4 = 1 / (R2 * C3 * C5 * Qp * Qp * wc * wc);
            
            document.getElementById('ergebnisTiefpass').innerText = `R2 = ${R2.toFixed(4)} Ω, R1 = ${R1.toFixed(4)} Ω, R4 = ${R4.toFixed(4)} Ω`;
        }

        function berechneHochpass() {
            let C = parseFloat(document.getElementById('C').value);
            let QpHP = parseFloat(document.getElementById('QpHP').value);
            let OmegaHP = parseFloat(document.getElementById('OmegaHP').value);
            
            let R3 = 1 / (3 * OmegaHP * QpHP * C);
            let R5 = (3 * QpHP) / (OmegaHP * C);
            
            document.getElementById('ergebnisHochpass').innerText = `R3 = ${R3.toFixed(4)} Ω, R5 = ${R5.toFixed(4)} Ω`;
        }
    </script>
</body>
</html>
