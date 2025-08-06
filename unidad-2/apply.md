# Unidad 2

## 🛠 Fase: Apply

### 👹 Actividad 06 👹

Considera el siguiente programa

```c++
int arr[] = {1,2,3,4,5,6,7,8,9,10};
int sum = 0;

for (int j = 0; j < 10; j++) {
    sum = sum + arr[j];
}
``` 
🪤Predice🪤

Este codigo genera una variable, la cual contiene los numeros del 1 al 10, empieza una suma de estos numeros en 0. Luego crea un ciclo que permite la suma de estos numeros hasta la posicion 9, la cual tiene como valor el 10. Esta suma debe de dar 55. 

🦧Ejecuta🦧

```asm
// RAM[0] -> p (puntero)
// RAM[1] -> sum (acumulador)

// declarar el puntero p = 16 y que su valor quede en M=0
@16
D=A
@0
M=D

// Carga valores del 1 al 10 en 16 hasta 25
@1
D=A
@16
M=D
@2
D=A
@17
M=D
@3
D=A
@18
M=D
@4
D=A
@19
M=D
@5
D=A
@20
M=D
@6
D=A
@21
M=D
@7
D=A
@22
M=D
@8
D=A
@23
M=D
@9
D=A
@24
M=D
@10
D=A
@25
M=D

// sum = 0
@1
M=0

@16
D=A
@0
M=D

// BUCLE de suma
(LOOP)
@0
A=M       // A = p
D=M       // D = *p

@1
M=D+M     // sum += *p

@0
M=M+1     // p++ aunmenta la posicion del puntero

@0
D=M
@26
D=D-A     // D = p - 26 para saber caundo se debe terminar 
@LOOP
D;JLT     // si p < 26, saltar a LOOP

// Fin
(END)
@END
0;JMP

```
Algunas revisiones:
1. Al declarar los valores de las posiciones 16-25 hice una revision para ver si los valores funcionaban
2. Busque en la posicion 0 el recorrido hecho con el puntero
3. Luego revise si se almacenaba la suma en la direccion correcta 1
4. Hice la suma por aparte y luego revise que en la posicion 1 quedara un valor igual al 55

🦖Reflexiona🦖
La realizacion de este ejercicio fue un poco compleja de entender, pues la utilizacion del puntero combinado con un bucle me parecio complejo, pero cuando comence a entender que simplemente debia ver la el arr como una variable que tiene diferentes valores y que el puntero debe ayudar a identificar que valor darle a esa variable se me hizo un poco mas sencillo de entender, de igual manera al basarme en un ejemplo que vimos en clase entendi que el puntero funcionaba como la i y que debia sumarle a este para que cambiara de posicion. En resumen el ejercicio me parecio complejo al principio, pero mientras iba avanzando entendia de una mejor manera la funcio que le podia dar al puntero. 


