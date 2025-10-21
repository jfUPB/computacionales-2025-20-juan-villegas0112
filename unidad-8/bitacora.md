# Bitácora de aprendizaje de la unidad 8

## Actividad 01

🧐🧪✍️ Reporta en tu bitácora

***Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?***

Al ejecutar el programa, veo que el círculo se mueve de izquierda a derecha como esperaba. Cuando hago clic, el círculo cambia de tamaño, pero en ese momento la aplicación se queda congelada por unos segundos. Yo pensaba que el cambio de tamaño sería instantáneo, pero claramente no lo es.

Creo que esto pasa porque el programa está haciendo un cálculo muy pesado (lo de sqrt(j) muchas veces) en la función heavyComputation(), y como todo eso se ejecuta en el mismo hilo principal, el programa no puede seguir dibujando el círculo mientras hace ese cálculo. Entonces, como solo hay un hilo trabajando, se queda ocupado haciendo esa tarea y no puede hacer nada más al mismo tiempo.

🧐🧪✍️ Reporta en tu bitácora

***Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?***



***Observa que el programa ahora no se congela, pero el círculo no cambia de tamaño inmediatamente. ¿Por qué crees que sucede esto? ¿Qué es lo que está pasando?***



## Actividad 02

## Actividad 03

## Actividad 03


## Actividad 04


## Actividad 05
