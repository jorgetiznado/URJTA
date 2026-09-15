# Bachillerato

El juego de papel y lápiz chileno (Tutti Frutti / Basta / Stop), para jugar en
sala, cada quien desde su teléfono.

## Cómo se juega

Se sortea una letra y todos llenan las ocho categorías con palabras que
empiecen con ella. El primero que termina grita **¡BACHILLERATO!** y la ronda
se cierra para todos.

| Categoría | |
|---|---|
| 1 | Nombre |
| 2 | Apellido |
| 3 | Animal |
| 4 | País o ciudad |
| 5 | Color o cosa |
| 6 | Fruta o verdura |
| 7 | Cantante o grupo |
| 8 | Peli o serie |

### Puntaje

| Puntos | Cuándo |
|---|---|
| **200** | Fuiste el único que respondió esa categoría |
| **100** | Respondiste y nadie repitió tu palabra |
| **50** | Alguien más puso exactamente lo mismo |
| **0** | En blanco, no empieza con la letra, o el anfitrión la anuló |

Las palabras se comparan sin tildes, sin mayúsculas y sin espacios de sobra:
`Mandarina` y `mandarína` cuentan como la misma.

Se sortean las letras sin repetir hasta agotarlas. Quedan fuera **K, Ñ, Q, W,
X, Y, Z**, que en español dejan rondas en blanco.

## Cómo está hecho

`index.html` es un artifact de Claude: una sola página, sin build, sin
dependencias. El estado de la partida vive en la capability `db` (documentos
JSON en tiempo real), así que no hay servidor propio que mantener.

    salas/{codigo}                       estado de la sala, letra, ronda
    salas/{codigo}/jugadores/{pid}       quién está en la mesa
    salas/{codigo}/respuestas/r{n}__{pid} la hoja entregada de esa ronda
    salas/{codigo}/resultados/r{n}       puntaje calculado y anulaciones

El anfitrión es quien crea la sala: reparte las letras, cierra las rondas y
puede anular respuestas inventadas. El puntaje total no se acumula en ningún
contador — se recalcula sumando los documentos de `resultados`, así que anular
una palabra ajusta el marcador sin arrastrar errores.

### Nota sobre el archivo

`index.html` está escrito como cuerpo de artifact: empieza en `<title>` y no
lleva `<html>`, `<head>` ni `<body>`. El publicador de Claude los envuelve.
Abrirlo directo en el navegador funciona a medias y sin base de datos.

## Publicar

Se publica con la herramienta Artifact declarando `capabilities: {db: {}}`.
Una advertencia que importa: **un artifact que usa `db` es interno de la
organización**. Solo lo abren personas con sesión iniciada dentro de la misma
cuenta. Para jugar con gente de afuera hace falta un servidor propio.
