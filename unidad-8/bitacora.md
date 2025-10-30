# Bitácora de aprendizaje de la unidad 8

## Actividad 01

🧐🧪✍️ Reporta en tu bitácora

***Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?***

Al ejecutar el programa, veo que el círculo se mueve de izquierda a derecha como esperaba. Cuando hago clic, el círculo cambia de tamaño, pero en ese momento la aplicación se queda congelada por unos segundos. Yo pensaba que el cambio de tamaño sería instantáneo, pero claramente no lo es.

Creo que esto pasa porque el programa está haciendo un cálculo muy pesado (lo de sqrt(j) muchas veces) en la función heavyComputation(), y como todo eso se ejecuta en el mismo hilo principal, el programa no puede seguir dibujando el círculo mientras hace ese cálculo. Entonces, como solo hay un hilo trabajando, se queda ocupado haciendo esa tarea y no puede hacer nada más al mismo tiempo.

🧐🧪✍️ Reporta en tu bitácora

***Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?***

Al ejecutar el programa y hacer clic, el círculo sigue moviéndose sin que la ventana se congele, pero su tamaño cambia solo después de unos segundos. Esto pasa porque heavyComputation() ahora se ejecuta en un hilo secundario mediante ofThread, lo que permite que la interfaz siga activa mientras el cálculo pesado se realiza en paralelo. El cambio de tamaño se retrasa porque ocurre solo cuando el hilo termina su tarea y actualiza la variable circleSize usando lock() y unlock() para evitar conflictos entre hilos.

***Observa que el programa ahora no se congela, pero el círculo no cambia de tamaño inmediatamente. ¿Por qué crees que sucede esto? ¿Qué es lo que está pasando?***

El círculo no cambia de tamaño de inmediato porque la función heavyComputation() tarda en completarse (el bucle con mil millones de iteraciones es muy costoso).
Durante ese tiempo, el hilo secundario sigue trabajando, pero el hilo principal solo dibuja el valor actual de circleSize, que aún no ha sido actualizado.

Cuando el cálculo termina, el hilo bloquea temporalmente el acceso con lock(), cambia el tamaño del círculo (circleSize = ofRandom(20, 70)), y luego libera el recurso con unlock().
Esto explica por qué el cambio de tamaño ocurre con retraso, justo cuando la tarea pesada finaliza.

🧐🧪✍️ Reporta en tu bitácora

***En tus propias palabras, explica la diferencia entre concurrencia y paralelismo. ¿Por qué es importante entender esta diferencia al trabajar con hilos?***

La concurrencia consiste en que un mismo procesador ejecuta varias tareas alternándolas muy rápido, dando la sensación de que ocurren al mismo tiempo. En cambio, el paralelismo sucede cuando varias tareas se ejecutan realmente al mismo tiempo, cada una en un núcleo distinto del procesador. Es importante entender esta diferencia porque al trabajar con hilos debemos saber si el sistema realmente puede ejecutar tareas en paralelo o si solo las está intercalando, lo que influye en cómo diseñamos y optimizamos nuestro programa.

## Actividad 02

🧐🧪✍️ Reporta en tu bitácora

***Analiza de nuevo el código de la actividad anterior. ¿En qué partes del código se está protegiendo el acceso a la variable circleSize?***
***Según lo que te he venido comentando, los hilos te permiten ejecutar tareas en paralelo; sin embargo, piensa qué ocurre con el paralelismo cuando se sincroniza el acceso a un recurso compartido. ¿Qué ocurre con el rendimiento del programa? ¿Es posible que el rendimiento se vea afectado por el uso de mutex? ¿Por qué?***

La variable circleSize se protege justo cuando se usa lock() y unlock() dentro de la función heavyComputation(), o sea en esta parte del código:

```c++
lock();
ofSeedRandom();
circleSize = ofRandom(20, 70);
unlock();
``` 

Ahí básicamente se asegura que solo un hilo pueda cambiar el valor del círculo a la vez, para evitar que varios lo modifiquen al mismo tiempo y se genere una condición de carrera.

Cuando se sincroniza el acceso con un mutex, el paralelismo se ve un poco limitado porque los hilos tienen que esperar a que el otro termine para poder entrar a esa parte del código. Eso puede afectar un poquito el rendimiento, ya que se crea como un pequeño cuello de botella. Aun así, es necesario hacerlo, porque si no se usa el mutex podrían darse errores al trabajar con el mismo recurso desde varios hilos.

