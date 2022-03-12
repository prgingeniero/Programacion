





## js









### Estructuras de control

| Código                                                       | Denominación                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **`if(condición) {   código true }else {   código false}`**  | [Estructura de control condicional](https://www.w3schools.com/js/js_if_else.asp) |
| **`(condición) ? valor_true : valor_false`**                 | [Operador de control condicional](https://www.w3schools.com/js/js_comparisons.asp) |
| **`switch(expresión) {  case condición_1:   código condición_1   [break;]  …  case condición_n:   código condición_n   [break;]  default:   código default}`** | [Estructura de control condicional basada en la evaluación del valor de una expresión](https://www.w3schools.com/js/js_switch.asp) |
| **`for(ini; condición; actualización){  código bucle}`**     | [Bucle condicional](https://www.w3schools.com/js/js_loop_for.asp) |
| **`while(condición) {  código bucle}`**                      | [Bucle incondicional](https://www.w3schools.com/js/js_loop_while.asp) |
| **`do {  código bucle} while(condicion)`**                   | [Bucle incondicional](https://www.w3schools.com/js/js_loop_while.asp) |
| **`break`**                                                  | [Salida de un bloque de código](https://www.w3schools.com/js/js_break.asp) |
| **`continue`**                                               | [Parada de la ejecución de un bucle para volver a evaluar la condición de parada](https://www.w3schools.com/js/js_break.asp) |
| **`try {  código js}catch(err) {  código que gestiona el error}finally {  código a ejecutar haya o no error}`** | [Captura y gestión de errores en el código](https://www.w3schools.com/js/js_errors.asp) |

### Operadores

| Operador                                                     | Denominación                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **`=`**                                                      | Asignación                                                   |
| **`+, -, \*, /, %`**                                         | [Operadores aritméticos](https://www.w3schools.com/js/js_arithmetic.asp) (actúan sobre valores numéricos) |
| **`++, --`**                                                 | [Incremento, decremento](https://www.w3schools.com/js/js_arithmetic.asp) |
| `**+=, -=, \*=, /=, %=** `                                   | [Operación aritmética + Asignación](https://www.w3schools.com/js/js_assignment.asp) |
| **`+, +=`**                                                  | Concatenación de Strings                                     |
| **`==, !=, >, <, >=, <=`**                                   | [Comparadores de valor](https://www.w3schools.com/js/js_comparisons.asp) |
| `**===** (igual valor e igual tipo)**!==** (distinto valor y distinto tipo)` | [Comparadores de valor y tipo](https://www.w3schools.com/js/js_comparisons.asp) |
| **`&&, ||, !`**                                              | [Operadores lógicos](https://www.w3schools.com/js/js_comparisons.asp) |



```html
<html>
<head>
    <script>
        var a = 3;
        
        function mostrarVariable(valor) {
            alert(valor);   // Aquí mostramos el valor que recibe como parámetro
            alert(a);       // Aquí, el valor de la variable global
        }
    </script>
</head>
<body>
    Ejemplo sencillo de uso de <i>JavaScript</i>
    <input type="button" value="Pulsar..." onclick="mostrarVariable(a)" />
    
    <script>
        alert(a);
        a = 5;
    </script>
</body>
</html>
```



La secuencia de acciones realizadas por el intérprete *JavaScript* al interpretar este código es:

- Crear una variable *a* y asignarle el valor numérico 3.*
  *
- Crear una función *mostrarVariable* que queda a la espera de ser invocada.
- Invocar a la función *alert* para mostrar el valor actual de *a*.
- Cambiar el valor de *a* asignándole el valor numérico 5.

¿Cuándo se invoca la función que hemos creado? En este caso, al  pulsar el botón que hemos añadido en el cuerpo del documento. Para ello  utilizamos su atributo *onclick*, en el que se indica el código *JavaScript* a ejecutar al "hacer clic" sobre el elemento. Lo que en realidad  estamos haciendo con esa definición es asociar una funcionalidad a un  evento, pero de momento no debes preocuparte por ello, en las siguientes secciones trataremos los eventos HTML en detalle.

## eventos



Estos son algunos de los eventos HTML que más habitualmente se  procesan en las aplicaciones web. Aunque procesando estos eventos  podrías desarrollar cualquier aplicación web típica, como ya sabes,  puedes encontrar la lista completa de eventos HTML en la [documentación de referencia de la W3C](https://www.w3schools.com/tags/ref_eventattributes.asp). Recuerda que para procesar un evento tienes que dar valor a la  propiedad correspondiente en el elemento HTML, por ejemplo, para  procesar el evento click debes fijar la propiedad *onclick*:

- *click*: se produce cuando el usuario hace click sobre el elemento HTML.
- *mouseover*: se produce cuando el usuario entra con el ratón dentro del elemento HTML.
- *mouseout*: se produce cuando el usuario sale con el ratón del elemento HTML.
- *focus*: se produce cuando el elemento HTML recibe el foco.
- *blur*: se produce cuando el elemento HTML pierde el foco.
- *change*: se produce cuando el valor del elemento HTML cambia (para <*input*>, <*select*> y <*textarea*>).
- *keydown/keypress*: se producen cuando el usuario presiona  una tecla estando dentro del elemento HTML. Aunque realmente son eventos distintos, en la mayoría de las ocasiones se pueden considerar  equivalentes.
- *keyup*: se produce cuando el usuario suelta una tecla estando dentro del elemento HTML.
- *submit*: se produce cuando se hace el submit de un formulario (para <*form*>).
- *load*: se produce cuando finaliza la carga del elemento HTML. Típicamente se utiliza para validar la carga del documento.
- *unload*: se produce cuando se descarga la página (para <*body*>).
- *error*: se produce cuando se produce un error al cargar un fichero externo.

A continuación, podéis ver un ejemplo ilustrativo de cómo vincular código *JavaScript* con alguno de estos eventos. El fichero [eventos.html](https://courses.edx.org/asset-v1:UAMx+WebApp+1T2019a+type@asset+block/eventos.html) contiene el código con el que se trabaja.



# Introducción a AJAX

La clave de todo este proceso de **llamadas asíncronas** en segundo plano al servidor es el objeto ***XMLHttpRequest\***. Al tratarse de un objeto *JavaScript*, la sintaxis para crearlo dentro de nuestro código JS es:

```
xmlhttp=new XMLHttpRequest();
```

Una vez instanciado, ofrece dos métodos para hacer una petición al servidor:

- ***open(tipo, url, asíncrona)***: Permite configurar los datos de la petición. En cierta medida, podemos considerar que la configuración de la llamada es análoga a la especificación de los datos de envío de un formulario  en el documento HTML. El tipo de petición (atributo *type* del elemento <*form*>) podrá ser "GET" o "POST". En el parámetro *url* indicaremos la url del servicio encargado de procesar la petición en el servidor (atributo *action* del elemento <*form*>). Y el tercer parámetro, sin equivalencia en el caso de un formulario en  el que las peticiones al servidor conllevan la carga síncrona de un  nuevo documento, es el indicador de si la petición debe procesarse de  forma asíncrona (*true*) o síncrona (*false*). Cuidado que es un indicador de asincronismo, no de sincronismo, lo que en ocasiones suele inducir a error a los desarrolladores.

- **send([query_string])**

  : Realiza el 

  envío de la petición al servidor

  . Si no se le pasan parámetros, se realiza una petición GET en la que los parámetros de la llamada se han debido informar como 

  query string

   en la url indicada en la llamada al método 

  open

  . Para peticiones POST, el método 

  send

   recibe un 

  query string

   con los parámetros que enviar al servidor (p.ej.,  "param1=valor1&param2=valor2"). En este último caso, para que los  parámetros se envíen en la cabecera HTTP en lugar de en la URL,  adicionalmente se debe incluir la siguiente línea antes del envío: 

  `xmlhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");`

Así, para realizar una petición GET asíncrona que descargue la página de acceso al sitio web de la Universidad Autónoma de Madrid, haríamos  lo siguiente:

```
xmlhttp = new XMLHttpRequest();xmlhttp.open("GET","http://www.uam.com",true);xmlhttp.send();
```

# jQuery





<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

```
$(selector).accion()
```

```
$("div#contenedor_lista input:checked").parent().hide()
```

```
$(document).ready(function() {   // Tú código irá aquí});
```

Esto se utiliza tan habitualmente que incluso existe una sintaxis abreviada para asignar funcionalidad al evento *ready()* del *document*. Lo siguiente es completamente equivalente a la asignación estándar:

```
$(function() {   // Tú código irá aquí});
```




Para reforzar los conocimientos adquiridos durante la lección 2, le recomendamos visitar los siguientes sitios: 

Página del gestor de paquetes que incluye Python

https://pypi.org 

https://realpython.com/what-is-pip/ 

https://realpython.com/pipenv-guide/ 

https://docs.scipy.org/doc/numpy-1.14.5/reference/ https://matplotlib.org 

https://www.edureka.co/blog/python-libraries/ 

https://packaging.python.org/tutorials/installing-packages/ 

https://packaging.python.org/tutorials/packaging-projects/ 

https://numpy.org/doc/stable/user/quickstart.html 

https://numpy.org/doc/stable/user/absolute_beginners.html 

https://www.geeksforgeeks.org/__init__-in-python/ 

https://www.w3schools.com/python/python_classes.asp 

https://www.w3schools.com/python/python_inheritance.asp https://es.wikipedia.org/wiki/Clase_(informática) 

https://es.wikipedia.org/wiki/Instancia_(informática) 

https://es.wikipedia.org/wiki/Constructor_(informática) 

https://www.w3schools.com/python/python_classes.asp 

https://www.w3schools.com/python/python_inheritance.asp 

https://www.programiz.com/python-programming/matrix https://matrix.reshish.com/es/multiplication.php 

https://realpython.com/python-modules-packages/#python-modules-overview 

https://www.geeksforgeeks.org/python-classes-and-objects/ 

Python Modules and Packages – An Introduction – Real Python

Python packages: How to create and import them?

Python Tutorial Python pip 

Python PIP Tutorial

pandas: powerful Python data analysis toolkit

numpy · PyPI

El Ingeniero González en cada video iba mostrando y explicando código de Python, lo mas recomendable es que usted vaya replicando el mismo. 

A continuación se comparte el código que se utilizó y explicó en los videos de lección 5 (es importante que usted ya haya instalado Python para correr este código):

Dar clic aquí para descargar código

Dar clic aquí para descargar código

Dar clic aquí para descargar código

Dar clic aquí para descargar código

Importante: el código fue creado siguiendo el siguiente formato: 

 PrintX_DIAPOSITIVAY_PZ

Donde X es el orden del programa en cuanto a que momento se utiliza, Y es la diapositiva donde se usa y Z la presentación.

