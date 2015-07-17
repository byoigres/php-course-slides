[TOC]

# Introducción

# PHP

## ¿Qué es PHP?

**PHP** es un lenguaje de programación de código abierto del lado del servidor. En un inicio PHP representaba __Personal Home Page__, hoy en día es el acrónimo recursivo __PHP: Hypertext Preprocessor__. PHP puede combinar código de PHP y HTML en un mismo archivo.

## Logotipo

El logotipo de PHP es el siguiente

![PHP logo](/images/php_logo_large.png)

Y con la llegada de PHP7 el logotipo pasó a tomar un estilo mas actual.

![Logo de PHP7](/images/php7_logo_large.png)

## ElePHPant

PHP tiene un elefante como mascota de nombre **ElePHPant** que fue creado por allá del año de 1998 por un francés de nombre **Vincent Pontier**, él mismo es quien diseñó el logotipo de PHP7 y es curioso como el elefante salio de visualizar las letras PHP desde cierto ángulo.

![ElePHPant](/images/php-elephant.png)
![Letras que forman el ElePHPant](/images/php-elephant-letters.png)
![](http://)

# Referencia del lenguaje

## Archivos PHP

Generalmente PHP utiliza la extensión __.php__ para representar a sus archivos pero ciertas veces suelen utilizarse las extensiones __.inc__ para archivos que serán incluidos y __.class.php__ para archivos de clase. Eso es por conveniencia de quien los utiliza pero no es regla, aunque lo más común seria utilizar la extensión __.php__.

## Etiquetas de PHP

Cuando PHP analiza un archivo, busca las etiquetas de apertura y cierre que le dicen a PHP donde comenzar y terminar de interpretar el código PHP entre ellas. Todo lo demás fuera de las etiquetas es ignorado por el interprete de PHP.

Las etiquetas de apertura y cierre de PHP son `<?php` y `?>` respectivamente. Además PHP permite el uso de las __short open tags__ `<?`las cuales se desaconseja utilizar ya que solo están disponibles si se habilita la opción __short open tag__ desde el archivo de configuración php.ini.

> ¡Por convención nunca utilices las Short Open Tags!

## Escapando código desde HTML

Todo fuera de las etiquetas de apertura y cierre de PHP es ignorado por el interprete de PHP el cual permite tener contenido mixto. Esto permite a PHP ser embedido en documentos HTML, por ejemplo, para crear una plantilla.

```php
<p>Esto será ignorado por el interprete de PHP y será desplegado en el navegador.</p>
<?php echo 'Mientras que esto será interpretado por PHP.'; ?>
<p>Esto también será ignorado por PHP y desplegado por el navegador.</p>
```

### Short Echo Tags

Si necesitamos mandar como salida algún texto almacenado en una variable podemos realizarlo de la siguiente manera:

```php
<?php echo $variable; ?>
```

Pero a partir de la versión __5.4__ de PHP se pueden utilizar las __Short Echo Tags__ para mandar como salida valores de variables de una manera un poco mas cómoda.

```php
<?= $variable =>
```

> Tome en cuenta que dentro de las __short echo tags__ no es posible realizar ninguna operación de cualquier tipo que no sea utilizar una variable para mandar su contenido como salida.


### Utilizando estructuras con condiciones

En el siguiente ejemplo PHP se saltará los bloques donde la condición no se cumpla, inclusive si los bloques se encuentran fuera de las etiquetas de apertura y cierre de PHP.

```php
<?php if ($expression == true): ?>
  Esto se mostrará si la expresión es verdadera.
<?php else: ?>
  De otro modo esto será mostrado.
<?php endif; ?>
```

Para desplegar como salida grandes cantidades de texto es mas eficiente realizarlo fuera de cualquier bloque de análisis de código del interprete de PHP que hacerlo mediante una instrucción `echo` o `print`.

## Separador de instrucciones

Así como en __C__ o __Perl__, PHP requiere que las instrucciones sean terminadas con un __punto y coma__ al final de cada sentencia. La etiqueta de cierre de un bloque de código de PHP automáticamente implica un punto y coma; no necesitas tener un punto y coma para terminar la última línea de un bloque código de PHP cuando exista una etiqueta de cierre. La etiqueta de cierre de un bloque puede omitirse cuando se halla alcanzado el final del archivo y será necesario colocar un punto y coma para terminar la expresión.

```php
<?php
echo 'Esta es una prueba';
?>

<?php echo 'Sin punto y coma por que existe una etiqueta de cierre.' ?>

<?php echo 'Sin la etiqueta de cierre, pero con un punto y coma';
```

> **Pro Tip**: Si el archivo con el que estas trabajando solo contiene código PHP omite la etiqueta de cierre, te ahorraras ciertos problemas al utilizar el archivo con instrucciones __require__ o __include__ cuando existan espacios extras que hallas olvidado omitir.


## Comentarios

PHP soporta comentarios al estilo __C__, __C++__ y __Unix shell__ (Perl style). Por ejemplo:

```php
<?php
echo 'Esta es una prueba'; // Este es un comentario de una linea al estilo C++.
/* Este es un comentario
   multi-linea */
echo 'Esta es otra prueba';
echo 'Una última prueba'; # Este es un comentario de una linea al estilo shell
```

## Namespaces

Un __namespace__ es una manera de encapsular elementos. Esto puede verse como un concepto abstracto en muchos lugares. Por ejemplo, cualquier directorio de un sistema operativo funciona como un grupo de archivos relacionados, y actua como un namespace para los archivos. Como un ejemplo concreto, el archivo `foo.txt` puede existir en ambos directorios `/home/greg` y `/home/other`, pero dos copias de `foo.txt` no deben co-existir en el mismo directorio. Adicionalmente, para acceder al archivo `foo.txt` por fuera del directorio `/home/greg`, deberemos incluir el nombre del directorio al nombre del archivo utilizando el separador de directorios para obtener `/home/greg/foo.txt`. Este mismo principio se extiende para los namespaces en el mundo de la programación.

En el mundo de PHP, los namespaces son diseñados para resolver dos problemas que los autores de librerías y aplicaciones se encuentran cuando crean elementos de código re-utilizables como clases y funciones:

- La colisión de nombres entre código que creas y clases/funciones/constantes internas de PHP o clases/funciones/constantes de proveedores externos.
- La habilidad para renombrar (o acortar) Nombres_Extra_Largos diseñados para solucionar el problema del punto anterior, promoviendo lectura del código fuente.

Los namespaces de PHP proveen una manera en la cual podemos agrupar clases, interfaces, funciones y constantes relacionadas.

> Para efectos de rapidez definiremos los namespaces de acuerdo al estándar de programación PSR-2.

Un namespace se declara utilizando la palabra reservada `namespace` seguida por el nombre que queremos proporcionar namespace. Por ejemplo:

```php
<?php

namespace Coppel;
```

Un namespace puede contener varios niveles de agrupación los cuales podemos definir utilizando el separador `\` (barra invertida).


```php
<?php

namespace Coppel\Database\PostgreSql;
```

- Un namespace debe declararse al inicio del archivo o después de la definición del bloque de inicio de PHP (<?php).
- El namespaces deberá iniciar con el nombre del __proveedor__ o __vendor__.

Ver [namespaces](http://php.net/manual/en/language.namespaces.php) en php.net.

## PDO

**PHP Data Objects** es una extensión que define una interfaz ligera y consistente para acceder a bases de datos en PHP. Cada driver de base de datos que implementa la interfaz PDO puede exponer caracteristias especificas de base de datos así como las funciones regulares de la extensión. Hay que tomar en cuenta que no se puede realizar cualquier funcionalidad de base de datos usando la extensión PDO por si sola; debe de utilizar un driver especifico para acceder a el servidor de base de datos que necesite conectarse.

PDO provee una capa de abstracción de acceso a datos, lo que quiere decir que, sin importar que base de datos estés utilizando, usas las mismas funciones para realizar consultas y obtener datos.

PDO está disponible desde PHP 5.1 y requiere las características de programación orientada a objetos de PHP 5, por lo tanto no funciona con versiones anteriores.

## Sesiones

PHP tiene soporte para el manejo y administración de sesiones la cual es una manera de preservar cierta información a través de accesos subsecuentes. Esto permite construir aplicaciones mas personalizadas e incrementar la experiencia de navegación.

# Build-in server

# Sobre el proyecto PHP

Vamos a realizar un proyecto en el cual se podrán realizar compras de articulos de manera electrónica el cual deberá cubrir los siguientes requerimientos:

- Registarse como usuario.
- Iniciar sesión.
- Buscar productos.
- Páginar el listado de los productos.
- Filtrar productos por categorías.
- Ver el detalle del producto.
- Agregar productos al carrito de compras.
- Hacer el checkout de los productos.

# Sobre el framework de desarrollo

El proyecto lo podemos realizar de una manera sencilla y ordenada en un solo proyecto, pero para cuestiones de conocer un poco mas como funciona todo vamos a implementar y desarrollar un micro-framework el cual deberá de cubrir los siguientes requerimientos:

- Implementar el patrón MVC.
- Implementar un mecanismo de ruteo de urls.
- Contar con un template engine el cual contenga un contexto de variables.
- Implementar una configuración general.
- Crear conexiones a base de datos.
- Configurar la estructura de directorios de los controladores, modelos, vistas y assets.

> Tanto como el proyecto y el framework deberán utilizar el gestor de paquetes Composer para realizar la auto carga de clases.

# Estructura del proyecto PHP.

El proyecto (directorio) deberá llamarse `shoppingcart` y dentro de el tendremos la siguiente estructura de directorios:

```
shoppingcart/
|-- composer.json
|-- index.php
|-- assets
|   |-- css
|   |-- fonts
|   |-- images
|   |-- js
|-- src
|   |-- config
|   |-- controllers
|   |-- models
|   |-- views
|-- vendor
```

Cada archivo/directorio tiene un fin en especifico:

- **composer.json**: archivo de configuración de composer, se auto-genera cuando ejecutamos la instrucción `composer init`.
- **index.php**: archivo de entrada del proyecto, este archivo es el que se ejecuta inicialmente cuando una petición HTTP entra al servidor.
- **assets**: archivos son archivos que representan recursos tales como imágenes, archivos de scripts, hojas de estilo, fuentes y todo otro recurso que el sitio web pudiera necesitar.
- **src**: directorio que contiene el código fuente del proyecto.
   - **config**: archivos de configuración de la aplicación.
   - **controllers**: clases PHP de tipo controlador.
   - **models**: clases PHP de tipo modelo.
   - **views**: vistas de la aplicación.
- **vendor**: directorio creada por __composer__ la cual contiene archivos de configuración de las dependencias y de la auto carga de clases.

# Ejecutando composer

Iniciamos creando los archivos de composer para manejar las dependencias (no en este proyecto, pero se pudiera hacer) y la auto carga de clases (esto si lo haremos).

En la terminal deberemos situarnos dentro del directorio `shoppingcart` y ejecutar el siguiente comando:

```
composer init
```

Aparecerá un mensaje como este `Welcome to the Composer config generator` seguido por otro mensaje que solicita ingresar el nombre del paquete (proyecto) que estamos creando. Como se indica en el mensaje es necesario ingresar un __vendor__ y un __name__, vendor es como el propietario del proyecto y nombre el nombre que llevará el proyecto. Ingresemos lo siguiente: `coppel/shoppingcart`.

> Note que el `package name` debe ser en minúsculas, trate de ingresar el nombre del proyecto o el propietario en mayúsculas y aparecerá un mensaje de error indicando que el nombre del paquete es incorrecto.

Después __composer__ solicitará una descripción del proyecto, aquí ingrese lo que crea que sea necesario. Al solicitar el autor es necesario ingresar un valor con el siguiente formato: __name <my@email>__, por ejemplo `Juan Perez <jperez@coppel.com>`.

Cuando solicite `Minimum Stability`, `Package Type` y `Licence` puede solamente presionar la tecla `<Enter>` para dejar esas propiedades vacias.

Lo siguiente son dos preguntas que son referentes a las dependencias y como en este proyecto no manejaremos dependencias deberemos de ingresar los valores `no` en las preguntas `Would you like to define your dependencies (require) interactively [yes]?` y `Would you like to define your dev dependencies (require-dev) interactively [yes]?` y presionar la tecla `<Enter>`.

Para terminar deberemos de confirmar todos los datos que hemos ingresado ingresando el valor `yes` y presionar la tecla `<Enter>`.

Realizado lo anterior podemos observar que dentro del proyecto existe un archivo de nombre `composer.json` el cual contiene toda la información que ingresamos con el uso del comando `composer init`.

```json
{
    "name": "coppel/shoppingcart",
    "description": "Tienda en linea para la venta de artículos",
    "authors": [
        {
            "name": "Juan Perez",
            "email": "jperez@coppel.com"
        }
    ],
    "require": {}
}
```

Ahora vamos a ejecutar el siguiente comando en la terminal.

```
composer dump-autoload
```

Con esto le decimos a composer que genere los archivos de configuración de auto carga los cuales se crean en el directorio `vendor`. El directorio `vendor` contiene lo siguiente:

```
vendor/
|-- autoload.php
|-- composer
    |-- autoload_classmap.php
    |-- autoload_namespaces.php
    |-- autoload_psr4.php
    |-- autoload_real.php
    |-- ClassLoader.php
```

En este momento es irrelevante lo que contiene cada uno de los archivos pero mas adelante veremos para que se necesitan algunos de los archivos cuando configuremos la auto carga de clases.

# Estructura del framework de desarrollo

El framework que crearemos será sumamente sencillo, conteniendo tareas básicas como las mencionadas en anteriormente. Vamos a elegir un nombre para el framework, puedes elegir el que gustes, yo utilizaré el nombre `Yelu` el cual lo he sacado de la palabra `Yellow` en ingles haciendo referencia al color primario que utiliza la empresa para su marca comercial.

Entonces vamos a crear el directorio `Yelu` en el mismo directorio en el cual creamos el proyecto `shoppingcart` y este contendrá la siguiente estructura.

```
yelu/
|-- composer.json
|-- src
|   |-- BaseController.php
|   |-- BaseModel.php
|   |-- Router.php
|   |-- Yelu.php
|-- vendor

```

Como ven, en la estructura del proyecto existe el archivo `composer.json` y el directorio `vendor` por lo cual deberemos ejecutar nuevamente el comando `composer init` dentro del directorio del framework. Para este caso, podemos ingresar los valores de la misma manera en la que los ingresamos para el proyecto `shoppingcart`, solo que para el framework vamos a utilizar otro `package name`, usaremos `coppel/yelu`.

> Si utilizaste un nombre diferente para el framework solo deberás reemplazarlo en la parte del `package name`, por ejemplo `coppel/myawesomename`.

# Escribiendo el framework de desarrollo.

En el proyecto `Yelu` vamos a crear el directorio `src` y dentro de el vamos a crear el archivo `Yelu.php`.

> Nuevamente, si usted creo el framework con otro nombre lo mas apropiado será crear un archivo de nombre `MyAwesomeFamework.php`.

Dentro de este archivo vamos a crear la clase `Yelu` con el namespace `Coppel\Yelu`.

```php
<?php

namespace Coppel\Yelu;

class Yelu
{
    public function __construct()
    {
        echo __METHOD__;
    }
}
```

Lo siguiente es cargar la clase desde el proyecto `shoppingcart`, por lo cual vamos a crear el archivo `index.php` que se encuentra en la raíz del proyecto y dentro de el vamos a ingresar lo siguiente.

```php
<?php

require_once "./vendor/autoload.php";

$yelu = new Coppel\Yelu\Yelu();
```

Ahora, si ejecutamos lo siguiente en la terminal:

```
php index.php
```

Deberá de aparecer un mensaje como el siguiente:

```
PHP Fatal error:  Class 'Coppel\Yelu\Yelu' not found in /shoppingcart/index.php on line 5
```

La clase no ha sido encontrada y esto es por que no hemos configurado composer para que auto cargue las clases. Para ello vamos a editar el archivo `composer.json` del proyecto `shoppingcart` para que quede de la siguiente manera:

```json
{
    "name": "coppel/shoppingcart",
    "description": "Online store",
    "authors": [
        {
            "name": "Juan Perez",
            "email": "jperez@coppel.com"
        }
    ],
    "require": {},
    "autoload": {
        "psr-4": {
            "Coppel\\Yelu\\": "../yelu/src/"
        }
    }
}
```

Como se pueden dar cuenta, se agrego la propiedad `autoload` y dentro de ella otra propiedad, `psr-4`. Con esto le indicamos a composer que realice la auto carga utilizando el estándar `PSR-4`. Ahora, dentro de la propiedad `psr-4` es donde vamos a definir en que directorio la auto carga deberá buscar las clases cuando determinado namespace sea utilizado.

Continuando con el proyecto y para realizar un ejemplo práctico vamos a tomar la definición anterior donde indicamos que cuando se necesite utilizar o cargar una clase que contenga el namespace `Coppel\Yelu` esta se deberá buscar un directorio atrás del directorio actual, seguido por un directorio `yelu` y un directorio `src`.

Para que composer actualice su configuración con los cambios de auto carga que hemos realizado es necesario ejecutar el comando `composer dump-autoload` en la terminal.

Antes de actualizar la configuración, el archivo `vendor/composer/autoload_psr4.php` contenía lo siguiente:

```php
<?php

// autoload_psr4.php @generated by Composer

$vendorDir = dirname(dirname(__FILE__));
$baseDir = dirname($vendorDir);

return array(
);
```

Y después de ejecutar el comando el archivo contiene esto:

```php
<?php

// autoload_psr4.php @generated by Composer

$vendorDir = dirname(dirname(__FILE__));
$baseDir = dirname($vendorDir);

return array(
    'Coppel\\Yelu\\' => array($baseDir . '/../yelu/src'),
);
```

La **magia** de la auto carga se puede explicar de una manera muy sencilla. Tenemos el archivo `autoload_psr4.php` en el directorio `shoppingcart/vendor/composer/` el cual contiene una variable de nombre `$vendorDir` a la cual le es asignado el valor `dirname(dirname(__FILE__))` el cual asigna el valor `shoppingcart/vendor` ya que el directorio del archivo `autoload_psr4.php` es `shoppingcart/vendor/composer` y el directorio de este directorio es `shoppingcart/vendor/`. Ahora la variable `$baseDir` contiene el valor asignado por `dirname($vendorDir)` el cual seria `shoppingcart/`. Entonces, siguiendo con la parte de la auto carga, en el arreglo de retorno tenemos el `key` `Coppel\\Yelu\\` al cual se le asigna el valor de un arreglo conteniendo un único valor `$baseDir` mas `../yelu/src/'`el cual resulta con la ruta `shoppingcart/../yelu/src` que dirige al directorio `yelu/src` que se encuentra un directorio atrás del directorio `shoppingcart`.

Vamos a ejecutar nuevamente el comando `php index.php` en la terminal para ver que es lo que sucede.

Ahora vemos que la clase si fue encontrada y como resultado en la terminal se mostrará el texto `Coppel\Yelu\Yelu::__construct`.

> Para cuestiones de una impresión de contenido limpia en la terminal, podemos eliminar la instrucción `echo` del constructor, de otra manera a medida que vayamos creando mas clases tendremos mas contenido innecesario imprimiéndose y podrá darse el caso se no identificar lo que necesitamos por todo el contenido impreso.

## Ventajas de utilizar la auto carga

- No es necesario especificar un `require` o `include` cada vez que necesitemos de una clase. Pero será necesario especificar el namespace mediante la palabra reservada `use`.
- Nos olvidamos por completo donde se encuentran los archivos de clase, si estos cambian de ubicación solo se necesita actualizar las referencias en el archivo `composer.json` y ejecutar el comando `composer dump-autoload` para actualizar las rutas.


Muchas veces es difícil recordar la ruta donde se encuentra cada archivo. Es mas fácil recordar un namespace tal como `Coppel\Database\PostgreSql` que incluir un archivo PHP con una ruta tal como`../../framework/conexiones/postgresql.php` que puede cambiar dependiendo del directorio donde se encuentre el archivo desde el que la estamos requiriendo.

# Definiendo la configuración

Antes de comenzar a escribir controladores, modelos y vistas vamos a definir la configuración que vamos a utilizar en el proyecto y vamos a pasarla al framework para que este administre esa configuración y defina todas las características a utilizar a como se encuentren definidas en el proyecto.

Los datos de configuración los vamos a definir en un arreglo, que a su vez contendrá otros sub-arreglos con configuración mas especifica. Vamos a crear el archivo `App.php` dentro del directorio `src/config` en el proyecto `shoppingcart`. Dentro de el vamos a ingresar lo siguiente:

```php
<?php

return [
];
```

## Directorio base

Cuando pasemos la configuración al framework, este necesita saber con que proyecto va a trabajar, o de otra manera, necesita conocer donde se encuentran los archivos con los que va interactuar, por ello necesitamos especificar la ruta absoluta donde se encuentra el proyecto. Vamos a agregar lo siguiente al arreglo de configuración `config/App.php`.

```php
<?php

return [
    "baseDir" => dirname(__DIR__)
];
```

Con esto, estamos asignando a la llave `baseDir` la ruta absoluta del directorio `src` del proyecto `shoppingcart`.

Vamos a realizar una prueba para observar cual es el valor asignado a la variable `baseDir`, agreguemos lo siguiente al final del archivo `index.php` del proyecto `var_dump(require_once './src/config/App.php');` y ejecutemos el archivo `index.php` con el interprete de PHP en la terminal.

Deberia aparecer algo como lo siguiente:

```
array(1) {
  ["baseDir"]=>
  string(58) "/home/sergio/Projects/shoppingcart/src"
}
```

## Inicializando el framework

Ya hemos definido un valor de configuración en el proyecto `shoppingcart`, ahora necesitamos pasar esa configuración al framework para que este comience a interpretarla y haga algo con ella.

Vamos a editar la clase `Yelu` contenida el archivo `src/Yelu.php` del framework para agregar un nuevo método público de nombre `init`, el cual deberá requerir un parámetro de nombre `$config`, a la vez necesitamos definir una propiedad privada con el mismo nombre.

```php
<?php

namespace Coppel\Yelu;

class Yelu
{
    private $config;

    public function __construct()
    {
        # echo __METHOD__;
    }

    public function init($config)
    {
        $this->config = $config;
    }
}
```
Ahora en el archivo `index.php` del proyecto `shoppingcart` vamos a pasar el arreglo de configuración al método `init`de la clase `Yelu`.

```php
<?php

require_once "./vendor/autoload.php";

$yelu = new Coppel\Yelu\Yelu();

$yelu->init(require_once './src/config/App.php');
```

Hecho esto, cualquier configuración que definamos en el archivo `App.php` será pasada al framework.

# Controladores

Los controladores son los puntos de entrada principal para el proyecto, cuando una petición llega al servidor, el framework deberá de encargarse de redirigirla hacia el controlador con su método indicado.

Para comenzar vamos a definir la configuración de los controladores, lo que necesitamos es darle a conocer al framework el namespace que un controlador deberá tener. Definiendo esto y con ayuda de la auto carga de composer fácilmente podemos ubicar una clase tipo controlador para ser cargada.

Vamos a crear el archivo `Namespaces.php` en el directorio `config` del proyecto `shoppingcart`, en el agregaremos el siguiente contenido:

```php
<?php

return [
    "controller" => "Coppel\\Controllers\\"
];
```

Como pueden ver, para los controladores estamos definiendo un namespace `Coppel\Controllers` y como el archivo de configuración principal es `config/App.php` deberemos cargarlo desde ahí. Hay que editar el archivo `config/App.php` para que quede de la siguiente manera:

```php
<?php

return [
    "baseDir" => dirname(__DIR__),
    "namespaces" => require_once "./src/config/Namespaces.php"
];
```

Ahora la configuración deberá ser como lo siguiente:

```
array(2) {
  ["baseDir"]=>
  string(58) "/home/sergio/Projects/shoppingcart/src"
  ["namespaces"]=>
  array(1) {
    ["controller"]=>
    string(19) "Coppel\Controllers\"
  }
}
```

## Agregando la ruta de los controladores a la auto carga

Para que la auto carga sepa como cargar un controlador deberemos especificarlo a como lo hicimos con el framework. Hay que editar el archivo `composer.json` y agregar lo siguiente a la propiedad `psr-4`.

```
"Coppel\\Controllers\\": "src/controllers/"
```

Cuando se necesite cargar una clase de tipo controlador (esto lo sabemos por el namespace `Coppel\Controllers`) la auto carga la buscará en el directorio `src/controllers` del proyecto `shoppingcart`.

> **Pro Tip**: Cada vez que se edite el archivo __composer.json_ y se agregue una nueva referencia a la propiedad __psr-4__ es necesario ejecutar el comando **composer dump-autoload** en la terminal para reflejar los cambios.

## Cargando el controlador en el framework

En el método `init` de la clase `Yelu` vamos a crear una instancia de un controlador, para ello primero necesitamos crear uno en el directorio `scr/controllers`, vamos a llamarlo `Home.php`y contendrá lo siguiente:

```php
<?php

namespace Coppel\Controllers;

class Home
{
    public function __construct()
    {
        echo __METHOD__;
    }
}
```

Ahora si, editemos la clase `Yelu` para agregar la carga del controlador:

```php
<?php

namespace Coppel\Yelu;

class Yelu
{
    private $config;

    public function __construct()
    {

    }

    public function init($config)
    {
        $this->config = $config;

        $className = "{$this->config['namespaces']['controller']}Home";

        $home = new $className();
    }
}
```

Como se puede observar, el nombre de la clase a cargar (controlador) es la unión del namespace de los controladores mas el nombre de la clase, cuando una clase se encuentra contenida en un namespace su nombre pasa a ser el namespace mas el nombre de clase y en este caso el nombre de la clase `Home` es `Coppel\Controllers\Home`.

Si ejecutamos el archivo `index.php` con PHP tendremos el siguiente resultado en la consola `Coppel\Controllers\Home::__construct`.

# Ruteo de URL's

Cuando hablamos de ruteo en un framework lo que se está haciendo es tomar la dirección url de la petición que llega al servidor y de acuerdo a ciertos criterios determinar que acción deberá ejecutarse. En este caso deberemos de determinar que método de que controlador vamos a llamar.

Vamos a crear el archivo `Router.php` dentro del directorio `src` del framework y dentro de el crearemos la clase `Router`.

```php
<?php

namespace Coppel\Yelu;

class Router
{
    public function __construct()
    {

    }
}
```

## Determinar la ruta

Una configuración de ruta mínimamente debe contar con dos elementos, el **método HTTP** y el **Path**, los parámetros son otro elemento muy importante pero no necesario para determinar una ruta, mas adelante veremos como utilizarlos.

El arreglo super global `$_SERVER` contiene los dos elementos que necesitamos y están especificados con las llaves `REQUEST_URI` y `REQUEST_METHOD`. Vamos a extraerlos en el constructor de la clase para observar los valores que contienen cuando una petición es lanzada al servidor.

```php
<?php

namespace Coppel\Yelu;

class Router
{
    public function __construct()
    {
        $path = filter_input(INPUT_SERVER, 'REQUEST_URI');

        $method = filter_input(INPUT_SERVER, 'REQUEST_METHOD');

        var_dump($path, $method);
    }
}
```

En el método `init` de la clase `Yelu` vamos a crear una instancia de la clase `Router` y llamaremos el archivo `index.php` con PHP. Como resultado en la terminal tendremos un resultado un poco extraño:

```
NULL
NULL
```

> **Y bueno, ¿por qué sucede esto?**

Como estamos ejecutando el script de PHP directamente desde el interprete, no desde un navegador web, no tenemos un método y una url. Necesitamos ejecutar el script con un servidor web, para ello podemos ejecutar el build-in server que viene integrado con PHP para poder acceder por medio de un navegador y poder lanzar peticiones HTTP.

```
php -S localhost:8888
```

Ahora desde `Postman` vamos a llamar la url `http://localhost:8888` con el método `GET`, el resultado será:

```
string(1) "/"
string(3) "GET"
```

Inclusive, si accede a la url desde el navegador también podrá obtener el mismo resultado.

> Intente lanzar mas peticiones agregando rutas a la url y cambiando el método HTTP, con ello verá que los valores también cambiarán. Utilize `Postman` ya que desde el navegador no puede cambiar el método HTTP

Ahora que podemos obtener el método HTTP y el path hay que almacenarlos para poder utilizarlos en el ruteo.

```php
<?php

namespace Coppel\Yelu;

class Router
{
    private $method;

    private $path;

    public function __construct()
    {
        $this->path = filter_input(INPUT_SERVER, 'REQUEST_URI');

        $this->method = filter_input(INPUT_SERVER, 'REQUEST_METHOD');
    }
}
```

## Configurar las rutas de la aplicación

Ya que tenemos almacenados los dos datos que necesitamos para realizar un ruteo debemos de configurar las rutas con las que trabajará la aplicación. Hay que crear el archivo de configuración `Routes.php` en el proyecto `shoppingcart` y agregar una ruta que dirija al controlador `Home`.

```php
<?php

return [
    [
        "method" => "GET",
        "path" => "/"
    ]
];
```

También hay que incluirlo en el archivo `App.php`.

```php
<?php

return [
    "baseDir" => dirname(__DIR__),
    "namespaces" => require_once "./src/config/Namespaces.php",
    "routes" => require_once "./src/config/Routes.php"
];
```

## Validar la ruta

Ya que tenemos configurada por lo menos una ruta en la configuración vamos a validar si cuando se accede al proyecto la ruta existe o no. Hay que pasar el arreglo de rutas a la clase `Router`, pero vamos a hacerlo en un nuevo método público de nombre `start` donde haremos la validación.

```php
<?php

namespace Coppel\Yelu;

class Router
{
    private $method;

    private $path;

    public function __construct()
    {
        $this->path = filter_input(INPUT_SERVER, 'REQUEST_URI');

        $this->method = filter_input(INPUT_SERVER, 'REQUEST_METHOD');
    }

    public function start($routes)
    {

    }
}
```

```php
<?php

namespace Coppel\Yelu;

class Yelu
{
    private $config;

    public function __construct()
    {

    }

    public function init($config)
    {
        $this->config = $config;

        $router = new Router();

        $router->start($this->config['routes']);
    }
}
```

Dentro del método `start` vamos a comparar cada par de método y ruta configurado en el arreglo de rutas con el método y ruta que llegaron al servidor y mostrar un mensaje que nos haga saber si la ruta existe o no.

```php
<?php

public function start($routes)
{
    foreach ($routes as $route) {
        if ($route['method'] === $this->method & $route['path'] === $this->path) {
            echo "La ruta $this->method $this->path existe!";
        } else {
            echo "La ruta $this->method $this->path NO existe!";
        }
    }
}
```

Ahora podemos comenzar a lanzar peticiones al servidor y validar si la ruta y método a la que estamos accediendo se encuentran configuradas.

> Puedes agregar mas rutas al arreglo para realizar la prueba, trata de cambiar tanto el __path__ como el __método__.

## Cargar el controlador y método de una ruta

Ya hemos definido **rutas**  y **métodos** en la configuración del ruteo.

> **¿Pero cómo sabemos a que controlador/método llamar?**

Es necesario especificar para cada ruta cual es el controlador y el método que llamaremos.

Al controlador `Home` hay que agregarlo un método público de nombre `homePage` que imprima algo.

```php
<?php

public function homePage()
{
    echo __METHOD__;
}
```

Ahora vamos a agregar la clase y método que llamaremos a la ruta.

```php
<?php

return [
    [
        "method" => "POST",
        "path" => "/",
        "handler" => [
            "class" => "Home",
            "method" => "homePage"
        ]
    ]
];
```

En la validación del ruteo, cuando la ruta exista cargaremos el controlador y llamaremos el método.

```php
<?php

public function start($routes)
{
    foreach ($routes as $route) {
        if ($route['method'] === $this->method &
            $route['path'] === $this->path) {
            $class = $route['handler']['class'];

            $handler = new $class();
        } else {
            echo "La ruta $this->method $this->path NO existe!";
        }
    }
}
```

Lancemos una petición al servidor de la forma `GET /`, como resultado obtendremos un error como el siguiente `Class 'Home' not found in /home/sergio/Projects/yelu/src/Router.php on line 26`. Esto es por que estamos tratando de crear una instancia de la clase `Home` sin un namespace, recordemos que en la configuración definimos el namespace que tendrán los controladores y necesitamos incluirlo al momento de crear la clase.

Para hacer esto, vamos a pasar el valor del namespace de los controladores como parámetro en el método `start`.

```php
<?php

public function init($config)
{
    $this->config = $config;

    $router = new Router();

    $router->start($this->config['routes'], $this->config['namespaces']['controller']);
}
```

```php
<?php

public function start($routes, $controllerNamespace)
{
    foreach ($routes as $route) {
        if ($route['method'] === $this->method &
            $route['path'] === $this->path) {
            $class = "{$controllerNamespace}{$route['handler']['class']}";

            $handler = new $class();
        } else {
            echo "La ruta $this->method $this->path NO existe!";
        }
    }
}
```

Ahora si podemos realizar una prueba desde `Postman` o desde un navegador web, inclusive podemos cambiar el contenido del método `homePage` para mostrar algo diferente.

## Un poco de información

Como hemos visto en este último tema hemos utilizado ciertas combinaciones de texto para crear la instancia de la clase y llamar al método. Existen muchas maneras de hacerlo aparte de la forma anterior.

```php
<?php
# Las dos sentencias producen el mismo resultado
$class = "{$controllerNamespace}{$route['handler']['class']}";
$class = $controllerNamespace . $route['handler']['class'];

# Las tres sentencias producen el mismo resultado
$handler->$route['handler']['method']();
call_user_func_array(array($handler, $route['handler']['method']), []);
call_user_func(array($handler, $route['handler']['method']), []);
```

# Vistas

Las vistas son pequeños fragmentos o secciones de una página (generalmente elementos HTML) que pueden ser cargados desde un controlador para ser mostrados como salida, esta salida puede ser modificada con la ayuda de variables de contexto que harán que una vista no sea un simple contenido estático.

Vamos a realizar la carga de vistas desde un controlador, para ello necesitamos contar con cierta información como el nombre de la vista a cargar, la ubicación o las variables de contexto, pero para no realizar estas tareas manualmente en cada controlador vamos a crear un `controlador base` el cual realice estas operaciones y desde los demás controladores podamos utilizarlas sin necesidad de reescribir las tareas en cada uno.

## Definiendo el constructor base

Crearemos el archivo `BaseController.php` en el directorio `src` del framework. Dentro de el crearemos la clase base.

```php
<?php

namespace Coppel\Yelu;

class BaseController
{
    public function __construct()
    {
        echo __METHOD__;
    }
}
```

Ahora vamos a `extender` o `heredar` la clase `Home` desde `BaseController`.

```php
<?php

namespace Coppel\Controllers;

use Coppel\Yelu\BaseController;

class Home extends BaseController
{
    public function __construct()
    {

    }

    public function homePage()
    {
        echo "Hello world!";
    }
}
```

Si accedemos nuevamente desde el navegador a la ruta `GET /` veremos que nada ha cambiado. Hay que notar algo, cuando definimos el constructor de la clase `BaseController` declaramos una sentencia `echo __METHOD__`.

> **¿Y por qué no se muestra?**

Cuando heredas o extiendes una clase de otra los constructores no son llamados automáticamente, de ser necesario se deben llamar manualmente de la siguiente manera `parent::__construct()`.

> **Pro Tip**: los destructores son llamados de la manera `parent::__destruct()` y tanto los constructores como los destructores pueden llamarse en cualquier método, no necesariamente en el constructor o destructor de la clase.

## Método render

Dentro de la clase `BaseController` agregaremos un método público de nombre `render` que contará con un parámetro de nombre `$view` la cual hará la búsqueda y carga de la vista indicada.

Antes de comenzar a escribir este método es necesario configurar la ruta donde se estarán ubicadas las vistas. Vamos a agregar lo siguiente al arreglo de configuración `"viewsDir" => "./src/views/"`.

```php
<?php

return [
    "baseDir" => dirname(__DIR__),
    "viewsDir" => "./src/views/",
    "namespaces" => require_once "./src/config/Namespaces.php",
    "routes" => require_once "./src/config/Routes.php"
];
```

Ahora necesitamos realizar un cambio a la manera como accedemos a la configuración para que sea accesible desde cualquier clase dentro del proyecto y del framework.

Vamos a cambiar la propiedad `$config` de la clase `Yelu` a `static` y eliminaremos los parámetros del método `start` la clase `Router`. Además, vamos a agregar una conversión para utilizar el arreglo de configuración con el operador de acceso a propiedades de objetos  en lugar de tener que estar accediendo a los valores por medio de los corchetes y comillas.

```php
<?php

namespace Coppel\Yelu;

class Yelu
{
    public static $config;

    public function __construct()
    {

    }

    public function init($config)
    {
        self::$config = json_decode(json_encode($config), false);

        $router = new Router();

        $router->start();
    }
}
```

```php
<?php

public function start()
{
    foreach (Yelu::$config->routes as $route) {
        if ($route->method === $this->method &
            $route->path === $this->path) {
            $class = Yelu::$config->namespaces->controller . $route->handler->class;

            $handler = new $class();

            $method = $route->handler->method;

            $handler->$method();
        } else {
            echo "La ruta $this->method $this->path NO existe!";
        }
    }
}
```

Vamos a crear el método `render` en la clase `BaseController` y la vista que pasemos como parámetro vamos a incluirla con la instrucción `require_once`, agregando al inicio el directorio de las vistas.

```php
<?php

namespace Coppel\Yelu;

class BaseController
{
    public function __construct()
    {

    }

    protected function render($view)
    {
        require_once Yelu::$config->viewsDir . $view;
    }
}
```

Dentro del directorio `src/views` vamos a agregar una vista de nombre `home.php` la cual tendrá el siguiente contenido:

```html
<h1>¡Bienvenido!</h1>
```

Y en el controlador `Home` vamos a cargar la vista de la siguiente manera:

```php
<?php

namespace Coppel\Controllers;

use Coppel\Yelu\BaseController;

class Home extends BaseController
{
    public function __construct()
    {

    }

    public function homePage()
    {
        $this->render('home.php');
    }
}
```

> ¿Incluir la extensión de las vistas estaría de mas no?

Vamos a corregir esto cambiando la siguiente línea en la clase `BaseController`: `require_once Yelu::$config->viewsDir . $view;` por `require_once Yelu::$config->viewsDir . $view . ".php";` y al cargar la vista eliminamos el `.php`.

Con esto simplemente cargamos las vistas con su respectivo nombre, y como en realidad lo que estamos haciendo es especificar un nombre de archivo para generar una ruta absoluta al archivo de vista fácilmente podemos crear un sub-directorio en el directorio de vistas para crear grupos y cargarlas de la manera `$this->render('subfolder/items');`

Entonces vamos a actualizar la página en el navegador para poder ver un encabezado con el texto `¡Bienvenido!` o desde `Postman` para ver el código fuente `<h1>¡Bienvenido!</h1>`.

## Creando layouts

Un layout en terminos de vistas y plantillas es una plantilla principal de la cual pueden extender las vistas, es decir, podemos utilizar un layout para definir la mayoria de los elementos de un sitio web y en ciertas partes mas pequeñas o de contenido dínamico podemos incluir el contenido de las vistas. Un layout es un elemento re-utilizable.

### Controlado la salida de la información

Este tema puede ser muy extenso y vamos a utilizar unas cuantas funciones referentes al **output buffering** para preservar la salida de información, hacer algo con ella y cuando sea necesario enviarla para que sea mostrada.

Si en cierto momento utilizamos una instrucción `require` o `include`, inmediatamente el contenido de los archivos que incluyamos será procesado por PHP y si en uno de esos archivos tenemos alguna instrucción que envie algo como salida este será enviado al momento.

> Toda la información referente al control de salida se encuentra disponible en la [documentación de PHP](http://php.net/manual/es/ref.outcontrol.php).

Hemos utilizado las instrucciones `require` o `include` para asignar el retorno de un archivo incluido a una variable, el archivo de configuración `App.php` es uno de ellos y si hechamos un vistazo al código veremos que podemos realizar algo como esto:

```php
<?php

$contenido = require_once "App.php";

var_dump($contenido);
```

El contenido del archivo `App.php` es asignado a la variable por que dentro de el tenemos una instrucción `return` y si tuvieramos algo como un `echo`, `var_dump` o `print`antes del  `return` este seria enviado como salida y mostrado al momento en el navegador, intentalo y veras.

Con las vistas no podemos hacerlo de esta manera ya que el contenido realmente es salida que necesitamos mostrar y no una variable PHP, claro, pudieramos escribir todas las salidas utilizando `strings` pero eso seria una muy mala practica.

De echo, hasta el momento lo tenemos de esta precisa manera:

```php
<?php

require_once Yelu::$config->viewsDir . $view . ".php";
```

Estamos utilizando un `require_once` para incluir la vista, perfecto.

> ¿Pero como le hacemos para trabajar con el layout y que esa vista sea incluida en una sección entre todo el contenido del layout? __La respuesta es almacenando esa salida hasta que la necesitemos__.

Vamos a crear un nuevo método privado en la clase `BaseController` y le llamaremos `internalRender`, este método aceptará un parámetro de nombre `$view` y en el método `render` llamaremos a `internalRender` pasando la vista que se necesita cargar.

```php
<?php

namespace Coppel\Yelu;

class BaseController
{
    public function __construct()
    {

    }

    protected function render($view)
    {
        $this->internalRender($view);
    }

    private function internalRender($view)
    {
        ob_start();

        include_once "Yelu::$config->viewsDir$view.php";

        $content = ob_get_contents();

        ob_end_clean();

        echo $content;
    }
}

```

Si recargamos el navegador veremos que no aparece nada y es por que cuando realizamos el armado de la cadena de la ruta del achivo en realidad lo PHP hace es retornar algo como esto `Yelu::Home.php` y no `".src/views/Home.php`. Hay un problema al escapar los valores de una variable estática en un string con comillas dobles, no es posible hacerlo, PHP entiende que en la expresión `"Yelu::$config->viewsDir$view.php"`, la variable a escapar es `$config->viewsDir` sin tomar en cuenta que es una variable estática de la clase`Yelu`.

Vamos a cambiar la expresión `include_once "Yelu::$config->viewsDir$view.php";` por lo siguiente:

```php
<?php

$viewsDir = Yelu::$config->viewsDir;

include_once "$viewsDir$view.php";

```

Recarguemos el navegador y veremos que nuevamente aparecerá el texto.

__¿Cómo funciona todo eso que hay dentro del método `internalRender`?__ Al iniciar el método ejecutamos la función `ob_start()`la cual a partir de ese momento inicializa la captura del bufer de salida __(object buffer start)__, toda información enviada como salida despues de esta instrucción no será enviada directamente como salida en el navegador, será almacenada hasta que le indiquemos ser mostrada o descartada. Luego incluimos el archivo de vista sin ser mandado como salida siguiendo con la ejecución de la función `ob_get_contents` __(object buffer get contents)__ que a como su nombre indica, obtiene el contenido del bufer de salida para asignarlo a una variable y por último ejecutamos la función `ob_end_clean` la cual detiene la captura del bufer de salida y limpia el contenido almacenado en el. Hay que notar que antes de limpiar el contenido del bufer debemos de obtenerlo, seria ilogico el limpiar el bufer y al final tratar de obtener su contenido.

> **Pero yo sigo mirando el mismo resultado, ¿qué ha cambiado?**

Lo que ha cambiado es que ahora el contenido de las vistas está siendo almacenado en una variable, algo que antes no podiamos realizar, y para darle mas sentido a la carga del layout en lugar de imprimir el contenido directamente vamos a retornarlo, cambiemos `echo $content;` al final del método por `return $content;`.

### Mostrando el archivo Layout

Vamos a crear el layout en el directorio de vistas, le daremos el nombre `layout.php` y su contenido será el siguiente:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello world</title>
    <meta charset="utf-8">
  </head>
  <body>
    <h1>Layout</h1>

  </body>
</html>
```

En el método `render` de la clase `BaseController` vamos incluir la vista layout e imprimirla, también lo haremos con la vista y recargaremos el navegador para ver el resultado. El nombre de la vista lo vamos a obtener de un nuevo valor de la configuración que llamaremos `layout`.

```php
<?php

return [
    "baseDir" => dirname(__DIR__),
    "viewsDir" => "./src/views/",
    "layout" => "layout",
    "namespaces" => require_once "./src/config/Namespaces.php",
    "routes" => require_once "./src/config/Routes.php",
    "database" => require_once "./src/config/Database.php"
];
```

```php
<?php

protected function render($view)
{
    echo $this->internalRender(Yelu::$config->layout);

    echo $this->internalRender($view);
}
```

**¡Perfecto!**, ahora vemos que tenemos las dos salidas, el contenido del archivo `layout.php` y la vista.

> **Sigo pensando que con un simple `require "layout.php"` e `include "$view.php"` hubiera sido suficiente para mostrar el contenido.**

Claro, pudimos haber incluido los archivos directamente, pero antes echemos un vistazo al código fuente en el navegador.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello world</title>
    <meta charset="utf-8">
  </head>
  <body>
    <h1>Layout</h1>

  </body>
</html>
<h1>¡Bienvenido!</h1>
```

De alguna manera el `<h1>¡Bienvenido!</h1>` que es el contenido de la vista no debiera de aparecer ahí. Deberíamos hacer algo para que ese contenido se encuentre dentro de las etiquetas `body` del código HTML.


## Utilizando variables de contexto

Algo que podemos hacer para resolver la situación anterior es almacenar el contenido de la vista a mostrar en una variable y pasarla a la __vista layout__ para mostrar su contenido donde sea necesario.

Para ello deberemos de procesar el contenido de la vista primero y almacenarlo en una variable, luego modificar el método `internalRender` para pasar las variable de contexto y hacerlas accesibles en el archivo de layout.

```php
<?php

namespace Coppel\Yelu;

class BaseController
{
    public function __construct()
    {

    }

    protected function render($view)
    {
        $content =  $this->internalRender($view);

        echo $this->internalRender(Yelu::$config->layout, $content);
    }

    private function internalRender($view, $context = [])
    {
        ob_start();

        $viewsDir = Yelu::$config->viewsDir;

        include_once "$viewsDir$view.php";

        $content = ob_get_contents();

        ob_end_clean();

        return $content;
    }
}
```

Hemos agregado una asignación de un valor predeterminado al parámetro `$context` ya que si no es necesario pasar variables de contexto podemos omitir el parámetro sin problemas.

Ya tenemos el contenido de la vista en una variable y esa variable está disponible al momento de cargar la vista.

> **¿Pero cómo hacemos que esa variable esté disponible en el contexto de la vista layout?**

[Extract](http://php.net/manual/es/function.extract.php) es una función que pertenece a la categoría de los arreglos y lo que hace es **importar** variables al contexto actual, o dicho de otro modo, crear variables a partir de los valores de un arreglo. Por ejemplo:

```php
<?php

$datos = [
    "hola" => "mundo!",
    "cantidad" => 12,
    "verdadero" => true
];

extract($datos);

var_dump($hola, $cantidad, $verdadero);
```

El resultado del código anterior es el siguiente:
```
string(6) "mundo!"
int(12)
bool(true)
```

Como pueden ver, nunca declaramos las variables `$hola`, `$cantidad` y `$verdadero`, solo eran valores contenidos en el arreglo `$datos` y la función `extract` creo las variables a partir de los datos del arreglo.

> Note que al utilizar la función `extract` la llave del elemento en el arreglo es el nombre que le dará a la variable al momento de crearla.

Si ejecutáramos el código anterior sin el uso de la función `extract` obtendríamos errores de variables sin definir.

```
PHP Notice:  Undefined variable: hola in /script.php on line 11
PHP Notice:  Undefined variable: cantidad in /script.php on line 11
PHP Notice:  Undefined variable: verdadero in /script.php on line 11
NULL
NULL
NULL
```

Ahora que podemos crear variables de manera dinámica vamos a pasar el contenido de la vista a un arreglo y le daremos el nombre o llave `content`, luego pasaremos el arreglo como parámetro de contexto al método `internalRender` y por último antes de incluir la vista y después de inicializar la captura del bufer de salida vamos a extraer las variables al contexto de la vista.

```php
<?php

namespace Coppel\Yelu;

class BaseController
{
    public function __construct()
    {

    }

    protected function render($view)
    {
        $content =  $this->internalRender($view);

        $context = [
            "content" => $content
        ];

        echo $this->internalRender(Yelu::$config->layout, $context);
    }

    private function internalRender($view, $context)
    {
        ob_start();

        extract($context);

        $viewsDir = Yelu::$config->viewsDir;

        include_once "$viewsDir$view.php";

        $content = ob_get_contents();

        ob_end_clean();

        return $content;
    }
}

```

Si recargamos el navegador veremos que solo aparece el contenido del archivo `layout.php` pero el de la vista no. Nos ha faltado imprimir el contenido de la variable recién creada de nombre `$content` en la vista del layout.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello world</title>
    <meta charset="utf-8">
  </head>
  <body>
    <h1>Layout</h1>
    <?= $content ?>
  </body>
</html>
```

Ahora si, al actualizar el contenido del navegador aparecerá el contenido de la vista y si observamos el código fuente veremos que el `<h1>¡Bienvenido!</h1>` aparece justamente donde imprimimos la variable `$content`.


```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello world</title>
    <meta charset="utf-8">
  </head>
  <body>
    <h1>Layout</h1>
    <h1>¡Bienvenido!</h1>
  </body>
</html>
```

# Assets

Para darle un diseño decente y de manera rápida a la página vamos a utilizar el famoso framework de front-end `Bootstrap`. Para ello necesitamos que la página sea capaz de cargar archivos de `CSS` y `Javascrit` y actualmente, con el `build-in server` se puede hacer.

Vamos a extraer el contenido del archivo `bootstrap-3.3.4-jquery-1.11.3-dist.zip` dentro del directorio `assets` en el proyecto `shppingcart` y vamos a realizar unos cambios en la vista layout para hacer referencia a esos archivos.


```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello world</title>
    <meta charset="utf-8">
    <link href="/assets/css/bootstrap.css" rel="stylesheet" />
  </head>
  <body>
    <h1>Layout</h1>
    <?= $content ?>
    <script src="/assets/js/jquery-1.11.3.js" rel="stylesheet"></script>
    <script src="/assets/js/bootstrap.js" rel="stylesheet"></script>
  </body>
</html>
```

Al recargar el navegador veremos que el texto a tomado otro estilo, esto es gracias a `Bootstrap`.

De una vez agregaremos unas etiquetas que utilizaran las clases de `Bootstrap` para formar el contenido de la página a como lo vamos a necesitar.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello world</title>
    <meta charset="utf-8">
    <link href="/assets/css/bootstrap.css" rel="stylesheet" />
  </head>
  <body>
    <div class="navbar navbar-default navbar-fixed-top">
      <div class="container-fluid">
        <div class="navbar-header">
          <a class="navbar-brand" href="/">Shopping Cart</a>
        </div>
      </div>
    </div>

    <div class="container">
      <div class="row">
        <?= $content ?>
      </div>
    </div>

    <script src="/assets/js/jquery-1.11.3.js" rel="stylesheet"></script>
    <script src="/assets/js/bootstrap.js" rel="stylesheet"></script>
  </body>
</html>
```

Recargamos el navegador para ver que ahora hay una barra de navegación en la parte superior con el texto `Shopping Cart` del lado izquierdo.

> ¿Notan que el contenido de la vista queda por debajo de la barra?

Podemos corregir ese detalle agregando unas reglas de `CSS`, hay que crear un nuevo archivo de nombre `shoppingcart.css` dentro del directorio `assets/css` y agregar el siguiente contenido:

```css
body {
  margin-top: 60px;
}
```

Ahora hay que agregar la referencia al archivo de `CSS` en el layout agregando la siguiente linea antes de cerrar la etiqueta `head`:

```html
<link href="/assets/css/bootstrap.css" rel="stylesheet" />
```

Con esto podemos realizar el siguiente cambio a la vista `home` para que el mensaje de bienvenida luzca mejor.

```html
<div class="col-md-12">
  <div class="jumbotron">
    <h1>Bienvenido</h1>
  </div>
</div>
```

# Modelos

Vamos a crear un nuevo controlador de nombre `Items` el cual deberá cargar una nueva vista de nombre `list` ubicada dentro de un sub-directorio de nombre `items`, la carga se hará dentro de un nuevo método público de nombre `listPage`.

El contenido del controlador `Items` es el siguiente:

```php
<?php

namespace Coppel\Controllers;

use Coppel\Yelu\BaseController;

class Item extends BaseController
{
    public function __construct()
    {

    }

    public function listPage()
    {
        $this->render('items/list');
    }
}
```

Y el contenido de la vista `list` es:

```html
<h1>Lista de artículos</h1>
```

> Aquí hemos creado el archivo `list.php` en la ruta `src/views/items`, como puede ver el archivo se creo en un sub-directorio, por lo cual es necesario especificar ese directorio al momento de cargarlo. Por ejemplo: `$this->render('items/list');`.

El método `listPage` deberá ejecutarse cuando se acceda a la ruta `GET /items` por medio del navegador, por lo cual hay que agregar la siguiente ruta al archivo de configuración de rutas:

```php
<?php

return [
    [
        "method" => "GET",
        "path" => "/",
        "handler" => [
            "class" => "Home",
            "method" => "homePage"
        ]
    ],
    [
        "method" => "GET",
        "path" => "/items",
        "handler" => [
            "class" => "Item",
            "method" => "listPage"
        ]
    ]
];
```

Accedemos a la ruta `/items` en el navegador para ver el contenido y nos daremos cuenta de que aparte del contenido de la vista `list` aparece un texto con el contenido `La ruta GET /items NO existe!`.

Esto es por que cuando realizamos la validación de las rutas en el método `start` de la clase `Router` tenemos una condición la cual valida por cada una de las rutas que existen en el arreglo de configuración de rutas si el __método__ y el __path__ concuerdan con los que llegaron al servidor, de no concordar enviamos un mensaje indicando que la ruta no existe. El problema es que como inicialmente teníamos una sola ruta no habia problema ya que o ejecutaba el método de la clase si existia o mostraba el mensaje indicando que la ruta no existe.

Vamos a cambiar ese mensaje para mostrarlo solo cuando realmente la ruta no exista y no cada vez que una ruta no exista dentro de la instrucción `foreach`.

```php
<?php

public function start()
{

    $routeExists = false;

    foreach (Yelu::$config->routes as $route) {
        if ($route->method === $this->method &
            $route->path === $this->path) {
            $routeExists = true;
            $class = Yelu::$config->namespaces->controller . $route->handler->class;

            $handler = new $class();

            $method = $route->handler->method;

            $handler->$method();
            break;
        }
    }

    if (!$routeExists) {
        echo "La ruta $this->method $this->path NO existe!";
    }
}
```

Igualmente que para los controladores, vamos a crear una clase `BaseModel` la cual implemente funcionalidades básicas para los modelos y nos sirva para extender de ella cada nuevo modelo que utilicemos. El archivo donde estará esta clase se llamará `BaseModel.php` y estará ubicado en el directorio `src` del framework.

```php
<?php

namespace Coppel\Yelu;

class BaseModel
{
    public function __construct()
    {

    }
}
```

Una de las principales funciones del modelo base será generar una conexión a base de datos, los datos de conexión deberá tomarlos desde un nuevo archivo de configuración de nombre `Database.php` el cual contendrá lo siguiente:

```php
<?php

return [
    "host" => "localhost",
    "database" => "shoppingcart",
    "user" => "root",
    "password" => ""
];
```

De igual manera, hay que agregarlo al archivo de configuración principal:

```php
<?php

return [
    "baseDir" => dirname(__DIR__),
    "viewsDir" => "./src/views/",
    "namespaces" => require_once "./src/config/Namespaces.php",
    "routes" => require_once "./src/config/Routes.php",
    "database" => require_once "./src/config/Database.php"
];
```

Ahora vamos a crear le método protegido `getConnection` en la clase `BaseModel`, el cual obtendrá los datos de configuración para crear una conexión a base de datos y retornarla

```php
protected function getConnection()
{
    $host = Yelu::$config->database->host;
    $dbname = Yelu::$config->database->database;
    $user = Yelu::$config->database->user;
    $password = Yelu::$config->database->password;

    $dsn = "mysql:host=$host;dbname=$dbname";

    return new \PDO(
        $dsn,
        $user,
        $password,
        [
            \PDO::ATTR_ERRMODE => \PDO::ERRMODE_EXCEPTION,
            \PDO::ATTR_DEFAULT_FETCH_MODE => \PDO::FETCH_ASSOC
        ]
    );
}
```

Con esto podemos obtener una conexión a base de datos si extendemos un modelo de esta clase. Hay que crear el modelo `Item` en el directorio `src/models` en el proyecto `shoppingcart`

```php
<?php

namespace Coppel\Models;

use Coppel\Yelu\BaseModel;

class Item extends BaseModel
{
    public function __construct()
    {

    }
}
```

De acuerdo al modelo **MVC**, deberemos poder cargar un modelo desde los controladores, para ello vamos a crear un nuevo método protegido de nombre `getModel` en la clase `BaseController` el cual debe aceptar un parámetro de nombre `$modelName`.

Recordemos que para cargar un controlador hicimos uso del namespace al que pertenecen los controladores, para los modelos haremos lo mismo. Hay que configurar el namespace para los modelos dentro de la configuración de namespaces.

```php
<?php

return [
    "controller" => "Coppel\\Controllers\\",
    "model" => "Coppel\\Models\\"
];
```

También deberemos agregarlo a la configuración de composer y posteriormente ejecutar el comando `composer dump-autoload`, el valor que vamos a agregar es `"Coppel\\Models\\": "src/models/"`.

Ahora vamos a cargar el modelo de una manera similar a como cargamos los controladores.

```php
protected function getModel($modelName)
{
    $model = Yelu::$config->namespaces->model . $modelName;

    return new $model();
}
```

Y en el método `listPage` del controlador `Item` cargamos el modelo.

```php
public function listPage()
{
    $itemModel = $this->getModel('Item');

    $this->render('items/list');
}
```

## Obteniendo los artículos

En el modelo `Item` vamos a agregar un nuevo método público de nombre `getItems` el cual deberá retornar un arreglo con todos los artículos que cuente la tabla `items` de la base de datos `shoppingcart`.

```php
public function getItems()
{
    $dbh = $this->getConnection();

    $sth = $dbh->query('SELECT * FROM items;');

    return $sth->fetchAll();
}
```

Y este método lo vamos a llamar desde el modelo que acabamos de cargar en el controlador para mostrar la información como salida.

```php
public function listPage()
{
    $itemModel = $this->getModel('Item');

    $items = $itemModel->getItems();

    var_dump($items);

    $this->render('items/list');
}
```

Si recargamos el navegador veremos que aparecerá el arreglo con toda la información en la página. Y si revisamos el código fuente veremos que nuevamente tenemos una situación similar a la de cuando intentábamos mostrar el contenido de la vista en cierta parte del contenido del layout.

```html
array(100) {
  [0]=> ...
}
<!DOCTYPE html>
<html>
  <head>
```

Entonces necesitamos mostrar el contenido del arreglo en cierta parte dentro de la vista que estamos utilizando, para ello deberemos de realizar lo mismo que hicimos para el layout, almacenar el contenido en una variable y pasarla como variable de contexto para la vista.

Vamos a modificar el método `render` de la clase `BaseController` y agregar el parámetro `$locals` y de valor predeterminado asignaremos un arreglo vacio.

```php
protected function render($view, $locals = [])
{
    $context = [];

    $context['content'] = $this->internalRender($view, $locals);

    echo $this->internalRender(Yelu::$config->layout, $context);
}
```

Ahora deberemos de enviar el resultado del módelo como variable de contexto a la vista que estamos utlilzando.

```php
public function listPage()
{
    $itemModel = $this->getModel('Item');

    $items = $itemModel->getItems();

    $this->render('items/list', [
        'items' => $items
    ]);
}
```

Como le hemos asignado el nombre `items` en la vista deberemos de utilizar el mismo nombre para imprimir su valor.

```php
<h1>Lista de artículos</h1>

<?php

var_dump($items);

?>
```

Ahora si refrescamos la página en el navegador podremos ver que la información sigue apareciendo pero ahora se encuentra después del título de la página.

## Variables de contexto predeterminadas

Antes de proceder a darle un formato a todo el contenido que hemos obtenido de la base de datos vamos a definir unas variables de contexto que tomaran un valor predeterminado si no las especeficamos, un ejemplo de ellas es una variable que va a contener el titulo de la pagina actual. Vamos a crear un nuevo archivo de configuración de nombre `Context.php` y en el vamos a definir las variables de contexto.

```php
<?php

return [
    "title" => "Shopping Cart"
];
```

Igualmente vamos a agregarlo a la configuración inicial.

```php
<?php

return [
    "baseDir" => dirname(__DIR__),
    "viewsDir" => "./src/views/",
    "layout" => "layout",
    "namespaces" => require_once "./src/config/Namespaces.php",
    "routes" => require_once "./src/config/Routes.php",
    "database" => require_once "./src/config/Database.php",
    "context" => require_once "./src/config/Context.php"
];
```

El funcionamiento que las variables de contexto predeterminadas van a tener es el siguiente: si una variable de contexto predeterminada existe, esta será pasada solamente al layout y no a las vistas como tal, si al mostrar una vista especificamos una variable de contexto que tenga exactamente el mismo nombre que una variable de contexto predeterminada el contenido de esta será reemplazado por el valor de la variable de contexto de la vista. Por ejemplo, definimos una variable de contexto predeterminada con el nombre `title` la cual tiene un valor de `Shopping Cart`, pero si al mostar una vista especificamos también una variable de contexto con el nombre `title` el valor de la variable de contexto predetarminada será reemplazado por el valor de la variable de contexto de la vista.

> **Como esto puede prestarse a confusiones y posiblemente a comportamientos inesperados es recomendable nombrar las variables de contexto predeterminadas con un nombre no tan común, por ejemplo, iniciarlas con un guión bajo.**

```php
protected function render($view, $locals = [])
{
    $context = [];

    $context = array_merge((array)Yelu::$config->context, $locals);

    $context['content'] = $this->internalRender($view, $locals);

    echo $this->internalRender(Yelu::$config->layout, $context);
}
```

La función `array_merge` toma dos arreglos, si algúna llave del primer arreglo existe en el segundo el valor retornado será reemplazado por el valor del segundo arreglo. Las llaves que no existan en el segundo arreglo serán retornadas como tal. Con esto podemos agregar tantas variables de contexto predeterminadas como necesitemos.

## Agregando un estilo a la información

La información que estamos mostrando en el listado de productos hasta el momento no representa nada, por cada uno de los productos que tenemos en el arreglo vamos a crear un recuadro en donde mostraremos el nombre, descripción y precio del producto.

Hay que editar la vista `items/list.php` y agregamos lo siguiente:

```php
<div class="col-md-12">

  <div class="page-header">
    <h1>Productos</h1>
  </div>

  <div class="container">
    <div class="row">
      <?php
      foreach ($items as $item) {
      ?>

      <div class="col-sm-6 col-md-4">
        <div class="thumbnail">
          <div class="caption">
            <h3><?= $item['producto'] ?></h3>
            <p><?= $item['descripcion'] ?></p>
            <p>
              <span class="label label-primary">$<?= number_format($item['precio'], 0) ?></span>
            </p>
          </div>
        </div>
      </div>

      <?php
      }
      ?>
    </div>
  </div>
</div>
```

Recargamos el navegador y veremos que los productos aparecen en un recuadro con su información y el precio se encuentra dentro de un recuadro azul.

## Paginación

El mostrar todos los productos en una sola pantalla es una mala idea, la información es bastante y no hay un orden. Vamos a realizar una paginación para ir mostrando de nueve productos por cada página.

Para comenzar, el calculo del rango de productos que vamos a mostrar se puede realizar de diferentes maneras y dependiendo del manejador de base de datos que estemos utilizando puede hacerse de una manera mas fácil que en otros.

Para este caso vamos a utilizar **MySql** y hacer uso de la clausula `LIMIT` de la sentencia `SELECT` la cual acepta dos argumentos, el primero que especifica el __offset__ de la primera fila a retornar y el segundo el número máximo de filas retornar.

> **Nota:** Podemos entender **offset** como el número de fila del cual  comenzará a obtener registros.

Vamos a agregar un nuevo método público al modelo `Item` de nombre `getItemsPerPage` el cual va a solicitar dos parámetros de nombre `$start` e `$itemsPerPage` en el cual vamos a obtener la cantidad de productos que contenga el parámetro `$itemsPerPage` de manera ordenada a partir del identificador `$start`.

```php
public function getItemsPerPage($start, $itemsPerPage)
{
    $dbh = $this->getConnection();

    $sth = $dbh->prepare('SELECT id, producto, descripcion, precio FROM items LIMIT :start, :itemsperpage;');

    $sth->bindParam('start', $start, \PDO::PARAM_INT);
    $sth->bindParam('itemsperpage', $itemsPerPage, \PDO::PARAM_INT);

    $sth->execute();

    return $sth->fetchAll();
}
```

Como ven, ordenamos los productos por el campo `id`y obtenemos un rango de registros que inicia a partir del parámetro `$start` y selecciona un total que define el parámetro `$itemsPerPage`.

Hay que reemplazar el uso del método `getItems` por `getItemsPerPage` y colocaremos los valores `0` y `9` como valores de los parámetros que solicita el método para realizar una prueba.

> El método `getItems` del modelo `Item` podemos eliminarlo, ya no es necesario utilizarlo.

Si recargamos el navegador veremos que solo aparecen nueve productos y si realizamos cambios a los valores de los parámetros `$start` e `$itemsPerPage` veremos como la información cambia.

Vamos a calcular que productos mostrar dependiendo del número de página proporcionada, para ello necesitamos aplicar la siguiente regla:

El orden de los registros en **MySql** comienza en cero, podemos restar una unidad al número de página actual y multiplicar por la cantidad de registros a mostrar para obtener el número de registro inicial de la página, por ejemplo:

|Página|-1| |Registros por página|Registro inicial|
|------|--|-|--------------------|----------------|
|1     |0 |X|9                   |0               |
|2     |1 |X|9                   |9               |
|3     |2 |X|9                   |18              |
|4     |3 |X|9                   |27              |
|5     |4 |X|9                   |36              |

Necesitaremos conocer que número de página vamos a mostrar, por lo tanto vamos a solicitar un parámetro de url de nombre `page`, esto lo haremos en el método `listPage` y si el parámetro no es enviado vamos a asignarle de manera predeterminada el valor 1, lo siguiente lo agregaremos al inicio del método.

```php
$page = filter_input(INPUT_GET, 'page');

$page = $page != null ? $page : 1;
```
Ya teniendo el número de página vamos a aplicar la regla anterior definiendo el número de páginas a mostrar como nueve:

```php
public function listPage()
{
    $page = filter_input(INPUT_GET, 'page');

    $page = $page != null ? $page : 1;

    $itemModel = $this->getModel('Item');

    $itemsPerPage = 9;

    $start = ($page - 1) * $itemsPerPage;

    $items = $itemModel->getItemsPerPage($start, $itemsPerPage);

    $this->render('items/list', [
        'items' => $items
    ]);
}
```

Hay que acceder a la ruta `/items` pero ahora vamos a agregar el parámetro `page` proporcionando un valor numérico como `/items?page=1`. Veremos que aparece un mensaje como este `La ruta GET /items?page=1 NO existe!` y es por que en realidad la configuración busca por una ruta de nombre `/items?page=1`, vamos a corregir esto separando los parámetros GET de las rutas, cambiemos lo siguiente del constructor de la clase `Router`:

```php
$this->path = filter_input(INPUT_SERVER, 'REQUEST_URI');
```

por

```php
$path = filter_input(INPUT_SERVER, 'REQUEST_URI');

$this->path = isset($path) ? explode('?', $path)[0] : '/';
```

para partir la url en dos en caso de encontrarse parámetros GET en la url y obtener solo el path, si no existe el path retornamos `/` de manera predeterminada.

Recarguemos nuevamente el navegador para ver el listado de los productos y trate de cambiar el número de página para observar como el listado de productos cambia.

Hace falta agregar un método de navegación entre las páginas, por que el usuario no debería cambiar el número de página en la url manualmente para buscar mas productos, para ello necesitamos mostrar cuantas páginas existen por todos los productos. Esto puede ser en una barra inferior en la cual el usuario pueda navegar entre cada una de las páginas.

Para conocer el total de páginas primero deberíamos conocer el total de productos, hay que agregar un nuevo método al modelo `Item` el cual haga lo que necesitamos, obtener el total de productos de la base de datos.

```php
public function getTotal()
{
    $dbh = $this->getConnection();

    $sth = $dbh->query('SELECT COUNT(*) FROM items;');

    return $sth->fetchColumn(0);
}
```

Hay que llamar al método desde el controlador  `Item` y calcular el número máximo de páginas dividiendo el total de productos entre los productos por pagina, despúes pasar el resultado de la operación a la vista.

```php
public function listPage()
{
    $page = filter_input(INPUT_GET, 'page');

    $page = $page != null ? $page : 1;

    $itemModel = $this->getModel('Item');

    $totalItems = $itemModel->getTotalItems();

    $itemsPerPage = 9;

    $maxPages = ceil($totalItems / $itemsPerPage);

    error_log("Número total de páginas: $maxPages");

    $start = ($page - 1) * $itemsPerPage;

    $items = $itemModel->getItemsPerPage($start, $itemsPerPage);

    $this->render('items/list', [
        'items' => $items,
        'maxPages' => $maxPages
    ]);
}
```

>  **Nota:** utilizamos la función `ceil` para redondear el resultado fraccional de la divición hacia arriba.

Si imprimimos el valor de la variable `$maxPages` en la vista `items/list` veremos el número máximo de páginas a mostar en la terminal.

```php
<?php echo "Número total de páginas: $maxPages"; ?>
```

Teniendo el número de páginas podemos crear la barra de navegación de la siguiente manera agregandolo despues del elemento `div` que cuenta con la clase `row`:

```html
<div class="row">
 <nav class="text-center">
   <ul class="pagination">
   <?php for ($i=1; $i <= $maxPages; $i++) { ?>
     <li>
       <a href="/items?page=<?= $i ?>"><?= $i ?>
       </a>
     </li>
   <?php } ?>
   </ul>
 </nav>
</div>
```

También deberiamos resaltar el número de página activa, hay que agregar el número de página a las variables de contexto.

```php
$this->render('items/list', [
   'items' => $items,
    'maxPages' => $maxPages,
    'currentPage' => $page
]);
```

Por cada elemento `li` validaremos si el número de página a imprimir es el actual, y si es asi, agregaremos la clase `active` al elemento.

```html
<div class="row">
  <nav class="text-center">
    <ul class="pagination">
    <?php
    for ($i=1; $i <= $maxPages; $i++) {
    ?>
      <li<?= $i == $currentPage ? ' class="active"' : ''; ?>>
        <a href="/items?page=<?= $i ?>"><?= $i ?>
        </a>
      </li>
    <?php
    }
    ?>
    </ul>
  </nav>
</div>
```

## Una vista mas llamativa

Vamos a copiar las imágenes al directorio `assets/images` y editaremos la vista `items/items.php` para agregar la imagen correspondiente a cada producto.

```html
<div class="col-sm-6 col-md-4">
 <div class="thumbnail">
   <div class="caption">
     <img src="/assets/images/<?= $item['id'] ?>.jpg" alt="" />
     <h3><?= $item['producto'] ?></h3>
     <p><?= $item['descripcion'] ?></p>
     <p>
       <span class="label label-primary">$<?= number_format($item['precio'], 0) ?></span>
     </p>
   </div>
 </div>
</div>
```

Además agregaremos lo siguiente al archivo `CSS` `assets/css/shoppingcart.css` para hacer que la imagen tenga un ancho fijo, el titulo tenga una altura fija y la descripción no sobrepase una altura que haga perder la alineación entre los productos.


```css
.thumbnail .caption h3 {
    min-height: 53px;
    max-height: 53px;
}

.thumbnail .caption p.description {
    position: relative;
    height: 15.7em;
    overflow: hidden;
}

.thumbnail .caption p.description:after {
  content: "";
  text-align: right;
  position: absolute;
  bottom: 0;
  right: 0;
  width: 70%;
  height: 1.2em;
  background: linear-gradient(to right, rgba(255, 255, 255, 0), rgba(255, 255, 255, 1) 50%);
}
```

También vamos a editar la vista `home.php` para agregar un enlace directo a la búsqueda de productos.

```html
<div class="col-md-12">
    <div class="jumbotron">
        <h1>Bienvenido</h1>
        <p>
          Comienze a buscar productos ingresando a <a href="/items">nuestro extenso catálogo</a>.
        </p>
    </div>
</div>
```

# Cuentas de usuario

Uno de los objetivos principales del proyecto es permitirle al usuario __realizar compras__, por lo cual es necesario que tengamos registrada la información del usuario que va a comprar. Para ello haremos un registro e inicio de sesión de usuario, donde solicitaremos un nombre de usuario y contraseña con los cuales identificaremos al usuario que se encuentra navegando en el sitio.

Hay que crear un controlador de autenticación de nombre `Authentication.php` el cual contendrá una clase de nombre `Authentication` y un método de nombre `registerPage` en el cual vamos a cargar una vista de nombre `auth/register`.

```php
<?php

namespace Coppel\Controllers;

use Coppel\Yelu\BaseController;

class Authentication extends BaseController
{
    public function __construct()
    {

    }

    public function registerPage()
    {
        $this->render('auth/register');
    }
}
```

El contenido de la vista es el siguiente:

```html
<div class="col-md-2"></div>
<div class="col-md-6">
  <container>
    <row>
      <h2 class="text-center">Registrar</h2>
      <form class="form-horizontal" action="/auth/new" method="POST">
        <div class="form-group">
          <label class="col-sm-4 control-label">Usuario</label>
          <div class="col-sm-8">
            <input class="form-control" type="text" name="usuario" maxlength="32" />
          </div>
        </div>
        <div class="form-group">
          <label class="col-sm-4 control-label">Nombre</label>
          <div class="col-sm-8">
            <input class="form-control" type="text" name="nombre" maxlength="60" />
          </div>
        </div>
        <div class="form-group">
          <label class="col-sm-4 control-label">Contrase&ntilde;a</label>
          <div class="col-sm-8">
            <input class="form-control" type="password" name="password" maxlength="64" />
          </div>
        </div>
        <div class="form-group">
          <label class="col-sm-4 control-label">Repetir contrase&ntilde;a</label>
          <div class="col-sm-8">
            <input class="form-control" type="password" name="password2" maxlength="64" />
          </div>
        </div>
        <div class="form-group">
          <div class="col-sm-4"></div>
          <div class="col-sm-8">
            <button class="btn btn-primary btn-block" type="submit">Registrar</button>
          </div>
        </div>
        <div class="pull-right">
          <a href="/auth/login">¿Iniciar sesi&oacute;n?</a>
        </div>
      </form>
    </row>
  </container>
</div>
<div class="col-md-4"></div>
```


Ahora, para poder mostrar esa vista es necesario configurar la ruta agregando lo siguiente:

```php
[
 "method" => "GET",
    "path" => "/auth/register",
    "handler" => [
        "class" => "Authentication",
        "method" => "registerPage"
    ]
]
```

Si ingresamos en el navegador la ruta `/auth/register` podremos ver que para registrar un usuario estamos solicitando su nombre de usuario, nombre y contraseña, y si nos fijamos en el código fuente veremos que el formulario enviará los datos la ruta `/auth/new` con el método `POST`, vamos a crear esa ruta en la configuración y crearemos el método `newAction` en el controlador `Authentication`.

```php
[
 "method" => "POST",
    "path" => "/auth/new",
    "handler" => [
        "class" => "Authentication",
        "method" => "newAction"
    ]
]
```

En el método `newAction` necesitamos obtener los datos de los campos del formulario y validar si fueron eviados.

```php
public function newAction()
{
    $usuario = filter_input(INPUT_POST, "usuario");
    $nombre = filter_input(INPUT_POST, "nombre");
    $password = filter_input(INPUT_POST, "password");
    $password2 = filter_input(INPUT_POST, "password2");

    if ($usuario != false && $nombre != false && $password != false && $password2 != false) {
        echo "Todos los datos fueron enviados";
        return;
    }

    echo "Faltan campos por enviar";
}
```

## Sesiones y persistencia de datos

Si en la pantalla de registro enviamos el formulario sin llenar todos los campos deberiamos de ver el mensaje `Faltan campos por enviar` en la pantalla, solo el mensaje sin ningúna vista, lo correcto seria redirigir a la ruta de registro y mostrar el mensaje. Para poder reelizar esto podemos agregar en el controlador base un método que nos sirva para redirigir a otra ruta como el siguiente:

```php
protected function redirect($uri)
{
    header("Location: $uri");
    exit(0);
}
```

Entonces, en lugar de mostrar el mensaje hay que redirigir a la ruta `/auth/register`:

```php
$this->redirect('/auth/register');
```

Entonces, si enviamos el formulario con algún campo vacio el navegador deberia de redirigirnos hacia la pantalla de registro, pero hace falta mostrar un mensaje en el que mostremos que faltaron campos por enviar. Para poder realizar esto es necesario habilitar o iniciar el uso de sesiones en PHP.

Hay que editar el método `start` de la clase `Render` en el framework y agregar al inicio del método la función `session_start()`. Con esto en cada petición iniciaremos el uso de las sesiones.

Con esto podemos utilizar la variable superglobal `$_SESSION` para preservar la información entre peticiones.

Vamos a agregar el mensaje de validación cuando hagan falta datos por enviar y lo asignaremos al arreglo de sesión con el nombre `message` y en el método `registerPage` vamos a verificar si existe la llave `message` en el arreglo de sesiones, de ser así hay que mostrarlo.


```php
<?php

namespace Coppel\Controllers;

use Coppel\Yelu\BaseController;

class Authentication extends BaseController
{
    public function __construct()
    {

    }

    public function registerPage()
    {
        if (isset($_SESSION['message'])) {
            $data = $_SESSION['message'];
            echo $data;
        }

        $this->render('auth/register');
    }

    public function newAction()
    {
        $usuario = filter_input(INPUT_POST, "usuario");
        $nombre = filter_input(INPUT_POST, "nombre");
        $password = filter_input(INPUT_POST, "password");
        $password2 = filter_input(INPUT_POST, "password2");

        if ($usuario != false && $nombre != false && $password != false && $password2 != false) {
            echo "Ok";
            return;
        }

        $_SESSION['message'] = 'Es necesario especificar todos los campos';
        $this->redirect('/auth/register');
    }
}
```

Si realizamos la prueba nuevamente, enviar el formulario sin llenar todos los campos, veremos que el mensaje se muestra en la página, pero en el código fuente  aparece fuera del contexto del código HTML, hay que pasarlo por las variables de contexto y mostrarlo en una sección en la página.

```php
public function registerPage()
{
    $locals = [];

    if (isset($_SESSION['message'])) {
        $locals['message'] = $_SESSION['message'];
    }

    $this->render('auth/register', $locals);
}
```

Dentro de la vista `/auth/register` vamos a validar si la variable `$message` existe y si es así mostraremos el mensaje en un recuadro de alerta. Lo siguiente hay que agregarlo despues de la rtiqueta de titulo `h2`.

```php
<?php
if (isset($message)) {
?>
<div class="alert alert-warning"><i class="glyphicon glyphicon-warning-sign"></i> <?= $message ?></div>
<?php
}
?>
```

> **Si nos fijamos bien, despues de enviar el formulario con datos faltantes, cada que ingresemos a la página de registro veremos el mensaje. El mensaje no desaparece por que el valor se mantiene hasta que lo eliminemos o lo desasignemos, o hasta que el servidor web sea reiniciado.**

Para evitar lo anterior hay que desasignar el mensaje después de obtener su valor.

```php
public function registerPage()
{
    $locals = [
        "title" => "Registro de nuevo usuario"
    ];

    if (isset($_SESSION['message'])) {
        $locals['message'] = $_SESSION['message'];
        unset($_SESSION['message']);
    }

    $this->render('auth/register', $locals);
}
```

Ahora que ya podemos contar con información de manera persistente vamos agregar una validacion, hay que validar que las contraseñas que son enviadas coincidan, en caso contrario enviaremos un mensaje y redirigiremos a la página de registro.

```php
if ($usuario != false && $nombre != false && $password != false && $password2 != false) {

    if ($password != $password2) {
        $_SESSION['message'] = "Las contrase&ntilde;as no coinciden";
        $this->redirect('/auth/register');
    }

    echo "Ok";
    return;
}
```

## Encriptando datos

Ya teniendo la información que necesitamos vamos a aplicar un método de encriptación a la contraseña proporcionada para no almacenarla tal cual es ingresada.

```php
$hash = password_hash($password, PASSWORD_BCRYPT);

error_log("El password es $hash");
```

Veremos que la contraseña una vez encriptada tendrá una forma similiar a `$2y$10$vXfTVJ.J3sY6noTQzRBTuekWjGQg6QJtY7f50rNpeTaP8b/MWMQzG`. Nada que ver con la contraseña proporcionada.


## Modelo de usuario

Vamos a crear un nuevo modelo de nombre `User` el cual se encargará de implemetar las acciones de registro e inicio de sesión de usuario.

```php
<?php

namespace Coppel\Models;

use Coppel\Yelu\BaseModel;

class User extends BaseModel
{
    public function __construct()
    {

    }
}
```

Y dentro de el crearemos un metodo en el cual vamos a registrar al usuario solicitando los datos de usuario para ser llamado desde del controlador `Authentication`.


```php
public function register($usuario, $hash, $nombre)
{
    $dbh = $this->getConnection();

    $sth = $dbh->prepare("INSERT INTO usuarios (usuario, nombre, hash) VALUES(:usuario, :nombre, :password)");

    $sth->bindParam("usuario", $usuario, \PDO::PARAM_STR);
    $sth->bindParam("nombre", $nombre, \PDO::PARAM_STR);
    $sth->bindParam("password", $hash, \PDO::PARAM_STR);

    $sth->execute();

    return $dbh->lastInsertId();
}
```

```php
public function newAction()
{
    $usuario = filter_input(INPUT_POST, "usuario");
    $nombre = filter_input(INPUT_POST, "nombre");
    $password = filter_input(INPUT_POST, "password");
    $password2 = filter_input(INPUT_POST, "password2");

    if ($usuario != false && $nombre != false && $password != false && $password2 != false) {
        if ($password != $password2) {
            $_SESSION['message'] = "Las contrase&ntilde;as no coinciden";
            $this->redirect('/auth/register');
        }

        $hash = password_hash($password, PASSWORD_BCRYPT);

        $userModel = $this->getModel('user');

        $userModel->register($usuario, $hash, $nombre);

        echo "Usuario registrado correctamente";

        return;
    }

    $_SESSION['message'] = 'Es necesario especificar todos los campos';
    $this->redirect('/auth/register');
}
```


Ahora vamos a crear un nuevo método publico en el controlador `Authentication` de nombre `loginPage` el cual mostrará una nueva vista de nombre `auth/login` y deberá estár configurado con la ruta `/auth/login`.

```php
public function loginPage()
{
    $this->render('auth/login');
}
```


```php
public function loginPage()
{
    $this->render('auth/login');
}
```

```php
[
    "method" => "GET",
    "path" => "/auth/login",
    "handler" => [
        "class" => "Authentication",
        "method" => "loginPage"
    ]
]
```

La vista tendrá lo siguiente:

```html
<div class="col-sm-4">
</div>
<div class="col-sm-4">
  <h2 class="text-center">Iniciar sesi&oacute;n</h2>
  <?php
  if (isset($message)) {
  ?>
  <div class="alert alert-warning"><i class="glyphicon glyphicon-warning-sign"></i><?= $message?></div>;
  <?php
  }
  ?>
  <form method="POST" action="/auth/authenticate" class="form-horizontal">
    <div class="form-group">
      <label class="control-label">Usuario</label>
      <input class="form-control" type="text" name="username" />
    </div>
    <div class="form-group">
      <label class="control-label">Contrase&ntilde;a:</label>
      <input class="form-control" type="password" name="password" />
    </div>
    <div class="form-group">
      <button class="btn btn-primary btn-block" type="submit">Iniciar sesi&oacute;n</button>
    </div>
    <div class="pull-right">
      <a href="/auth/register">¿Registrarse?</a>
    </div>
  </form>
</div>
<div class="col-sm-4">
</div>
```

Con esta vista el usuario podrá iniciar sesión y deberemos crear un nuevo método publico en el controlador `Authentication` de nombre `authenticateAction` para obtener los datos de inicio de sesión y validar que existan en la base de datos.


```php
[
    "method" => "POST",
    "path" => "/auth/authenticate",
    "handler" => [
        "class" => "Authentication",
        "method" => "authenticateAction"
    ]
]
```

En el modelo usuario agregaremos un nuevo método publico de nombre `getDataByUsername`.

```php
public function getDataByUsername($username)
{
    $dbh = $this->getConnection();

    $sth = $dbh->prepare("SELECT id, usuario, nombre, hash FROM usuarios WHERE usuario = :usuario");

    $sth->bindParam("usuario", $username, PDO::PARAM_STR);
    $sth->execute();

    return $sth->fetch();
}
```


```php

```

```php

```

```php

```

```php

```




# Implementando sesiones

PHP tiene soporte para el manejo y administración de sesiones la cual es una manera de preservar cierta información a través de accesos subsecuentes. Esto permite construir aplicaciones mas personalizadas e incrementar la experiencia de navegación.
