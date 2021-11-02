# django-curso-completo
## Este proyecto hace referencia al curso **Introduccion a Django - Curso Completo**

### INSTALACION DEL AMBIENTE
* Después de tener instalado python, pip, y virtualenv, el primer paso es crear un entorno virtual para el proyecto, esto nos va a permitir tener nuestras dependencias separadas para cuando queramos escalar nuestro proyecto y compartir el código. Para ello creamos el ambiente con el comando *virtualenv env*
* Activamos el entorno con el comando activate.
* Vinculamos git con el proyecto, esto no lo había hecho así antes, creamos nuestro archivo git ignore y buscamos en la web git ignore python y se lo copiamos.
* Creamos el archivo requirements.txt, es en este archivo dónde pondremos todos nuestros paquetes.
* Para instalar los paquetes desde este archivo necesitamos utilizar -r de la siguiente manera *pip install -r requirements.txt* 
* Creamos el proyecto django *django-admin startproject [nombreProyecto] .*
* Agregamos la app a *INSTALLED_APPS* en el archivo settings.py.
* Podemos correr las migraciones, esto crearía el mecanismo necesario para la autenticación y otras funciones además en la BD. *python manage.py migrate*
* Creamos el super usuario *python manage.py createsuperuser 
