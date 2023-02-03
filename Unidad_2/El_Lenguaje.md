# El Lenguaje
Un mar tranquilo nunca hizo a un marinero hábil

La sintaxis de Elixir está basada en otros lenguajes como Ruby y
Erlang y agrega el suficiente azúcar sintáctico para dar flexibilidad al
programador para escribir código simple. Permite expresar fácilmente el
código escrito. No obstante debemos recordar que Elixir es un lenguaje
funcional. La especificación de la solución al problema a resolver
mediante código difiere un poco al planteamiento en otros lenguajes
imperativos como Java, C/C++, Perl o PHP.

`def area(base,altura), do: base * altura`

En este ejemplo definimos una función en Elixir. El área de un rectángulo.
Los parámetros son base y altura. 

```
for i <- 1..10,
	clavar(i) == "si",
	do: martillea_clavo(i)
```

Es lo mismo que hacer lo siguiente.

```
1..10 
|> Enum.filter(&(clavar(&1) == "si" ))
|> Enum.each(&martillea_clavo/1)
```

```
1..10
|> Stream.filter(&(clavar(&1) == "si"))
|> Enum.each(&martillea_clavo/1)
```

## El intérprete de Elixir (iex)

La mayoría del código de ejemplo lo vamos a ejecutar en la línea de
comandos o el intérprete de Elixir. Antes de continuar te recomiendo que
instales Elixir y pruebes a acceder al intérprete ejecutando iex en una
consola de tu sistema operativo. 

```
$ iex
Erlang/OTP 21 [erts-10.1.3] [source] [64-bit] [smp:8:8]
[ds:8:8:10] [async-threads:1] [hipe] [kernel-poll:false]
[dtrace]
Interactive Elixir (1.7.4) - press Ctrl+C to exit (type h()
ENTER for help)
iex(1)>
```

