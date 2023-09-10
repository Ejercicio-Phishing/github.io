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
        
        <!-- Agrega un enlace que abre un mapa de Google en una ventana emergente -->
        <section>
            <p>Ubicación actual:</p>
            <a href="#" id="openMapLink">Ver en Google Maps</a>
        </section>
    </main>
    <footer>
        <p>&copy; Ciberseguridad 2023</p>
    </footer>

    <!-- JavaScript para obtener y mostrar el número de visitante, dirección IP, hora de la visita y geolocalización -->
    <script>
        var visitorNumber = localStorage.getItem('visitorNumber');
        var visitorIP = "";

        if (!visitorNumber) {
            visitorNumber = 1;
        } else {
            visitorNumber = parseInt(visitorNumber) + 1;
        }

        fetch('https://api.ipify.org?format=json')
            .then(response => response.json())
            .then(data => {
                visitorIP = data.ip;
                document.getElementById('visitorIP').textContent = visitorIP;

                fetch('https://ipapi.co/' + visitorIP + '/json/')
                    .then(response => response.json())
                    .then(data => {
                        var location = data.country_name + ', ' + data.region + ', ' + data.city;
                        document.getElementById('ipLocation').textContent = location;
                    })
                    .catch(error => console.error(error));
            })
            .catch(error => console.error(error));

        var visitTime = new Date();
        var visitTimeString = visitTime.toLocaleString();

        localStorage.setItem('visitorNumber', visitorNumber);

        document.getElementById('visitorNumber').textContent = visitorNumber;
        document.getElementById('visitTime').textContent = visitTimeString;

        // JavaScript para abrir un mapa de Google en una ventana emergente
        document.getElementById('openMapLink').addEventListener('click', function(event) {
            event.preventDefault();
            window.open('https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d387244.7113812835!2d-74.25819122283952!3d40.70531136956898!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x89c24fa5d33f083b%3A0xc80b8f06e177fe62!2sNew%20York%2C%20NY!5e0!3m2!1sen!2sus!4v1632101594397!5m2!1sen!2sus', 'Google Maps', 'width=800,height=600');
        });
    </script>
</body>
</html>








