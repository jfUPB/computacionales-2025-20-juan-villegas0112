# Unidad 1

## 🤔 Fase: Reflect

### Actividad 05

#### Parte 1: recuperación de conocimiento (retrieval practice)

Describe con tus palabras las tres fases del ciclo Fetch-Decode-Execute. ¿Qué rol juega el Program Counter (PC) en este ciclo?

Fetch es para que el programa busque donde etsan ubicadas las instrucciones, el decode es para entender las instrucciones y buscar las formulas o operaciones adecuadas para la realizacion de la instruccion, luego el execude las ejecuta basandose en las operaciones anteriormente encontradas. El PC es a donde van las instrucciones y lineas de codigo que se realizaron en el ciclo. 

¿Cuál es la diferencia fundamental entre una instrucción-A (que empieza con @) y una instrucción-C (que involucra D, M, A, etc.) en el lenguaje ensamblador de Hack? Da un ejemplo de cada una.

La instruccion que contiene D, M, A se usan directamente para darle un valor a una variable o asigar el valor en un lugar de la ram como es el caso de la M,es decir, realizar operaciones. El caso del @a es para cargar un valor en cierta direccion del ROM.

ejemplos:

@2 --> carga un valor de 2 en el registro A

D=M --> carga el valor de D en la memoria M



Explica la función de los siguientes componentes del computador Hack: el registro D, el registro A y la ALU.

En el computador Hack, el registro A se usa para guardar valores, y también determina a qué posición de memoria se refiere M. El registro D es un registro que almacena datos temporales para operaciones. La ALU realiza todas las operaciones entre el contenido de D y A o M, y puede enviar el resultado a D, A o M, además de generar señales para saltos condicionales según el resultado. Estos tres componentes trabajan en conjunto para ejecutar instrucciones y manipular datos en el sistema.

¿Cómo se implementa un salto condicional en Hack? Describe un ejemplo (p. ej., saltar si el valor de D es mayor que cero).

Un salto condicional en Hack se hace usando una instrucción-C con una condición de salto al final, como ;JGT, ;JEQ, etc. Primero se calcula una expresión con la ALU, y luego, si se cumple la condición, se salta a la dirección almacenada en el registro A.

¿Cómo se implementa un loop en el computador Hack? Describe un ejemplo (p. ej., un loop que decremente un valor hasta que llegue a cero).

Un loop se implementa usando una etiqueta y un salto condicional o incondicional que regresa a esa etiqueta, formando un ciclo.

Un ejemplo:loop en Hack que cuenta de 0 a 3.

¿Cuál es la diferencia entre la instrucción D=M y la instrucción M=D?

D=M: Copia el valor de la memoria al registro D.

M=D: Copia el valor de D a la memoria en la dirección indicada por A.

Describe brevemente qué se necesita para leer un valor del teclado (KBD) y para “pintar” un pixel en la pantalla (SCREEN).

Se accede al valor que está almacenado en la dirección de memoria asignada al teclado (KBD), que refleja la tecla que se está presionando en ese momento. Para pintar un píxel en la pantalla, se escribe un valor en la dirección de memoria correspondiente a la pantalla (SCREEN), lo que enciende o apaga píxeles según los bits que se modifiquen en esa posición.


#### Parte 2: reflexión sobre tu proceso (metacognición)

¿Cuál fue el concepto o actividad más desafiante de esta unidad para ti y por qué?

Entender el codigo de la segunda actividad, porque creo que fue un salto grande de un ejemplo simple a algo mkas complejo y estruturado, aun asi al final logre entenderlo de la mejor manera.

La metodología de “predecir, ejecutar, observar y reflexionar” fue central en nuestras actividades. ¿En qué momento esta metodología te resultó más útil para entender algo que no tenías claro?

Al hacer la activdad 3, porq el profe guio yu explico de una buena forma para enteder como se debe usar este modelo y se vieron lo simples que pueden ser las instrucciones a la hora de verlo asi. 

Describe un momento “¡Aha!” que hayas tenido durante estas dos semanas. ¿Qué estabas haciendo cuando ocurrió?

Cuando entendi que la utilizacion de la M era para almacenar en la memoria y no una variable con un valor mas.

Pensando en la próxima unidad, ¿Qué harás diferente en tu proceso de estudio para aprender de manera más efectiva?

copiare un poco mas en mis apuntes para entender mejor la esturctura a la hora de trabajar en la casa.
