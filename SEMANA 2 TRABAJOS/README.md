# Proyecto de Normalización de Bases de Datos
## David Santiago Beltran Pedraza
## Ficha: 3203084 - ADSO - CBA MOSQUERA

---

## Parte 1: Análisis conceptual – Devart

1. ¿Qué problema principal busca resolver la normalización en una base de datos y por qué es crítica en sistemas empresariales?

R/ Básicamente la normalización busca reducir la **redundancia de datos** en donde un mismo dato esta repetido en varias talas o filas, también busca que se mejoren problemas de **integridad** donde esta normalización busca que las dependencias entre los datos estén bien definidas. Ya que cuando una base de datos está desorganizada esta puede contener registros duplicados, errores y rendimiento lento los cuales también son justamente problemas que se buscan resolver con la normalización en bases de datos. 

Todos estos problemas en bases de datos son críticos en sistemas empresariales justamente por lo anteriormente comentado ya que todo esto puede causar complicaciones al actualizar información, generar reportes que puedan contener  información erronea o desactualizada, o simplemente causar problemas como al hacer mantenimiento en una base de datos que este desorganizada o sin esa normalización pues al realizar alguna operación en la base de datos como crear o eliminar algo en la estructura se puede a llegar afectar datos que hasta pueden no estar relacionados o que se pierda información, en pocas palabras se incrementa como ese riesgo de errores y más encima puede causar un funcionamiento más lento y menos eficaz en la base de datos por lo que al aplicar la normalización se mitigan todos esos problemas que se pueden ocasionar en las bases de datos de alguna empresa.

2. Describe con tus propias palabras las diferencias entre 1NF, 2NF y 3NF según los ejemplos del artículo.

R/ Las diferencias entre estas 3 primeras etapas de la normalizaciín son:

- **Primera forma normal (1NF):** Básicamente este primero se centra en que cada campo contenga un solo valor indivisible osea que no pueden existir listas, repeticiones o grupos de valores dentro de una misma celda y su objetivo es eliminar los grupos repetidos y garantizar que cada fila sea única e identificable.

Como ejemplo del artículo si un estudiante tiene los cursos “Matemáticas, Ciencias” en una sola celda, eso no cumple la 1NF. La solución sería crear una fila por cada curso que el estudiante tome pues cada campo debe contener un único valor.

- **Segunda forma normal (2NF):** En esta se comienza desde esa base de la 1NF pero ya no solo busca eliminar grupos repetidos sino que también busca eliminar la redundancia causada por dependencias parciales, es decir, cuando un atributo depende solo de una parte de la clave primaria (en lugar de toda la clave) y se aplica más que todo a tablas con claves compuestas.

En el ejemplo se repite el nombre y correo del estudiante en cada fila de curso, esos datos dependen solo del estudiante, no del curso y para cumplir con la 2NF se mueve esa información a una tabla ("Estudiantes" en el ejemplo) y se guarda solo el ID del estudiante en la tabla de cursos ya que los datos deben depender de toda la clave primaria, no de una parte.

- **Tercera forma normal (3NF):** Por último en este se parte desde la base de 2NF pero ya no existen dependencias transitivas osea que un atributo no clave no debe depender de otro atributo no clave, sino solo de la clave primaria Siendo su objetivo evitar que un dato se derive de otro dato dentro de la misma tabla, lo que puede causar inconsistencias.

Y como muestra el artículo si por ejemplo en una tabla de estudiantes se guarda “Código postal” y “Ciudad”, pero la ciudad puede determinarse solo a partir del código postal, entonces la ciudad depende del código postal y no directamente del estudiante. Para cumplir con la 3FN se debe mover “Código postal” y “Ciudad” a una tabla aparte de direcciones ya que los atributos no clave deben depender solo de la clave primaria, no de otros atributos.

- En conclusión básicamente la diferencia entre las 3 es que cada una exceptuando la primera se va basando de la anterior Norma Formal pero se añade otra regla por así decirlo en este caso en la 1NF se elimina grupos repetidos y garantiza atributos atómicos después se pasa a la 2NF, que se basa en la 1NF, donde se elimina las dependencias parciales (columnas no clave que dependen de una parte de la clave primaria) y se pasa a la 3NF, que se basa en 2NF, donde se elimina las dependencias transitivas (columnas no clave que dependen de otras columnas no clave). 


## Parte 2: Caso Fred’s Furniture
### Retos y resultados
(Descripción de cada reto, decisiones y código relevante)
### Modelo E-R final
(Incluir imagen o enlace)
### Reglas de negocio
(Enumerar reglas derivadas)
### Justificación del diseño
(Explicar decisiones de normalización)

## Parte 3: Proyecto personal
### Título y descripción
(Breve resumen)
### Diagrama E-R
(Imagen o enlace)
### Reglas de negocio y justificación
(Análisis final)