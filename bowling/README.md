# Bowling Game

[Original](https://kata-log.rocks/bowling-game-kata)

## El problema

La kata consiste en crear un programa para calcular las puntuaciones del juego de los Bolos, aunque para evitar complicarla mucho solo se calcula el resultado final y no se hacen validaciones sobre las puntuaciones.

Si no tienes familiaridad con el juego y su sistema de puntuación, aquí van las reglas que es necesario conocer:

* En cada juego, el jugador o jugadora tiene 10 turnos, llamados frames.
* Dentro de cada frame, se dispone de dos intentos para tumbar los 10 bolos (eso hace un total de 20 intentos o lanzamientos de bola en todo el juego).
* En cada intento, se cuentan los bolos tumbados y la puntuación del frame es la suma de ambos intentos.
* Si no se tira ningún bolo es un Gutter.
* Si no se han tirado todos los bolos en los dos intentos esa será la puntuación. Por ejemplo 3 + 5 = 8 puntos en el frame.
* Si se han tumbado los 10 bolos en el frame (por ejemplo 4 + 6), a eso se le llama spare y se obtiene un bonus que será la puntuación del siguiente lanzamiento, el primero del siguiente frame (10 del frame actual + 3 del siguiente lanzamiento = 13). Esto es, la puntuación final de un spare se calcula después del siguiente lanzamiento y, por así decir, ese lanzamiento se cuenta dos veces (una como bonus y otra normal).
* Si se han tumbado los 10 bolos en un solo lanzamiento es un strike y en ese caso, el bonus es la puntuación del siguiente frame (por ejemplo, 10 + (3 + 4) = 17).
* En el caso de que esto se produzca en el último frame, se hacen uno o dos lanzamientos extras según sea necesario.

## Ideas para resolverla

* Vamos a contar los tantos para una sola jugadora
* Cada lanzamiento de bola es un roll y se indican cuantos bolos ha derribado en ese roll, hasta un máximo de 10
* Hay que tener en cuenta que, en algunos casos (spare y strike) se suman puntos del siguiente frame

## Sugerencias

* La clase Bowling podría tener dos métodos: roll y score
  
## Más difícil todavía

* Mofifica Bowling Game para permitir controlar los puntos de varias jugadoras
