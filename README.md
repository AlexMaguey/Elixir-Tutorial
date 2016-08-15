#Introducción
¡Bienvenido!

En este tutorial vamos a enseñarte las bases de Elixir, la sintaxis del lenguaje, cómo definir módulos, cómo manipular las características de estructuras de datos comunes y más. Éste capítulo se enfocará en asegurar que Elixir esté instalado y de que puedas correr exitosamente el Shell Interactivo de Elixir, llamado IEx.

Nuestros requerimientos son:
* Elixir - Versión 1.2.0 en adelante
* Erlang - Version 18.0 en adelante

¡Empecemos!

##Instalación
Si aún no has instalado Elixir, corre a nuestra [página de instalación](https://github.com/alexmaguey). Una vez que termines, puedes correr `elixir -v` para obtener la versión de Elixir actual.

##Modo interactivo

Cuando instalas Elixir, tendrás tres ejecutables nuevos `iex`, `elixir` y `elixirc`. Si compilaste Elixir desde la fuente o estas usando una versión empaquetada, puedes encontrar estos dentro del directorio `bin`.

Por ahora, empecemos corriendo `iex` (o `iex.bat` si estas en Windows) que significa Interactive Elixir. En el modo interactivo podemos escribir cualquier expresión de Elixir y obtener su resultado. Calentemos con algunas expresiones básicas.

Abre `iex`y escribe las siguientes expresiones.

```
Interactive Elixir - press Ctrl+C to exit (type h() ENTER for help)

iex> 40 + 2
42
iex> "hola" <> " mundo"
"hola mundo"
```

¡Parece que estamos listos para seguir! Usaremos el shell interactivo bastante en los capítulos siguientes para familiarizarnos un poco más con las expresiones del lenguaje y los tipos básicos, comenzando en el siguiente capítulo.

>Nota: si estas en Windows, también puedes intentar `iex.bat --werl` el cual puede proveer una mejor experiencia dependiendo de la consola que estés usando.

##Corriendo scripts

Después de familiarizarnos con lo básico del lenguaje puede ser que quieras intentar escribir programas simples. Esto puede ser logrado poniendo el código siguiente en un archivo:

```elixir
IO.puts "Hola mundo Elixir"
```

Sálvalo como `simple.exs` y ejecútalo con `elixir`:

```
$ elixir simple.exs
Hola mundo Elixir
```
Después aprenderemos cómo compilar código Elixir el Mix build tool. Por ahora, movámonos al [Capítulo 2](https//:github.com/alexmaguey).
