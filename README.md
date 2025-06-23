<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Veridian: Tu Compañero de Bienestar Digital</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #e0f2fe; /* Light blue background for a calming effect */
            display: flex;
            justify-content: center;
            align-items: flex-start; /* Align to top for longer content */
            min-height: 100vh;
            padding: 30px;
        }
        .app-container {
            background-color: #ffffff;
            padding: 40px;
            border-radius: 16px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            max-width: 900px;
            width: 100%;
            text-align: center;
            display: flex;
            flex-direction: column;
            gap: 30px;
            position: relative;
        }
        .section {
            background-color: #f8fafc; /* Lighter background for sections */
            padding: 25px;
            border-radius: 12px;
            box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.05);
            text-align: left;
        }
        .premium-badge {
            display: inline-block;
            background-color: #fbbf24; /* Amber for premium */
            color: #1f2937; /* Dark text */
            font-size: 0.75rem;
            font-weight: bold;
            padding: 4px 8px;
            border-radius: 6px;
            margin-left: 10px;
            vertical-align: middle;
        }
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            display: flex;
            justify-content: center;
            align-items: center;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease-in-out, visibility 0.3s ease-in-out;
            z-index: 1000;
        }
        .modal.show {
            opacity: 1;
            visibility: visible;
        }
        .modal-content {
            background-color: #fff;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.3);
            width: 90%;
            max-width: 500px;
            text-align: center;
            position: relative;
            transform: translateY(-30px);
            transition: transform 0.3s ease-in-out;
            border: 3px solid #60a5fa; /* Blue border for the modal */
        }
        .modal.show .modal-content {
            transform: translateY(0);
        }
        .close-button {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 28px;
            cursor: pointer;
            color: #6b7280;
            transition: color 0.2s;
        }
        .close-button:hover {
            color: #333;
        }
        .voice-text {
            font-style: italic;
            color: #4a5568;
            margin-top: 15px;
            font-size: 1.1em;
            line-height: 1.5;
        }
        .exercise-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        .exercise-card {
            background-color: #fff;
            border: 1px solid #e2e8f0;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
            transition: transform 0.2s;
            cursor: pointer;
            text-align: center;
            position: relative;
        }
        .exercise-card:hover {
            transform: translateY(-5px);
        }
        .exercise-card.premium .overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.6);
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-weight: bold;
            font-size: 1.2rem;
            z-index: 10;
        }
        .exercise-card img {
            width: 100%;
            height: 150px;
            object-fit: cover;
        }
        .exercise-card h4 {
            font-weight: 600;
            margin: 15px 0 10px;
            color: #333;
        }
        .exercise-card p {
            font-size: 0.9em;
            color: #666;
            padding: 0 15px 15px;
        }
        .exercise-detail-modal-content {
            background-color: #fff;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.3);
            width: 90%;
            max-width: 600px;
            text-align: center;
            position: relative;
            transform: translateY(-30px);
            transition: transform 0.3s ease-in-out;
            border: 3px solid #60a5fa;
        }
        .exercise-detail-modal-content h3 {
            font-size: 1.8rem;
            font-weight: bold;
            color: #2c5282;
            margin-bottom: 15px;
        }
        .exercise-detail-modal-content video {
            width: 100%;
            max-width: 400px;
            border-radius: 10px;
            margin-bottom: 20px;
            border: 1px solid #e2e8f0;
        }
        .exercise-detail-modal-content p {
            font-size: 1.1rem;
            color: #4a5568;
            line-height: 1.6;
            text-align: justify;
        }
        .gamification-item {
            background-color: #fff;
            border: 1px solid #e2e8f0;
            border-radius: 10px;
            padding: 15px;
            display: flex;
            align-items: center;
            gap: 15px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
            margin-bottom: 15px;
        }
        .gamification-item.premium .overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.6);
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-weight: bold;
            font-size: 1rem;
            z-index: 10;
            border-radius: 10px;
        }
    </style>
