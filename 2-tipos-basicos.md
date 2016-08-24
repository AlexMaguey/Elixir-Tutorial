#Tipos Básicos

En éste capítulo aprenderemos más acerca de los tipos básicos de Elixir: enteros, flotantes, booleanos, átomos, cadenas, listas y tuplas. Algunos tipos básicos son:

```
iex> 1          # entero
iex> 0x1F       # entero
iex> 1.0        # flotante
iex> true       # booleano
iex> :atom      # átomo
iex> "elixir"   # cadena
iex> [1, 2, 3]  # lista
iex> {1, 2, 3}  # tupla
```

##Aritmética básica

Abre `iex` y escribe las siguientes expresiones:

```
iex> 1 + 2
3
iex> 5 * 5
25
iex> 10 / 2
5.0
```

Nota que `10 / 2` regresa un flotante `5.0` en lugar de un entero `5`. Ésto es esperado. En Elixir, el operador `/` siempre regresa un flotante. Si quieres hacer una división entera u obtener el resto de la división, puedes llamar a las funciones `div` y `rem`:

```
iex> div(10, 2)
5
iex> div 10, 2
5
iex> rem 10, 3
1
```

Nota que los paréntesis no son requeridos para llamar a la función.

Elixir también soporta notaciones para ingresar números binarios, octales y hexadecimales:

```
iex> 0b1010
10
iex> 0o777
511
iex> 0x1F
31
```

Los números flotantes requieren un punto seguido de al menos un dígito y también soportan `e` por el número de exponente:

```
iex> 1.0
1.0
iex> 1.0e-10
1.0e-10
```

Los flotantes en Elixir tienen una precisión doble de 64 bits.

Puedes llamar a la función `round` para obtener el entero más cercano al número flotante dado, o la función `trunc` para obner la parte entera de un flotante:

```
iex> round(3.58)
4
iex> trunc(3.58)
3
```

##Booleanos

Elixir soporta `true` y `false` como booleanos:

```
iex> true
true
iex> true == false
false
```

Elixir provee un montón de funciones base para checar el tipo de un valor. Por ejemplo, la función `is_boolean/1` puede ser usada para checar si un valor es booleano o no:

>Nota: Las funciones en Elixir son identificadas por un nombre y un número de argumentos. Por lo tanto `is_boolean/1` identifica a una función llamada `is_boolean` que toma un argumento. `is_boolean/2` identifica una función diferente (no existente) con el mismo nombre pero diferente aridad.

```
iex> is_boolean(true)
true
iex> is_boolean(1)
false
```

También puedes usar `ìs_integer/1`, `is_float/1` o `is_number/1` para verificar, respectivamente, si el argumento es un entero, un flotante o ambos.

>Nota: En cualquier momento puedes escribir `h` en el shell para imprimir información de cómo usar el shell. El ayudante `h` también puede ser usado para accesar a la documentación de cualquier función.
>Por ejemplo, escribir `h is_integer/1` va a imprimir la documentación para la función `is_integer/1`. También funciona con operadores y otros constructores (prueba `h ==/2`).

## Átomos

Los átomos son constantes donde su nombre es su único valor. Algunos otros lenguajes los llaman símbolos.

```
iex> :hola
:hola
iex> :hola == :mundo
false
```

Los booleanos `true` y `false` son, de hecho, átomos:

```
iex> true == :true
true
iex> is_atom(false)
true
iex> is_boolean(:false)
true
```

##Cadenas

Las cadenas en Elixir son insertadas entre comillas dobles, y están codificadas en UTF-8:

```
iex> "höla"
"höla"
```

>Nota: si estás corriendo en Windows, hay una probabilidad de que tu terminal no use UTF-8 por defecto. Puedes cambiar la codificación de tu sesión actual corriendo `chcp 65001` antes de entrar a IEx.

Elixir también soporta interpolación de cadenas:

```
iex> "höla #{:mundo}"
"höla mundo"
```

Las cadenas pueden tener saltos de línea en ellas. Puedes introducirlas usando secuencias de escapado:

```
iex> "hola
...> mundo"
"hola\nmundo"
iex> "hola\nmundo"
"hola\nmundo"
```

Puedes imprimir una cadena usando la función `IO.puts/1` del módulo `IO`:

```
iex> IO.puts "hola\nmundo"
hola
mundo
:ok
```

Nota que la función `IO.puts/1` regresa el átomo `:ok` como resultado después de imprimir.

Las cadenas en Elixir son representadas internamente por binarios que son secuencias de bytes:

