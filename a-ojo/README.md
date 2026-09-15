# A Ojo

Sale un número del 1 al 20 y cada jugador dibuja una línea recta de ese largo.
Se miden todas y gana quien acumule menos error. De dos a seis jugadores,
cinco rondas.

## Reglas

1. Antes de la primera ronda se muestra una barra de referencia que vale **5**.
   Se ve una sola vez en toda la partida.
2. Cada ronda sale un número del 1 al 20, sin repetirse.
3. Arrastras una línea recta sobre el recuadro. Puedes redibujarla todas las
   veces que quieras; entregar es definitivo.
4. Cuando todos entregaron se miden las líneas y se ven superpuestas, cada una
   con su color y su medida.
5. Gana quien termine con **menos error acumulado**.

## Las dos decisiones que sostienen el juego

**La referencia vale 5, no 1.** Calibrar hasta 20 desde una sola unidad
multiplica el error de estimación por veinte y el juego se vuelve ruido. Desde
5 el jugador duplica o divide, que es una operación que el ojo sí sabe hacer.

**La escala no es física.** En pantalla no se puede medir en centímetros: los
píxeles CSS no corresponden a centímetros reales, cambian con el zoom y con la
densidad del monitor, y en un teléfono de 7 cm de ancho no cabe una línea de 20.
Por eso el lienzo es un `viewBox` de 1000×1000 y una unidad de juego son 40 de
esas — 20 unidades ocupan el 80% del lado, en cualquier pantalla. Cada jugador
ve la referencia en su propio lienzo y a su propia escala, así que dos personas
con monitores muy distintos juegan exactamente el mismo juego.

## Cómo está hecho

`index.html` es un artifact de Claude: una página, sin build, sin dependencias.

    reglas/{codigo}                      estado, ronda, números de la partida
    reglas/{codigo}/jugadores/{pid}      nombre
    reglas/{codigo}/trazos/r{n}__{pid}   la línea entregada, en coordenadas del viewBox

**Cada uno escribe su propio trazo.** Un documento por jugador y ronda, así que
aunque todos entreguen a la vez no hay escrituras que se pisen.

**Nada de lo medido se guarda.** Los largos, los errores y el acumulado se
calculan desde los trazos cada vez que se pintan. No hay contadores que puedan
desincronizarse ni sumar dos veces.

**El trazo se mueve, no se redibuja.** Durante el arrastre sólo se actualizan
los extremos de la línea que ya existe; rehacer el SVG completo en cada
`pointermove` va a tirones en un teléfono.

### Los trazos son visibles antes de tiempo

La interfaz no muestra las líneas de los demás hasta que todos entregaron, pero
los documentos están en la base compartida: alguien con las herramientas del
navegador abiertas podría ver un trazo ajeno antes de dibujar el suyo. Entre
amigos no es un problema; conviene saberlo igual.

### Nota sobre el archivo

`index.html` empieza en `<title>` y no lleva `<html>`, `<head>` ni `<body>`: el
publicador de Claude los envuelve.

## Publicar

Con la herramienta Artifact, declarando `capabilities: {db: {}}`. Un artifact
que usa `db` es interno de la organización: solo lo abren personas con sesión
iniciada en la misma cuenta.
