# Obfuscator

Debido a los requisitos de privacidad exigidos en nuestro negocio hemos tenido que desarrollar un servicio que nos permita ofuscar información cuando se muestra en determinadas circunstancias. Este servicio funciona muy bien y se puede configurar mediante unas recetas muy sencillas en formato de texto.

Sin embargo, hemos tenido un problema y necesitamos recuperar información de algunos documentos que fueron ofuscados y de los que se ha perdido el original. Por suerte, conocemos la recetas que se usaron, pero tenemos que desarrollar un programa que automatice la "desofuscación". Básicamente, tenemos que invertir la receta, ejecutando los pasos en orden inverso e invirtiendo su efecto.

## Comandos

Estos son los comandos que componen las recetas: Rotar (R) y Transponer (T)

### Rotar

Rotar mueve las letras del texto hacia la derecha tantos caracteres como se indique. Los caracteres del final se añaden al principio. Por ejemplo:

| comando | texto    | ofuscado |
|---------|----------|----------|
| R1      | password | dpasswor |
| R2      | password | rdpasswo |
| R4      | password | wordpass |


### Transponer

Transponer cambia las letras del texto por otras del abecedario que estén a la distancia indicada.

| comando | texto | ofuscado |
|---------|-------|----------|
| T1      | a     | b        |
| T2      | a     | c        |
| T3      | a     | d        |

Si alcanzamos el final del abecedario se empieza de nuevo:

| comando | texto | ofuscado |
|---------|-------|----------|
| T1      | z     | a        |
| T2      | y     | a        |
| T4      | y     | c        |

Si las letras están en mayúsculas, se transponen en mayúscula. Los signos de puntuación y espacios se dejan como están. Para este ejercicio no se da soporte a caracteres acentuados, ni a números.

Este será nuestro abecedario:

A, B, C, D, E, F, G, H, I, J, K, L, M, N, O, P, Q, R, S, T, U, V, W, X, Y, Z

a, b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u, v, w, x, y, z

### Recetas

Las recetas son combinaciones de comandos. Por ejemplo:

| Receta.  | Original | Ofuscado |
|----------|----------|----------|
| T1:R1    | ab       | cb       |
| T1:R2:T3 | abc      | fge      |

## El desafío

Nuestro desafío es crear una clase (o función) que pueda revertir el efecto de la receta. Es decir, que si le pasamos la receta y el texto ofuscado sea capaz de desvelar el mensaje oculto.

Esta es la receta que se aplicó para ofuscar el mensaje que necesitamos recuperar:

```
T22R39
```

Y este el mensaje ofuscado que queremos desvelar

```
Bahev ranwjk. Jko raiko aj hw lqhlkYkj.
```

### Pistas

Para desofuscar, tendremos que aplicar la receta en sentido inverso. Por ejemplo. Imagina que creamos una función `reveal`:

```
reveal("R2", "rdpasswo") // devuelve "password", sería algo así como aplicar R-2
reveal("T2", "c") // devuelve "a", sería como aplicar T-2 
```

Si la receta tiene varios pasos, entonces los tenemos que aplicar en orden inverso

```
reveal("T1:R2:T3", "fge") // devuelve "abc", aplicando (invertidas) T-3 -> R-2 -> T-1
```