🧐🧪✍️ Reporta en tu bitácora

***Ejecuta el código y observa el resultado. ¿Qué ocurre si cambias el valor de la variable useLock? ¿Por qué crees que ocurre esto?***

<img width="400" height="140" alt="image" src="https://github.com/user-attachments/assets/a3fd1e6b-8e90-40c9-b3ff-6d4d4e5d0aaf" />

<img width="375" height="131" alt="image" src="https://github.com/user-attachments/assets/d607af8e-cdfe-488c-be17-365d930afff9" />


Al ejecutar el código y cambiar el valor de useLock, se nota que cuando está en false, el resultado final del contador no es el esperado: algunos valores se repiten o faltan. Esto pasa porque varios hilos están accediendo y modificando la variable counter al mismo tiempo, lo que genera condiciones de carrera. En cambio, cuando useLock está en true, el programa usa el mutex para que solo un hilo a la vez pueda leer y escribir el valor del contador. Así los resultados son correctos, aunque el programa se tarde un poquito más, ya que cada hilo debe esperar su turno para modificar la variable.


🧐🧪✍️ Reporta en tu bitácora

***Explica en tus propias palabras ¿Cómo puede presentarse la condición de carrera en este caso? ¿Qué es lo que está pasando? Te pido que propongas un ejemplo.***

La condición de carrera pasa cuando varios hilos intentan usar y cambiar una misma variable al mismo tiempo. Por ejemplo, si dos hilos leen que el contador vale 10, ambos suman 1 y escriben 11, en lugar de que el resultado final sea 12. Esto ocurre porque no esperan su turno. Al usar un lock, solo un hilo puede modificar la variable a la vez y se evita ese error. Es como cuando varias personas quieren entrar al mismo baño: si no hay seguro, todos entran a la vez y se hace un caos; con seguro, entran de uno en uno y todo funciona bien.


## Actividad 03

🧐🧪✍️ Reporta en tu bitácora

***Ejecuta el código y observa el resultado.***


<img width="1019" height="762" alt="image" src="https://github.com/user-attachments/assets/b26ac8ba-6e46-408e-a65b-7275fab84ed1" />


<img width="1022" height="765" alt="image" src="https://github.com/user-attachments/assets/fa261c70-8b96-4255-9d2c-ddcac9633213" />


En la versión secuencial, hubo un pequeño drop de frames de 60 a 55 por un instante, probablemente porque todo el cálculo pesado se hacía en el hilo principal y eso afectó un poquito la animación. En la versión paralela, los frames se mantuvieron casi siempre en 60, porque la tarea pesada se movió a un hilo aparte y no bloqueó la interfaz, haciendo que el programa se vea mucho más fluido. El drop que pudo ocurrir fue tan breve e insignificante que prácticamente no se notó.

***Analiza el código y estudia detenidamente su funcionamiento. En la fase de aplicación tendrás que retomar este código para resolver un reto.***

Analizando el código, en `threadedFunction()` se recorre cada píxel de la ventana y se calculan los colores según el número de iteraciones hechas y el máximo definido, mapeando ese valor al color correspondiente. En el `setup()` se define el número máximo de iteraciones (que controla el nivel de detalle del fractal) y se ajusta la cantidad de píxeles según el tamaño de la ventana. En `draw()` solo se muestra información de debug como fps, iteraciones, etc.

Al presionar espacio, se incrementa el número máximo de iteraciones y se recalculan los colores; al presionar n, se resetea a 0. Si hago “spam” de espacio después de resetear, se ve cómo el detalle del fractal aumenta progresivamente. No hay locks en el programa.

La diferencia principal entre la versión secuencial y la paralela es la velocidad: en la secuencial todo se hace en un solo hilo y tarda más en actualizar cada píxel; en la paralela se usan 16 hilos, lo que permite calcular muchos píxeles al mismo tiempo y acelera muchísimo el proceso, manteniendo la misma base de cálculos pero mucho más rápido.


***Experimenta modificando, PERO, no olvides cómo investigamos en este curso:***

 Cambiar el color

* **Cambio:** Varié el hue a 10 para ver si el fondo cambiaba de rojo a otro color.
* **Hipótesis:** Esperaba que el color fuera distinto, algo más diferente al rojo.
* **Resultado:** En realidad la imagen quedó todavía más roja, porque con ese hue hay menos variación de color.
* **Conclusión:** Mi hipótesis no se cumplió del todo, pero logré un efecto interesante; el hue bajo hizo que el rojo dominara.



