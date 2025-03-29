<doctype html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Transcripción en Vivo</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        #texto-transcrito {
            font-size: 24px;
            margin-top: 20px;
            color: #333;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 18px 32px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 10px;
            cursor: pointer;
            border-radius: 5px;
        }
    </style>
    </head>
<body>
</head>
<body>
    <h1>Transcripción en Tiempo Real</h1>
    <p>Haz clic en el botón para empezar a hablar.</p>
    <button id="iniciar" onclick="iniciarReconocimiento()">Iniciar Reconocimiento de Voz</button>
    <p id="texto-transcrito"></p>
<p id="texto">Di algo...</p>    
<br>
<br>
<br>



</br>
</br>
    <label for="idioma">Selecciona un idioma de salida:</label>
    <select id="idioma">

     <option value="es-ES">Español</option>
        <option value="en">Inglés</option>
        <option value="fr">Francés</option>
        <option value="de">Alemán</option>
        <option value="it">Italiano</option>
        <option value="pt">Portugués</option>
    </select>

    <br>
    <p id="traduccion">Traducción aquí...</p>
 <script>

        let recognition;

        try {

            recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();

            recognition.lang = 'es-ES';

            recognition.onresult = function(event) {

                const transcript = event.results[0][0].transcript;

                document.getElementById('texto').innerText = "Dijiste: " + transcript;

                traducirTexto(transcript);

            };

            recognition.onerror = function(event) {

                document.getElementById('texto').innerText = "Error en reconocimiento: " + event.error;

            };

        } catch (e) {

            document.getElementById('texto').innerText = "Tu navegador no soporta reconocimiento de voz.";

        }

        function iniciarReconocimiento() {

            if (!recognition) {

                document.getElementById('texto').innerText = "El reconocimiento de voz no está disponible.";

                return;

            }

            document.getElementById('texto').innerText = "Escuchando...";

            recognition.start();

        }

        function traducirTexto(texto) {

            const idiomaDestino = document.getElementById('idioma').value;

            const url = `https://api.mymemory.translated.net/get?q=${encodeURIComponent(texto)}&langpair=es|${idiomaDestino}`;

            fetch(url)

                .then(response => response.json())

                .then(data => {

                    const traduccion = data.responseData.translatedText;

                    document.getElementById('traduccion').innerText = "Traducción: " + traduccion;

                })

                .catch(error => {

                    document.getElementById('traduccion').innerText = "Error en la traducción.";

                    console.error("Error en la traducción:", error);

                });

        }

    </script>

  <br>

  <br>

  <br>

    

</body>

</html>