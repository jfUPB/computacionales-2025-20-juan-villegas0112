# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 01

🥸***Predice***🥸

Esta actividad va a permitir entender de una mejor manera como es la traduccion entre codigos, es decir, como pasa del c++ al ensamblador y del ensamblador al idioma maquina. 
Por otro lado, los breake points sirven para realizar vectores de prueba o ver como van fucionando las partes de codigo de forma que no involucren la operacion siguiente al break point.

🦕***Ejecuta***🦕

``` c++
int sum(int a, int b)
{
    return a + b;
}

int main()
{
    int a = 5;
    int b = 7;
    int c = sum(a, b);
    std::cout << "La suma de " << a << " y " << b << " es " << c << "\n";
}
```

- Break Point

<img width="825" height="147" alt="image" src="https://github.com/user-attachments/assets/b94da814-4d91-4a8c-a479-d0441781de93" />

- Ventada de depuracion Autos

<img width="917" height="151" alt="image" src="https://github.com/user-attachments/assets/0c583743-f290-477d-933e-5fe27a631ad5" />



🎰***Reflexiona**🎰

¿Para qué sirven los breakpoints?

Para deter el programa en un punto, esto sirve para realizar cambio o una experimentacion, haciendo que el resto dle codigo no se vea afectado.

¿Para qué se usa la ventana de depuración Autos?

Ver como todas las variables localaes se van definiendo mediante el programa se va ejecutando.

### Actividad 01

🥸***Predice***🥸
Esta actividad permitira ver como es la utilizacion de punteros dentro de un codigo en c++

🦕***Ejecuta***🦕

- al usar el cout se imprime un mensaje

```c++
#include <iostream>

using namespace std;

void swapPorValor(int a, int b)
{
    int cambio = b;
    b = a;
    a = cambio;
}

void swapPorReferencia(int& a, int& b)
{
    int cambio = b;
    b = a;
    a = cambio;
}

void swapPorPuntero(int* a, int* b)
{
    int cambio = *b;
    *b = *a;
    *a = cambio;
}

int main() {
    int a = 12;
    int b = 15;

    cout << "Valor inicial de a: " << a << endl;
    cout << "Valor inicial de b: " << b << endl;

    cout << "\nLlamando a swapPorValor..." << endl;
    swapPorValor(a, b);
    cout << "Despues de swapPorValor, valor de a, b: " << a << ", " << b << endl;

    cout << "\nLlamando a swapPorReferencia..." << endl;
    swapPorReferencia(a, b);
    cout << "Despues de swapPorReferencia, valor de a, b: " << a << ", " << b << endl;

    cout << "\nLlamando a swapPorPuntero..." << endl;
    swapPorPuntero(&a, &b);
    cout << "Despues de swapPorPuntero, valor de a, b: " << a << ", " << b << endl;

    return 0;
}
```
 ¿Por qué pasa?
Paso por (a):
La función recibe un tipo de copia del valor.
Si la copia cambia, el original no.

Paso por (b):
La función recibe un acceso directo al original.
Cualquier cambio dentro se ve afuera.

Paso por (c):
La función recibe la dirección del original.
Usando esa dirección, puede cambiarlo en su lugar real.

🎰***Reflexiona**🎰

Esta actividad permite entender de buena forma el funcionamiento de las diferentes fucniones que hey en el codigo, permitiendo ver como se pueden realizar cambios dentro de una variable de forma permanente o solo para la utilizacion momentanea.


### 🕺Actividad integradora de aplicación🕺

***A. Predicción (sin ejecutar el código):***

**🐳 ¿Cuál será la salida final en la consola de este programa?
Escribe la salida completa que esperas.**

- val_A no cambia después de sumaPorValor.

- val_B y val_C sí cambian porque se pasan por referencia/puntero.

- contador_estatico recuerda su valor entre llamadas.

``` c++
--- Experimento con paso de parámetros ---

Valor inicial de val_A: 20

  -> Dentro de sumaPorValor, 'a' ahora es: 30
  
Valor final de val_A: 20


Valor inicial de val_B: 20

  -> Dentro de sumaPorReferencia, 'a' ahora es: 30
  
Valor final de val_B: 30


Valor inicial de val_C: 20

  -> Dentro de sumaPorPuntero, '*a' ahora es: 30
  
Valor final de val_C: 30


--- Experimento con variables estáticas ---

  -> Llamada a ejecutarContador. Valor de contador_estatico: 1
  
  -> Llamada a ejecutarContador. Valor de contador_estatico: 2
  
  -> Llamada a ejecutarContador. Valor de contador_estatico: 3
```



