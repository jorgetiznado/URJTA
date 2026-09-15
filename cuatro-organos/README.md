# Cuatro Órganos

Juego de cartas para dos a seis. Ganas al tener cuatro órganos sanos de colores
distintos, mientras el resto intenta infectártelos.

Es la mecánica de **Virus!** (Tranjis Games, 2016). Las reglas de un juego no
son propiedad de nadie; el arte, los textos y la marca sí. Por eso el mazo, los
iconos, los nombres de las cartas y todos los textos de este proyecto son
propios. No es el producto oficial ni pretende parecerlo.

## El mazo — 68 cartas

| Tipo | Cuántas | Reparto |
|---|---|---|
| Órganos | 21 | 5 de cada color + 1 comodín |
| Virus | 17 | 4 de cada color + 1 comodín |
| Medicinas | 20 | 4 de cada color + 4 comodines |
| Tratamientos | 10 | 3 Trasplante, 3 Robo, 2 Contagio, 1 Manos limpias, 1 Error de pabellón |

Los cuatro colores son corazón (rojo), estómago (verde), cerebro (azul) y hueso
(amarillo). El comodín vale por cualquiera.

## Reglas

Tienes 3 cartas. En tu turno **juegas una carta o botas hasta tres**, y después
rellenas la mano a 3.

**Órgano** — va a tu cuerpo. No puedes tener dos del mismo color.

**Virus** — sobre un órgano rival del mismo color.

| Estado del órgano | Qué pasa |
|---|---|
| Limpio | queda infectado |
| Ya infectado | el órgano se destruye |
| Protegido | se anulan virus y medicina |
| Inmunizado | no se puede atacar |

**Medicina** — sobre un órgano tuyo del mismo color.

| Estado del órgano | Qué pasa |
|---|---|
| Infectado | queda limpio |
| Limpio | queda protegido |
| Protegido | queda **inmunizado**, para siempre |

**Tratamientos**

| Carta | Qué hace |
|---|---|
| Trasplante | Intercambia un órgano tuyo por uno de un rival. Ninguno inmunizado, y nadie puede terminar con dos del mismo color. |
| Robo de órgano | Te llevas un órgano rival con lo que tenga encima. No inmunizado, y sin repetirte color. |
| Contagio | Cada virus de tus órganos salta a un órgano limpio de un rival del color que corresponda. |
| Manos limpias | Todos los rivales botan su mano. Roban al empezar su turno. |
| Error de pabellón | Intercambias tu cuerpo entero con el de un rival. |

Ganas al tener cuatro órganos **sin virus** de colores distintos. Protegido e
inmunizado cuentan como sanos. Cuando se acaba el mazo se baraja el descarte.

### Diferencia con las reglas originales

El trasplante aquí intercambia un órgano **tuyo** con uno de un rival. En el
juego original puedes intercambiar entre dos jugadores cualesquiera, incluso dos
rivales. La interfaz de tres pasos que eso pide no pagaba lo que costaba.

## Las manos no son secretas de verdad

Esto importa antes de jugar. La capability `db` comparte todos los documentos
entre los jugadores de una partida, y la capability `user` —la que permitiría
guardar cada mano en un subárbol privado por persona— no está disponible en
esta cuenta. La interfaz oculta la mano del rival, pero alguien que abra las
herramientas del navegador puede leerla.

Entre amigos funciona. Contra alguien dispuesto a hacer trampa, no.

## Cómo está hecho

`index.html` es un artifact de Claude: una página, sin build, sin dependencias.

    clinicas/{codigo}                    mazo, descarte, manos, cuerpos, turno, bitácora
    clinicas/{codigo}/jugadores/{pid}    nombre

**El mazo no viaja.** El catálogo de las 68 cartas se genera igual en cada
navegador, siempre en el mismo orden, así que en la base sólo viajan índices del
0 al 67. Una partida entera cabe en unos pocos kilobytes.

**Los órganos recuerdan sus cartas.** Un órgano guarda el id de su propia carta
y los de los virus y medicinas encima. Sin eso, destruir un órgano haría
desaparecer esas cartas del juego y el mazo se degradaría partida a partida.

**Sólo escribe quien tiene el turno.** Cada jugada es un `update` del documento
completo, y como los turnos son exclusivos no hay escrituras que choquen.

### Nota sobre el archivo

`index.html` empieza en `<title>` y no lleva `<html>`, `<head>` ni `<body>`: el
publicador de Claude los envuelve.

## Publicar

Con la herramienta Artifact, declarando `capabilities: {db: {}}`. Un artifact
que usa `db` es interno de la organización: solo lo abren personas con sesión
iniciada en la misma cuenta.
