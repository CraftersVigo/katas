# Cupcake kata

[Original](https://codingdojo.org/kata/cupcake/)

Este kata se hizo originalmente para implementar el patron decorador y el patrón composite.

## Descripción del problema

Escribe un programa que pueda hacer muchos pasteles con muchos ingredientes como: "Cupcake con chocolate y nueces" O "🧁 con  🍫 negro y 🥜 y 🍬". Ten cuidado, el orden de las capas es **muy importante**.

Escribe una función o método que pueda mostrar el nombre del pastel.

Escribe una función que pueda mostrar el precio del pastel. El precio se compone del precio del pastel base y el precio de la cobertura.

# Paquete de pasteles no frescos

Ahora podemos hacer paquetes de pasteles. El precio de un paquete es un 10% menos que los precios de cada pastel.

Es posible construir un paquete de paquetes con pasteles individuales.

## Casos de prueba sugeridos

### Patrón decorador

En pseudocódigo para construir una magdalena con chocolate, nueces y azúcar, escribiríamos algo así como:

```
Var myCake = Sugar(Nuts(Chocolate(Cupcake())))
```

Con la escritura, podemos empezar a probar:

* Puedo poner un cupcake en una variable de tipo Cake

Acerca de la función o método de nombre del cupcake: 

* La función de nombre debería devolver "🧁"
* La función de nombre debería devolver "🍪"
* La función de nombre debería devolver "🧁 con 🍫"
* La función de nombre debería devolver "🍪 con 🍫"
* La función de nombre debe devolver "🍪 con 🍫 y 🥜"
* La función de nombre debe devolver "🍪 con 🥜 y 🍫"

Acerca de la función o método de precio:

* La función de precio debería devolver 1 $ para "🧁"
* La función de precio debería devolver 2 $ para "🍪"
* La función de precio debería devolver 1,1 $ para "🧁 con 🍫"
* La función de precio debería devolver 2,1 $ para "🍪 con 🍫"
* La función de precio debería devolver 2,2 $ por "🍪 con 🥜"

### Paquete

* Podemos construir un paquete con 1 magdalena y comprobar el precio o la descripción
* Podemos construir un paquete con 1 magdalena y 1 galleta y comprobar el precio o la descripción
* Podemos construir un paquete con 2 magdalenas y 1 galleta y comprobar el precio o la descripción
* Podemos construir un paquete con 1 paquete de 2 pasteles y 1 magdalena y comprobar el precio o la descripción
* Podemos construir un paquete con muchos paquetes de paquetes y muchos pasteles y comprobar el precio o la descripción
