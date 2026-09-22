# Las que no salen en el libro

Juego individual para estudiar Historia de 6° básico: Chile entre 1831 y hoy.
Sigue punto por punto el temario de la Evaluación N°1 del segundo semestre
(república conservadora y liberal, Constitución de 1833 y sus reformas, ciclo
del salitre, cuestión social, democratización, democracia y derechos).

Seis capítulos. Cada uno tiene una lección de cuatro tarjetas, una quinta
tarjeta llamada **¿Y ellas?** que cuenta dónde estaban las mujeres en ese
momento, y **dos juegos**. Cada juego da un puntaje de 0 a 100; con 60 de
promedio se pasa y se desbloquea una mujer real que vivió esa época. Con 90,
tres estrellas.

## Los juegos

| Mecánica | Qué practica | Dónde |
|---|---|---|
| **Clasificar** | Una tarjeta, dos lados. ¿Vota o no vota en 1833? ¿Idea conservadora o liberal? ¿Democracia o dictadura? Cada respuesta explica por qué. | Caps. 1, 2, 5, 6 |
| **Memorice** | Doce naipes boca abajo: concepto y su significado. Menos intentos, más puntos. | Caps. 1, 4, 6 |
| **Línea del tiempo** | Los años en orden con huecos; se toca el hecho que va en el año marcado. Cuenta los colocados a la primera. | Caps. 2, 4, 5 |
| **Palabra oculta** | Ahorcado con pista: SALITRE, PULPERIA, PAMPINO, ENGANCHE, FICHA. | Cap. 3 |
| **La pulpería** | Una semana en Santa Laura con fichas en vez de dinero. Los precios suben, en Iquique no las aceptan, el tren no se paga con ellas. Cierra con una pregunta. | Cap. 3 |

La pulpería es el único juego con guion: enseña el sistema de fichas
haciéndolo vivir, no describiéndolo. Es la parte del temario que más se
entiende jugándola.

## El simulacro

Las 36 preguntas de tipo prueba (elegir, verdadero o falso, ordenar) no están
en los capítulos: son un **simulacro** desde la portada, doce al azar cada vez,
con explicación en cada respuesta. Las falladas quedan guardadas y se repasan
aparte hasta que salen bien. Dos días antes de la prueba es lo que más sirve.

## Por qué "ellas"

El objetivo OA7 del temario dice textualmente *"la participación de la mujer en
la vida pública"*. Los libros lo cubren en un párrafo. Aquí es la recompensa de
cada capítulo, y la tarjeta ¿Y ellas? de cada lección deja ver la ausencia antes
de mostrar a quien la rompió.

| Capítulo | Contenido del temario | Ella |
|---|---|---|
| 1 | República Conservadora, Constitución de 1833, voto censitario | Mercedes Marín del Solar — primera poeta publicada; escribió el canto fúnebre a Portales (1837) |
| 2 | República Liberal, reformas de 1871 y 1874, leyes laicas, Guerra del Pacífico | Eloísa Díaz — primera médica de Sudamérica (1887), entró por el decreto Amunátegui |
| 3 | Ciclo del salitre: oficinas, fichas, pulpería, capitales ingleses, fin del ciclo | Teresa Flores — dirigenta obrera de Iquique, fundó el Centro Femenino Belén de Sárraga (1913) |
| 4 | Cuestión social: conventillos, huelgas, Santa María 1907, leyes sociales de 1924 | Carmela Jeria — tipógrafa, fundó *La Alborada* (1905), primer periódico de obreras |
| 5 | Democratización: voto (1874 → 1934 → 1949 → 1970), Ley de 1920, Constitución de 1925, cultura | Elena Caffarena — MEMCh, redactó la ley del voto femenino y no la invitaron a la firma |
| 6 | Democracia: características, quiebre (1973) y recuperación (1988–1990), derechos (OA17) | Inés Enríquez — primera intendenta (1950) y primera diputada (1951) |

Todos los datos de las seis son verificables. No hay retratos porque no hay
fotos libres de todas ellas, y no se inventan caras: cada una es un marco de
archivo con sus iniciales.

## Cómo está pensado para estudiar

- **Se equivoca y aprende ahí mismo.** En clasificar y en la pulpería cada
  respuesta trae una explicación. En la línea del tiempo el error rebota sin
  castigo y se sigue buscando; en el memorice y la palabra oculta el juego
  mismo enseña.
- **Se puede terminar en una tarde.** Seis capítulos de unos ocho minutos cada
  uno. Un simulacro toma cinco.
- **Sin tiempo ni penalizaciones.** Es para estudiar, no para competir. Las
  estrellas premian; nada castiga.

## Cómo está hecho

`index.html` es un artifact de Claude: una página, sin build, sin dependencias
y **sin base de datos**. Todo el progreso vive en `localStorage` del navegador
de quien juega. Por eso este juego, a diferencia de los multijugador del mismo
repositorio, no arrastra la restricción de organización y puede compartirse con
cualquiera.

El contenido está en un solo arreglo `CAPITULOS` al principio del script.
Cambiar una pregunta, corregir un dato o agregar un capítulo es editar ahí.

### Nota sobre el archivo

`index.html` empieza en `<title>` y no lleva `<html>`, `<head>` ni `<body>`: el
publicador de Claude los envuelve.

## Publicar

Con la herramienta Artifact, sin `capabilities`. Es una página estática.
