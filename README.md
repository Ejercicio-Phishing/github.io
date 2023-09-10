<html>
<head>
    <title>Has mordido el anzuelo</title>
    <style>
        body {
            background-color: black;
            color: white;
        }
    </style>
</head>
<body>
    Has mordido el anzuelo
    <main>
        <section>
            <p>Lamentamos informarte que has sido víctima de un intento de phishing. Tu información ha sido comprometida <a href="https://rb.gy/799bl">
            <img src="https://drive.google.com/uc?id=1wchi4XR7w5Tuh2Qx-54_RuSbFhfltr4R" alt="Imagen de phishing" />
            </a> </p>
        </section>
        <section>
            <p>Número de visitante: <span id="visitorNumber"></span></p>
            <p>Dirección IP del visitante: <span id="visitorIP"></span></p>
            <p>Hora de la visita: <span id="visitTime"></span></p>
            <p>Ubicación de la IP: <span id="ipLocation"></span></p>
        </section>
    </main>
    <footer>
        <p>&copy; Ciberseguridad 2023</p>
    </footer>

    <script>
        // JavaScript para obtener y mostrar el número de visitante, dirección IP, hora de la visita y geolocalización
        var visitorNumber = localStorage.getItem('visitorNumber');
        var visitorIP = "";

        // Incrementa el número de visitante
        if (!visitorNumber) {
            visitorNumber = 1;
        } else {
            visitorNumber = parseInt(visitorNumber) + 1;
        }

        // Obtiene la dirección IP del visitante utilizando un servicio externo (ipify.org)
        fetch('https://api.ipify.org?format=json')
            .then(response => response.json())
            .then(data => {
                visitorIP = data.ip;
                // Muestra la dirección IP en el HTML
                document.getElementById('visitorIP').textContent = visitorIP;

                // Obtiene la geolocalización de la dirección IP usando la respuesta XML
                var response = '<?xml version="1.0" encoding="UTF-8"?>\n' +
                    '<query>\n' +
                    '  <status>success</status>\n' +
                    '  <country>Canada</country>\n' +
                    '  <countryCode>CA</countryCode>\n' +
                    '  <region>QC</region>\n' +
                    '  <regionName>Quebec</regionName>\n' +
                    '  <city>Montreal</city>\n' +
                    '  <zip>H3V</zip>\n' +
                    '  <lat>45.4998</lat>\n' +
                    '  <lon>-73.6087</lon>\n' +
                    '  <timezone>America/Toronto</timezone>\n' +
                    '  <isp>Le Groupe Videotron Ltee</isp>\n' +
                    '  <org>Videotron Ltee</org>\n' +
                    '  <as>AS5769 Videotron Telecom Ltee</as>\n' +
                    '  <query>24.48.0.1</query>\n' +
                    '</query>';

                var parser = new DOMParser();
                var xmlDoc = parser.parseFromString(response, "text/xml");
                var country = xmlDoc.querySelector('country').textContent;
                document.getElementById('ipLocation').textContent = country;
            })
            .catch(error => console.error(error));

        // Obtiene la hora actual
        var visitTime = new Date();
        var visitTimeString = visitTime.toLocaleString();

        // Almacena el número de visitante y la hora de la visita en el almacenamiento local
        localStorage.setItem('visitorNumber', visitorNumber);

        // Muestra el número de visitante y la hora de la visita en el HTML
        document.getElementById('visitorNumber').textContent = visitorNumber;
        document.getElementById('visitTime').textContent = visitTimeString;
    </script>
</body>
</html>


