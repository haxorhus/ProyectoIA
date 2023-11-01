# ProyectoIA
## Problematica 
En Materias de **alta retencion** (Materias con cientos de alumnos que no pueden pasarla) cada semestre se habilitan varias secciones de la materia, pero al finalizar el semestre se observa que varios alumnos dejaron de ir a clase y abandonaron la materia lo que significa que las clases terminan desarrollandose con menos alumnos de lo esperado.

Cada seccion significa ocupar un aula de la facultad en el horario respectivo, pagar el salario del profesor y el auxiliar y ,en algunos casos, utilizar los laboratorios con todos los gastos que conlleva este uso. En resumen, **cada seccion abierta es un gasto de recursos de la facultad** que podrian enfocarse en otros lugares mas necesitados.

Debido a esto, esos alumnos que abandonan una materia terminan siendo un gasto innecesario para la facultad, ya que por ejemplo:
Si cada seccion permite un maximo de 40 alumnos y hay 180 alumnos inscritos, entonces se habilitan  5 secciones de 36 alumnos en cada una; Pero si al final entre todas las secciones terminan abandonando 20 alumnos (11%), entonces las clases las terminan utilizando 160 alumnos que perfectamente entrarian en 4 secciones, por lo tanto podemos decir que *en ese semestre hubo una seccion de más, generando un gasto innecesario*.

## Objetivo
Desarrollar una IA capaz de predecir la cantidad de alumnos que van a abandonar la materia **antes** de que esta materia se abra, para que asi la directiva pueda tomar mejores decisiones sobre cuantas secciones abrir y asi, evitar gastos que no hacen falta.
## Materia 
**Calculo 2**

## Criterio de abandono
Mi criterio para asumir que alguien abandonó la materia es:
- **Ausente en los 3 finales**
- **Ausente en el 2do parcial**

Quiero que este criterio sea lo mas simple y general posible por ahora.

Todos los que cumplen esos dos criterios son personas que probablemente decidieron abandonar la materia para cursarla el siguiente semestre, *lo mas probable es que hayan dejado de asistir a clase antes de que estas se terminen* (que es lo que queremos predecir, para reducir estos "cupos vacios" en las clases y se puedan abrir menos secciones sin afectar a los que si quieren cursar la materia). 

Hay una probabilidad de que los que cumplan estos criterios hayan asistido a todas las clases, pero justo antes de los 2dos parciales se hayan desanimado y hayan abandonado. Estas personas *no entran en nuestro criterio*, ya que como asistieron a las clases no son un "cupo vacio"

Debido a esto podemos agregar un filtro más, el si cumplen o no el **requisito de asistencia**.
El requisito de asistencia es del 70%, por lo que todos los que cumplen con el requisito son *personas que asistieron a la mayoria de clases* (esto sin tener en cuenta a la gente que pide que se le firme).

## Preprocesamiento
Yo quiero saber la probabilidad de que el alumno degenere la materia. Esta informacion se necesita *antes* de que empiece el semestre, para que asi los directivos puedan tener un estimado de cuantas aulas abrir. 

## Features
Voy a elegir unas cuantas materias correlativas de donde voy a sacar los fixtures necesarios. 
### Para identificar al alumno:
- 'ID alumno' me permite identificar al alumno
- 'Carrera' me indica la carrera a la que esta matriculado 

### De las correlativas saco:
- 'Cantidad de veces cursada' es la cantidad de veces que se inscribio el alumno a esta materia
-  'Anho', 'Ciclo' Me permite saber el momento en el que el alumno esta cursando la materia
- 'Nota final','Firma' para saber que tan bien le fue al alumno 
### De la materia estudiada (dinamica) saco:
#### Para el training
- 'Cantidad de veces cursada' es la cantidad de veces que se inscribio el alumno a esta materia
- 'Cantidad de materias' ve el numero de materias a las que el alumno se inscribio mientras cursa la materia estudiada
- 'Anho', 'Ciclo' Me permite saber el momento en el que el alumno esta cursando la materia
#### Para mi criterio de abandono
- 'Asistencia' verifica si se cumplió el requisito de asistencia
- '2P', 'Nota final' me permite saber si asistio o no a esos examenes
