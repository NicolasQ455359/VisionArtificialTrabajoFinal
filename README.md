# VisionArtificialTrabajoFinal

## Idea: La idea nació de la idea del primer proyecto y quiero que el cuerpo pueda ser una forma de expresión de arte digital.

### IDEAS GENERADAS CON CHAT GPT

1. Cuerpo-Lienzo
   
•	Técnica: Detección de pose (poseNet o MediaPipe Pose).
•	Idea: Tu cuerpo es el pincel. Cada movimiento genera trazos, partículas o colores que llenan la pantalla.
•	Interacción: Levantar brazos cambia el color; moverse rápido genera más energía; moverse lento calma la escena.
•	Intención: Explorar la conexión entre movimiento, emoción y arte.
•	Sensación: danza, energía, libertad, expresión corporal.

💠 2. Umbral
•	Técnica: Segmentación corporal (BodyPix o MediaPipe SelfieSegmentation).
•	Idea: El cuerpo es una puerta que revela mundos ocultos; donde tú te mueves, el fondo se transforma.
•	Interacción: Tu silueta abre ventanas de color, textura o luz. Si te alejas, se cierran.
•	Intención: Representar la presencia, el paso entre lo real y lo digital, o el equilibrio entre ambos mundos.
•	Sensación: misterio, introspección, poesía visual.

💠 3. Gestos de Luz
•	Técnica: Clasificación/detección de manos (Handpose o MediaPipe Hands).
•	Idea: Invocas partículas o luces con tus gestos (pinch, abrir la palma, girar la mano).
•	Interacción: Juntas dedos → creas luz; abres la mano → expandes o destruyes; giras → cambias color.
•	Intención: Mostrar cómo la energía creativa surge del cuerpo, del gesto, del control sutil.
•	Sensación: magia, meditación, conexión, creación.
El mecanismo de interacción del proyecto Cuerpo-Lienzo se basa en la detección de pose corporal en tiempo real mediante PoseNet. A partir de estos datos como la posición, distancia y movimiento de las manos, los hombros y el torso se generan respuestas visuales que permiten al usuario pintar con su cuerpo, transformando su movimiento físico en una experiencia artística digital.
El cuerpo actúa como un pincel interactivo, y sus gestos se traducen en variables visuales dentro del entorno de p5.js. Por ejemplo, la distancia entre las manos controla el grosor del trazo, la altura de la mano derecha regula el brillo o la intensidad del color, y la velocidad de los movimientos define la cantidad de partículas emitidas. Estos mapeos convierten gestos naturales y espontáneos en parámetros que alimentan los elementos generativos, como sistemas de partículas, trazos de luz o manchas dinámicas, que evolucionan de forma fluida según la energía corporal.

Modelo Handpose, cada gesto se interpreta como un tipo de pincel o modo de pintura, permitiendo que el usuario cree diferentes estilos visuales solo con el movimiento de sus manos frente a la cámara. 
Gestos
Al juntar el índice y el pulgar, se activa un pincel de partículas luminosas que varía su intensidad según la velocidad del movimiento; al abrir la palma se produce un efecto de expansión que limpia y aclara ciertas zonas; al señalar con un solo dedo se traza una tinta fina y precisa; y con el gesto de paz  se dibujan cintas fluidas que siguen el recorrido de la mano de forma suave y orgánica. Además, mantener el gesto de el índice y el pulgar durante un segundo cambia la paleta de colores y un doble guarda una captura del lienzo. 
Para que la experiencia sea fácil y agradable, el proyecto incluye un pequeño tutorial interactivo que guía al usuario en los primeros segundos. Primero le pide al participante que alinee su mano frente a la cámara; luego le enseña que puede pintar con partículas haciendo el gesto de pulgar e indice, limpiar o expandir la luz abriendo la palma, y dibujar trazos finos o cintas suaves con los gestos de señalar o de paz . Al final, el sistema le recuerda que puede presionar “H” para ver una ayuda rápida con todos los gestos y “S” para guardar su creación.
Las paletas de color también forman parte esencial de la interacción, ya que cada una refleja un estado emocional diferente. Serenidad combina azules y verdes para transmitir calma y equilibrio; Energía utiliza tonos cálidos como magenta y naranja para expresar vitalidad y dinamismo; y Noche mezcla violetas y cian evocando introspección y misterio. Estas paletas pueden cambiarse mediante un gesto largo con la mano, lo que refuerza la idea de que el color también responde al cuerpo y a las emociones del usuario. 

