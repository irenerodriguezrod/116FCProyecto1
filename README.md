# Fundamentos de contenerización

## Actividad 1. Servidor Web Simple con Nginx

- **Paso 1.** Construir la imagen con el mismo nombre que el repositorio con la versión 1.0
    ```
    sudo docker image build --tag 116fcproyecto1:1.0 .
    ```

- **Paso 2.** Ejecutar el contenedor en el puerto 80, 116fcproyecto1
    ```
    sudo docker container run -d -p 80:80 --name 116fcproyecto1 116fcproyecto1:1.0
    ```

- **Paso 3.** Comprobación: http://localhost
    ```
    http://localhost
    ```
    * Comprobación opcional desde consola
    ```
    sudo docker container ls
    ```

- **Paso 4.** Se pide modificar el fichero `index.html` desde el contenedor
    * Entramos al contenedor con el siguiente comando (a partir de aquí se usarán comandos bash)
        ```
        sudo docker exec -it 116fcproyecto1 bash
        ```
    * Actualizamos la terminal 
        ```
        apt update
        ```
    * Instalamos un editor de texto, en este caso nano
        ```
        apt install nano
        ```
    * Abrimos el editor que acabamos de instalar 
        > **[!CAUTION]**
        > Ojo: cualquier cambio dentro del contenedor se pierde si lo paras y eliminas. Si quieres que el cambio se mantenga, lo mejor es editar el archivo `index.html` fuera del contenedor y luego reconstruir la imagen.
        ```
        nano /usr/share/nginx/html/index.html 
        ```
    * Una vez hayamos finalizado, salimos del contenedor
        ```
        exit
        ```

### Guardar la imagen para poder utilizarla más adelante (Docker Hub)
- **Paso 1.** Crear una imagen a partir del contenedor creado.
    ```
    docker commit 116fcproyecto1 116fcproyecto1:1.0
    ```
    > **[!WARNING]** 
    >El primer nombre es el del contenedor, el segundo es el nombre de la imagen junto con la versión utilizada.

- **Paso 2.** Verificar que la imagen se ha creado correctamente
    ```
    docker images
    ```

- **Paso 3.** Guardar la imagen como un archivo (En caso de querer guardar la imagen como un archivo `.tar`)
    ```
    docker save -o 116fcproyecto1version1.tar 116fcproyecto1:1.0
    ```
    > **[!IMPORTANT]**
    > Para importar la imagen que acabamos de crear en otro Sistema Operativo
    ```
    sudo docker load -i 116fcproyecto1version1.tar
    ```

### Subir imagen a Docker Hub
- **Paso 1.** Iniciar sesión en Docker Hub (Se abrirá una ventana en el navegador web pidiendo confirmación)
    ```
    docker login
    ```

- **Paso 2.** Etiquetar la imagen para asociarla con la cuenta de Docker Hub
    ```
    sudo docker tag 116fcproyecto1:1.0 irenerodriguez/116fcproyecto1:1.0
    ```

- **Paso 3.** Subir la imagen a Docker Hub
    ```
    sudo docker push irenerodriguez/116fcproyecto1:1.0
    ```
    > **[WARNING]** 
    > Si no existe un repo en DockerHub, da el error `denied: requested access to the resource is denied`. En caso de que el error persista, puede ser porque el login no está bien hecho (Volver a realizar el paso 1).

* [LINK AL PROYECTO EN DockerHub](https://hub.docker.com/r/irenerodriguez/116fcproyecto1)

**Última actualización: lunes 07 de abril de 2025**