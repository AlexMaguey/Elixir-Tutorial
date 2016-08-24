En el [capítulo anterior](https://github.com/AlexMaguey/Elixir-Tutorial/blob/master/2-tipos-basicos.md), vimos que Elixir provee `+`, `-`, `*`, `/` como operadores aritméticos, más las funciones `div/2` y `rem/2` para la división entera y el resto.

Elixir también provee `++` y `--` para manipular listas:

```
iex> [1, 2, 3] ++ [4, 5, 6]
[1, 2, 3, 4, 5, 6]
iex> [1, 2, 3] -- [2]
[1, 3]
```
La concatenación de cadenas es realizada con `<>`:

```
iex> "foo" <> "bar"
"foobar"
```

Elixir también provee tres operadores booleanos: `or`,  `and` y `not`. Éstos operadores son estrictos en el sentido de que esperan un booleano (`verdadero` o `falso`) como primer argumento: 

```
iex> true and true
true
iex> false or is_atom(:ejemplo)
true
```

Proveer un no-booleano mandará una excepción:

```
iex> 1 and true
** (ArgumentError) argument error: 1
```

`or` y `and` son operadores de cortocircuito. Solamente se ejecuta el lado derecho si el lado izquierdo no es suficiente para determinar el resultado:

```
iex> false and raise("This error will never be raised")
false
iex> true or raise("This error will never be raised")
true
```

>Nota: Si eres un desarrollador  Erlang, `and`y `or` en elixir son equivalentes a los operadores `andalso` y `orelse` en Erlang

Además de estos operadores booleanos, Elixir también provee `||`, `&&` y `!` los cuales aceptan argumentos de cualquier tipo. Para estos operadores, todos los valores excepto `false` y `nil` evaluarán verdadero:

```
# or
iex> 1 || true
1
iex> false || 11
11

# and
iex> nil && 13
nil
iex> true && 17
17

# !
iex> !true
false
iex> !1
false
iex> !nil
true
```

Como regla de oro, usa `and`, `or` y `not` cuando estés esperando booleanos. Si cualquiera de los argumentos es no booleano, usa `&&`, `||` y `!`.

Elixir también provee `==`, `!=`, `===`, `!==`, `<=`, `>=`, `<` y `>` como operadores de comparación:

```
iex> 1 == 1
true
iex> 1 != 2
true
iex> 1 < 2
true
```

La diferencia entre `==` y `===` es que el último es más estricto al comparar enteros y flotantes:

```
iex> 1 == 1.0
true
iex> 1 === 1.0
false
```

En Elixir, podemos comparar dos diferentes tipos de datos:

```
iex> 1 < :atom
true
```

La razón de que podamos comparar tipos de datos diferentes es pragmatismo. Los algoritmos de ordenamiento no necesitan preocuparse acerca de diferentes tipos de datos a fin de ordenar. El orden de ordenamiento esta definido abajo:

```
number < atom < reference < functions < port < pid < tuple < maps < list < bitstring
```

No es necesario memorizar el orden, pero es importante saber que un orden existe.

En el siguiente capítulo, vamos a discutir algunas funciones básicas, conversión entre tipos de datos y un poco de flujos de control.
