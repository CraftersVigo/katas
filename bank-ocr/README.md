# Bank OCR

[Original](https://codingdojo.org/kata/BankOCR/)

## User Story 1

Trabajas para un banco que ha comprado recientemente una máquina que ayuda a leer cartas y faxes enviados por las sucursales. La máquina escanea los documentos en papel y produce un fichero con un número de entradas que tienen este aspecto:

```
  _  _     _  _  _  _  _ 
| _| _||_||_ |_   ||_||_|
||_  _|  | _||_|  ||_| _|

```

Cada entrada tiene 4 líneas de longitud y cada línea tiene 27 caracteres. Las 3 primeras líneas de cada entrada contienen un número de cuenta escrito usando pipes `|` y subrayados `_`, y la cuarta línea está en blanco. Cada número de cuenta debería tener 9 cifras, todas las cuales deberían estar en el rango de 0 a 9. Un archivo normal contiene alrededor de 500 entradas.

La primera tarea es escribir un programa que pueda tomar este archivo y parsearlo en forma de números de cuenta.


## User Story 2

Habiendo hecho esto, enseguida te das cuenta de que la ingeniosa máquina no es infalible. A veces se equivoca con el escaneo. El siguiente paso, por tanto es validar que los números obtenidos son, de hecho, números de cuenta válidos. Un número de cuenta vålido tiene un _checksum_ válido, que se puede calcular como sigue:

```
account number:  3  4  5  8  8  2  8  6  5
position names:  d9 d8 d7 d6 d5 d4 d3 d2 d1

checksum calculation:
(d1+2*d2+3*d3+...+9*d9) mod 11 = 0
```

Así que ahora tienes que escribir código que calcule el checksum para un número dado y verifique si es un número de cuenta válido o no.


## User Story 3

Tu jefe está deseando ver los resultados. Te pide que escribas un archivo con tus hallazgos, uno por archivo de entrada, con este formato:

```
457508000
664371495 ERR
86110??36 ILL
```

El archivo tiene un número de cuenta por fila. Si algunos caracteres son ilegibles, se reemplazan por un `?`. En el caso de que el número tenga un checksum erróneo o sea ilegible, el estado se indica en la segunda columna.

## User Story 4

Resulta que en algunos casos cuando un número aparece como erróneo (ERR) o no válido (ILL) es porque el escáner ha fallado al capturar una pipe o un subrayado para alguna de las cifras. Por ejemplo:


```
    _  _  _  _  _  _     _ 
|_||_|| || ||_   |  |  ||_
  | _||_||_||_|  |  |  | _|

``` 

El 9 podría ser un 8 si el escáner hubiese fallado una `|`. O el 0 podría ser un 8. O el 1 podría ser un 7. El 5 podría ser un 9 o un 6. 

Por eso, tu siguiente tarea sería examinar los números que han resultado con ERR o ILL y tratar de averiguar si cual serían añadiendo o quitando una pipe o un subrayado.

Si resulta que hay solo un número posible con un checksum válido, entonces úsalo. Si hay varias opciones, el estado debería ser AMB.

Si a pesar de todo, no puedes encontrar qué debería ser, el estado entonces tendrá que reportarse como ILL.

## Ejemplos para tests

```
user story 1
 _  _  _  _  _  _  _  _  _ 
| || || || || || || || || |
|_||_||_||_||_||_||_||_||_|
                           
=> 000000000
                           
  |  |  |  |  |  |  |  |  |
  |  |  |  |  |  |  |  |  |
                           
=> 111111111
 _  _  _  _  _  _  _  _  _ 
 _| _| _| _| _| _| _| _| _|
|_ |_ |_ |_ |_ |_ |_ |_ |_ 
                           
=> 222222222
 _  _  _  _  _  _  _  _  _ 
 _| _| _| _| _| _| _| _| _|
 _| _| _| _| _| _| _| _| _|
                           
=> 333333333
                           
|_||_||_||_||_||_||_||_||_|
  |  |  |  |  |  |  |  |  |
                           
=> 444444444
 _  _  _  _  _  _  _  _  _ 
|_ |_ |_ |_ |_ |_ |_ |_ |_ 
 _| _| _| _| _| _| _| _| _|
                           
=> 555555555
 _  _  _  _  _  _  _  _  _ 
|_ |_ |_ |_ |_ |_ |_ |_ |_ 
|_||_||_||_||_||_||_||_||_|
                           
=> 666666666
 _  _  _  _  _  _  _  _  _ 
  |  |  |  |  |  |  |  |  |
  |  |  |  |  |  |  |  |  |
                           
=> 777777777
 _  _  _  _  _  _  _  _  _ 
|_||_||_||_||_||_||_||_||_|
|_||_||_||_||_||_||_||_||_|
                           
=> 888888888
 _  _  _  _  _  _  _  _  _ 
|_||_||_||_||_||_||_||_||_|
 _| _| _| _| _| _| _| _| _|
                           
=> 999999999
    _  _     _  _  _  _  _ 
  | _| _||_||_ |_   ||_||_|
  ||_  _|  | _||_|  ||_| _|
                           
=> 123456789

user story 3
 _  _  _  _  _  _  _  _    
| || || || || || || ||_   |
|_||_||_||_||_||_||_| _|  |
                           
=> 000000051
    _  _  _  _  _  _     _ 
|_||_|| || ||_   |  |  | _ 
  | _||_||_||_|  |  |  | _|
                           
=> 49006771? ILL
    _  _     _  _  _  _  _ 
  | _| _||_| _ |_   ||_||_|
  ||_  _|  | _||_|  ||_| _ 
                           
=> 1234?678? ILL

user story 4
                           
  |  |  |  |  |  |  |  |  |
  |  |  |  |  |  |  |  |  |
                           
=> 711111111
 _  _  _  _  _  _  _  _  _ 
  |  |  |  |  |  |  |  |  |
  |  |  |  |  |  |  |  |  |
                           
=> 777777177
 _  _  _  _  _  _  _  _  _ 
 _|| || || || || || || || |
|_ |_||_||_||_||_||_||_||_|
                           
=> 200800000
 _  _  _  _  _  _  _  _  _ 
 _| _| _| _| _| _| _| _| _|
 _| _| _| _| _| _| _| _| _|
                           
=> 333393333 
 _  _  _  _  _  _  _  _  _ 
|_||_||_||_||_||_||_||_||_|
|_||_||_||_||_||_||_||_||_|
                           
=> 888888888 AMB ['888886888', '888888880', '888888988']
 _  _  _  _  _  _  _  _  _ 
|_ |_ |_ |_ |_ |_ |_ |_ |_ 
 _| _| _| _| _| _| _| _| _|
                           
=> 555555555 AMB ['555655555', '559555555']
 _  _  _  _  _  _  _  _  _ 
|_ |_ |_ |_ |_ |_ |_ |_ |_ 
|_||_||_||_||_||_||_||_||_|
                           
=> 666666666 AMB ['666566666', '686666666']
 _  _  _  _  _  _  _  _  _ 
|_||_||_||_||_||_||_||_||_|
 _| _| _| _| _| _| _| _| _|
                           
=> 999999999 AMB ['899999999', '993999999', '999959999']
    _  _  _  _  _  _     _ 
|_||_|| || ||_   |  |  ||_ 
  | _||_||_||_|  |  |  | _|
                           
=> 490067715 AMB ['490067115', '490067719', '490867715']
    _  _     _  _  _  _  _ 
 _| _| _||_||_ |_   ||_||_|
  ||_  _|  | _||_|  ||_| _|
                           
=> 123456789
 _     _  _  _  _  _  _    
| || || || || || || ||_   |
|_||_||_||_||_||_||_| _|  |
                           
=> 000000051
    _  _  _  _  _  _     _ 
|_||_|| ||_||_   |  |  | _ 
  | _||_||_||_|  |  |  | _|
                           
=> 490867715 

```

Ejemplo de representación de los números:

```json
{
	"0": [
		" _ ",
		"| |",
		"|_|"
	],
	"1": [
		"   ",
		"  |",
		"  |"
	],
	"2": [
		" _ ",
		" _|",
		"|_ "
	],
	"3": [
		" _ ",
		" _|",
		" _|"
	],
	"4": [
		"   ",
		"|_|",
		"  |"
	],
	"5": [
		" _ ",
		"|_ ",
		" _|"
	],
	"6": [
		" _ ",
		"|_ ",
		"|_|"
	],
	"7": [
		" _ ",
		"  |",
		"  |"
	],
	"8": [
		" _ ",
		"|_|",
		"|_|"
	],
	"9": [
		" _ ",
		"|_|",
		" _|"
	]
}
```
