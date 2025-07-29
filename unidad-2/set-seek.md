# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01

Al tener en cuenta lo que dice la situacion problema, la finalidad del codigo es generar un punto negro utilizando el 1 en la ubicacion 16384.

<img width="332" height="102" alt="image" src="https://github.com/user-attachments/assets/f96189d6-74af-4042-9d43-c40c363d92bc" />

<img width="333" height="37" alt="image" src="https://github.com/user-attachments/assets/b1954ac9-3d3e-44e4-875a-33fc840520b9" />

c++

screen = 1 // Supuesto: el compilador asigne la variable screen a la posicion de memoria? ---> 16384


### Actividad 02

Para esta actividad se debe comprender el codigo binario, donde cada linea contiene 16 bits con 1 y 0, al usar los 16 bits es necesario poner un -1 y asi llegar a la utilizacion de los 16 bits que contiene la instruccion. 

<img width="327" height="74" alt="image" src="https://github.com/user-attachments/assets/c65f2e08-14c4-4800-8f5c-b930c6e3b4bd" />

<img width="330" height="34" alt="image" src="https://github.com/user-attachments/assets/da2ae96e-0f94-49a9-ad7e-be729485d28a" />

c++;

screen = -1; //forzar al compilador para que asigne la variable screen a la direccion 16384

screen = 0xFFFF;

### Actividad 03
@SCREEN
M=-1
@CONTADOR
M=0

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

(DERECHA)

//BORRO LA POSICION ACTUAL
@CONTADOR
D=M
@SCREEN
A=D+A
M=0

//

@CONTADOR
M=M+1
D=M
@SCREEN
A=D+A
M=-1

@LEER
0;JMP


(IZQUIERDA)

//BORRO LA POSICION ACTUAL
@CONTADOR
D=M
@SCREEN
A=D+A
M=0

//

@CONTADOR
M=M-1
D=M
@SCREEN
A=D+A
M=-1

@LEER
0;JMP

