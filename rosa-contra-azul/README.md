# Rosa contra Azul

Timbiriche (dots and boxes) para dos, en línea. Tablero de 6×6 cuadrados —
49 puntos, 84 líneas.

## Reglas

1. Por turnos, cada jugador une dos puntos vecinos con una línea.
2. Quien pone el **cuarto** lado de un cuadrado se lo queda: sale su X, rosa o
   azul.
3. **Si cierras un cuadrado, vuelves a jugar.** Ésta es la regla que sostiene
   el juego: sin ella no hay cadenas, ni sacrificios, ni razón para no cerrar.
   Encadenando te llevas cinco cuadrados en un turno.
4. Cuando no quedan líneas, gana quien tenga más cuadrados. 36 es par, así que
   el empate existe.

Rosa siempre parte. En la revancha parte quien perdió.

## Cómo está hecho

`index.html` es un artifact de Claude: una página, sin build, sin dependencias.
El estado vive en la capability `db`, en un solo documento por partida.

    duelos/{codigo}                    tablero completo, turno, orden de colores
    duelos/{codigo}/jugadores/{pid}    nombre

El tablero son tres arrays de enteros — `0` libre, `1` rosa, `2` azul:

    h[43]       líneas horizontales, índice r*6 + c
    v[42]       líneas verticales,   índice r*7 + c
    cuadros[36] dueño de cada cuadrado

Guardar el número del jugador en vez de su id deja el documento en unos pocos
cientos de bytes, así que cada jugada es un solo `update` barato.

**La jugada se pinta antes de confirmarse.** Tocar una línea la dibuja al
instante y recién después escribe; si la escritura falla, el tablero vuelve a
lo que diga el servidor. Esperar el ida y vuelta en cada línea hace que el
juego se sienta pegajoso.

**Los turnos no chocan.** Sólo escribe quien tiene el turno, así que no hay dos
jugadas simultáneas sobre el mismo documento.

### Área de toque

Las líneas se ven de 3px pero el botón mide 22px de grosor, y va acortado 12px
en el largo para que en las intersecciones no se solapen horizontales con
verticales — si no, el último elemento del DOM se roba el toque y marcas la
línea equivocada.

### Nota sobre el archivo

`index.html` empieza en `<title>` y no lleva `<html>`, `<head>` ni `<body>`: el
publicador de Claude los envuelve.

## Publicar

Con la herramienta Artifact, declarando `capabilities: {db: {}}`. Un artifact
que usa `db` es **interno de la organización**: solo lo abren personas con
sesión iniciada en la misma cuenta.