</head>
<body class="bg-blue-50 flex flex-col items-center justify-center min-h-screen p-5">

    <div class="app-container">
        <h1 class="text-4xl font-bold text-blue-800 mb-6">Veridian: Tu Compañero de Bienestar Digital</h1>
        <p class="text-lg text-gray-700 mb-8">
            Tu aliado para una mejor postura, una espalda sin dolor y una mente tranquila.
            Ideal para personas frente a pantallas y para el bienestar de personas de avanzada edad.
        </p>

        <div class="section">
            <h2 class="text-2xl font-semibold text-blue-700 mb-4">
                Detección Inteligente de Postura y Actividad
            </h2>
            <div class="mb-4">
                <p class="text-gray-700 font-bold">Versión de Escritorio:</p>
                <p class="text-gray-600">
                    Utiliza la cámara web para analizar tu postura en tiempo real. Proporciona retroalimentación visual instantánea con indicadores de color y sugerencias claras.
                    <span class="premium-badge">PREMIUM</span>
                </p>
                <div class="mt-4 p-4 bg-yellow-50 border border-yellow-200 rounded-lg text-yellow-800">
                    <p class="font-semibold">Simulación de Detección (Solo para Prototipo):</p>
                    <p>Aquí se mostraría tu cámara web con indicadores de postura. Por ejemplo, si tu postura es incorrecta, un recuadro rojo aparecería y te daría una sugerencia como: "¡Espalda recta, hombros hacia atrás!"</p>
                </div>
            </div>
            <div>
                <p class="text-gray-700 font-bold">Versión Móvil:</p>
                <p class="text-gray-600">
                    Detecta períodos de inactividad prolongada. Al detectarla, envía recordatorios suaves y no intrusivos para animarte a moverte o cambiar de postura.
                </p>
            </div>
            <div class="mt-8">
                <h3 class="text-xl font-semibold text-blue-600 mb-3">Recordatorios Personalizados de Pausas Activas</h3>
                <label for="intervalInput" class="block text-gray-700 text-sm font-semibold mb-2">
                    Intervalo de pausa (minutos):
                </label>
                <input
                    type="number"
                    id="intervalInput"
                    value="60"
                    min="10"
                    class="shadow-sm appearance-none border rounded-lg w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent transition duration-200"
                >
                <div class="flex flex-col sm:flex-row justify-center space-y-4 sm:space-y-0 sm:space-x-4 mt-6">
                    <button
                        id="startButton"
                        class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-lg shadow-md transition duration-300 ease-in-out transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
                    >
                        Iniciar Recordatorios
                    </button>
                    <button
                        id="stopButton"
                        class="bg-red-500 hover:bg-red-600 text-white font-bold py-3 px-6 rounded-lg shadow-md transition duration-300 ease-in-out transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-red-400 focus:ring-offset-2"
                        disabled
                    >
                        Detener Recordatorios
                    </button>
                </div>
                <p id="statusMessage" class="text-gray-500 text-sm mt-4"></p>
                <p class="text-gray-600 mt-4 text-sm">
                    *Las notificaciones con voz amigable (ej. voz infantil) son una característica <strong class="text-blue-700">Premium</strong>.
                </p>
            </div>
        </div>

        <div class="section">
            <h2 class="text-2xl font-semibold text-blue-700 mb-4">
                Biblioteca de Pausas Activas Guiadas
            </h2>
            <p class="text-gray-600 mb-6">
                Una amplia colección de ejercicios cortos (1-5 minutos) enfocados en estiramientos, movilidad y relajación.
                Cada ejercicio incluye videos animados cortos de demostración y descripciones claras.
            </p>
            <div class="exercise-grid">
                <div class="exercise-card" onclick="showExerciseDetail('cuello')">
                    <img src="https://placehold.co/300x150/60a5fa/ffffff?text=Estiramiento+Cuello" alt="Estiramiento de Cuello">
                    <h4>Alivio de Cuello y Hombros</h4>
                    <p>Libera la tensión acumulada por mirar la pantalla.</p>
                </div>
                <div class="exercise-card" onclick="showExerciseDetail('espalda_baja')">
                    <img src="https://placehold.co/300x150/34d399/ffffff?text=Movilidad+Espalda" alt="Movilidad de Espalda">
                    <h4>Movilidad de Espalda Baja y Alta</h4>
                    <p>Ejercicios para prevenir la rigidez y el dolor lumbar.</p>
                </div>
                <div class="exercise-card" onclick="showExerciseDetail('munecas')">
                    <img src="https://placehold.co/300x150/fde047/ffffff?text=Estiramiento+Muñecas" alt="Estiramiento de Muñecas">
                    <h4>Estiramiento de Muñecas y Antebrazos</h4>
                    <p>Fundamental para quienes usan teclado y ratón.</p>
                </div>
                <div class="exercise-card premium">
                    <img src="https://placehold.co/300x150/a78bfa/ffffff?text=Activacion+Piernas" alt="Activación de Piernas">
                    <div class="overlay">PREMIUM</div>
                    <h4>Activación de Piernas y Glúteos</h4>
                    <p>Movimientos para contrarrestar la inactividad de las extremidades inferiores.</p>
                </div>
                <div class="exercise-card premium">
                    <img src="https://placehold.co/300x150/d8b4fe/ffffff?text=Relajacion+Mindfulness" alt="Relajación y Mindfulness">
                    <div class="overlay">PREMIUM</div>
                    <h4>Relajación y Mindfulness</h4>
                    <p>Técnicas de respiración y mini-meditaciones para reducir el estrés mental.</p>
                </div>
                <div class="exercise-card premium">
                    <img src="https://placehold.co/300x150/f0abfc/ffffff?text=Rutinas+Personalizadas" alt="Rutinas Personalizadas">
                    <div class="overlay">PREMIUM</div>
                    <h4>Creación de Rutinas Personalizadas</h4>
                    <p>Diseña tus propias secuencias de ejercicios según tus necesidades.</p>
                </div>
            </div>
            <p class="text-gray-600 mt-6 text-sm">
                *Acceso a la biblioteca completa y creación de rutinas son características <strong class="text-blue-700">Premium</strong>.
            </p>
        </div>

        <div class="section">
            <h2 class="text-2xl font-semibold text-blue-700 mb-4">
                Consejos Integrales para el Bienestar en el Escritorio
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                    <h3 class="text-xl font-semibold text-blue-600 mb-2">Mejora de Postura</h3>
                    <p class="text-gray-600 text-justify">
                        Guías detalladas sobre la postura ideal al sentarse, configuración del monitor, teclado, mouse y silla para optimizar la ergonomía.
                        <span class="premium-badge">DETALLES PREMIUM</span>
                    </p>
                </div>
                <div>
                    <h3 class="text-xl font-semibold text-blue-600 mb-2">Prevención de Dolores de Espalda</h3>
                    <p class="text-gray-600 text-justify">
                        Información sobre las causas comunes del dolor de espalda por el sedentarismo y cómo los ejercicios de la app ayudan a prevenirlos.
                    </p>
                </div>
                <div>
                    <h3 class="text-xl font-semibold text-blue-600 mb-2">Manejo del Estrés y Estado de Ánimo</h3>
                    <p class="text-gray-600 text-justify">
                        Consejos prácticos para reducir el estrés asociado a las jornadas laborales largas, incluyendo técnicas de manejo del tiempo, respiración y la importancia de las pausas.
                        <span class="premium-badge">MÓDULOS COMPLETOS PREMIUM</span>
                    </p>
                </div>
            </div>
        </div>

        <div class="section">
            <h2 class="text-2xl font-semibold text-blue-700 mb-4">
                Seguimiento de Progreso y Motivación
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                    <h3 class="text-xl font-semibold text-blue-600 mb-2">Diario de Bienestar</h3>
                    <p class="text-gray-600 mb-3">
                        Registra tu nivel de dolor, estrés y estado de ánimo a lo largo del día o la semana para ver cómo los hábitos influyen en tu bienestar.
                    </p>
                    <div class="p-3 bg-blue-50 border border-blue-200 rounded-lg text-blue-800 text-sm">
                        <p>Simulación: Aquí irían campos para seleccionar tu estado de ánimo, dolor, etc.</p>
                        <p>Ej: **Hoy me siento:** [Feliz / Neutro / Estresado] **Nivel de dolor:** [Bajo / Medio / Alto]</p>
                    </div>
                </div>
                <div>
                    <h3 class="text-xl font-semibold text-blue-600 mb-2">Retos y Recompensas</h3>
                    <div class="gamification-item">
                        <span class="text-blue-500 text-3xl">&#127942;</span>
                        <div>
                            <h4 class="font-semibold text-gray-800">Reto Diario: "Mueve tu Cuerpo"</h4>
                            <p class="text-gray-600 text-sm">Completa 3 pausas activas hoy.</p>
                        </div>
                    </div>
                    <div class="gamification-item">
                        <span class="text-green-500 text-3xl">&#127881;</span>
                        <div>
                            <h4 class="font-semibold text-gray-800">Logro: "Insignia de Constancia"</h4>
                            <p class="text-gray-600 text-sm">Realiza pausas activas por 7 días consecutivos.</p>
                        </div>
                    </div>
                    <div class="gamification-item premium relative">
                        <div class="overlay">PREMIUM</div>
                        <span class="text-purple-500 text-3xl">&#128176;</span>
                        <div>
                            <h4 class="font-semibold text-gray-800">Recompensa Exclusiva</h4>
                            <p class="text-gray-600 text-sm">Desbloquea nuevo contenido al alcanzar la meta de 30 días.</p>
                        </div>
                    </div>
                    <div class="gamification-item premium relative">
                        <div class="overlay">PREMIUM</div>
                        <span class="text-yellow-500 text-3xl">&#128200;</span>
                        <div>
                            <h4 class="font-semibold text-gray-800">Estadísticas Avanzadas</h4>
                            <p class="text-gray-600 text-sm">Accede a gráficos detallados de tu progreso.</p>
                        </div>
                    </div>
                </div>
            </div>
            <p class="text-gray-600 mt-6 text-sm">
                *Recompensas exclusivas y estadísticas avanzadas son características <strong class="text-blue-700">Premium</strong>.
            </p>
        </div>

        <div class="section bg-blue-100 border border-blue-300">
            <h2 class="text-2xl font-bold text-blue-800 mb-4">¡Desbloquea tu Bienestar Completo con Veridian Premium!</h2>
            <p class="text-blue-700 mb-6">
                Obtén detección avanzada de postura, biblioteca completa de ejercicios, estadísticas detalladas y mucho más.
            </p>
            <button class="bg-gradient-to-r from-purple-500 to-indigo-600 hover:from-purple-600 hover:to-indigo-700 text-white font-bold py-4 px-8 rounded-full shadow-lg transition duration-300 ease-in-out transform hover:scale-105">
                ¡Conoce Veridian Premium!
            </button>
        </div>

    </div>

    <div id="pauseModal" class="modal">
        <div class="modal-content">
            <button class="close-button" onclick="closeModal()">&times;</button>
            <h2 class="text-2xl font-bold text-blue-700 mb-3">¡Hora de una pequeña pausa!</h2>
            <p class="voice-text">"¡Hola! Soy Veri. Tómate un minutito para estirarte y sentirte mejor."</p>
            <img id="exerciseImage" src="https://placehold.co/300x200/60a5fa/ffffff?text=Ejercicio+Veri" alt="Ejercicio de Veri" class="rounded-lg mx-auto my-5 w-full max-w-xs object-cover border border-blue-300">
            <p id="exerciseText" class="text-lg text-gray-700 mb-5">Estira suavemente tu cuello, inclinando la oreja hacia el hombro. Respira profundo. (Haz clic para más detalles).</p>
            <button
                onclick="closeModal()"
                class="mt-6 bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-5 rounded-lg shadow transition duration-300 ease-in-out transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-green-400 focus:ring-offset-2"
            >
                Entendido
            </button>
        </div>
    </div>

    <div id="exerciseDetailModal" class="modal">
        <div class="exercise-detail-modal-content">
            <button class="close-button" onclick="closeExerciseDetailModal()">&times;</button>
            <h3 id="detailTitle"></h3>
            <video id="detailVideo" controls src="" class="mx-auto" poster="https://placehold.co/300x200/e0e0e0/ffffff?text=Video+del+Ejercicio"></video>
            <p id="detailDescription" class="mb-5"></p>
            <button onclick="closeExerciseDetailModal()" class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-5 rounded-lg shadow transition duration-300">Cerrar</button>
        </div>
    </div>

    <script>
        // Array de ejercicios de ejemplo para recordatorios y detalles
        const exercisesData = {
            cuello: {
                title: "Estiramiento de Cuello y Hombros",
                description: "Siéntate derecho y relaja los hombros. Inclina suavemente tu cabeza hacia un lado, intentando que tu oreja toque tu hombro. Mantén por 15-20 segundos y repite al otro lado. Luego, haz círculos suaves con los hombros hacia adelante y hacia atrás.",
                video: "https://www.w3schools.com/html/mov_bbb.mp4" // Placeholder video
            },
            espalda_baja: {
                title: "Movilidad de Espalda Baja y Alta",
                description: "Siéntate en el borde de tu silla, manos en los muslos. Inhala, arquea tu espalda y mira hacia arriba (como una vaca). Exhala, redondea tu espalda y mete el ombligo (como un gato). Repite 5-10 veces. Este ejercicio ayuda a aliviar la rigidez en la columna.",
                video: "https://www.w3schools.com/html/mov_bbb.mp4" // Placeholder video
            },
            munecas: {
                title: "Estiramiento de Muñecas y Antebrazos",
                description: "Extiende un brazo con la palma hacia arriba. Con la otra mano, sujeta los dedos y suavemente jállos hacia abajo, estirando el antebrazo. Mantén 15-20 segundos. Luego, jala los dedos hacia tu cuerpo. Repite con el otro brazo. Ideal para aliviar la tensión de usar el teclado y el ratón.",
                video: "https://www.w3schools.com/html/mov_bbb.mp4" // Placeholder video
            },
            piernas: {
                title: "Activación de Piernas y Glúteos (Premium)",
                description: "De pie, realiza 5-10 mini-sentadillas. Baja ligeramente tu cadera como si fueras a sentarte, sin ir demasiado profundo. Esto activa los músculos de las piernas y glúteos después de un tiempo sentado.",
                video: "https://www.w3schools.com/html/mov_bbb.mp4" // Placeholder video
            },
            relajacion: {
                title: "Relajación y Mindfulness (Premium)",
                description: "Cierra los ojos si te sientes cómodo. Inhala profundamente por la nariz contando hasta 4, siente cómo tu abdomen se expande. Sostén la respiración por 1 segundo, luego exhala lentamente por la boca contando hasta 6 u 8. Repite 5-10 veces para calmar tu mente.",
                video: "https://www.w3schools.com/html/mov_bbb.mp4" // Placeholder video
            }
        };

        const randomExercisesForReminders = [
            { text: "¡Hola! Soy Veri. Tómate un minutito para estirarte y sentirte mejor. Estira tus brazos hacia arriba, como si quisieras tocar el techo.", image: "https://placehold.co/300x200/60a5fa/ffffff?text=Estiramiento+brazos" },
            { text: "¡Hola! Soy Veri. Es momento de mover un poco tu cuello. Rota suavemente el cuello de lado a lado.", image: "https://placehold.co/300x200/34d399/ffffff?text=Rotacion+cuello" },
            { text: "¡Hola! Soy Veri. ¡A activarnos! Levántate y da una pequeña caminata alrededor de tu espacio de trabajo. Puedes ir por un vaso de agua.", image: "https://placehold.co/300x200/fde047/ffffff?text=Caminata+corta" },
            { text: "¡Hola! Soy Veri. Tus hombros te agradecerán este movimiento. Haz círculos con tus hombros hacia adelante y hacia atrás.", image: "https://placehold.co/300x200/a78bfa/ffffff?text=Circulos+hombros" },
            { text: "¡Hola! Soy Veri. Tus muñecas necesitan un respiro. Estira tus muñecas y dedos. Entrelaza tus manos y estíralas hacia afuera.", image: "https://placehold.co/300x200/d8b4fe/ffffff?text=Estiramiento+manos" }
        ];

        let intervalId;
        const intervalInput = document.getElementById('intervalInput');
        const startButton = document.getElementById('startButton');
        const stopButton = document.getElementById('stopButton');
        const statusMessage = document.getElementById('statusMessage');
        const pauseModal = document.getElementById('pauseModal');
        const exerciseText = document.getElementById('exerciseText');
        const exerciseImage = document.getElementById('exerciseImage');
        const detailModal = document.getElementById('exerciseDetailModal');
        const detailTitle = document.getElementById('detailTitle');
        const detailVideo = document.getElementById('detailVideo');
        const detailDescription = document.getElementById('detailDescription');

        function showPauseModal() {
            const randomIndex = Math.floor(Math.random() * randomExercisesForReminders.length);
            const selectedExercise = randomExercisesForReminders[randomIndex];
            exerciseText.textContent = selectedExercise.text.split('. ').slice(1).join('. '); // Remove voice intro for actual exercise text
            exerciseImage.src = selectedExercise.image;
            exerciseImage.alt = selectedExercise.text;

            // Simulate voice:
            const voiceElement = pauseModal.querySelector('.voice-text');
            voiceElement.textContent = selectedExercise.text.split('. ')[0] + '.';

            pauseModal.classList.add('show');
            // In a real app, you'd trigger a voice API here to play the audio.
        }

        function closeModal() {
            pauseModal.classList.remove('show');
            statusMessage.textContent = `Pausa completada. Próximo recordatorio en ${intervalInput.value} minutos.`;
        }

        function showExerciseDetail(exerciseKey) {
            const exercise = exercisesData[exerciseKey];
            if (exercise) {
                detailTitle.textContent = exercise.title;
                detailVideo.src = exercise.video;
                detailDescription.textContent = exercise.description;
                detailModal.classList.add('show');
            }
        }

        function closeExerciseDetailModal() {
            detailModal.classList.remove('show');
            detailVideo.pause();
            detailVideo.currentTime = 0; // Reset video
        }

        startButton.addEventListener('click', () => {
            const intervalMinutes = parseInt(intervalInput.value);
            if (isNaN(intervalMinutes) || intervalMinutes < 10) {
                statusMessage.textContent = 'Por favor, introduce un intervalo válido (mínimo 10 minutos).';
                return;
            }

            clearInterval(intervalId);
            const intervalMilliseconds = intervalMinutes * 60 * 1000;
            intervalId = setInterval(showPauseModal, intervalMilliseconds);

            startButton.disabled = true;
            stopButton.disabled = false;
            intervalInput.disabled = true;
            statusMessage.textContent = `Recordatorios iniciados cada ${intervalMinutes} minutos.`;
        });

        stopButton.addEventListener('click', () => {
            clearInterval(intervalId);
            startButton.disabled = false;
            stopButton.disabled = true;
            intervalInput.disabled = false;
            statusMessage.textContent = 'Recordatorios detenidos.';
            closeModal(); // Ensure modal is closed if active
            closeExerciseDetailModal(); // Ensure detail modal is closed
        });

        window.onload = () => {
            startButton.disabled = false;
            stopButton.disabled = true;
            intervalInput.disabled = false;
        };
    </script>
</body>
</html>
