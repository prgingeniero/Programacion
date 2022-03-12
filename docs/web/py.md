



# py



## links



- [Introduction to Python: Absolute Beginner](https://www.edx.org/es/course/introduction-to-python-absolute-beginner) (edX).
- [Introducción al desarrollo de aplicaciones web](https://learning.edx.org/course/course-v1:UAMx+WebApp+1T2019a/)(edx) ** de aqui es la documentacion

- [Curso de Python Básico Gratis](https://codigofacilito.com/cursos/Python) (Web Código Facilito).



## venv



requirements.txt

```
flask
```



```bash
pk@pk:~$ type vvvv
vvvv () 
{ 
    deactivate;
    python3.8 -m venv ./.venv;
    source ./.venv/bin/activate;
    pip install -r requirements.txt;
    python app.py
}
pk@pk:~$ 
pk@pk:~$ 

```



## flask

app.py

```python
import sys

from flask import Flask,request
app = Flask(__name__)


@app.route('/')
def index():
    user_agent = request.headers.get('User-Agent')
    return '<p>Your browser is %s</p>' % user_agent

@app.route('/processLogin', methods=['POST'])
def process_login():
       missing = []
       fields = ['email', 'passwd', 'login_submit']
       for field in fields:
              value = request.form.get(field, None)
              if value is None:
                  missing.append(field)
       if missing:
              return "Warning: Some fields are missing"

       return '<!DOCTYPE html> ' \
           '<html lang="es">' \
           '<head>' \
           '<link href="static/css/my-socnet-style.css" rel="stylesheet" type="text/css"/>' \
           '<title> Home - SocNet </title>' \
           '</head>' \
           '<body> <div id ="container">' \
           '<a href="/"> SocNet </a> | <a href="home"> Home </a> | <a href="login"> Log In </a> | <a href="signup"> Sign Up </a>' \
           '<h1>Data from Form: Login</h1>' \
           '<form><label>email: ' + request.form['email'] + \
           '</label><br><label>passwd: ' + request.form['passwd'] + \
           '</label></form></div></body>' \
           '</html>'


if __name__ == '__main__':
    if sys.platform == 'ubuntu':  
        app.run(debug=True, port=8080)
    else:
        app.run(debug=True, port=80)
```

index.html

```

```





## json



Las estructuras de JSON tienen una traducción directa a estructuras Python:

- Los objetos JSON son representados como diccionarios en Python
- Los arrays JSON son representados como listas en Python
- true y false en JSON son valores del tipo *boolean* en Python
- Las cadenas en JSON son cadenas en Python
- Los números en JSON son *float* o *integer*, según corresponda, en Python

Por este motivo, las funciones para leer y escribir ficheros JSON son muy sencillas de utilizar. En ambos casos recurrimos a la biblioteca  JSON, así que lo primero que debemos hacer es:

```
import json
```

### Lectura

La función para leer un fichero JSON es json.load. Como parámetro un fichero, así que una forma normal de usarla es:

```
with open(“nombre_fichero.json”, 'r') as f:
   data = json.load(f)
```

Después de ejecutar esto, la variable *data* contendrá un  diccionario con los datos cargados del fichero. Si por ejemplo  hubiéramos cargado el fichero con los datos del usuario *James*  visto en la sección anterior, ahora data[‘user_name’] sería “James” y  data[‘messages’] sería una lista Python con los mensajes publicados por  James.

### Escritura

Volcar una estructura Python a un fichero JSON es igual de sencillo.  Supongamos que tenemos la siguiente inicialización de la variable datos:

```
datos = {  "user_name": "James",  "password": “007”,  "messages": [(1532648502.113984, “mensaje 1”), (1532648642.729385,   “mensaje 1”)],   "email": session['email'],  "friends": session['friends']}
```

Entonces guardar los datos en el fichero correspondiente sería:

```
with open(“james.bond@mi6.uk”, 'w') as f:  json.dump(datos, f)
```







## sesiones



Ya hemos dicho en varias  oportunidades que el protocolo HTTP no tiene estado, que no recuerda.  ¿Qué significa eso en la práctica? Que necesitamos información adicional para implementar una “conversación” entre cliente y servidor. Esta idea de conversación, donde ambas partes recuerdan lo que han hablado hasta  el momento, se llama **sesión**.

Aunque el concepto o la duración de una sesión puede variar en distintos entornos, básicamente es el conjunto de interacciones entre cliente y servidor en un lapso de tiempo razonable.

La primera vez que un cliente realiza una petición, después de un tiempo sin interactuar, el servidor **abre una sesión**. Las subsecuentes peticiones desde ese cliente se consideran dentro de  la misma sesión. Si pasa mucho tiempo sin que el cliente realice una  petición, el servidor asume que ya no está conectado y termina la  sesión.

La biblioteca Flask nos ofrece este concepto de sesión. Pero si HTTP  no tiene información específica que permita identificar al usuario o la  sesión, ¿cómo sabe Flask a qué usuario corresponde una determinada  petición?

Existen al menos 3 formas de que una petición HTTP transporte información que permita identificar al usuario o la sesión:

- **Cookies**: las *cookies* son pequeños ficheros que se adjuntan a una respuesta HTTP, con información de identificación de usuario. En sucesivas peticiones HTTP, el navegador incluye ese  fichero automáticamente, por lo que el servidor podrá tener la  identificación de ese usuario.
- **Campos ocultos**: en los formularios que el servidor envía a cliente para que sean completados, incluyo un campo del tipo *input* que no se muestra al usuario; ese campo lleva información que cuando  los datos del formulario se envíen de vuelta al servidor le servirá para identificar al cliente.
- **Reescritura de URLs**: aunque nos parezcan iguales,  el servidor introduce automáticamente pequeñas modificaciones a las  URLs; de esta forma, la URL específica que solicite permitirá al  servidor identificar al cliente.

La buena noticia es que, generalmente, el mecanismo que se use para  transportar la información de sesión no es visible al desarrollador de  la aplicación web. Esto es exactamente lo que ocurre con el soporte de  sesiones que nos ofrece Flask, y que veremos a continuación.









Vamos a ver cómo podemos  manejar una sesión en Python y Flask para poder almacenar información  entre cada una de las peticiones que el cliente haga al servidor.

### Objeto Flask Session

El objeto que nos guarda la información entre sesiones se llama  session. Lo primero será importarlo dentro de nuestro código Python para luego poder usarlo:

```
from flask import Flask, session
```

Como la información de la sesión viaja del servidor al cliente ida y  vuelta, es importante que nadie en el camino, ni siquiera el propio  cliente, puedan alterar esa información. En particular, se debe evitar  que alguien de fuera “tome control” de la sesión. En seguridad  informática, este tipo de ataque se conoce como CSRF (Cross-site request forgery) o robo de sesión.

Para asegurarse que eso no ocurre, Flask utiliza técnicas de  encriptación para proteger la información. Para eso, necesita una clav  de encriptación/desencriptación. Esta clave, que sólo debe conocer el  servidor y que debe ser distinta para todos los programas servidor, se  crea en el propio código del servidor. Por ejemplo:

```
app.secret_key = 'esto-es-una-clave-muy-secreta'
```

De hecho, en el código de nuestra aplicación SocNet habrás visto una línea similar a esta:

```
app.secret_key = 'A0Zr98j/3yX R~XHH!jmN]LWX/,?RT'
```

Ahora ya sabes para qué sirve. Si quieres tener más información de  este problema de seguridad informática y su solución, puedes leer [aquí](http://flask.pocoo.org/snippets/3/).







Ahora vamos a ver ejemplo de cómo utilizamos las sesiones en nuestra aplicación favorita.

La primera función, ***load_user(email, passwd)\***, intenta cargar los datos desde un fichero.

**Importante**: aquí almacenamos los datos en un fichero por una cuestión de  simplicidad. En aplicaciones con cientos o miles de usuarios lo normal  es almacenar los datos en una base de datos propiamente dicha.

Si el fichero existe, carga los datos y a continuación comprueba que la clave suministrada coincida con la que está almacenada.

**Nota de seguridad**: otra vez, para facilitar las explicaciones y la comprensión de los  conceptos básicos, realizamos algunas simplificaciones que antes de  hacer público un sistema deben ser corregidas. Por ejemplo, nunca se  debe guardar una clave de usuario “en claro”, siempre se debe hacer  codificada con algún algoritmo como por ejemplo SHA-256. Lamentable  estas cuestiones quedan fuera del ámbito de este curso.

Si todas las condiciones son correctas, la función **guarda** los datos relevantes del usuario (nombre, mensajes que ha escrito hasta el momento, la clave, su correo electrónico y la lista de amigos) en la **sesión**, para que estén disponibles para las próxima llamadas desde el cliente.

```python
def load_user(email, passwd):
    """
    It loads data for the given user (identified by email) from the data directory.
    It looks for a file whose name matches the user email
    :param email: user id
    :param passwd: password to check in order to validate the user
    :return: content of the home page (app basic page) if user exists and password is correct
    """
    file_path = os.path.join(SITE_ROOT, "data/", email)
    if not os.path.isfile(file_path):
        return process_error("User not found / No existe un usuario con ese nombre", url_for("login"))
    with open(file_path, 'r') as f:
        data = json.load(f)
    if data['password'] != passwd:
        return process_error("Incorrect password / la clave no es correcta", url_for("login"))
    session['user_name'] = data['user_name']
    session['messages'] = data['messages']
    session['password'] = passwd
    session['email'] = email
    session['friends'] = data['friends']
    return redirect(url_for("home"))
```

De la misma forma, cuando un usuario quiere salir del sistema, debemos guardar los datos en el fichero (base de datos) para que estén disponibles la próxima vez que el  usuario vuelva a nuestra aplicación. Este es el objetivo de la función *save_current_user()*, que vuelca los datos de session en el fichero correspondiente.

Por otra parte, cuando un usuario se da de alta, se debe crear el fichero, previa comprobación que no exista un usuario con el mismo identificador (correo electrónico). Esto es lo que hace la función *create_user_file(name, email, passwd, passwd_confirmation)*.

```

```



```python
def save_current_user():
    datos = {
        "user_name": session["user_name"],
        "password": session['password'],
        "messages": session['messages'], # lista de tuplas (time_stamp, mensaje)
        "email": session['email'],
        "friends": session['friends']
    }
    file_path = os.path.join(SITE_ROOT, "data/", session['email'])
    with open(file_path, 'w') as f:
        json.dump(datos, f)


def create_user_file(name, email, passwd, passwd_confirmation):
    """
    It creates the file (in the /data directory) for storing user data. The file name will match the user email.
    If the file already exists, it returns an error.
    If the password does not match the confirmation, it returns an error.
    :param name: Name or nickname of the user
    :param email: user email, which will be later used for retrieving data
    :param passwd: password for future logins
    :param passwd_confirmation: confirmation, must match the password
    :return: if no error is found, it sends the user to the home page
    """

    directory = os.path.join(SITE_ROOT, "data")
    if not os.path.exists(directory):
        os.makedirs(directory)
    file_path = os.path.join(SITE_ROOT, "data/", email)
    if os.path.isfile(file_path):
        return process_error("The email is already used, you must select a different email / Ya existe un usuario con ese nombre", url_for("signup"))
    if passwd != passwd_confirmation:
        return process_error("Your password and confirmation password do not match / Las claves no coinciden", url_for("signup"))
    datos = {
        "user_name": name,
        "password": passwd,
        "messages": [],
        "friends": []
    }
    with open(file_path, 'w') as f:
        json.dump(datos, f)
    session['user_name'] = name
    session['password'] = passwd
    session['messages'] = []
    session['friends'] = []
    session['email'] = email
    return redirect(url_for("home"))
```