## 1) Resumen del proyecto

Cuerpo-Lienzo es una experiencia interactiva donde el cuerpo pinta. La mano funciona como pincel a través de visión artificial (ml5.js handPose) y un conjunto de gestos mapeados a herramientas expresivas:

Palma abierta → Cinta fluida (acuarela viva)

Puño → Energía (partículas luminosas)

Pinch (pulgar+índice) → Precisión (puntillismo controlado)

Pinch sostenido (~1s) → cambia paleta de color

Índice extendido → Tinta caligráfica (trazo orientado con suavizado)

V (índice+medio) → Spray estelar

Tres dedos (índice+medio+anular) mantenidos → Borrar (wipe animado)

Incluye un tutorial interactivo que muestra el gesto y avanza solo cuando el usuario lo realiza correctamente (con barra de progreso).

## 2) Motivación e intención artística

La idea surge de observar cómo el cuerpo puede ser un medio expresivo: los gestos naturales evocan emociones y ritmo. Quise trasladar esa física del movimiento a un lienzo vivo—sin dispositivos intermedios—para que la persona diseñe con su presencia. La intención es democratizar el control creativo: sin mouse, sin menús complejos; solo cuerpo, gesto, color y tiempo.

## 3) Diseño de interacción 
### 3.1 Mapa gesto →

<img width="882" height="374" alt="image" src="https://github.com/user-attachments/assets/c87bbc3e-940a-4ae8-becd-cc8b99e4821f" />


### 3.2 Tutorial interactivo

Secuencia guiada: muestra demo simbólica de cada gesto + barra de progreso.

Criterio de avance: detección estable durante t ms.

Salida: Espacio cambia a modo libre.

## 4) Sistema visual

Paletas: Serenidad, Energía, Noche, Aurora (cíclicas con pinch sostenido).

Fondo aurora: capas noise con alpha para “respirar” color sin distraer.

Post-FX: RGB split sutil + viñeta suave.

Pinceles:

Cinta fluida: polilínea con noise y grosor por velocidad.

Energía: partículas ADD con “chispas” proporcionales al movimiento.

Precisión: puntillismo micro con cursor filtrado (lerp) para estabilidad.

Caligrafía: rects orientados por la dirección muñeca→índice + suavizado temporal (ventana móvil).

Spray estelar: partículas rectangulares rotadas con decaimiento temporal.

Borrado: wipe circular expandido y reseteo de buffers.

## 5) Desafíos y soluciones
### 5.1 “No se ve el tutorial”

Causa: el overlay quedaba bajo el image(pg,0,0) o no había mano detectada.

Solución: reordenar draw() (tutorial después de pintar) y añadir mensajes claros “Manos: 0”.

### 5.2 Falsos positivos en gestos

Causa: variación de luz/ángulos.

Solución: ventanas temporales (hold), umbrales separados y lerp en cursores.

### 5.3 Dibujo “tembloroso”

Causa: ruido natural del tracking.

Solución: estabilizador de trazo (ventana móvil) + cursor filtrado en precisión.

### 5.4 Borrado accidental

Solución: gesto raro (tres dedos) + mantener + animación de confirmación.

## 6) Protocolo de pruebas

Iluminación: luz frontal; probar con luz cálida y fría.

Distancia: 30–60 cm de la cámara.

Fondo: evitar fondos muy oscuros o con movimiento.

Mano derecha/izquierda: validado con ambas.

Estabilidad: medir tasa de detección por gesto (≥ 90% en 10 repeticiones).

Latencia: objetivo < 60 ms (navegador de escritorio).

## 7) Reflexiones del proceso creativo

Lo que funcionó: vincular gestos metafóricamente a pinceles, y el tutorial demostrativo reduce confuciones con los gestos.

Aprendizaje: balance entre control (precisión, suavizado) y expresión (ruido, aditivos, glow).

## Link: 
[Trabajo final en p5.js](https://editor.p5js.org/NicolasQ455359/sketches/9Y0JLWCSY)

## Presentación
[Ver presentación en Gamma](https://gamma.app/docs/Cuerpo-Lienzo-pintar-con-gestos-uhyhduws5z27yyd)







