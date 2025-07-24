# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01

#### El prposito de esta actividad es entender como funciona el Ciclo fetch-decode-execute

¿Que es el fetch? ¿Que es el decode? ¿Que es el execude?

Fetch: significa buscar, lo que hace es que la cpu al obtener una instruccion, el programa indica donde esta esta instruccion.

Decode: significa decodificar, es donde la cpu interpreta la instuccion, entiende operaciones, datos y recursos para realizar la instruccion.

Execude: significa ejecutar, aqui la cpu realiza la operacion indicada en la instruccion. 
```asm
@1
D=A
@2
D=D+A
@16
M=D
@END
(END)
0;JMP
```
¿Que sucede?

el codigo genera una suma y le da valores a dos diferentes variables.

¿Qué valor se almacena en la dirección de memoria 16? ¿Por qué crees que es ese valor?

El valor almacenado en la dirección de memoria 16 es 3. Esto pasa porque el programa realiza la suma de los valores 1 y 2 usando A y D. Primero, @1 carga el valor 1 en A, y D=A en D. Despues, @2 carga el valor 2 en A, y D=D+A suma los valores de lo anterior, lo que da en D = 3. Al final, la instrucción @16 pone la dirección 16 en A y M=D guarda el 3 en la dirección de memoria 16.

¿Qué instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute?

Cada que se le da step en el programa se realiza el ciclo.El fecht; busca e indica donde esta la instruccion. Luego se decodifica o se comprede lo que hay en el codigo, para finalizar ejecutando lo peido. Esto pasa en cada linea del codigo lo que hace que en cada uso del step se realice el ciclo.

¿Qué cambios observas en el contenido de la memoria y los registros? 

En la memoria hay un nuevo almacenamiento en la posicion 16 y en los registros se encuentran los valores de las variales dadas durnate el codigo.

#### Escribe un programa en lenguaje ensablador que sume los números 5 y 10, y almacene el resultado en la dirección de memoria 20. Utiliza el simulador de la CPU Hack para ejecutar tu programa y verifica que el resultado es correcto.
```asm
@5
D=A
@10
D=D+A
@20
M=D
@END
(END)
0;JMP
```

¿Qué diferencia hay entre los datos almancenados en la memoria ROM y en la RAM?

La memoria Rom contiene las instruciones y la memoria Ram las carga para que comience su funcionamiento.

### Actividad 02





