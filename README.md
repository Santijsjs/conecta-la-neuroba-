# conecta-la-neurona-
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Conecta la Neurona | Juego educativo del sistema nervioso</title>
  <meta name="description" content="Juego educativo interactivo para aprender las partes de la neurona, el impulso nervioso y la sinapsis." />
  <link rel="stylesheet" href="style.css" />
</head>
<body>

  <!-- ============================================================
       DEFINICIONES SVG COMPARTIDAS (gradientes y filtros)
       ============================================================ -->
  <svg id="defs-global" width="0" height="0" aria-hidden="true">
    <defs>
      <linearGradient id="grad-soma" x1="0" y1="0" x2="1" y2="1">
        <stop offset="0%" stop-color="#8b5cf6" />
        <stop offset="100%" stop-color="#22d3ee" />
      </linearGradient>
      <linearGradient id="grad-axon" x1="0" y1="0" x2="1" y2="0">
        <stop offset="0%" stop-color="#22d3ee" />
        <stop offset="100%" stop-color="#a78bfa" />
      </linearGradient>
      <linearGradient id="grad-mielina" x1="0" y1="0" x2="0" y2="1">
        <stop offset="0%" stop-color="#c4b5fd" />
        <stop offset="100%" stop-color="#6d28d9" />
      </linearGradient>
      <linearGradient id="grad-musculo" x1="0" y1="0" x2="1" y2="1">
        <stop offset="0%" stop-color="#f472b6" />
        <stop offset="100%" stop-color="#a78bfa" />
      </linearGradient>
      <filter id="brillo" x="-60%" y="-60%" width="220%" height="220%">
        <feGaussianBlur stdDeviation="7" result="desenfoque" />
        <feMerge>
          <feMergeNode in="desenfoque" />
          <feMergeNode in="SourceGraphic" />
        </feMerge>
      </filter>
      <filter id="resplandor" x="-60%" y="-60%" width="220%" height="220%">
        <feGaussianBlur stdDeviation="3" result="d2" />
        <feMerge>
          <feMergeNode in="d2" />
          <feMergeNode in="SourceGraphic" />
        </feMerge>
      </filter>
    </defs>
  </svg>

  <!-- ============================================================
       HUD (puntos, vidas, nivel)
       ============================================================ -->
  <header id="hud" class="oculto">
    <div class="hud-bloque">
      <span class="hud-etiqueta">Nivel</span>
      <span id="hud-nivel" class="hud-valor">1/4</span>
    </div>
    <div class="hud-bloque">
      <span class="hud-etiqueta">Puntos</span>
      <span id="hud-puntos" class="hud-valor">0</span>
    </div>
    <div class="hud-bloque">
      <span class="hud-etiqueta">Vidas</span>
      <span id="hud-vidas" class="hud-valor">❤️❤️❤️</span>
    </div>
    <div class="hud-botones">
      <button id="btn-sonido" class="btn-icono" title="Activar o desactivar sonido">🔊</button>
      <button id="btn-reiniciar" class="btn-icono" title="Reiniciar el juego">↻</button>
    </div>
    <div class="barra-progreso"><div id="barra-relleno"></div></div>
  </header>

  <main id="app">

    <!-- ============ PANTALLA DE INICIO ============ -->
    <section id="pantalla-inicio" class="pantalla activa">
      <div class="logo-neurona" aria-hidden="true">
        <svg viewBox="0 0 420 200">
          <path class="linea-logo" d="M40 100 C90 100 110 60 150 60" />
          <path class="linea-logo" d="M40 100 C90 100 110 140 150 140" />
          <path class="linea-logo" d="M150 100 L260 100" />
          <path class="linea-logo" d="M260 100 C310 100 330 60 380 55" />
          <path class="linea-logo" d="M260 100 C310 100 330 140 380 145" />
          <circle cx="150" cy="100" r="34" fill="url(#grad-soma)" filter="url(#brillo)" />
          <circle cx="150" cy="100" r="13" fill="#0b1020" />
          <circle class="nodo-logo" cx="40" cy="100" r="8" />
          <circle class="nodo-logo" cx="380" cy="55" r="8" />
          <circle class="nodo-logo" cx="380" cy="145" r="8" />
        </svg>
      </div>
      <h1 class="titulo-juego">Conecta la Neurona</h1>
      <p class="frase-inicio">“Aprende anatomía mientras transmites el impulso nervioso.”</p>
      <button id="btn-jugar" class="btn-principal btn-grande">JUGAR</button>
      <button id="btn-aprender" class="btn-secundario">📖 Repaso rápido de conceptos</button>
      <p class="nota-inicio">Sistema nervioso · Ciencias de la Salud I · Universidad del Valle de México, Campus Texcoco</p>
    </section>

    <!-- ============ NIVEL 1: CONSTRUYE LA NEURONA ============ -->
    <section id="pantalla-nivel1" class="pantalla">
      <div class="cabecera-nivel">
        <span class="chip-nivel">Nivel 1 de 4</span>
        <h2>Construye la neurona</h2>
        <p>Arrastra cada estructura hasta su lugar correcto. Si aciertas, se acomodará y te explicaremos su función.</p>
      </div>

      <div class="zona-juego">
        <svg id="svg-nivel1" class="lienzo" viewBox="0 0 860 470" role="img" aria-label="Neurona para armar por partes">

          <!-- ---------- ZONAS VACÍAS (fantasmas punteados) ---------- -->
          <g id="zona-dendritas" class="zona" data-parte="dendritas">
            <rect class="zona-forma" x="40" y="90" width="150" height="290" rx="32" />
            <rect class="zona-hit" x="32" y="82" width="166" height="306" rx="34" />
          </g>

          <g id="zona-soma" class="zona" data-parte="soma">
            <circle class="zona-forma" cx="250" cy="235" r="66" />
            <circle class="zona-hit" cx="250" cy="235" r="70" />
          </g>

          <g id="zona-axon" class="zona" data-parte="axon">
            <rect class="zona-forma" x="320" y="205" width="315" height="60" rx="30" />
            <rect class="zona-hit" x="316" y="198" width="323" height="74" rx="37" />
          </g>

          <g id="zona-mielina" class="zona" data-parte="mielina">
            <rect class="zona-forma" x="342" y="196" width="90" height="78" rx="39" />
            <rect class="zona-forma" x="442" y="196" width="90" height="78" rx="39" />
            <rect class="zona-forma" x="542" y="196" width="90" height="78" rx="39" />
            <rect class="zona-hit" x="342" y="192" width="290" height="86" rx="40" />
          </g>

          <g id="zona-terminales" class="zona" data-parte="terminales">
            <rect class="zona-forma" x="655" y="90" width="175" height="290" rx="32" />
            <rect class="zona-hit" x="647" y="82" width="191" height="306" rx="34" />
          </g>

          <!-- ---------- FIGURAS (aparecen al colocar la pieza) ---------- -->

          <!-- Dendritas -->
          <g id="fig-dendritas" class="figura">
            <path class="rama" d="M188 235 C150 235 120 235 80 235" />
            <path class="rama" d="M188 235 C150 220 122 178 82 158" />
            <path class="rama" d="M188 235 C155 250 130 292 96 312" />
            <path class="rama-fina" d="M118 178 C104 150 92 132 74 118" />
            <path class="rama-fina" d="M146 214 C124 194 106 186 86 184" />
            <path class="rama-fina" d="M132 262 C112 282 96 300 76 310" />
            <path class="rama-fina" d="M162 250 C150 280 140 304 126 322" />
            <circle class="punta" cx="80" cy="235" r="6" />
            <circle class="punta" cx="82" cy="158" r="6" />
            <circle class="punta" cx="96" cy="312" r="6" />
            <circle class="punta" cx="74" cy="118" r="6" />
            <circle class="punta" cx="86" cy="184" r="6" />
            <circle class="punta" cx="76" cy="310" r="6" />
            <circle class="punta" cx="126" cy="322" r="6" />
            <text class="fig-texto" x="108" y="418" text-anchor="middle">Dendritas</text>
          </g>

          <!-- Cuerpo celular o soma -->
          <g id="fig-soma" class="figura">
            <circle cx="250" cy="235" r="62" fill="url(#grad-soma)" />
            <circle cx="250" cy="235" r="24" fill="#0b1020" stroke="#22d3ee" stroke-width="3" />
            <text class="fig-texto" x="250" y="160" text-anchor="middle">Cuerpo celular (soma)</text>
          </g>

          <!-- Axón -->
          <g id="fig-axon" class="figura">
            <line x1="300" y1="235" x2="640" y2="235" stroke="url(#grad-axon)" stroke-width="16" stroke-linecap="round" />
            <text class="fig-texto" x="400" y="320" text-anchor="middle">Axón</text>
          </g>

          <!-- Vaina de mielina -->
          <g id="fig-mielina" class="figura">
            <rect x="342" y="196" width="90" height="78" rx="39" fill="url(#grad-mielina)" opacity="0.95" />
            <rect x="442" y="196" width="90" height="78" rx="39" fill="url(#grad-mielina)" opacity="0.95" />
            <rect x="542" y="196" width="90" height="78" rx="39" fill="url(#grad-mielina)" opacity="0.95" />
            <text class="fig-texto" x="492" y="150" text-anchor="middle">Vaina de mielina</text>
          </g>

          <!-- Terminales axónicas -->
          <g id="fig-terminales" class="figura">
            <path class="rama" d="M640 235 C690 235 700 210 742 176" />
            <path class="rama" d="M640 235 C700 235 710 235 756 235" />
            <path class="rama" d="M640 235 C690 235 700 262 742 296" />
            <circle class="boton" cx="752" cy="168" r="14" />
            <circle class="boton" cx="762" cy="235" r="14" />
            <circle class="boton" cx="752" cy="304" r="14" />
            <text class="fig-texto" x="742" y="418" text-anchor="middle">Terminales axónicas</text>
          </g>

          <!-- Etiqueta flotante de explicación dentro del SVG -->
          <text id="etiqueta-n1" class="etiqueta-flotante" x="430" y="452" text-anchor="middle"></text>
        </svg>

        <div id="banner-n1" class="banner oculto">
          <p class="banner-titulo">¡Neurona completa!</p>
          <p class="banner-sub">Ya reconoces las cinco estructuras principales. Ahora vamos a encenderla.</p>
          <button id="btn-completar-n1" class="btn-principal">TRANSMITIR IMPULSO ⚡</button>
        </div>
      </div>

      <div class="bandeja-contenedor">
        <div id="nivel1-tray" class="bandeja"></div>
        <div class="bandeja-acciones">
          <button id="btn-pista-n1" class="btn-secundario">💡 Pista (señala la zona correcta)</button>
        </div>
      </div>
    </section>

    <!-- ============ NIVEL 2: TRANSMITE EL IMPULSO ============ -->
    <section id="pantalla-nivel2" class="pantalla">
      <div class="cabecera-nivel">
        <span class="chip-nivel">Nivel 2 de 4</span>
        <h2>Transmite el impulso</h2>
        <p>La neurona ya está construida. Presiona el botón y observa cómo viaja la señal eléctrica.</p>
      </div>

      <div class="zona-juego">
        <svg id="svg-nivel2" class="lienzo" viewBox="0 0 860 470" role="img" aria-label="Neurona completa con impulso nervioso">
          <g id="n2-dendritas">
            <path class="rama" d="M188 235 C150 235 120 235 80 235" />
            <path class="rama" d="M188 235 C150 220 122 178 82 158" />
            <path class="rama" d="M188 235 C155 250 130 292 96 312" />
            <path class="rama-fina" d="M118 178 C104 150 92 132 74 118" />
            <path class="rama-fina" d="M146 214 C124 194 106 186 86 184" />
            <path class="rama-fina" d="M132 262 C112 282 96 300 76 310" />
            <path class="rama-fina" d="M162 250 C150 280 140 304 126 322" />
          </g>
          <g id="n2-soma">
            <circle cx="250" cy="235" r="62" fill="url(#grad-soma)" />
            <circle cx="250" cy="235" r="24" fill="#0b1020" stroke="#22d3ee" stroke-width="3" />
          </g>
          <g id="n2-axon">
            <line x1="300" y1="235" x2="640" y2="235" stroke="url(#grad-axon)" stroke-width="16" stroke-linecap="round" />
          </g>
          <g id="n2-mielina">
            <rect x="342" y="196" width="90" height="78" rx="39" fill="url(#grad-mielina)" opacity="0.95" />
            <rect x="442" y="196" width="90" height="78" rx="39" fill="url(#grad-mielina)" opacity="0.95" />
            <rect x="542" y="196" width="90" height="78" rx="39" fill="url(#grad-mielina)" opacity="0.95" />
          </g>
          <g id="n2-terminales">
            <path class="rama" d="M640 235 C690 235 700 210 742 176" />
            <path class="rama" d="M640 235 C700 235 710 235 756 235" />
            <path class="rama" d="M640 235 C690 235 700 262 742 296" />
            <circle class="boton" cx="752" cy="168" r="14" />
            <circle class="boton" cx="762" cy="235" r="14" />
            <circle class="boton" cx="752" cy="304" r="14" />
          </g>

          <!-- Ruta invisible que sigue el impulso nervioso -->
          <path id="ruta-impulso" d="M70 235 L120 235 L188 235 L250 235 L300 235 L640 235 L700 210 L752 168"
                fill="none" stroke="none" />
          <circle id="chispa" cx="70" cy="235" r="11" fill="#ffffff" opacity="0" filter="url(#brillo)" />

          <text id="etiqueta-n2" class="etiqueta-flotante" x="430" y="452" text-anchor="middle">
            Presiona el botón para iniciar el impulso
          </text>
        </svg>
      </div>

      <div class="bandeja-acciones centrada">
        <button id="btn-impulso" class="btn-principal btn-grande">⚡ INICIAR IMPULSO NERVIOSO</button>
      </div>
    </section>

    <!-- ============ NIVEL 3: CONECTA DOS NEURONAS ============ -->
    <section id="pantalla-nivel3" class="pantalla">
      <div class="cabecera-nivel">
        <span class="chip-nivel">Nivel 3 de 4</span>
        <h2>Conecta dos neuronas</h2>
        <p>Arrastra desde las <strong>terminales axónicas</strong> de la primera neurona hasta la zona de la segunda neurona donde la señal debe llegar.</p>
      </div>

      <div class="zona-juego">
        <svg id="svg-nivel3" class="lienzo" viewBox="0 0 900 430" role="img" aria-label="Dos neuronas comunicándose por medio de una sinapsis">
          <!-- Neurona 1 -->
          <g class="neurona-a">
            <path class="rama" d="M96 215 C70 215 52 215 38 215" />
            <path class="rama" d="M96 215 C74 196 58 176 48 162" />
            <path class="rama" d="M96 215 C74 236 58 258 48 272" />
            <circle cx="140" cy="215" r="46" fill="url(#grad-soma)" />
            <circle cx="140" cy="215" r="17" fill="#0b1020" stroke="#22d3ee" stroke-width="2.5" />
            <line x1="182" y1="215" x2="330" y2="215" stroke="url(#grad-axon)" stroke-width="13" stroke-linecap="round" />
            <rect x="212" y="186" width="52" height="58" rx="26" fill="url(#grad-mielina)" opacity="0.95" />
            <rect x="278" y="186" width="52" height="58" rx="26" fill="url(#grad-mielina)" opacity="0.95" />
            <path class="rama-fina" d="M330 215 C348 215 356 190 366 176" />
            <path class="rama-fina" d="M330 215 C352 215 358 215 372 215" />
            <path class="rama-fina" d="M330 215 C348 215 356 240 366 254" />
            <text class="fig-texto pequena" x="140" y="360" text-anchor="middle">Neurona 1 (presináptica)</text>
          </g>

          <!-- Espacio sináptico -->
          <g id="sinapsis-gap">
            <line x1="382" y1="150" x2="382" y2="285" stroke="#22d3ee" stroke-width="2" stroke-dasharray="6 6" opacity="0.5" />
            <line x1="438" y1="150" x2="438" y2="285" stroke="#22d3ee" stroke-width="2" stroke-dasharray="6 6" opacity="0.5" />
            <text class="fig-texto pequena" x="410" y="128" text-anchor="middle">Espacio sináptico</text>
            <text class="fig-texto mini" x="410" y="308" text-anchor="middle">(sinapsis)</text>
          </g>

          <!-- Neurotransmisores (se animan al acertar) -->
          <g id="neurotransmisores" opacity="0"></g>

          <!-- Línea de arrastre de la conexión -->
          <path id="linea-conexion" d="" fill="none" stroke="#facc15" stroke-width="5"
                stroke-dasharray="10 8" opacity="0.9" filter="url(#resplandor)" />

          <!-- Neurona 2 -->
          <g class="neurona-b">
            <path class="rama-fina" d="M438 130 C450 140 452 158 452 176" />
            <path class="rama-fina" d="M438 215 C452 215 458 215 468 215" />
            <path class="rama-fina" d="M438 300 C450 290 452 272 452 254" />
            <circle cx="524" cy="215" r="46" fill="url(#grad-soma)" />
            <circle cx="524" cy="215" r="17" fill="#0b1020" stroke="#22d3ee" stroke-width="2.5" />
            <line x1="566" y1="215" x2="706" y2="215" stroke="url(#grad-axon)" stroke-width="13" stroke-linecap="round" />
            <rect x="598" y="186" width="52" height="58" rx="26" fill="url(#grad-mielina)" opacity="0.95" />
            <rect x="660" y="186" width="52" height="58" rx="26" fill="url(#grad-mielina)" opacity="0.95" />
            <path class="rama-fina" d="M706 215 C724 215 730 190 740 176" />
            <path class="rama-fina" d="M706 215 C728 215 734 215 748 215" />
            <path class="rama-fina" d="M706 215 C724 215 730 240 740 254" />
            <text class="fig-texto pequena" x="600" y="360" text-anchor="middle">Neurona 2 (postsináptica)</text>
          </g>

          <!-- Ruta del impulso dentro de la neurona 2 -->
          <path id="ruta-n3b" d="M455 215 L524 215 L566 215 L706 215 L748 215" fill="none" stroke="none" />
          <circle id="chispa-n3" cx="455" cy="215" r="10" fill="#ffffff" opacity="0" filter="url(#brillo)" />

          <!-- Puertos interactivos -->
          <g id="puerto-a" class="puerto" data-rol="salida" tabindex="0">
            <circle class="puerto-anillo" cx="378" cy="215" r="24" />
            <circle class="puerto-centro" cx="378" cy="215" r="13" />
          </g>
          <g id="puerto-b" class="puerto" data-rol="dendritas" tabindex="0">
            <circle class="puerto-anillo" cx="452" cy="215" r="24" />
            <circle class="puerto-centro" cx="452" cy="215" r="13" />
            <text class="puerto-texto" x="452" y="262" text-anchor="middle">Dendritas</text>
          </g>
          <g id="puerto-c" class="puerto" data-rol="axon" tabindex="0">
            <circle class="puerto-anillo" cx="624" cy="215" r="20" />
            <circle class="puerto-centro" cx="624" cy="215" r="10" />
            <text class="puerto-texto" x="624" y="262" text-anchor="middle">Axón</text>
          </g>
          <g id="puerto-d" class="puerto" data-rol="soma" tabindex="0">
            <circle class="puerto-anillo" cx="524" cy="215" r="20" />
            <circle class="puerto-centro" cx="524" cy="215" r="10" />
            <text class="puerto-texto" x="524" y="152" text-anchor="middle">Soma</text>
          </g>

          <text id="etiqueta-n3" class="etiqueta-flotante" x="450" y="408" text-anchor="middle">
            Arrastra del puerto amarillo (terminales) al puerto correcto de la neurona 2
          </text>
        </svg>
      </div>

      <div class="bandeja-acciones centrada">
        <button id="btn-sinapsis-info" class="btn-secundario">❓ ¿Qué es una sinapsis?</button>
      </div>
    </section>

    <!-- ============ NIVEL 4: DEL CEREBRO AL MÚSCULO ============ -->
    <section id="pantalla-nivel4" class="pantalla">
      <div class="cabecera-nivel">
        <span class="chip-nivel">Nivel 4 de 4</span>
        <h2>Del cerebro al músculo</h2>
        <p>Haz clic sobre las estructuras en el <strong>orden correcto</strong> para armar el recorrido de una señal nerviosa.</p>
      </div>

      <div class="zona-juego">
        <svg id="svg-nivel4" class="lienzo" viewBox="0 0 900 520" role="img" aria-label="Recorrido de la señal nerviosa desde el cerebro hasta el músculo">
          <!-- Silueta del cuerpo -->
          <g class="silueta">
            <circle cx="250" cy="78" r="56" />
            <path d="M206 132 Q250 112 294 132 L308 300 Q250 336 192 300 Z" />
            <path d="M292 168 Q392 176 452 214" stroke-width="30" stroke-linecap="round" />
            <ellipse cx="512" cy="240" rx="52" ry="36" transform="rotate(-16 512 240)" fill="url(#grad-musculo)" opacity="0.9" stroke="none" />
          </g>

          <!-- Cerebro -->
          <g id="n4-cerebro">
            <ellipse cx="230" cy="72" rx="34" ry="27" fill="url(#grad-soma)" opacity="0.9" />
            <ellipse cx="272" cy="72" rx="34" ry="27" fill="url(#grad-soma)" opacity="0.6" />
            <path d="M230 50 Q244 66 230 92 M272 50 Q258 66 272 92" fill="none" stroke="#0b1020" stroke-width="3" />
          </g>

          <!-- Médula espinal -->
          <g id="n4-medula">
            <rect x="238" y="146" width="24" height="164" rx="12" fill="#0e7490" stroke="#22d3ee" stroke-width="2.5" />
            <path d="M238 172 H262 M238 198 H262 M238 224 H262 M238 250 H262 M238 276 H262 M238 302 H262"
                  stroke="#a5f3fc" stroke-width="2" />
          </g>

          <!-- Nervio -->
          <g id="n4-nervio">
            <path d="M262 250 Q360 250 452 236" fill="none" stroke="#22d3ee" stroke-width="7"
                  stroke-dasharray="16 10" stroke-linecap="round" />
          </g>

          <!-- Músculo -->
          <g id="n4-musculo">
            <ellipse cx="512" cy="240" rx="52" ry="36" transform="rotate(-16 512 240)"
                     fill="url(#grad-musculo)" stroke="#f9a8d4" stroke-width="2.5" />
            <path d="M478 226 Q512 240 546 254" fill="none" stroke="#7c2d63" stroke-width="3" />
          </g>

          <!-- Ruta final luminosa -->
          <path id="ruta-n4" d="M250 100 L250 250 L390 244 L512 240" fill="none" stroke="#a78bfa"
                stroke-width="6" stroke-linecap="round" opacity="0" filter="url(#resplandor)" />
          <circle id="chispa-n4" cx="250" cy="100" r="12" fill="#ffffff" opacity="0" filter="url(#brillo)" />

          <!-- Etiquetas que aparecen conforme se ordena -->
          <text id="et-n4-cerebro" class="fig-etiqueta" x="250" y="24" text-anchor="middle" opacity="0">Cerebro</text>
          <text id="et-n4-medula" class="fig-etiqueta" x="352" y="196" text-anchor="middle" opacity="0">Médula espinal</text>
          <text id="et-n4-nervio" class="fig-etiqueta" x="352" y="300" text-anchor="middle" opacity="0">Nervio</text>
          <text id="et-n4-musculo" class="fig-etiqueta" x="600" y="300" text-anchor="middle" opacity="0">Músculo</text>

          <text id="etiqueta-n4" class="etiqueta-flotante" x="450" y="500" text-anchor="middle">
            Ordena el recorrido: ¿qué estructura va primero?
          </text>
        </svg>
      </div>

      <div class="bandeja-contenedor">
        <div id="nivel4-opciones" class="bandeja"></div>
        <div class="bandeja-acciones">
          <button id="btn-reiniciar-n4" class="btn-secundario">↺ Empezar el recorrido de nuevo</button>
        </div>
      </div>
    </section>

    <!-- ============ PANTALLA DE VICTORIA ============ -->
    <section id="pantalla-victoria" class="pantalla">
      <div class="victoria-caja">
        <p class="victoria-icono">🏆</p>
        <h2>¡Excelente! Completaste el recorrido de una señal nerviosa.</h2>
        <p class="victoria-puntos">Puntaje final: <strong id="victoria-puntos">0</strong> puntos</p>
        <div id="victoria-stats" class="victoria-stats"></div>
        <div class="victoria-repaso">
          <h3>Lo que aprendiste</h3>
          <ul>
            <li><strong>Neurona:</strong> célula del sistema nervioso que genera y transmite impulsos eléctricos.</li>
            <li><strong>Dendritas:</strong> reciben las señales de otras células nerviosas.</li>
            <li><strong>Soma (cuerpo celular):</strong> contiene el núcleo, integra la información y mantiene viva a la neurona.</li>
            <li><strong>Axón:</strong> conduce el impulso desde el soma hasta las terminales.</li>
            <li><strong>Vaina de mielina:</strong> aísla el axón y acelera el impulso (conducción saltatoria).</li>
            <li><strong>Terminales axónicas:</strong> liberan neurotransmisores hacia la siguiente célula.</li>
            <li><strong>Sinapsis:</strong> comunicación entre neuronas mediante neurotransmisores que cruzan el espacio sináptico.</li>
            <li><strong>Recorrido:</strong> cerebro → médula espinal → nervio → músculo.</li>
          </ul>
        </div>
        <button id="btn-rejugar" class="btn-principal btn-grande">JUGAR DE NUEVO</button>
      </div>
    </section>
  </main>

  <!-- ============================================================
       MODAL DE PREGUNTAS
       ============================================================ -->
  <div id="modal-pregunta" class="modal">
    <div class="modal-caja">
      <span class="chip-nivel">Pregunta rápida</span>
      <h3 id="pregunta-texto"></h3>
      <div id="opciones" class="opciones"></div>
      <div id="feedback" class="feedback oculto"></div>
      <button id="btn-continuar" class="btn-principal oculto">CONTINUAR</button>
    </div>
  </div>

  <!-- ============================================================
       MODAL DE FIN DE JUEGO
       ============================================================ -->
  <div id="modal-gameover" class="modal">
    <div class="modal-caja">
      <p class="victoria-icono">💔</p>
      <h3>Te quedaste sin vidas</h3>
      <p class="modal-texto">No pasa nada: repasa las explicaciones y vuelve a intentarlo. ¡La práctica hace al maestro!</p>
      <button id="btn-reintentar" class="btn-principal btn-grande">REINTENTAR</button>
    </div>
  </div>

  <!-- ============================================================
       MODAL DE REPASO DE CONCEPTOS
       ============================================================ -->
  <div id="modal-aprender" class="modal">
    <div class="modal-caja modal-ancha">
      <span class="chip-nivel">Ficha educativa</span>
      <h3>La neurona y el impulso nervioso</h3>
      <div class="repaso-grid">
        <article>
          <h4>¿Qué es una neurona?</h4>
          <p>Es la célula principal del sistema nervioso. Recibe información, la procesa y la transmite en forma de impulso nervioso (una señal eléctrica).</p>
        </article>
        <article>
          <h4>Partes principales</h4>
          <p>Dendritas → soma → axón → vaina de mielina → terminales axónicas.</p>
        </article>
        <article>
          <h4>Impulso nervioso</h4>
          <p>Cambio eléctrico que viaja por la membrana de la neurona. Gracias a la mielina, el impulso salta entre los nódulos y avanza más rápido.</p>
        </article>
        <article>
          <h4>Sinapsis</h4>
          <p>Es el punto de comunicación entre dos neuronas. El axón libera neurotransmisores que cruzan el espacio sináptico y llegan a las dendritas de la siguiente neurona.</p>
        </article>
        <article>
          <h4>Del cerebro al músculo</h4>
          <p>El cerebro decide el movimiento, la orden baja por la médula espinal, viaja por los nervios y llega al músculo, que responde contrayéndose.</p>
        </article>
        <article>
          <h4>Pregunta guía</h4>
          <p>¿Qué estructura recibe las señales de otras neuronas? → <strong>Las dendritas.</strong></p>
        </article>
      </div>
      <button id="btn-cerrar-aprender" class="btn-principal">ENTENDIDO</button>
    </div>
  </div>

  <!-- Aviso flotante (toast) para explicaciones breves -->
  <div id="toast" class="toast"><span id="toast-texto"></span></div>

  <script src="script.js"></script>
</body>
</html>
