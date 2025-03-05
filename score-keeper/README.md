# Score Keeper

[Original](https://kata-log.rocks/score-keeper-kata)

## El problema

Necesitamos software para proporcionar los datos adecuados al marcador de un equipo de baloncesto. Desafortunadamente, las personas que usan nuestro software no son las más brillantes, por lo que necesitan seis botones (cada equipo puede anotar 1, 2 o 3 puntos con un solo tiro).

## La tarea

Escribe una clase `ScoreKeeper` que ofrezca los siquientes métodos:

```
void scoreTeamA1()
void scoreTeamA2()
void scoreTeamA3()
void scoreTeamB1()
void scoreTeamB2()
void scoreTeamB3()
String getScore()
```

## Reglas

* La cadena retornada siempre tiene **siete** caracteres. Un ejemplo sería `000:000`
* Hay que resolverlo obligatoriamente en TDD

## Sugerencias para darle _picante_ a este ejercicio

Puedes aplicar algunas de las siguientes reglas

* No utilizar tipos primitivos.
* Hacer TDD ping-pong: una persona escribe el primer test, la otra escribe el código de producción y un nuevo test a continuación. Se lo pasa a la primera persona y así sucesivamente.
* Introducir una clase `ScoreDisplay` y aplicar el patrón _Observer_ para actualizarla.
* Añadir mecanismos para rebobinar, avanzar o resetear el marcador. Y para reproducir la historia del partido.