## Actividad 04

🧐✍️ Reporta en tu bitácora

**¿Cuál es la estructura de datos principal que contiene la información de todos los boids y que es accedida por múltiples hilos (el hilo principal para dibujar, el hilo trabajador para actualizar)?**

La estructura principal es un **`std::vector<Boid>` llamado `boids` dentro de la clase `Flock`**. Este vector almacena todos los boids y es accedido tanto por el hilo principal (para dibujar) como por el hilo trabajador (para actualizar posiciones y movimientos).

**Observa la función `Flock::threadedFunction()` donde el hilo trabajador calcula el movimiento. ¿Qué operaciones realizan sobre el vector de boids compartido?**

Dentro de `threadedFunction()`:

* Se hace un **`lock()`** antes de manipular el vector.
* Se recorre **cada boid** del vector y se llama a `b.run(boids)`, donde cada boid actualiza su posición y velocidad tomando en cuenta a los demás boids.
* Después de actualizar todos los boids, se hace un **`unlock()`**.

Es decir, el hilo **lee y escribe** sobre el vector de boids, calculando su comportamiento.


**Observa la función `ofApp::draw()`. ¿Qué operación realiza sobre el vector compartido?**

En `draw()`:

* Se hace un **`lock()`** del vector compartido.
* Se recorre el vector de boids y se llama a `b.draw()` para dibujar cada boid en pantalla.
* Se hace un **`unlock()`** después de dibujar.

Así que esta función **solo lee** los datos del vector para dibujarlos, pero el lock asegura que no haya escritura simultánea mientras se dibuja.


**Observa `Flock::addBoid()` y `ofApp::mouseDragged()`. ¿Qué operación realizan?**

* `Flock::addBoid(int x, int y)` hace un **`lock()`**, agrega un nuevo boid al final del vector usando `boids.emplace_back(x, y)`, y luego hace un **`unlock()`**.
* `ofApp::mouseDragged()` llama a `addBoid()` cada vez que el usuario arrastra el mouse, creando nuevos boids dinámicamente.

Es decir, ambas funciones **modifican el vector** añadiendo elementos al final.


**Describe un escenario específico y concreto donde la falta de sincronización podría causar un problema.**

Ejemplo:

* El **hilo X** recorre el vector de boids en `threadedFunction()` para calcular la separación entre boids.
* Al mismo tiempo, el **hilo Y**, desde `mouseDragged()`, llama a `addBoid()` y agrega un boid al final del vector.

**Problema:** el iterador del hilo X podría quedar **invalido** o calcular posiciones incorrectas, causando **crasheos** o resultados de movimiento erráticos.


**Localiza todas las llamadas a `lock()` y `unlock()` dentro de la clase Flock (o donde se acceda al vector compartido).**

* **`Flock::threadedFunction()`**:

```cpp
lock();
for (Boid& b : boids) {
    b.run(boids);
}
unlock();
```

* **`Flock::addBoid()`**:

```cpp
lock();
boids.emplace_back(x, y);
unlock();
```

* **`ofApp::draw()`**:

```cpp
flock.lock();
for (Boid& b : flock.boids) {
    b.draw();
}
flock.unlock();
```


**Justificación: para uno de los escenarios problemáticos que describiste arriba, explica cómo las llamadas a `lock()/unlock()` en las secciones de código relevantes evitan que ocurra ese problema específico.**

Si el hilo que dibuja (`draw()`) quiere acceder al vector mientras el hilo trabajador está actualizando posiciones:

* El **lock en `threadedFunction()`** asegura que ningún otro hilo puede leer/escribir el vector mientras se actualiza.
* El **lock en `draw()`** asegura que el dibujo solo ocurre después de que se terminó la actualización.

Esto evita que un boid lea información parcial o que un iterador quede inválido, eliminando **condiciones de carrera**.


**Aunque los locks aseguran la correctitud, ¿por qué tener muchos hilos esperando para adquirir un lock sobre el mismo vector podría limitar el beneficio de rendimiento del paralelismo?**

Porque todos los hilos compiten por el mismo lock. Mientras uno accede al vector, los demás **quedan bloqueados**, esperando su turno. Esto genera **alta contención** y hace que muchos hilos estén inactivos, reduciendo el **beneficio de paralelismo**.


