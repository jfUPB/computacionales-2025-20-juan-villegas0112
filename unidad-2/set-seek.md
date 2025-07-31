# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01

🪤***Predice***🪤

Al ver la instruccion se puede inferir que se debe guardar un valor en una posicion especifica de la memoria, el valor o numero debe corresponder al color que muestra en la instruccion, es decir, el negro. Ademas la posicion en la memoria debe ser la del inicio de la pantalla.

🪚***Ejecuta***🪚

<img width="332" height="102" alt="image" src="https://github.com/user-attachments/assets/f96189d6-74af-4042-9d43-c40c363d92bc" />

<img width="333" height="37" alt="image" src="https://github.com/user-attachments/assets/b1954ac9-3d3e-44e4-875a-33fc840520b9" />

c++
``` c++
screen = 1 // Supuesto: el compilador asigne la variable screen a la posicion de memoria? ---> 16384
````

🫐***Reflexiona***🫐

Esta actividad ayuda a comprender como puede funcionar los puestos o lugares en la memoria, dando a entender que de cierta forma cada posicion puede generar algo en especifico en la pantalla, como puede ser ubicar un pu to en el extremo de la pantalla. 


### Actividad 02

🪤***Predice***🪤

Para esta actividad se debe comprender el codigo binario, donde cada linea contiene 16 bits con 1 y 0, al usar los 16 bits es necesario poner un -1 y asi llegar a la utilizacion de los 16 bits que contiene la instruccion. 

🪚***Ejecuta***🪚

<img width="327" height="74" alt="image" src="https://github.com/user-attachments/assets/c65f2e08-14c4-4800-8f5c-b930c6e3b4bd" />

<img width="330" height="34" alt="image" src="https://github.com/user-attachments/assets/da2ae96e-0f94-49a9-ad7e-be729485d28a" />

c++
``` c++
screen = -1; //forzar al compilador para que asigne la variable screen a la direccion 16384

screen = 0xFFFF;
```

🫐***Reflexiona***🫐

Para la realizacion de esta actividad se teneia que entender el codigo binario, cosa que la verdad si fue muy util, pues es esencial entender como funcionan los computadores en su interior y ver como la ubicacion de los 1 y 0.




### Actividad 03

🪤***Predice***🪤

Para la realizacion de esta actividad es necesario desglosar bien las indicaciones dadas, empezando por la finalodad que tiene el codigo y luego ir probando cada paso que se hace para ver si en realidad funciona.

🪚***Ejecuta***🪚

```asm
@i
M=0

@SCREEN
M=-1
(LEER)

@KBD
D=M
@100
D=D-A

@DERECHA
D;JEQ
@KBD
D=M
@105
D=D-A

@IZQUIERDA
D;JEQ
@LEER
0;JMP

(DERECHO)
//dirección screen + n(DERECHA)
//borro la posición actual
@i
D=M
@SCREEN
A=D+A
M=0
//subirle el valor al contador
@i
M=M+1
D=M
@SCREEN
A=D+A
M=-1
@LEER
0;JMP

(IZQUIERDA)
//borro la posición actual
@i
D=M
@SCREEN
A=D+A
M=0
//bajarle el valor al contador
@i
M=M-1
D=M
@SCREEN
A=D+A
M=-1
@LEER
0;JMP
```

🫐***Reflexiona***🫐

La realizacion de esta actividad fue muy interesante, porque entendi mejor la manera de como hacer y realizar los codigos de forma estructurada, ademas que comprendi la utilizacion del 0;jmp y el D;jeq, uno salta hasta el inicio y el otro hasta una ubicacion exacta para repetir el proceso.


### Actividad 04


@sum
M=0        // sum = 0

@i
M=1        // i = 1

(LOOP)
  @i
  D=M      // D = i
  @100
  D=D-A    // D = i - 100
  @END
  D;JGT    // if(i > 100) goto END

  // sum = sum + i
  @i
  D=M
  @sum
  M=D+M

  // i++
  @i
  M=M+1

  @LOOP
  0;JMP    // goto LOOP

(END)
  @END
  0;JMP    // infinite loop
´´´ 


