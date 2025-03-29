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