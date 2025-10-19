## Esquema para el ejercicio
![Imagen](esquema-4-ejercicio.PNG)

### Crear la red
# COMPLETAR

![creacion de la red](image-14.png)

### Crear el contenedor mysql a partir de la imagen mysql:8, configurar las variables de entorno necesarias
# COMPLETAR

![creacion del contenedor mysql](image-15.png)

### Crear el contenedor wordpress a partir de la imagen: wordpress, configurar las variables de entorno necesarias
# COMPLETAR

![creacion del contenedor wordpress](image-16.png)

De acuerdo con el trabajo realizado, en el esquema del ejercicio el puerto a es **80**

Ingresar desde el navegador al wordpress y finalizar la configuración de instalación.
# COLOCAR UNA CAPTURA DE LA CONFIGURACIÓN

![configuracion del servidor wordpress](image-17.png)

Desde el panel de admin: cambiar el tema y crear una nueva publicación.
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress
# COLOCAR UNA CAPTURA DEL SITO EN DONDE SEA VISIBLE LA PUBLICACIÓN.

![publicacion con tema cambiado](image-18.png)

### Eliminar el contenedor wordpress
# COMPLETAR

![eliminacion del contenedor](image-19.png)

### Crear nuevamente el contenedor wordpress
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress

### ¿Qué ha sucedido, qué puede observar?
# COMPLETAR

![comporbacion del contenedor luego de ser eliminado](image-20.png)

El tema del sitio se mantiene y los datos persisten, pero las opciones de inicio de sesion y panel de administracion no se encuentran disponibles.
