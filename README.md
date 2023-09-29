
**1. Descarga la imagen 'httpd' y comprueba que está en tu equipo**

Para descargar la imagen 'httpd' versión 2.4, utiliza el siguiente comando:

```bash
docker pull httpd:2.4
```

Puedes verificar que la imagen se ha descargado correctamente ejecutando el siguiente comando para listar las imágenes de Docker:

```bash
docker images
```

**2. Crea un contenedor con el nombre 'dam_web1'.**

Utiliza el siguiente comando para crear un contenedor con el nombre 'dam_web1', mapeando el puerto 8000 de tu máquina al puerto 80 del contenedor:

```bash
docker run -di --name dam_web1 -p 8000:80 httpd:2.4
```

**3. Si quieres poder acceder desde el navegador de tu equipo, ¿que debes hacer?.**

Para permitir el acceso desde el navegador de tu equipo, simplemente mapeaste el puerto 80 del contenedor al puerto 8000 de tu máquina en el paso anterior (-p 8000:80).

**4. Utiliza bind mount para que el directorio del apache2 'htdocs' este montado un directorio que tu elijas.**

Utiliza el siguiente comando para montar el directorio actual en tu máquina en el directorio '/usr/local/apache2/htdocs/' del contenedor:

```bash
docker run -di --name dam_web1 -p 8000:80 -v $PWD/htdocs:/usr/local/apache2/htdocs/ httpd:2.4
```

Esto garantizará que los archivos en el directorio 'htdocs' de tu máquina estén disponibles para el servidor Apache en el contenedor.

**5. Realiza un 'hola mundo' en html (usa Code) y comprueba que accedes desde el navegador.**

Utiliza tu editor de texto preferido, como Visual Studio Code, para crear un archivo 'index.html' en el directorio 'htdocs'. Asegúrate de que el archivo contiene el contenido que deseas mostrar en tu página web.

**6. Crea otro contenedor 'dam_web2' con el mismo volumen y a otro puerto, por ejemplo 9080.**

Crea un segundo contenedor llamado 'dam_web2' utilizando el mismo volumen montado y mapeando el puerto 9080 de tu máquina al puerto 80 del contenedor:

```bash
docker run -di --name dam_web2 -p 9080:80 -v "$PWD/htdocs:/usr/local/apache2/htdocs/" httpd:2.4
```

**7. Comprueba que los dos servidores 'sirven' la misma página, es decir, cuando consultamos en el navegador:**

Puedes verificar que ambos servidores sirven la misma página 'index.html' al acceder a las siguientes direcciones en tu navegador:

- http://localhost:9080
- http://localhost:8000

Ambos puertos deberían mostrar la misma página web.

**8.Realiza modificaciones de la página y comprueba que los dos servidores 'sirven' la misma página**

Edita el archivo 'index.html' en el directorio 'htdocs' utilizando tu editor de texto y guarda los cambios. Luego, actualiza tus navegadores en las direcciones anteriores:

- http://localhost:9080
- http://localhost:8000

Ambos servidores mostrarán la versión actualizada de la página 'index.html'.
