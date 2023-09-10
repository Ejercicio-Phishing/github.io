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
    <h1>Has mordido el anzuelo</h1>
    <main>
        <section>
            <p>Lamentamos informarte que has sido víctima de un intento de phishing. Tu información ha sido comprometida.</p>
            <p>Número de visitante: <span id="visitorNumber"></span></p>
            <p>Dirección IP del visitante: <span id="visitorIP"></span></p>
            <p>Hora de la visita: <span id="visitTime"></span></p>
        </section>
    </main>
    <footer>
        <p>&copy; Ciberseguridad 2023</p>
    </footer>

    <!-- JavaScript para obtener y mostrar el número de visitante, dirección IP y hora de la visita -->
    <script>
        var visitorNumber = localStorage.getItem('visitorNumber') || 0;
        var visitorIP = "";

        // Incrementa el número de visitante
        visitorNumber = parseInt(visitorNumber) + 1;

        fetch('https://api.ipify.org?format=json')
            .then(response => response.json())
            .then(data => {
                visitorIP = data.ip;
                document.getElementById('visitorIP').textContent = visitorIP;
            })
            .catch(error => console.error(error));

        var visitTime = new Date();
        var visitTimeString = visitTime.toLocaleString();

        localStorage.setItem('visitorNumber', visitorNumber);

        document.getElementById('visitorNumber').textContent = visitorNumber;
        document.getElementById('visitTime').textContent = visitTimeString;
    </script>
</body>
</html>