```
iex> is_binary("höla")
true
```

También puedes obtener el número de bytes en una cadena:

```
iex> byte_size("höla")
5
```

Nota que el número de bytes en la cadena es 5, a pesar de que tiene 4 caracteres. Eso es porque el caracter “ö” toma 2 bytes para ser representado en UTF-8. Podemos obtener la longitud de la cadena, basado en el número de caracteres, usando la función `String.length/1`:

```
iex> String.length("höla")
4
```

El [módulo String](http://elixir-lang.org/docs/stable/elixir/String.html) contiene un montón de funciones para usar cadenas como está definido en el estándar Unicode:

```
iex> String.upcase("höla")
"HÖLA"
```

##Funciones anónimas

Las funciones están delimitadas por las palabras reservadas `fn` y `end`:

```
iex> agregar = fn a, b -> a + b end
#Function<12.71889879/2 in :erl_eval.expr/5>
iex> is_function(agregar)
true
iex> is_function(agregar, 2)
true
iex> is_function(agregar, 1)
false
iex> agregar.(1, 2)
3
```

Las funciones son "ciudadanos de primera clase" en Elixir, lo que significa que pueden ser pasadas como argumentos a otras funciones así como los enteros o las cadenas pueden. En el ejemplo, pasamos la función en la variable `agregar` a la función `is_function/1` la cual regresó correctamente `true`. Tambien podemos checar la aridad de la función llamando `is_function/2`.

Nota que un punto (`.`) entre la variable y el paréntesis es requerido para llamar a una función anónima.

Las funciones anónimas son cierres (closures) y como tales pueden acceder a variables que están en el ámbito donde la función es definida. Definamos una nueva función anónima que use la funcion anónima `agregar` que previamente definimos:

```
iex> doble = fn a -> agregar.(a, a) end
#Function<6.71889879/1 in :erl_eval.expr/5>
iex> doble.(2)
4
```

Ten en cuenta que una variable asignada dentro de una función no afecta el ambiente que le rodea:

```
iex> x = 42
42
iex> (fn -> x = 0 end).()
0
iex> x
42
```

La sintaxis de captura `&()` también puede ser usada para crear funciones anónimas. Éste tipo de sintaxis será discutido en el [Capítulo 9](https://github.com/AlexMaguey/Elixir-Tutorial/blob/master/8-algo.md)

##Listas (Enlazadas)

Elixir usa corchetes para especificar una lista de valores. Los valores pueden ser de cualquier tipo:

```
iex> [1, 2, true, 3]
[1, 2, true, 3]
iex> length [1, 2, 3]
3
```

Dos listas pueden ser concatenadas y sustraídas usando los operadores `++/2` y `--/2`:

```
iex> [1, 2, 3] ++ [4, 5, 6]
[1, 2, 3, 4, 5, 6]
iex> [1, true, 2, false, 3, true] -- [true, false]
[1, 2, 3, true]
```

A lo largo del tutorial, hablaremos mucho acerca de la cabeza y la cola de una lista. La cabeza es el primer elemento de una lista y la cola es el sobrande de la lista. Pueden ser obtenidos con las funciones `hd/1` y `tl/1`. Asignemos una lista a una variable i obtengamos su cabeza y su cola:

```
iex> lista = [1, 2, 3]
iex> hd(lista)
1
iex> tl(lista)
[2, 3]
```

Obtener la cabeza o la cola de una lista vacía es un error:

```
iex> hd []
** (ArgumentError) argument error
```

A veces crearás una lista y ésta regresará un valor en comillas simples. Por ejemplo: 

```
iex> [11, 12, 13]
'\v\f\r'
iex> [104, 101, 108, 108, 111]
'hello'
```

Cuando Elixir ve una lista de números ASCII imprimibles, Elixir la imprimirá como una lista de chars (literal una lista de caracteres). Las listas de Chars son bastante comunes cuando te interconectas con código Erlang. Cuando veas un valor en IEx y no estes seguro que es, puedes usar la función `i/1` para obtener información acerca de el:

```
iex> i 'hello'
Term
  'hello'
Data type
  List
Description
  ...
Raw representation
  [104, 101, 108, 108, 111]
Reference modules
  List
```

Ten en mente que las representaciones de comillas simples y comillas dobles no son equivalentes en Elixir ya que son representadas por diferentes tipos:

```
iex> 'hola' == "hola"
false
```

Las comillas simples son listas de caracteres, las comillas dobles son cadenas. Hablaremos más acerca de ellas en el capítulo ["Binarios, cadenas y listas de caracteres"(https://github.com/AlexMaguey/Elixir-Tutorial/blob/master/algo.md).

##Tuplas

Elixir usa llaves para definir tuplas. Como las listas, las tuplas pueden guardar cualquier valor:

```
iex> {:ok, "hola"}
{:ok, "hola"}
iex> tuple_size {:ok, "hola"}
2
```

Las tuplas almacenan elementos contiguamente en memoria. Ésto significa que acceder a un elemento de una tupla por su índice u obtener el tamaño de la tupla es una operación rápida. Los índices empiezan desde cero:

```
iex> tupla = {:ok, "hola"}
{:ok, "hola"}
iex> elem(tupla, 1)
"hola"
iex> tuple_size(tupla)
2
```

También es posible poner un elemento en un índice particular de una tupla con la función `put_elem/3`:

```
iex> tupla = {:ok, "hola"}
{:ok, "hola"}
iex> put_elem(tupla, 1, "mundo")
{:ok, "mundo"}
iex> tupla
{:ok, "hola"}
```

Nota que `put_elem/3` regresó una nueva tupla. La tupla original almacenada en la variable `tupla` no fue modificada porque los tipos de datos en Elixir son inmutables. Siendo inmutable, el código Elixir es más fácil de razonar ya que nunca te tienes que preocupar si un código en particular está mutando tu estructura de datos en su lugar.

##¿Listas o tuplas?

¿Cuál es la diferencia entre listas y tuplas?

Las listas son almacenades en memoria como listas enlazadas, lo que significa que cada elemento en la lista guarda su valor y apunta al siguiente elemento hasta que el final de la lista es alcanzado. Llamamos a cada par de valor y apuntador un **cons cell**:

```
iex> lista = [1 | [2 | [3 | []]]]
[1, 2, 3]
```

Esto significa que acceder al tamaño da la lista es una operación lineal: necesitamos atravesar la lista entera con el fin de averiguar su tamaño. Actualizar una lista es rápido siempre y cuando antepongamos los elementos:

```
iex> [0 | lista]
[0, 1, 2, 3]
```

Las tuplas, por otra parte, son almacenadas contiguamente en memoria. Ésto significa que obtener el tamaño de la tupla o accesar a un elemento por su índice es rápido. Sin embargo, actualizar o agregar elementos a tuplas es caro porque requiere copiar la tupla entera en memoria.

Esas características de rendimiento dictan el uso de esas estructuras de datos. Un cuso muy común de las tuplas es usarlas para devolver información extra de una función. Por ejemplo, `File.read/1` es una función que puede ser usada para leer el contenido de un archivo y regresar tuplas:

```
iex> File.read("ruta/a/archivo/existente")
{:ok, "... contenido ..."}
iex> File.read("ruta/a/archivo/desconocido")
{:error, :enoent}
```

Si la ruta dada a `File.read/1` existe, regresa una tupla con el átomo `:ok` como el primer elemento y el contenido del archivo como el segundo elemento. De otra manera, regresa una tupla con `:error` y la descripción del error.

La mayor parte del tiempo, Elixir va a guiarte para que hagas las cosas correctas. Por ejemplo, hay una función `elem/2` para acceder a un elemento de una tupla pero no hay una función equivalente para listas:

```
iex> tupla = {:ok, "hola"}
{:ok, "hola"}
iex> elem(tupla, 1)
"hola"
```

Cuando "cuenta" el número de elementos en una estructura de datos, Elixir también se atiene a una simple regla: la función es llamada `size` si la operación es realizada en tiempo constante (es decir, el valor es precalculado) o `length` si la operación es lineal (es decir, calcular la longitud se vuelve lento conforme la entrada crece).

Por ejemplo, hemos usado 4 funciones para contar hasta ahora: `byte_size/1` (para el número de bytes en una cadena), `tuple_size/1` (para el tamaño de una tupla), `length/1` (para la longitud de una lista) y `String.length/1` (para el número de grafemas en una cadena). Dicho eso, usamos `byte_size` para obtener el número de bytes en una cadena, lo cual es barato, pero obtener el número de caracteres unicode usa `String.length`, el cual puede ser caro ya que la cadena entera tiene que ser recorrida.

Elixir tambien provee `Port`, `Reference` y `PID` como tipos de datos (usualmente usados en procesos de comunicación), y echaremos un vistazo a ellos cuando hablemos de procesos. Por ahora, veamos acerca de los operadores básicos que vienen con nuestros tipos básicos.