## Comentarios
En elixir podemos agregar comentarios empleando el símbolo almohadilla (#)

```
# Este código calcula el área del rectángulo:
area = base * altura # multiplica área por base
```

## Tipos de Datos


En Elixir disponemos de distintos tipos de datos desde simples átomos o
números hasta estructuras compuestas por otros tipos de datos, mapas y
listas. Cada tipo de dato tiene sus propias particularidades y su cometido


## Átomos
Los átomos son una unidad muy pequeña y auto-explicativa que
podemos usar para agregar código más legible y errores más
comprensibles en consola al emplear texto en lugar de números para
indicar estados, códigos de error o indicadores para configuración entre
otros.
Este tipo de dato nos ayuda a dar nombre al contenido de variables
sin necesidad de ocupar mucho tamaño en memoria.


```
iex> is_atom Atom
true
iex> is_atom :atom
true
iex> is_atom :my_atom_12
true
```

Hay varios textos que definen un átomo válido como la mezcla de
letras, números, signo de subrayado (_) y arroba (@) como únicos valores
válidos para formar el átomo. Pero de hecho hay bastantes excepciones.
Cualquier operador puede ser un átomo también (:=== es un átomo
válido). El signo de interrogación se permite pero solo como terminador:
:is_binary?.

El módulo Atom provee únicamente un par de funciones para convertir
un átomo a una lista de caracteres con `Atom.to_charlist/1` o una
cadena de texto `Atom.to_string/1`.

## Bolleanos

```
iex> true === :true
true
```

## Valur nulo nil

```
iex> :nil
nil
iex> :nil == nil
true
```

## Números enteros y reales

```
iex> 1 * 2
2
iex> 12_000_500
12000500
iex> 1_000 * 1_000 == 1_000_000
true
```

```
iex> Integer.to_string(1_000)
"1000"
iex> Integer.to_charlist(1_024)
'1024'
iex> Integer.digits 101
[1, 0, 1]
iex> Integer.undigits v(-1)
101
iex> Integer.gcd 10, 15
5
```

```
iex> 0o10
8
iex> 0x10
16
iex> 0b10
2
```
Podemos especificar la base en la que representamos los números
enteros anteponiendo un prefijo específico a cada número escrito. Por
ejemplo para los números hexadecimales anteponemos 0x, para los
números binarios 0b y para los octales el prefijo 0o. Podemos ver algunos
ejemplos a continuación:

```
iex> 0o10
8
iex> 0x10
16
iex> 0b10
2
```
Los números reales se representan en su forma científica si exceden una
cierta dimensión. A la hora de escribirlos podemos optar por escribir
el número completo empleando como separador decimal el punto (.) o
podemos escribirlos de forma científica especificando la base en formato
decimal, la letra e (para indicar exponente en base a 10) y el número del
exponente para la base 10. Escribir 2.0e1 (o 2 por 10 elevado a 1) nos
da como resultado 20.0.

```
iex> Float.to_charlist 0.10
'0.1'
iex> Float.to_string 0.10
"0.1"
iex> Float.floor 0.10
0.0
iex> Float.ceil 0.10
1.0
iex> Float.round 0.10
0.0
iex> Float.round 0.51
1.0
iex> Float.round 0.52
1.0
iex> Float.ratio 0.5
{1, 2}
```

```
iex> Float.parse "0.10"
{0.1, ""}
iex> Float.parse "a1"
:error
iex> Float.parse "1"
{1.0, ""}
```
Si ejecutamos el
siguiente código veremos varias pantallas de números:

```
iex> List.duplicate(2048, 1000) |> Enum.reduce(&(&1 * &2))
213772730161759466399474188010951...
```
En resumen, el código se encarga de repetir mil veces 2048 dentro de
una lista y la reducción se encarga de multiplicar cada elemento por el
siguiente. Es lo mismo que elevar 2048 a 1000. Por pantalla obtenemos
el resultado.

## Variables e inmutabilidad
Las variables son nombres a los que se asigna un valor. Podemos emplear
un nombre que esté compuesto por letras (mayúsculas y/o minúsculas),
números y guion bajo o subrayado (_) aunque con algunas salvedades. No
podemos emplear una letra mayúscula al inicio del nombre ni podemos
emplear ninguna de las palabras reservadas por Elixir.

En el ejemplo inicial definimos una función para calcular el área de un
rectángulo. Si en el intérprete de Elixir definimos un par de variables
conteniendo un número entero cada una y realizamos una operación
aritmética con ellas veremos el resultado:

```
iex> base = 10
10
iex> altura = 5
5
iex> base * altura
50
```

```
iex> a = 10
10
iex> b = a
10
iex> a = 5
5
iex> b
10
```
Descripción del código anterior.

1-> Asignamos a la variable a el valor 10. Elixir lo que hace es
reservar un espacio de memoria para un número entero y
almacena el número 10.
2-> Copiamos la referencia de a a b. En esta ocasión como el dato
no varía de una variable a otra se copia la referencia y ambas
apuntan al mismo espacio de memoria.
3-> Asignamos a la variable a un nuevo espacio de memoria que
contiene el valor 5. El espacio de memoria anterior queda
inmutable. No se modifica. Pero la variable a comienza a
apuntar al nuevo espacio de memoria que contiene 5.
4-> La variable b sigue apuntando al espacio de memoria anterior
y por lo tanto sigue conteniendo 10.

El uso de memoria no suele ser un problema porque cada proceso tiene
su espacio de memoria y cuando una función termina la reserva de
memoria se desecha completamente quedando únicamente los datos
del retorno de la función. Si el lenguaje trabajase con referencias a
otros datos o incluso retornase referencias, no sería seguro realizar esta
limpieza o sería mucho más complicado de realizar.
Por este motivo Elixir puede realizar tareas de tiempo real blando. Al
finalizar la ejecución de una función todas las variables internas se
desechan y son recogidas por el recolector de basura

## Listas

Las listas en Elixir son vectores de información heterogénea, es decir,
pueden contener información de distintos tipos, ya sean números,
átomos, tuplas, estructuras, mapas u otras listas.

```
iex> [ 1, 2, 3, 4, 5 ]
[1,2,3,4,5]
iex> [ 1, "Hola", 5.0, :hola ]
[1,"Hola",5.0,:hola]
```
Podemos realizar modificaciones de estas listas agregando o
sustrayendo elementos con los operadores especiales ++ y -- tal y como
podemos ver en los siguientes ejemplos:

```
iex> [1,2,3] ++ [4]
[1,2,3,4]
iex> [1,2,3] -- [2]
[1,3]
```
Otra ventaja de las listas es la forma en la que podemos ir tomando
elementos de la cabeza de la lista dejando el resto en otra sublista.


```
iex> [cabeza|cola] = [1,2,3,4]
[1,2,3,4]
iex> cabeza
1
iex> cola
[2,3,4]
iex> [cabeza1,cabeza2|cola] = [1,2,3,4]
[1,2,3,4]
iex> cabeza1
1
iex> cabeza2
2
iex> cola
[3,4]
```

De esta forma tan sencilla podemos implementar los algoritmos de
manejo de pilas como son push (empujar a la pila) y pop (extraer de la
pila) de la siguiente forma:

```
iex> lista = []
[]
iex> lista = [1|lista]
[1]
iex> lista = [2|lista]
[2,1]
iex> [extrae|lista] = lista
[2,1]
iex> extrae
2
iex> lista
[1]
```
