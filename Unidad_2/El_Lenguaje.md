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




