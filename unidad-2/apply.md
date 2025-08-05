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
// Inicializa el puntero en la dirección 16
@16
D=A
@p
M=D       // p = 16

// Guardar valores del 1 al 10 en RAM[16] a RAM[25]
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

// Inicializar sum = 0
@sum
M=0

// Resetear el puntero a 16
@16
D=A
@p
M=D

// Bucle: sumar desde RAM[16] a RAM[25]
(LOOP)
@p
A=M       // A = RAM[p]
D=M       // D = *p

@sum
M=M+D     // sum += *p

@p
M=M+1     // p++

@p
D=M
@26
D=D-A     // D = p - 26
@LOOP
D;JLT     // Si p < 26, seguir

// Fin
(END)
@END
0;JMP

```

🦖Reflexiona🦖
La realizacion de este ejercicio fue un poco compleja de entender, pues la utilizacion del puntero combinado con un bucle me parecio complejo, pero cuando comence a entender que simplemente debia ver la el arr como una variable que tiene diferentes valores y que el puntero debe ayudar a identificar que valor darle a esa variable se me hizo un poco mas sencillo de entender, de igual manera al basarme en un ejemplo que vimos en clase entendi que el puntero funcionaba como la i y que debia sumarle a este para que cambiara de posicion. En resumen el ejercicio me parecio complejo al principio, pero mientras iba avanzando entendia de una mejor manera la funcio que le podia dar al puntero. 