🧐✍️ Reporta en tu bitácora

**¿Qué pasaría si tuviéramos varios hilos que calculan el movimiento de los boids? ¿Cómo podrías implementarlo? ¿Qué problemas podrían surgir? ¿Cómo solucionarlos?**

* Se podrían dividir los boids en **grupos** y asignar un hilo a cada grupo.
* Problema: cada boid necesita información de **todos los boids cercanos**, no solo de su grupo, por lo que podrían leer datos inconsistentes.
* Otra opción: un hilo calcula **separación**, otro **alineación**, otro **cohesión**, pero habría que sincronizar entre hilos para no usar datos incompletos.
* Solución parcial: usar **locks finos o copias de snapshot** de los datos para que cada hilo trabaje con información consistente sin bloquear demasiado.

🧐🧪✍️ Reporta en tu bitácora

**Analiza el código del Flocking sin hilos y el Flocking con hilos. ¿Qué diferencias encuentras? ¿Por qué es importante la sincronización en el segundo caso?**

* Sin hilos: las actualizaciones y el dibujo ocurren secuencialmente; no hay riesgo de datos inconsistentes.
* Con hilos: múltiples hilos acceden al mismo vector; sin sincronización podrían ocurrir **condiciones de carrera**.
* Por eso es importante el **lock/unlock**: asegura que un hilo termine su operación antes de que otro acceda al mismo vector.


**¿Por qué al añadir un nuevo boid la simulación se ralentiza? ¿Qué ocurre si añades muchos boids?**

* Cada boid debe calcular su movimiento tomando en cuenta **todos los demás boids**.
* Al añadir más boids, el número de cálculos crece **aproximadamente cuadráticamente** (O(n²)), por eso la simulación se ralentiza.
* Con muchos boids, los FPS caen drásticamente y los movimientos pueden volverse poco fluidos.


**Notaste que la versión con hilos tiene un `sleep(5)` en el hilo trabajador. ¿Por qué crees que se ha añadido? ¿Qué pasaría si lo eliminamos?**

* `sleep(5)` **alivia la CPU** evitando que el hilo trabajador consuma 100% de un núcleo continuamente.
* Si se elimina, el hilo se ejecutaría a máxima velocidad, usando mucho CPU y pudiendo generar **lag o inestabilidad** en la simulación.


**Compara el rendimiento de ambos enfoques. ¿Cuál crees que es más eficiente? ¿Por qué?**

* Con pocos boids: **sin hilos** puede ser más eficiente porque evita overhead de locks y threads.
* Con muchos boids: **con hilos** es más eficiente porque permite que la actualización y el dibujo ocurran en paralelo, manteniendo mejor responsividad.


**El uso de `lock` y `unlock` en la versión con hilos es crucial para evitar condiciones de carrera. ¿Qué pasaría si no se usaran? ¿Cómo afectaría esto al comportamiento del programa?**

* Habría **condiciones de carrera**, con resultados impredecibles:

  * Boids que “teletransportan” su posición.
  * Movimientos erráticos o inconsistentes.
  * Iteradores inválidos y posibles **crashes** del programa.

🧐✍️ Reporta en tu bitácora

**¿Qué ocurre si mientras el hilo trabajador está calculando el movimiento de los boids, el hilo principal intenta añadir un nuevo boid? ¿Se congelará la aplicación? ¿Por qué?**

* No se congelará completamente si se usan locks; el hilo principal **esperará** hasta que el hilo trabajador termine su lock.
* Si no hubiera locks, podrían ocurrir **crashes o datos inconsistentes**, pero con locks, solo hay una breve espera.



## Actividad 05 APPLY

🧐🧪✍️ Reporta en tu bitácora

***Pega la parte clave de tu función modificada que calcula el píxel para el conjunto de Julia. Recuerda utilizar un bloque cpp.***

```c++
int computeJuliaPixel(int x, int y) {
    // Convertir coordenadas de píxel a coordenadas complejas
    float zx = ofMap(x, 0, imgW, -1.5f, 1.5f);
    float zy = ofMap(y, 0, imgH, -1.5f, 1.5f);
    int iter = 0;

    // Iterar según la fórmula de Julia: z = z² + k
    while ((zx * zx + zy * zy < 4.0f) && (iter < maxIterations)) {
        float temp = zx * zx - zy * zy + juliaConst.x;  // parte real
        zy = 2.0f * zx * zy + juliaConst.y;             // parte imaginaria
        zx = temp;
        ++iter;
    }

    return iter;
}

```