**🐳 Dibuja un mapa de memoria conceptual de este programa justo antes de que main finalice. Debes indicar en qué segmento de memoria (Stack, Heap, Datos Globales/Estáticos, Código) se encontraría cada una de las siguientes variables: contador_global, contador_estatico, val_A, val_B, val_C (dentro de main), el parámetro a de la función sumaPorValor, la función main misma.**

<img width="603" height="481" alt="image" src="https://github.com/user-attachments/assets/89da54e1-2999-477e-bc05-9b1849dcec40" />



***B. Verificación y análisis (usando el depurador):***

**Ejecuta el programa paso a paso (F10) con un breakpoint al inicio de main.**

**🐳 Compara la salida real con tu predicción. Si hubo diferencias, explica por qué ocurrieron. Evidencia clave: capturas de pantalla antes y después de los puntos de interés (¿Cuáles son esos puntos? -> tu tarea analizarlo).**

- No hubieron diferencias con respetacto a mi prediccion.

*Puntos de interes*

- Antes de llamar a sumaPorValor(val_A)

<img width="434" height="122" alt="image" src="https://github.com/user-attachments/assets/62f41bf7-5a60-489d-af5e-a64dbb204b43" />


- Dentro de sumaPorValor

<img width="434" height="121" alt="image" src="https://github.com/user-attachments/assets/c10e041e-1586-4724-9127-70e65e3b5a64" />

-Afuera de sumaPorValor

<img width="435" height="121" alt="image" src="https://github.com/user-attachments/assets/60907d9e-c3e7-449d-8f35-cc24eb461a2d" />

  
- Antes de llamar a sumaPorReferencia(val_B)

<img width="431" height="121" alt="image" src="https://github.com/user-attachments/assets/7f34003f-84fd-487c-8842-a872bc002725" />


- Dentro de sumaPorReferencia

<img width="430" height="121" alt="image" src="https://github.com/user-attachments/assets/7cd9ff5a-e687-461f-b4d4-e14da3021a97" />

- Afuera de sumaPorReferencia

<img width="434" height="121" alt="image" src="https://github.com/user-attachments/assets/4361bd4f-164a-4239-8556-4afb55281c0d" />


- Antes de llamar a sumaPorPuntero(&val_C)

<img width="433" height="117" alt="image" src="https://github.com/user-attachments/assets/c632db0b-16ec-4028-aa0c-967a00464544" />


- Dentro de sumaPorPuntero

<img width="430" height="122" alt="image" src="https://github.com/user-attachments/assets/e7153d7c-9ed0-4bb5-b006-c1d33bd2c0d2" />

- Afuera de sumaPorPuntero
  
<img width="438" height="120" alt="image" src="https://github.com/user-attachments/assets/7747ac27-613a-406d-8f77-5a1a437ab8df" />



- Cada llamada a ejecutarContador()

<img width="431" height="122" alt="image" src="https://github.com/user-attachments/assets/916e91e6-fa15-4102-a1d0-4e86e432652b" />

<img width="433" height="123" alt="image" src="https://github.com/user-attachments/assets/eac6daf4-0f52-43c4-b7cc-7afe7668e5a5" />

<img width="430" height="120" alt="image" src="https://github.com/user-attachments/assets/b6741b0c-5421-42cf-a15a-100b01fcbc55" />



**🐳 Describe qué demuestran estas capturas sobre la diferencia entre los diferentes tipos de paso por parámetros analizados.**

1. Paso por valor: Se crea una copia del valor. Modificar la copia no afecta al original.

2. Paso por referencia: Se usa la variable original directamente. Cualquier cambio dentro de la función modifica al original.

3. Paso por puntero: Se pasa la dirección de memoria, y usando * se modifica el valor en esa dirección. También cambia el original.


**🐳 Explica con tus propias palabras el comportamiento de contador_estatico. ¿Por qué “recuerda” su valor entre llamadas a la función ejecutarContador? ¿En qué se diferencia de una variable local normal?**

La variable local normal se crea cuando la función empieza y se destruye cuando la función termina.

Una variable estática local se crea una sola vez en la parte de datos estáticos, no en el stack.





