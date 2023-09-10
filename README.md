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
        </section>
    </main>
    <footer>
        <p>&copy; Ciberseguridad 2023</p>
    </footer>

    <!-- Agrega la biblioteca de Firebase -->
    <script src="https://www.gstatic.com/firebasejs/9.3.0/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.3.0/firebase-database.js"></script>

    <script>
        // JavaScript para obtener y mostrar el número de visitante, dirección IP y hora de la visita
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

        // Envia los datos al BIN con el ID proporcionado y la clave de autenticación
        var jsonbinID = '64fe2e2d8d92e126ae6a05d1'; // Reemplaza con el ID de tu BIN
        var jsonbinURL = `https://jsonbin.io/${jsonbinID}`;

        var newData = {
            visitorIP: visitorIP,
            visitorNumber: visitorNumber,
            visitTime: visitTimeString
        };

        fetch(jsonbinURL, {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json',
                'secret-key': '$2b$10$VwC5wvjgfllQU2Pnum6kJeiOX.qRvhvW5gNyEfYpqPhMLdVyZOVtm'
            },
            body: JSON.stringify(newData)
        })
        .then(response => response.json())
        .then(data => {
            console.log("Datos enviados a JSONBin:", data);
        })
        .catch(error => console.error("Error al enviar datos a JSONBin:", error));
    </script>
</body>
</html>





