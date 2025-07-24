# Unidad 1

## 🛠 Fase: Apply

### ACTIVIDAD 03

Escribe un programa que compare el valor almacenado en la dirección de memoria 5 con el valor 10. Si el valor es menor que 10, guarda el valor 1 en la dirección 7. Si el valor es mayor o igual a 10, guarda el valor 0 en la dirección 7.

```asm
(LOOP)

@5
D=M
@10
D= D-A
@MENOR
D;JLT
(MAYOR)
@7
M=0
@LOOP
0;JMP


(MENOR)
@7
M=1
@LOOP
0;JMP
```

### ACTIVIDAD 04

Crea un programa que use un ciclo para sumar los números del 1 al 5 y guarde el resultado en la dirección de memoria 12.

``` asm
@1    
D=A
@10     
M=D

@0     
D=A
@11     
M=D

(LOOP)
@10     
D=M
@6
D=D-A   
@END
D;JGE  
@10     
D=M
@11   
M=D+M
@10   
M=M+1
@LOOP  
0;JMP

(END)
@11    
D=M
@12
M=D
@END    
0;JMP
```
