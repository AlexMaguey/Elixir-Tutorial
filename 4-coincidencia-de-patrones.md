#Coincidencia de patrones

En este capítulo, mostraremos como el operador `=` en Elixir es un operador de coincidencia y como usarlo para coincidir patrones dentro de estructuras de datos. Finalmente, aprenderemos acerca del operador pin `^` usado para accesar a valores previamente ligados.

#El operador de coincidencia

Hemos usado el operador `=` un par de veces para asignar variables en Elixir:
```
iex> x = 1
1
iex> x
1
```

En Elixir, el operador `=` es llamado *el operador de coincidencia*. Veamos porque:

```
iex> 1 = x
1
iex> 2 = x
** (MatchError) no match of right hand side value: 1
```

Nota que `1 = x` es una expresión válida, y coincidio porque tanto como el lado derecho como el lado izquierdo eran igual a 1. Cuando los lados no coincide, se produce un `MatchError`.

Una variable sólo puede ser asignada en el lado izquierdo de `=`:

```
iex> 1 = desconocido
** (CompileError) iex:1: undefined function desconocido/0
```

Debido a que no hay una variable `desconocido` previamente definida, Elixir imagina que trataste de llamar a una función llamada `desconocido/0`, pero tal función no existe.

#Coincidencia de patrones

El operador de coincidencia no solo es usado para hacer coincidir valores simples, también es útil para desestructurar tipos de datos más complejos. Por ejemplo podemos coincidir patrones en tuplas:

```
iex> {a, b, c} = {:hola, "mundo", 42}
{:hola, "mundo", 42}
iex> a
:hola
iex> b
"mundo"
```

Una coincidencia de patrones fallará en el caso de que los lados no puedan coincidir. Por ejemplo, el caso cuando las tuplas tienen diferentes tamaños:

```
iex> {a, b, c} = {:hola, "mundo"}
** (MatchError) no match of right hand side value: {:hola, "mundo"}
```

Y también cuando se comparan diferentes tipos de datos:

```
iex> {a, b, c} = [:hola, "mundo", 42]
** (MatchError) no match of right hand side value: [:hola, "mundo", 42]
```

Curiosamente, podemos coincidir valores específicos. El ejemplo debajo afirma que el lado izquierdo sólo coincidirá con el lado derecho cuando el lado derecho es una tupla que empieza con el átomo `:ok`:

```
iex> {:ok, resultado} = {:ok, 13}
{:ok, 13}
iex> resultado
13

iex> {:ok, resultado} = {:error, :oops}
** (MatchError) no match of right hand side value: {:error, :oops}
```

Podemos coincidir patrones en listas:

```
iex> [a, b, c] = [1, 2, 3]
[1, 2, 3]
iex> a
1
```

Una lista tambipen soporta coincidencias en su cabeza y cola:

```
iex> [cabeza | cola] = [1, 2, 3]
[1, 2, 3]
iex> cabeza
1
iex> cola
[2, 3]
```

Similarmente a las funciones `hd/1` y `tl/1`, no podemos coincidir una lista vacía con un patrón de cola y cabeza:

```
iex> [cabeza | cola] = []
** (MatchError) no match of right hand side value: []
```

El formato `[cabeza | cola] no sólo es usado para coincidencia de patrones, también es usado para anteponer elementos a una lista:

```
iex> lista = [1, 2, 3]
[1, 2, 3]
iex> [0 | lista]
[0, 1, 2, 3]
```

La coincidencia de patrones le permite a los desarrolladores fácilmente desestructurar tipos de datos tales como tuplas y listas. Como veremos en los siguientes capítulos, es uno de los cimientos de la recursión en Elixir y aplica a otros tipos también, como mapas y binarios.

#El operador pin

Las variables en Elixir pueden ser reasignadas:

```
iex> x = 1
1
iex> x = 2
2
```

El operador pin `^` debe ser usado cuando quieres coincidir patrones contra el valor de una variable existente en vez de reasignar la variable:

```
iex> x = 1
1
iex> ^x = 2
** (MatchError) no match of right hand side value: 2
iex> {y, ^x} = {2, 1}
{2, 1}
iex> y
2
iex> {y, ^x} = {2, 2}
** (MatchError) no match of right hand side value: {2, 2}
```

Porque hemos asignado el valor de 1 a la variable x, éste último ejemplo también pudo ser escrito como:

```
iex> {y, 1} = {2, 2}
** (MatchError) no match of right hand side value: {2, 2}
```

Si una variable es mencionada más de una vez en un patrón, todas las referencias deben de enlazar al mismo patrón:

```
iex> {x, x} = {1, 1}
{1, 1}
iex> {x, x} = {1, 2}
** (MatchError) no match of right hand side value: {1, 2}
```

En algunos casos, no te importa un valor en particular en un patrón. Es una práctica común enlazar esos valores a un guión bajo, `_`. Por ejemplo, si sólo la cabeza de la lista nos importa, podemos asignar a la cola un guión bajo:

```
iex> [cabeza | _] = [1, 2, 3]
[1, 2, 3]
iex> cabeza
1
```

La variable `_` es especial porque nunca puede ser leída. Al tratar de leerla da un error de variable no asignada:

```
iex> _
** (CompileError) iex:1: unbound variable _
```

Aunque la coincidencia de patrones nos permite hacer poderosas construcciones, su uso es limitado. Por ejemplo, no puedes hacer llamados a funciones en el lado izquierdo de una coincidencia. El siguiente ejemplo es inválido:

```
iex> length([1, [2], 3]) = 3
** (CompileError) iex:1: illegal pattern
```

Con esto terminamos nuestra introducción a las coincidencias de patrones. Como veremos en el siguiente capítulo, la coincidencia de patrones es muy común en muchas de las construcciones del lenguaje.

