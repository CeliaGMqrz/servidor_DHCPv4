# Desplegando aplicaciones flask 

## Despliegue en el entorno de desarrollo

* Clonamos el repositorio 

```sh
git clone https://github.com/josedom24/flask_temperaturas.git
```

* Miramos los paquetes del fichero requirements.txt

```sh
click==6.7
Flask==0.12.2
itsdangerous==0.24
Jinja2==2.9.6
lxml==4.6.1
MarkupSafe==1.0
Werkzeug==0.12.2
```

* ¿Podríamos instalar estos paquetes con apt?

Sí pero es mejor trabajar en un entorno virtual para el control de versiones.

* ¿Sería buena idea instalar como root estos paquetes en el sistema con pip?

No, ya que podríamos causar conflictos con las dependencias de los paquetes que tenemos en el sistema.

* ¿Cómo sería la mejor manera de instalar estos paquetes?

Usando un entorno virtual.

## Trabajamos con entornos virtuales

Crea un entorno virtual con el módulo **venv** e instala en él los paquetes necesarios para que el programa funcione. Una vez instalado, ejecuta la aplicación con el servidor de desarrollo y comprueba que funciona.

* Instalamos el módulo venv con privilegios de superusuario

```sh
apt-get install python3-venv
```

* Creamos el entorno virtual 

```sh
$ python3 -m venv entorno
```

* Activamos el entorno

```sh
$ source entorno3/bin/activate
```

* Para desactivarlo

```sh
(entorno3)$ deactivate
$ 
```

* Instalamos los paquetes del fichero requirements.txt

```sh
(entorno)$ pip install -r requirements.txt
```

## Despliegue contínuo en el entorno de producción

¿Cómo podemos hacer que un servidor web como apache2 sea capaz de servir una aplicación escrita en python? Para ello se utiliza un protocolo que nos permite comunicar al servidor web con la aplicación web: **WSGI** (Web Server Gateway Interface).

Es decir, el protocolo WSGI define las reglas para que el servidor web se comunique con la aplicación web. Cuando al servidor llega una petición que tenemos que mandar a la aplicación web python tenemos al menos dos cosas que tener en cuenta:

Tenemos un fichero de entrada, es decir la petición siempre se debe enviar un único fichero., Este fichero se llama fichero WSGI.
La aplicación web python con la que se comunica el servidor web utilizando el protocolo WSGI se debe llama application. Por lo tanto el fichero WSGI entre otras cosas debe nombrar a la aplicación de esta manera.

### Configuración de apache2 para servir una aplicación web flask

* Primero instalamos el móduclo de apache2 wsgi

```sh
apt install libapache2-mod-wsgi-py3
```
* Suponemos que tenemos un servidor web apache2 con el módulo wsgi activado.

* Suponemos que nuestra aplicación se encuentra en /var/www/html/flask_temperatura. (tiene que ser en el directorio de nuestro virtualhost !!!!!!!!!!!!!!!!)

```sh
(entorno) celiagm@debian:/var/www/html/flask_temperatura$ ls
app.py  Procfile  README.md  requirements.txt  sevilla.xml  static  templates

```
* Suponemos que hemos creado un entorno virtual con los paquetes instalados en /home/debian/venv/flask.

### Creación del fichero wsgi

Lo primero que vamos a hacer es crear el fichero WSGI, que vamos a llamar app.wsgi estará en /var/www/html/flask_temperatura y tendrá el siguiente contenido:

```sh
from app import app as application
```

Veamos:

* El primer app corresponde con el nombre del módulo, es decir del fichero del programa, en nuestro caso se llama app.py.

* El segundo app corresponde a la aplicación flask creada en app.py: app = Flask(__name__).

* Importamos la aplicación flask, pero la llamamos application necesario para que el servidor web pueda enviarle peticiones.