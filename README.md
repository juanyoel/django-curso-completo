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
* Creamos el super usuario *python manage.py createsuperuser*
* En el archivo *settings.py* recordar que cuando se pasa a despliegue debemos poner la variable DEBUG en False, por defecto viene verdadero.

### PROYECTO
NOTA: Este es un curso de Django básico, recordarme que hay muchas cosas que quizás estén diferentes a como lo he visto en otros cursos, estaré contruyendo el ejemplo tal como lo dicen en el curso, aunque creo que algunas no son las mejores prácticas, supongo que al ser básico lo hacen así para aprender los fundamentos.

### CREAMOS LA PRIMERA VISTA
* Para ello creamos en la app *core* que es en la que estamos trabajando, aunque no es lo recomendado, esta app debería solo para las cosas generales de los proyectos como buena práctica, creamos un archivo *views.py*.
* Nota: Existen vistas de clases y vistas de funciones.
* Para crear la vista definimos la clase de la vista con los métodos que definamos y si vamos usar un html predefinido para ello hacemos las importaciones necesarias

![image](https://user-images.githubusercontent.com/84333525/139864587-ea2791ca-5977-4c7b-8b9a-7b6dee6c6d39.png)

* En este caso de este inicio del curso deciden crear la carpeta de las templates fuera de la app, por lo que para decirle a django dónde buscar los templates, modifican el archivo *settings.py* de la siguiente manera:

![image](https://user-images.githubusercontent.com/84333525/139864868-8204951a-a0e8-40e9-b692-ef06c6949381.png)

### PROTEGER LAS CONTRASENNAS E INFORMACION SENSIBLE
* Creamos una archivo .env dentro de la app.
* Instalamos un paquete llamado django-environ
* Nota: Esta parte del curso se encuentra a partir del minuto 55, no lo voy hacer en mi código sólo voy a observar.

### INICIAR APP DE BLOG
* Creamos el app *python manage.py startapp [nombreApp]*
* Instalamos la app en las INSTALLS_APP
* Adicionamos en el urls.py de core el código necesario para incluir las urls de la app del blog

![image](https://user-images.githubusercontent.com/84333525/139869296-cc2f71b7-ddb1-4fdd-9c93-c7438e6ede3c.png)

* Creamos el archivo de urls del blog de forma básica dónde estaremos adicionando las urls.

### CREAR LA VISTA DE LISTAR BLOG
* Creamos la vista, haciendo las importaciones pertinentes

![image](https://user-images.githubusercontent.com/84333525/139875026-9d0164b5-6f03-4537-9967-861e58528a6b.png)

### CREAR LA URL
* Se crea la url para acceder a la vista antes descrita.

### VINCULAMOS EL HTML CON LA VISTA Y LA URL

![image](https://user-images.githubusercontent.com/84333525/139875992-ed0225ee-f6b2-4c2f-afff-f096e86459e7.png)

* Me parece interesante ver este funcionamiento, en este caso analizando la url, la palabra blog hace referencia al namespace que se le definió en el archivo urls.py de core, y la palabra hombe al name del url que se encuentra en el archivo urls.py pero de la app blog.

### SOBRE MODELOS
* Los modelos nos permiten editar la información de manera dinámica, es el concepto que nos permite interactuar con la BD.
* Para ello nos ubicamos en el archivo models.py y creamos un modelo de Post básico.

![image](https://user-images.githubusercontent.com/84333525/139877763-68af3790-aff6-4546-8beb-912c86b3179e.png)

* Cada vez que trabajamos con los modelos debemos crear y correr las migraciones.
  - python manage.py makemigrations
  - python manage.py migrate

### ADMIN AREA
* Una vez creado el o los modelos, podemos visualizarlos y trabajar con ellos desde el área de administración, para ello debemos registrar los modelos con los que queremos trabajar en el archivo *admin.py*
* Importamos nuestro modelo y para registralo en el área de admin escribimos el siguiente código admin.site.register(nombreModelo)

![image](https://user-images.githubusercontent.com/84333525/139879785-09d0c36c-7ca3-4794-ab7a-17405942dfae.png)

De esta manera ya podemos trabajar con ese modelo desde el área de admin.
* En el área de admin los modelos de este tipo que creemos se visualizaran con el id generalmente y como un objeto para hacerlo humanamente leíble podemos hacer uso de la función __str__() en el modelo de la siguiente forma:

![image](https://user-images.githubusercontent.com/84333525/139880175-e6070969-9a45-4dfe-ae07-fbc0a989bc07.png)

### FORMULARIOS
* Para el uso de formularios, lo primero que debemos hacer es crear nuestro archivo forms.py en nuestra app de blog

![image](https://user-images.githubusercontent.com/84333525/139882320-d423fbb1-6a92-437b-bb78-d980e8506970.png)

- En la clase Meta le vinculamos el modelo con el formulario en el campo model y en fields es la vinculación de los campos del modelo con los del formulario, esos campos que vienen en fields son los que mostrará el formulario.

###  CREAR VISTA PARA CREAR UN POST
* Teniendo creado ya el formulario con los campos deseados además de vinculados al modelo en cuestión con el que queremos trabajar, pasamos a crear la vista, para ellos creamos una nueva clase:

![image](https://user-images.githubusercontent.com/84333525/139935616-367a6442-f4bb-40c8-8fa7-c3fbc944decc.png)

- creamos una variable form (por convención el nombre) dónde almacenaremos una instancia del formulario creado, por supuesto que para ello hay que haber importado el formulario a nuestro archivo de las vistas.
- recordamos que siempre a estos métodos se le debe pasar como argumentos self, y request obligatoriamente y que siempre debemos retornar request, la página a renderizar y el contexto, es en el contexto dónde se encuentran las respuestas de las lógicas ejecutadas por la petición al servidor, y que serán retornados al cliente.

* Modificamos el método def post() que es el que se utilizará para obtener los datos desde el formulario y guardar los mismos en la BD
  - verificamos que el método sea post, que es el mismo que se le definió al formulario en el html.
  - En caso de que el método sea post se guarda nuevamente en una variable una instancia del formulario pero esta vez se le pasa como parámetro lo que trae el request mediante request.POST como veremos en la imagen de muestra.
  - una vez obtenidos estos datos verificamos si el formulario es válido.
  - En caso de que el formulario sea válido obtenemos los datos con los que queremos trabajar, en este caso son los mismos campos que tiene el modelo Post, title y content.
  - Por último creo y salvo el post con el método save()
  - Hacemos uso del redirect para redireccionar a la página anterior

  ![image](https://user-images.githubusercontent.com/84333525/139944205-94eb391d-6084-44a0-b413-a172ca973467.png)

### CREAR LA URL
* Luego de haber al menos creado la vista, necesitamos una forma de acceder a ella desde el navegados, ahí es cuando la adicionamos a las urls de la app:

![image](https://user-images.githubusercontent.com/84333525/139939088-43460bc9-81d9-4ad8-91e2-df3ae7243650.png)

### CREAR LA PAGINA
* El código de la página es bastante sencillo y ya lo he visto antes, creo que con la imagen y viendo el código puedo entenderlo con relativa facilidad.

![image](https://user-images.githubusercontent.com/84333525/139940239-2ee82c35-a29b-444e-8fde-19b8b75a1a05.png)

### NOTA
* Siempre que se hace un formulario con Django es necesario incluirle el siguiente código *{% csrf_token %}*

### ENLISTAR LOS POST

![image](https://user-images.githubusercontent.com/84333525/139944393-557a0ace-2b2c-4151-b4cd-92818d59cdd6.png)

### DETALLES DE POST
* Para crear los detalles del post creamos una nueva vista (VIEW):

![image](https://user-images.githubusercontent.com/84333525/139949632-421a4c20-79c8-41bb-a5c9-0de36a4527cd.png)

Tener en cuenta que para obtener los detalles del elemento en cuestión lo hacemos haciendo una búsqueda por el pk. En otros cursos lo he visto por el slug.

* Como ya vimos en la vista se hace la búsqueda por el pk, por lo que el próximo paso es crear la url con la que podremos acceder a dicha vista.

![image](https://user-images.githubusercontent.com/84333525/139949871-3ac80f2b-df57-4c21-84df-3725a92fb941.png)

Tener en cuenta que todo se hace exactamente igual, a diferencia del primer parámetro, en el que se pasa el parámetro dinámico por el que estaremos accediendo a los detalles del Post. Este atríbuto siempre irá entre **<>**
* Luego creamos el archivo html en el que visualizaremos dicha información. Ya creo esto es bastante sencillo y no necesita de mucha más descripción.

## MODIFICAR Y ELIMINAR
* Está fácil de entender con solo ver el código siempre teniendo en cuenta los mismos pasos a los que estamos acostumbrados ya, en estos casos también se hace por el pk de los objestos con los cuáles se quiere trabajar.

## UI
* Los últimos 9 minutos me parecen interesante si se necesitan trabajar con el lenguaje de plantillas de Django. Se habla sobre una librería para estilizar la UI.
