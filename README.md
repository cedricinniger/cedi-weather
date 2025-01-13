<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cedi's Weather</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            text-align: center;
            padding: 20px;
        }
        h1 {
            color: #333;
        }
        iframe {
            margin-top: 20px;
            max-width: 100%;
            border: 1px solid #cccccc;
        }
        .latest-value {
            font-size: 18px;
            color: #333;
            margin-top: 20px;
        }
        footer {
            margin-top: 30px;
            font-size: 14px;
            color: #555;
        }
    </style>
</head>
<body>
    <h1>Cedi's Weather</h1>
    <div class="latest-value">
        <strong>Letzter Wert:</strong> 
        <span id="latestValue">Laden...</span>
    </div>
    <iframe
        width="450" height="260" style="border: 1px solid #cccccc;"
        src="https://thingspeak.com/channels/2787015/charts/1?bgcolor=%23ffffff&color=%23d62020&days=1&dynamic=true&type=line">
    </iframe>

    <footer>
        Cedric Inniger, <span id="currentDate"></span>
    </footer>

    <script>
        // Aktuelles Datum anzeigen
        const currentDateElement = document.getElementById('currentDate');
        const today = new Date();
        const formattedDate = today.toLocaleDateString('de-DE');
        currentDateElement.textContent = formattedDate;

        // Letzten Wert von ThingSpeak abrufen
        const apiKey = "YMO44T6QD7W3AON8"; // Ersetze durch deinen Read API Key (falls erforderlich)
        const channelId = "2787015"; // Channel-ID
        const fieldNumber = "1"; // Feldnummer, aus dem die Daten abgerufen werden
        const latestValueElement = document.getElementById('latestValue');

        async function fetchLatestValue() {
            try {
                const url = `https://api.thingspeak.com/channels/${channelId}/fields/${fieldNumber}/last.json?api_key=${apiKey}`;
                const response = await fetch(url);
                if (response.ok) {
                    const data = await response.json();
                    const value = data.field1; // Aktuellen Wert abrufen
                    latestValueElement.textContent = value + " °C"; // Wert anzeigen
                } else {
                    latestValueElement.textContent = "Fehler beim Abrufen der Daten.";
                }
            } catch (error) {
                console.error("Fehler beim Abrufen der Daten:", error);
                latestValueElement.textContent = "Fehler.";
            }
        }

        // Abrufen des letzten Werts beim Laden der Seite
        fetchLatestValue();
    </script>
</body>
</html>
