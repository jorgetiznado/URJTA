# Las que no salen en el libro

Juego individual para estudiar Historia de 6° básico: Chile entre 1831 y hoy.
Sigue punto por punto el temario de la Evaluación N°1 del segundo semestre
(república conservadora y liberal, Constitución de 1833 y sus reformas, ciclo
del salitre, cuestión social, democratización, democracia y derechos).

Seis capítulos. Cada uno tiene una lección de cuatro tarjetas, una quinta
tarjeta llamada **¿Y ellas?** que cuenta dónde estaban las mujeres en ese
momento, y un desafío de seis preguntas. Con cuatro buenas se pasa y se
desbloquea una mujer real que vivió esa época. Con seis, tres estrellas.

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

- **Se equivoca y aprende ahí mismo.** Cada respuesta, buena o mala, viene con
  una explicación de dos líneas. Las preguntas falladas quedan guardadas y se
  repasan desde la portada, barajadas, hasta que salen bien.
- **Se puede terminar en una tarde.** Seis capítulos de unos siete minutos cada
  uno. El repaso de lo fallado toma cinco.
- **Sin tiempo ni penalizaciones.** Es para estudiar, no para competir. Las
  estrellas premian; nada castiga.
- **Tres tipos de pregunta**: elegir una, verdadero o falso con explicación, y
  ordenar hechos tocándolos en secuencia. La de ordenar es la que más se parece
  a lo que preguntan en la prueba.

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
