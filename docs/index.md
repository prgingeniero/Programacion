#
<center>
    <h1 style="color:Orange;">Programacion</h1>
</center>


# webscarpt


### Beautiful Soup



Como se observó en esta unidad, **BeautifulSoup** toma el  contenido de la página web y lo interpreta generando una estructura más  manejable. Si bien nos enfocaremos en las etiquetas principales, vale la pena mencionar los tipos de objetos producidos:

- **Tag**: es el objeto que nos interesa principalmente y corresponde a las etiquetas en el documento de HTML. ([documentación](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#tag))
- **NavigableString**: esta cadena de texto representa el contenido dentro de una etiqueta.  Tiene capacidades extras relacionadas con la navegación dentro de la  estructura. ([documentación](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#navigablestring))
- **BeautifulSoup**: este objeto representa el documento HTML interpretado como una  estructura jerárquica. Para fines convencionales, puede ser considerado  como objeto de tipo tag, soportando los mismos tipos de métodos. ([documentación](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#beautifulsoup))
- **Comment**: este objeto es un tipo especial de NavigatableString, que se representa con un formato especial al momento de impresión.  

En resumen, se ha descrito de forma general el funcionamiento del módulo de BeautifulSoup para, en conjunto de la herramiento de  peticiones requests, interpretar la estructura de un documento HTML. En  las siguientes unidades se expandirá la información sobre las funciones, métodos y atributos relacionados con la extracción de los datos de  interés. Sin embargo, existen propiedades y capacidades que pueden  resultar interesantes como elementos auxiliares en el árbol generado, o  notaciones abreviadas que sirven para crear un código más compacto.

------

*Referencias*:

​       

- Reitz, K. (2020). *Requests: HTTP for Humans.*
  https://docs.python-requests.org/en/master/
- Richardson, L. (2020). *Beautiful Soup Documentation.* 
  https://www.crummy.com/software/BeautifulSoup/bs4/doc/



### Iterando sobre los elementos en **Beautiful Soup**



Hasta el momento se han visto dos principales maneras de cómo se  puede utilizar el árbol jerárquico producido por BeautifulSoup con base a una página web: utilizando métodos de búsqueda, y navegando manualmente por los elementos, cada uno con sus ventajas y desventajas. Sin  embargo, podemos utilizar un enfoque intermedio entre estos dos extremos y es el de utilizar métodos de iteración sobre los elementos. De esta  forma podemos tener la ventaja de la flexibilidad de la búsqueda, pero  con el poder de ajustar la selección de los elementos de forma manual.

Para lograr este objetivo, BeautifulSoup cuenta con diferentes herramientas y métodos,siendo uno de ellos el atributo “**descendants**”. Su comportamiento es similar al de “**children**” pero no solo se limita a los elementos inmediatos, si no que enlista  todos los elementos, es decir, los hijos, los hijos de los hijos, etc.
