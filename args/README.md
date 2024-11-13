# Args

## Acerca de este Kata

Este Kata se presenta en el libro de Robert C. Martin, *Código Limpio*, capítulo 14.

## Descripción del Problema

La mayoría de nosotros ha tenido que analizar argumentos de línea de comandos de vez en cuando. Si no contamos con una utilidad conveniente, simplemente recorremos el arreglo de cadenas que se pasa a la función principal. Existen varias utilidades útiles disponibles de diversas fuentes, pero probablemente no hagan exactamente lo que necesitamos. Así que, ¡escribamos una nosotros mismos!

Los argumentos que se pasan al programa consisten en banderas y valores. Las banderas deben ser caracteres individuales precedidos por un signo de menos. Cada bandera puede tener asociado cero o un valor.

Deberás escribir un analizador para este tipo de argumentos. Este analizador toma un esquema que detalla qué argumentos espera el programa. El esquema especifica el número y tipos de banderas y valores que el programa espera.

Una vez que se haya especificado el esquema, el programa deberá pasar la lista de argumentos reales al analizador de argumentos. Este verificará que los argumentos coincidan con el esquema. El programa podrá entonces solicitar al analizador cada uno de los valores, usando los nombres de las banderas. Los valores se devuelven con los tipos correctos, según lo especificado en el esquema.

Por ejemplo, si el programa se llama con los siguientes argumentos:

```
-l -p 8080 -d /usr/logs
```

Esto indica un esquema con 3 banderas: `l`, `p`, `d`. La bandera `l` (logging) no tiene valores asociados, por lo que es una bandera booleana: `True` si está presente, `False` si no lo está. La bandera `p` (puerto) tiene un valor entero, y la bandera `d` (directorio) tiene un valor de cadena.

Si una bandera mencionada en el esquema falta en los argumentos, se debe devolver un valor predeterminado adecuado, como `False` para una booleana, `0` para un número y `""` para una cadena. Si los argumentos dados no coinciden con el esquema, es importante que se dé un mensaje de error claro, explicando exactamente cuál es el problema.

Si te sientes ambicioso, extiende tu código para soportar listas, por ejemplo:

```
-g this,is,a,list -d 1,2,-3,5
```

Así, la bandera `g` indicaría una lista de cadenas: `["this", "is", "a", "list"]` y la bandera `d` indicaría una lista de enteros: `[1, 2, -3, 5]`.

Asegúrate de que tu código sea extensible, de modo que sea sencillo y evidente cómo agregar nuevos tipos de valores.

### Pistas

El aspecto que debe tener el esquema y cómo especificarlo se deja intencionadamente vago en la descripción del Kata. Una parte importante del Kata es diseñar un formato conciso y legible para él.

### Casos de Prueba Sugeridos

- Asegúrate de tener una prueba con un entero negativo (para manejar correctamente el signo `-`).
- El orden de los argumentos no necesita coincidir con el orden dado en el esquema.
- Incluye pruebas que verifiquen que los valores predeterminados se asignan correctamente si las banderas presentes en el esquema faltan en los argumentos dados.