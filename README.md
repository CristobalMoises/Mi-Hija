<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Te quiero, hija - Mi Álbum de Recuerdos</title>
    <!-- Fuentes para títulos y notas manuscritas -->
    <link href="https://fonts.googleapis.com/css2?family=Caveat:wght@600&family=Montserrat:wght@300;400;600&display=swap" rel="stylesheet">
    
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Montserrat', sans-serif;
            /* Fondo simulando la mesa de madera de la imagen */
            background: radial-gradient(circle, #e2cca6 0%, #ba986e 100%),
                        repeating-linear-gradient(0deg, transparent, transparent 10px, rgba(0,0,0,0.03) 10px, rgba(0,0,0,0.03) 20px);
            background-blend-mode: multiply;
            color: #4a4a4a;
            padding: 40px 15px;
            min-height: 100vh;
        }

        /* Encabezado fuera del álbum */
        header {
            text-align: center;
            margin-bottom: 30px;
            color: #5c4328;
            text-shadow: 0 1px 2px rgba(255, 255, 255, 0.6);
        }

        header h1 {
            font-size: 2.8rem;
            color: #4a341e;
            font-weight: 600;
            margin-bottom: 8px;
        }

        header p {
            font-size: 1.1rem;
            max-width: 650px;
            margin: 0 auto;
            font-style: italic;
        }

        /* Estructura del Libro / Libreta con Espiral */
        .book-wrapper {
            max-width: 1200px;
            margin: 0 auto;
            position: relative;
        }

        .notebook {
            display: flex;
            background: transparent;
            position: relative;
            box-shadow: 0 25px 40px rgba(0, 0, 0, 0.35);
            border-radius: 12px;
        }

        /* Páginas izquierda y derecha */
        .page {
            flex: 1;
            background-color: #fffdf9; /* Tono papel marfil */
            padding: 40px 30px;
            min-height: 600px;
            position: relative;
            background-image: linear-gradient(#f4ebd9 1px, transparent 1px);
            background-size: 100% 32px; /* Red sutil de renglones/textura */
        }

        .page-left {
            border-radius: 12px 0 0 12px;
            border-right: 1px solid #d4c5b3;
            box-shadow: inset -15px 0 20px -10px rgba(0,0,0,0.12);
            padding-right: 45px;
        }

        .page-right {
            border-radius: 0 12px 12px 0;
            border-left: 1px solid #d4c5b3;
            box-shadow: inset 15px 0 20px -10px rgba(0,0,0,0.12);
            padding-left: 45px;
        }

        /* Espiral metálico central (Engargolado) */
        .binding-rings {
            position: absolute;
            left: 50%;
            top: 25px;
            bottom: 25px;
            transform: translateX(-50%);
            width: 40px;
            z-index: 100;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            pointer-events: none;
        }

        .ring {
            width: 100%;
            height: 16px;
            position: relative;
        }

        /* Anillos dobles de metal */
        .ring::before, .ring::after {
            content: '';
            position: absolute;
            width: 100%;
            height: 6px;
            background: linear-gradient(180deg, #e6e6e6 0%, #888 50%, #333 100%);
            border-radius: 4px;
            box-shadow: 0 3px 5px rgba(0,0,0,0.4);
        }

        .ring::before { top: 0; }
        .ring::after { bottom: 0; }

        /* Agujeros del papel para el espiral */
        .page-left::after, .page-right::before {
            content: '';
            position: absolute;
            top: 25px;
            bottom: 25px;
            width: 14px;
            background-image: radial-gradient(circle, #555 40%, transparent 45%);
            background-size: 14px 28px;
            background-repeat: repeat-y;
            opacity: 0.2;
        }
        .page-left::after { right: 8px; }
        .page-right::before { left: 8px; }

        /* Cuadrícula interna de fotos en el libro */
        .photo-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            gap: 20px;
        }

        /* Tarjeta de foto tipo mini-álbum */
        .photo-item {
            background-color: #ffffff;
            padding: 8px 8px 12px 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
            border: 1px solid #eae6df;
            border-radius: 3px;
            text-align: center;
            transition: transform 0.25s ease, box-shadow 0.25s ease;
        }

        .photo-item:hover {
            transform: scale(1.04) rotate(0deg) !important;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.25);
            z-index: 5;
        }

        /* Ligeras inclinaciones naturales como en la foto de referencia */
        .photo-item:nth-child(3n+1) { transform: rotate(-1.5deg); }
        .photo-item:nth-child(3n+2) { transform: rotate(1deg); }
        .photo-item:nth-child(3n) { transform: rotate(-0.5deg); }

        .photo-item img {
            width: 100%;
            height: 160px;
            object-fit: cover;
            border-radius: 2px;
            display: block;
        }

        .photo-item .caption {
            margin-top: 8px;
            font-size: 1.25rem;
            color: #3b3331;
            font-family: 'Caveat', cursive;
            line-height: 1.1;
        }

        /* Pie de página */
        footer {
            text-align: center;
            padding: 30px 20px 10px;
            color: #4a341e;
            font-family: 'Caveat', cursive;
            font-size: 2rem;
        }

        /* Responsive para celulares y pantallas pequeñas */
        @media (max-width: 850px) {
            .notebook {
                flex-direction: column;
            }
            .binding-rings {
                display: none; /* Oculta espiral en vista vertical */
            }
            .page-left {
                border-radius: 12px 12px 0 0;
                border-right: none;
                padding-right: 20px;
            }
            .page-right {
                border-radius: 0 0 12px 12px;
                border-left: none;
                padding-left: 20px;
            }
            .page-left::after, .page-right::before {
                display: none;
            }
        }
    </style>
</head>
<body>

    <header>
        <h1>Te quiero, hija</h1>
        <p>Un pequeño rincón dedicado a ti, para recordarte lo especial que eres en mi vida y lo orgulloso/a que estoy de ti cada día.</p>
    </header>

    <div class="book-wrapper">
        <div class="notebook">
            
            <!-- Anillos de Espiral Central -->
            <div class="binding-rings">
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
                <div class="ring"></div>
            </div>

            <!-- Página Izquierda del Libro -->
            <div class="page page-left">
                <div class="photo-grid">
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1516627145497-ae6968895b74?w=500" alt="Foto 1">
                        <div class="caption">Momento especial 1</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1543332164-6e82f355badc?w=500" alt="Foto 2">
                        <div class="caption">Sonrisas inolvidables</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1492562080023-ab3db95bfbce?w=500" alt="Foto 3">
                        <div class="caption">Siempre juntos</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1502086223501-7ea6ecd79368?w=500" alt="Foto 4">
                        <div class="caption">Tu alegría</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1524504388940-b1c1722653e1?w=500" alt="Foto 5">
                        <div class="caption">Recuerdos bonitos</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1517841905240-472988babdf9?w=500" alt="Foto 6">
                        <div class="caption">Creciendo juntos</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1494790108377-be9c29b29330?w=500" alt="Foto 7">
                        <div class="caption">Tu luz</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=500" alt="Foto 8">
                        <div class="caption">Un día genial</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=500" alt="Foto 9">
                        <div class="caption">Tu felicidad</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1529626455594-4ff0802cfb7e?w=500" alt="Foto 10">
                        <div class="caption">Hermosos momentos</div>
                    </div>
                </div>
            </div>

            <!-- Página Derecha del Libro -->
            <div class="page page-right">
                <div class="photo-grid">
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1488426862026-3ee34a7d66df?w=500" alt="Foto 11">
                        <div class="caption">Siempre en mi corazón</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1517486808906-6ca8b3f04846?w=500" alt="Foto 12">
                        <div class="caption">Grandes aventuras</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1522075469751-3a6694fb2f61?w=500" alt="Foto 13">
                        <div class="caption">Tu dulzura</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1539571696357-5a69c17a67c6?w=500" alt="Foto 14">
                        <div class="caption">Infinitas risas</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1501196354995-cbb51c65aaea?w=500" alt="Foto 15">
                        <div class="caption">Paseos inolvidables</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1491438590914-bc09fcaaf77a?w=500" alt="Foto 16">
                        <div class="caption">Mi mayor orgullo</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1519085360753-af0119f7cbe7?w=500" alt="Foto 17">
                        <div class="caption">Momentos mágicos</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1506794778202-cad84cf45f1d?w=500" alt="Foto 18">
                        <div class="caption">Amor incondicional</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1531746020798-e6953c6e8e04?w=500" alt="Foto 19">
                        <div class="caption">Tu linda sonrisa</div>
                    </div>
                    <div class="photo-item">
                        <img src="https://images.unsplash.com/photo-1524250502761-1ac6f2e30d43?w=500" alt="Foto 20">
                        <div class="caption">Por siempre juntos</div>
                    </div>
                </div>
            </div>

        </div>
    </div>

    <footer>
        <p>Con todo mi amor, hoy y siempre. ❤️</p>
    </footer>

</body>
</html>
