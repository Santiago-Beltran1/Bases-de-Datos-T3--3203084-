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

3. En los ejemplos de Devart, identifica una situación donde la normalización mejora la integridad de datos, pero podría afectar el rendimiento. Explica el motivo.

R/ Uno de los ejemplos del artículo es cuando separan los métodos de pago en la tabla nueva “PaymentMethods (OrderID, PaymentMethod)”. Este cambio forma parte de llevar la base de datos a 4NF (y antes 3NF/BCNF). En la original, en la tabla Orders se tenía campos PaymentMethod1, PaymentMethod2, lo que genera dependencias de múltiples valores y redundancias. 

Al mover los métodos de pago a una tabla separada, cada orden solo tiene tantos registros como métodos de pago tenga, no hay campos vacíos, no hay múltiples valores embebidos en una celda, se evita la repetición de “Cash”, “Voucher”, etc como parte de la tabla principal. Esto reduce anomalías de inserción, actualización, borrado: por ejemplo, si se necesitara añadir un tercer método de pago, no habría que modificar el esquema de la tabla Orders. Además, la integridad referencial (clave externa) asegura que cada método de pago corresponde a un OrderID existente y no se duplican métodos innecesarios.
Pero más sin embargo, al normalizar, cualquier consulta que necesite recuperar la información completa de un pedido y sus métodos de pago tendrá que hacer una join (una combinación) entre la tabla Orders y la tabla PaymentMethods y si se hacen consultas muy frecuentes (por ejemplo, un listado de órdenes con sus métodos de pago) esto implica más operaciones de unión, lo cual puede afectar el rendimiento (más lecturas, más índices, más exigencia computacional). Además, cuando hay muchas tablas y muchos joins, la latencia puede subir, los índices pueden requerir más mantenimiento, y la optimización de la consulta es más compleja, en pocas palabras básicamente por estar saltando de tbblas en tablas el rendimiento en el computador se puede ver afectado.

4. ¿Qué papel juegan las dependencias funcionales en el proceso de normalización y cómo las identificarías en una tabla?

Las dependencias funcionales son la base teórica de los procesos de normalización. Una dependencia funcional ocurre cuando un atributo o conjunto de atributos, identifica o determina otro atributo en la tabla. Es decir: si A → B, entonces valor de A determina valor de B. 

En la normalización:

- En la 1NF no se habla como tal de dependencias funcionales, se habla más de valor atómico.

- En la 2NF se revisan las dependencias funcionales parciales: si hay una clave compuesta por ejemplo, (OrderID, ItemID), se revisa que ningún atributo no clave dependa únicamente de una parte de la clave donde identificamos si un atributo depende de toda la combinación o solo de una parte.

- En la 3NF se revisan las dependencias transitivas: un atributo no clave que depende de otro atributo no clave, que a su vez depende de la clave. Por ejemplo: OrderID → CustomerID → City. 

- En BCNF, se exige que cada determinante sea una clave candidata (candidate key). Si existe A → B, y A no es clave candidata, se viola BCNF como cuando ZipCode → City cuando ZipCode no es clave. 

Para identificar las dependencias funcionales de una tabla se siguen estos pasos:

- **Examinar las claves de la tabla:** identificar cuál es la clave primaria (o si hay clave compuesta).

- **Verificar cada atributo no clave:** Ver si el atributo está determinado por la clave o solo por una parte osea si la clave es (OrderID, ItemID) y un atributo Precio está determinado solo por ItemID, entonces hay dependencia parcial.

- **Verificar si algún atributo no clave determina otro atributo no clave:** Es decir si el atributo A → atributo B, y A no es clave. Si se encuentra, hay dependencia transitiva.

- **Verificar si alguna combinación de atributos no clave actúa como determinante de otro no clave y no es clave candidata:** En este caso se revisa BCNF.
Dentro del artículo, se muestran en la tabla los “Functional Dependency Explanation” (L611-L616) donde se listan cosas como “OrderID → Customer Info, Order Date …” “Customer Info → Name, Primary Phone …” “OrderID, ItemName → Price…” 

- **En la práctica, se puede revisar los datos:** buscar atributos repetidos, buscar si al cambiar un valor de la clave cambia el otro atributo, y si al cambiar otro no clave afecta otro. También se pueden usar herramientas de minería de dependencias o inspección manual de patrones de repetición.

Y asi las dependencias funcionales nos muestran cómo descomponer tablas, detectar dónde hay redundancia estructural, y guían la regla de qué debe depender de qué y evitar que dependa de algo incorrecto.

5. Explica, con tus palabras, cuándo sería justificable “desnormalizar” una base de datos según el contexto de negocio.

Desnormalizar significa introducir deliberadamente cierta redundancia o agrupar datos en forma menos purista con el objetivo de mejorar el rendimiento, sobre todo cuando la carga es de lectura intensiva o cuando se necesitan consultas de agregación/resumen de forma muy frecuente.
Sería justificable cuando:

El sistema es principalmente de lectura, no de escritura (es decir, los datos se consultan mucho, pero se modifican poco). Por ejemplo, dashboards, reportes, análisis de datos. En ese escenario, evitar muchas uniones (joins) entre tablas puede mejorar significativamente el tiempo de respuesta. 

Se ejecutan muchas consultas de agregación, resumen o exploración de grandes volúmenes de datos, y el costo de uniones múltiples empieza a afectar la experiencia del usuario. Por ejemplo, un portal de informes que muestra datos al instante y no puede esperar que el sistema combine 10 tablas cada vez. El artículo lo menciona: “If your app is slow and users are just looking at the data (not updating it), denormalization might help.” 

La prioridad del contexto de negocio es la velocidad de acceso en vez de la mínima redundancia pura. Si se acepta algun grado de redundancia para lograr que el sistema responda rápido. Tipos de sistemas: OLAP, data-warehouses, sistemas de BI donde las operaciones de lectura dominan. 

Y, adicionalmente, cuando se asume que los datos repetidos/duplicados no van a causar un gran problema de inconsistencias o mantenimiento, o se han implementado mecanismos para mitigar los riesgos de redundancia. El artículo advierte que “over-normalizing” puede generar demasiados joins y afectar el rendimiento. 

En resumen: aunque la normalización es una buena práctica para asegurar integridad y claridad, en el negocio real no siempre es la única prioridad; cuando la velocidad de lectura, la experiencia del usuario o la complejidad de consultas lo requieren, desnormalizar parcialmente puede estar justificado. Pero siempre con cuidado, evaluando el coste de mantenimiento y riesgo de inconsistencia.

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