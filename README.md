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
        footer {
            margin-top: 30px;
            font-size: 14px;
            color: #555;
        }
    </style>
</head>
<body>
    <h1>Cedi's Weather</h1>
    <iframe width="450" height="260" style="border: 1px solid #cccccc;" 
            src="https://thingspeak.com/channels/2787015/charts/1?bgcolor=%23ffffff&color=%23d62020&dynamic=true&results=10&type=line">
    </iframe>

    <footer>
        Cedric Inniger, <span id="currentDate"></span>
    </footer>

    <script>
        // JavaScript, um das aktuelle Datum automatisch einzufügen
        const currentDateElement = document.getElementById('currentDate');
        const today = new Date();
        const formattedDate = today.toLocaleDateString('de-DE');
        currentDateElement.textContent = formattedDate;
    </script>
</body>
</html>
