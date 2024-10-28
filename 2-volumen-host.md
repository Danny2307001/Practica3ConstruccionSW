# VOLUMEN TIPO HOST
Un volumen host (o bind mount) es un tipo de volumen donde se monta un directorio o archivo específico del sistema de archivos del host en un contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](img/directorio.PNG)

### Crear un volumen tipo host con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](img/volumen-host.PNG)
```
docker run -d --name Con_nginx -p 8080:80 -v C:\Users\USER\Desktop\ConstruccionSW\Practica3\nginx\html:/usr/share/nginx/html nginx:alpine
```
### ¿Qué sucede al ingresar al servidor de nginx?
Al ingresar al servidor de nginx mediante http://localhost:8080, se presenta un mensaje de error "403 Forbidden". Este error indica que el servidor web nginx no puede mostrar el contenido esperado porque el directorio html montado está vacío

### ¿Qué pasa con el archivo index.html del contenedor?
Si el directorio html está vacío, nginx no mostrará una página de inicio hasta que agregues contenido a esa carpeta, esto significa que en lugar de ver el mensaje "403 Forbidden", verás el contenido del archivo index.html que agregaste. 

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
uego de descargar y descomprimir un template en la carpeta html, al ingresar nuevamente al servidor de nginx (http://localhost:8080), se muestra el contenido del template descargado. Es decir, la interfaz visual del diseño del template.

### Eliminar el contenedor
```
docker rm -f Con_nginx
```

### ¿Qué sucede al crear nuevamente el mismo contenedor con volumen de tipo host a los directorios definidos anteriormente?
Al crear nuevamente el contenedor con el volumen html, nginx mostro el mismo contenido del template descargado previamente, sin cambios.

### ¿Qué hace el comando pwd?
El comando pwd muestra la ruta completa del directorio actual en el que te encuentras en la línea de comandos. Es útil para especificar rutas absolutas en el comando docker run.

Si quieres incluir el comando pwd dentro de un comando de Docker, lo puedes hacer de diferentes maneras dependiendo del shell que estés utilizando.


### Volumen tipo host usando PWD y PowerShell
```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v ${PWD}/<ruta relativa>:<ruta absoluta> <nombre imagen>:<tag> 
```

### Volumen tipo host usando PWD (Git Bash)

```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v $(pwd -W)/html:/usr/share/nginx/html <nombre imagen>:<tag> 
```

### Volumen tipo host usando PWD (en Linux)

```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v $(pwd)/html:/usr/share/nginx/html <nombre imagen>:<tag> 
```

