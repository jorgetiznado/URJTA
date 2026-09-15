# Cuadritos

Juego de dos: uno canta un número, el otro lo busca en una grilla revuelta, y
mientras busca el que cantó va rayando cuadritos. Lo que alcanzó a rayar es
suyo. Después se dan vuelta los papeles.

## Reglas

Seis turnos, tres cantadas por lado.

1. El cantor elige un número del 1 al 100 desde una grilla **ordenada** — nunca
   ve dónde cayó en la revuelta.
2. El buscador recibe una grilla de 100 números barajados y tiene que encerrar
   ese número. Si toca el equivocado no pasa nada: sigue buscando.
3. Mientras tanto el cantor raya: **un toque, un cuadrito**, hasta 120.
4. Al encerrar el número el turno se cierra y los cuadritos rayados se anotan.

Gana quien junte más cuadritos en total.

### Por qué un toque por cuadrito

Rayar arrastrando el dedo llenaría los 120 en tres segundos y el juego se
rompe. Un toque por cuadrito conserva el esfuerzo que en el papel pone la mano,
y como se raya en orden no hay que apuntar: tocas cualquier parte de tu
cuadrícula y se raya el que sigue.

## Cómo está hecho

`index.html` es un artifact de Claude: una página, sin build, sin dependencias.
El estado vive en la capability `db`.

    mesas/{codigo}                    estado, turno, cantor, número, tablero barajado
    mesas/{codigo}/jugadores/{pid}    nombre y cuánto lleva rayado ahora mismo
    mesas/{codigo}/turnos/t{n}        turno cerrado: cuántos rayó y en cuánto tiempo

Dos detalles que importan:

**El rayado no escribe en cada toque.** Sería una escritura por pulsación. El
conteo es local y se avisa al rival con un write cada ~700 ms; el valor
definitivo se guarda una vez, al cerrar el turno.

**Los totales no se acumulan en un contador.** Se suman los documentos de
`turnos`, así que un reintento no puede contar dos veces lo mismo.

Si el cantor se desconecta antes de cerrar su turno, el buscador lo cierra a
los 4 segundos con el último conteo que alcanzó a ver.

### Nota sobre el archivo

`index.html` empieza en `<title>` y no lleva `<html>`, `<head>` ni `<body>`: el
publicador de Claude los envuelve. Abrirlo directo en el navegador funciona a
medias y sin base de datos.

## Publicar

Con la herramienta Artifact, declarando `capabilities: {db: {}}`. Un artifact
que usa `db` es **interno de la organización**: solo lo abren personas con
sesión iniciada en la misma cuenta.