***Muestra cómo mapeaste la posición del mouse a la constante k.***

```c++
//--------------------------------------------------------------
void ofApp::mouseMoved(int x, int y) {
    // Mapeo de la posición del mouse a valores entre -1.5 y 1.5
    juliaK.x = ofMap(x, 0, ofGetWidth(), -1.5f, 1.5f);   // Parte real
    juliaK.y = ofMap(y, 0, ofGetHeight(), -1.5f, 1.5f);  // Parte imaginaria

    // Indicar que se debe recalcular la imagen con el nuevo valor de k
    needsRecalculation = true;
}
```


***Describe brevemente cómo reutilizaste la estructura de hilos de la versión Mandelbrot. ¿Tuviste que cambiar mucho esa parte?***

- Renombré la clase del hilo a JuliaSetThread y cambié la función interna para que usara calculateJuliaPixel() en lugar de calculateMandelbrotPixel().

- Agregué la constante juliaK como parámetro, para que cada hilo pudiera acceder al valor actual de la constante compleja k.

- Mantuvé el mismo sistema de creación, inicio y espera de hilos, sin modificar la lógica de sincronización o el manejo del vector threads.

***¿Cómo te aseguraste de que la imagen se recalculara cuando el mouse se movía?***

Para asegurarme de que la imagen del conjunto de Julia se recalculara cuando el mouse se movía, usé un sistema de bandera y actualización controlada:

En la función mouseMoved(int x, int y) actualizo la constante compleja k según la posición del mouse y activo una bandera:

```c++
juliaK.x = ofMap(x, 0, ofGetWidth(), -1.5f, 1.5f);
juliaK.y = ofMap(y, 0, ofGetHeight(), -1.5f, 1.5f);
needsRecalculation = true;  // Marca que se debe recalcular
```

En el método update(), verifico esa bandera:
```c++
if (needsRecalculation && !calculating) {
    startCalculation();      // Lanza los hilos para recalcular la imagen
    needsRecalculation = false;
}
```

***Incluye al menos dos capturas de pantalla que muestren diferentes fractales de Julia generados al mover el mouse en tu aplicación.***

<img width="1010" height="757" alt="image" src="https://github.com/user-attachments/assets/bee7de16-2b82-45b6-889a-352f096b2813" />


<img width="997" height="742" alt="image" src="https://github.com/user-attachments/assets/3f43ba90-1517-4cb8-a17b-346e008dba73" />


<img width="1003" height="746" alt="image" src="https://github.com/user-attachments/assets/a6ce8531-bbad-4bfb-b5db-7f3758204bfb" />



***¿Encontraste algún desafío particular al implementar la interacción o modificar el cálculo?***

Lo más complicado fue entender bien la diferencia entre Mandelbrot y Julia, porque al principio solo cambié la fórmula y no me daba nada visible. Después me di cuenta de que en Julia el valor inicial de z es el píxel, y k es constante, mientras que en Mandelbrot es al revés.

También me costó un poco hacer que la imagen se actualizara de forma fluida con el movimiento del mouse. Al principio recalculaba todo en cada frame y se trababa un poco, así que tuve que usar una bandera (needsRecalculation) para que solo se regenerara cuando realmente cambiaba k.

En general, no fue tan difícil modificar la parte de los hilos, pero sí entender bien la lógica matemática y cómo hacer que reaccionara en tiempo real sin colapsar el programa.


## MI NOTA ES: 5.0

Mi nota debería ser 5.0, ya que cumplí todas las actividades al 100%, demostrando un dominio completo del tema y un trabajo constante y profundo en cada parte del proceso. En cada actividad no solo respondí correctamente, sino que analicé, expliqué con mis propias palabras y generé hipótesis fundamentadas sobre el funcionamiento del código y los conceptos vistos. Además, en el Apply, logré una implementación totalmente funcional, bien explicada y argumentada, mostrando que comprendí la teoría y su aplicación práctica. En conjunto, mi trabajo refleja dedicación, comprensión profunda y capacidad de análisis, lo que justifica la calificación máxima.


***💀👻🎃 GRACIAS PROFE!!!! 💀👻🎃***




