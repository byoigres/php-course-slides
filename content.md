# PHP - Framework y carrito de compras

<!-- TOC depth:6 withLinks:1 updateOnSave:1 -->
- [PHP - Framework y carrito de compras](#php-framework-y-carrito-de-compras)
	- [Introducción](#introduccin)
		- [Caracteristicas](#caracteristicas)
		- [Etiquetas](#etiquetas)
			- [Ejemplo](#ejemplo)
	- [Sobre los tipos de datos](#sobre-los-tipos-de-datos)
		- [Booleans](#booleans)
		- [Variables](#variables)
		- [Conversión de string a entero](#conversin-de-string-a-entero)
		- [Casteo de variables.](#casteo-de-variables)
		- [Type Juggling](#type-juggling)
	- [Built-in Web Server](#built-in-web-server)
		- [Ejecutando el servidor integrado](#ejecutando-el-servidor-integrado)
		- [Ruteo de contenido estático](#ruteo-de-contenido-esttico)
		- [Simulando un sitio web](#simulando-un-sitio-web)
<!-- /TOC -->

## Introducción

### Caracteristicas

- PHP es un lenguaje de programación de código abierto del lado del servidor.
- En un inicio PHP representaba <i>Personal Home Page</i>, hoy en dia es el acrónimo recursivo __PHP: Hypertext Preprocessor__.
- PHP puede combinar código de PHP y HTML en un mismo archivo.
- PHP puede ejecutarse en __Windows__, __Linux__ y __OSX__.
- Funciona sobre __Apache__, __NGINX__ e __IIS__.

![Elephpant](/images/php-elephant.png)
![Elephpant letters](/images/php-elephant-letters.png)

### Etiquetas

Cuando PHP parsea un archivo, busca las etiquetas de apertura y cierre que le dicen a PHP donde comenzar y terminar de interpretar el código entre ellas. Todo lo demás fuera de las etiquetas es ignorado por el interprete de PHP.

- &lt;?php y ?&gt;
- &lt;? y ?&gt; conocidas como <i>Short Open Tags</i>
- &lt;?= y ?&gt; para escapar variables

> ¡Nunca utilizes las Short Open Tags!

#### Ejemplo

```php
1.- Hello
<?php
echo " world!";
$variable = "2.- Hello PHP";
?>

<br>

<? echo $variable; ?> <!-- Con short_open_tag habilitado -->

<br>

<?= $variable ?> <!-- Forma abreviada de echo (v5.4+) -->
```

### Variables

- Se declaran anteponiendo el caracter _$_.
- No se requiere la definición explicita de su tipo de dato.

```php
<?php
$variable = 'Hello world';
$numero = 15;
$flotante = 12.5
```

## Sobre los tipos de datos

PHP soporta ocho tipos de datos primitivos.

Cuatro tipos escalares:

- boolean
- integer
- float (floating-point number, también conocido como double)
- string

Dos tipos compuestos:

- array
- object

Y finalmente dos tipos especiales:

- resource
- NULL

[Referencia](http://php.net/manual/en/language.types.intro.php)

### Booleans

Son un tipo de dato simple. Puede ser TRUE o FALSE.

Típicamente el resultado de una operación que retorna un boolean es pasado a una estructura de control.

```php
<?php
// == es un operador que evalua
// igualdad y retorna un boolean.
if ($action == "show_version") {
    echo "The version is 1.23";
}

// esto no es necesario...
if ($show_separators == TRUE) {
    echo "<hr>\n";
}

// ...por que esta manera puede ser usada exactamente con el mismo significado:
if ($show_separators) {
    echo "<hr>\n";
}
?>
```

Podemos expresar  __FALSE__ de las siguientes maneras:

- El boolean FALSE.
- El valor entero 0.
- El valor flotante 0.0.
- Una cadena de texto vacia o el string "0" (cero).
- Un arreglo con cero elementos.
- El tipo especial NULL (incluyendo variables sin asignar).
- Objetos SimpleXML creados con tags vacias.

Cualquier otro valor es considerado __TRUE__ (incluyendo resources)

```php
<?php
var_dump((bool) "");        // bool(false)
var_dump((bool) 1);         // bool(true)
var_dump((bool) -2);        // bool(true)
var_dump((bool) "foo");     // bool(true)
var_dump((bool) 2.3e5);     // bool(true)
var_dump((bool) array(12)); // bool(true)
var_dump((bool) array());   // bool(false)
var_dump((bool) "false");   // bool(true)
```

### Strings

Una cadena de texto puede ser expesada de 4 maneras diferentes:

- Comillas simples
- Comillas dobles
- Sintaxis Heredoc
- Sintaxis Newdoc (desde PHP 5.3.0)

#### Comillas simples

La manera mas simple de especificar un string en utilizando comillas simples.

Para especificar una literarl de comilla simple dentro de la cadena de texto
podemos escaparla con un backslash (\\). Para especificar una literal backslash
simplemente se colocan dos (\\\\). Todas las demás literales expresadas con
backslash serán tratadas como backslash: esto significa que todas las demás
secuencias que se especifiquen como \\n o \\r darán como salida el texto a como
se especifica y no con algún significado especial.

```php
<?php
echo 'Esta es una cadena simple';

echo 'También puedes tener saltos de linea en
las cadenas, esta es una manera correcta
de hacerlo';

echo 'Una vez dijo Terminator: I\'ll be back';
// Imprime: Una vez dijo Terminator: I'll be back

echo 'Eliminar C:\\*.*?';
// Imprime: Eliminar C:\*.*?

echo 'Borraste C:\*.*?';
// Imprime: Borraste C:\*.*?

echo 'Esto no genera una: \n nueva línea';
// Imprime: Esto no genera una: \n nueva línea

echo 'Las variables no se $interpretan $tampoco';
// Imprime: Las variables no se $interpretan $tampoco
```

#### Comillas dobles

Si la cadena de texto se encuentra con comillas dobles, PHP interpretará mas
secuencias de escape para caracteres especiales como `\n`, `\r`, `\t` o `\$`.
Además de poder escapar variables dentro de la cadena.

```php
<?php
$texto = "mundo!";
echo "Hola $texto";
// Imprime: Hola mundo!

```

Mas adelante ver otras maneras de escapar variables.


#### Sintaxis Heredoc

Una tercera manera de delimitar una cadena de texto es con esta sintaxis: Se inicia con los caracteres `<<<` seguidos de un identificador mas un salto de línea. Luego se procede con el contenido de la cadena de texto como tal. Para cerrar la cadena de texto esta debe estar en la primera columna de la linea y con el identificador inicial mas un punto y coma.

```php
<?php
class foo {
	public $bar = <<<EOT
bar
    EOT;
}
```

#### Sintaxis Newdoc

Aligual que la sintaxis Heredoc, Newdoc funciona de la misma manera solo tomando en cuenta de que Nowdoc es como las comillas simples, no es posible escapar variables.

La sintaxis Heredoc se comporta como una cadena en comillas dobles, puedes escapar variables

[Referencia](http://php.net/manual/en/language.types.string.php)

### Conversión de string a entero

Cuando una cadena de texto es evaluada en un contexto de entero, el valor resultante y el tipo de dato son determinados de la siguiente manera:

Si la cadena de texto no contiene ninguno de los caracteres ',', 'e' o 'E' y el valor numérico __encaja__ en los limites del tipo numérico, la cadena de texto será evaluada como un entero. En cualquier otro caso será evaluada como flotante.

El valor es dado por la porción inicial de la cadena de texto. Si la cadena comienza con un dato numérico válido, este es el valor que será utilizado. De otra manera, el valor será 0 (cero).

```php
<?php
$foo = 1 + "10.5";                // $foo es float (11.5)
$foo = 1 + "-1.3e3";              // $foo es float (-1299)
$foo = 1 + "bob-1.3e3";           // $foo es integer (1)
$foo = 1 + "bob3";                // $foo es integer (1)
$foo = 1 + "10 Small Pigs";       // $foo es integer (11)
$foo = 4 + "10.2 Little Piggies"; // $foo es float (14.2)
$foo = "10.0 pigs " + 1;          // $foo es float (11)
$foo = "10.0 pigs " + 1.0;        // $foo es float (11)
```

[Referencia](http://php.net/manual/en/language.types.string.php#language.types.string.conversion)

### Casteo de variables.

El casteo de variables en PHP funciona de manera similar a C, el nombre del tipo de dato a castear se coloca dentro de un par de parentesis antes de la variable a ser casteada.

Los tipos de casteos permitidos son:

- **(int)**, **(integer)** - castea a integer
- **(bool)**, **(boolean)** - castea a boolean
- **(float)**, **(double)**, **(real)** - castea a float
- **(string)** - castea a string
- **(array)** - castea a array
- **(object)** - castea a object
- **(unset)** - castea a NULL (PHP 5)


### Arreglos

Un arreglo en PHP es un mapa ordenado. Un mapa es un tipo que asocia llaves y valores. Este tipo de dato está optimizado para diferentes usuarios ya que puede ser utilizado como un arreglo, una lista, un hash table, un diccionario, una colección, una cola y probablemente muchos mas. Los valores pueden ser otros arreglos, inclusive, arreglos multidimencionales.

Los arreglos pueden crearse mediante la palabra reservada `array` o utilizando `[]` en la versión de PHP 5.4+.

```php
<?php
$arreglo = array(
	"foo" => "bar",
	"bar" => "foo"
);

// PHP 5.4+
$arreglo = [
	"foo" => "bar",
	"bar" => "foo"
];

```

#### Keys, keys, key!

Adicionalmente ocurren los siguientes casteos con las llaves:

- Cadenas de texto conteniendo enteros validos serán casteados al tipo entero.
Por ejemplo, la llave `"8"` será interpretada como `8`. Por otro lado, la llave
`"08"` no será casteada.
- Las llaves float también serán casteadas a enteros, lo que significa que la
parte fraccional será truncada. Por ejemplo, la llave `8.7` en realidad será `8`.
- Boleanos también son convertidos a enteros, `True` es `1` y `False` es `0`.
- `Null` será una cadena de texto vacia.
- **No se pueden utilizar arreglos u objetos como llaves**, esto lanzará un `warning: Illegal offset type`.

Si multiples elementos en el arreglo se declaran con la misma llave, solamente
el último elemento con esa llave será usado ya que los demás elementos serán sobreescritos.

```php
<?php
$data = [
	"8"=>"String to Integer",
	"08" => "String",
	9.7 => "Float to Integer",
	true => "True is Integer",
	null => "Null is empty string"
];

array(5) {
  [8] => string(17) "String to Integer"
  ["08"] => string(6) "String"
  [9] => string(16) "Float to Integer"
  [1] => string(15) "True is Integer"
  [""] => string(20) "Null is empty string"
}
```

Podemos crear un arreglo sin especificar la llave, la cual se agregará de manera
incremental iniciando con el indice 0:

```php
<?php

$data = array("foo", "bar", "baz", "zab");

array(4) {
  [0] => string(3) "foo"
  [1] => string(3) "bar"
  [2] => string(5) "baz"
  [3] => string(5) "zab"
}
```

Podemos especificar llave solo para algunos elementos:

```php
<?php
$array = array(
         "a",
         "b",
    6 => "c",
         "d",
);

array(4) {
  [0] => string(1) "a"
  [1] => string(1) "b"
  [6] => string(1) "c"
  [7] => string(1) "d"
}
```

### Type Juggling

El tipo de dato de la variable es determinado al momento de su asignación, es decir, si a la variable `$var` le asignamos una cadena de texto la variable el tipo será string, si asignamos un entero tl tipo será entero.

```php
<?php
$foo = "0";  // $foo es string
$foo += 2;   // $foo es ahora un entero (2)
$foo = $foo + 1.3;  // $foo es ahora un flotante (3.3)
$foo = 5 + "10 Little Piggies"; // $foo es entero (15)
$foo = 5 + "10 Small Pigs";     // $foo es entero (15)
```

[Type Juggling]: http://php.net/manual/en/language.types.type-juggling.php



## Built-in Web Server

### Ejecutando el servidor integrado

```shell
// Linux
$ cd my_awesome_project
$ php -S localhost:8080
```

```shell
// Windows
> cd my_awesome_project
> c:\xampp\php\php.exe -S localhost:8080
```

```shell
// Linux
$ php -S localhost:8080 -t /home/sergio/projects/my_awesome_project
```

```shell
// Windows
> php.exe -S localhost:8080 -t c:\projects/my_awesome_project
```

### Ruteo de contenido estático

Para utilizar un script de ruteo en el desarrollo con el CLI Web Server que sea funcional en producción podemos utilizar la funcion php_sapi_name() que nos regresa el tipo de interfaz en la que se está ejecutando PHP.

```php
<?php
// router.php
if (php_sapi_name() == 'cli-server') {
    /* rutear contenido estático y retornar false */
}
/* continuar con el flujo normal del archivo .php */
?>
```

### Simulando un sitio web

Con ayuda de los archivos host y el servidor integrado tanto en linux como en windows podemos simular el estár trabajando con una página .com.

```
// C:\Windows\System32\drivers\etc\host

// localhost name resolution is handled within DNS itself.
127.0.0.1       localhost
127.0.0.1       mipagina.com
```


```shell
> php.exe -S mipagina.com:80 -t C:\mipagina.com
```
