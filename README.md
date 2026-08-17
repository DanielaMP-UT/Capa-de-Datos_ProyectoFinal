# Servicio de Base de Datos 

## Descripción
Este servicio despliega una base de datos **MariaDB** usando Docker Compose, con una imagen personalizada construida desde un Dockerfile. 

## Clonar el repositorio de la siguiente URL
```https://github.com/DanielaMP-UT/Capa-de-Datos_ProyectoFinal```


### Abre la carpeta del repositorio en tu Visual Studio Code
    Capa-de-Datos_ProyectoFinal


### Configura las variables de entorno 
    Duplica el archivo **mariadb_example.env** y renómbralo a **entorno.env**
    Duplica el archivo **phpmyadmin_example.env** y renómbralo a **phpmyadmin.env**

    **Y Remplaza la información de estos archivos por la real**

## Construir y levantar los servicios con Docker Compose
    Abre una terminal en la raíz del proyecto y ejecuta los siguientes comandos:


### 1. Construir la imagen personalizada
    docker compose -f serviciosdb.yml build


### 2. Levantar los contenedores en segundo plano
    docker compose -f serviciosdb.yml up -d


### 3. Verificar que los servicios estén ejecutándose
    docker compose -f serviciosdb.yml ps


## Acceso a la interfaz de administración (phpMyAdmin)
Una vez desplegado el entorno, abre tu navegador web e ingresa a:

URL: ```http://localhost:9090```

Accede con las credenciales que configuraste en tu archivo entorno.env.

*(Nota: El puerto 9090 se configuró en el aarchivo serviciodb.yml en la línea 18, es posible ajustarlo a cualquier pueto disponible del equipo principal que ejecuta el contenedor. En caso de utilizar otro puerto es necesario editar esa línea y remplazar todas los enlaces relacionados con el servicio de PhpMyAdmin de este manual por el pueto configurado.
 
Si no se desplegó el contenedor de PhpMyAdmin al reiniciar el equipo es porque el contenedor no tiene habilitada la opción de reinicio, para solucionar este error, es necesario acceder a tu Docker Desktop y activarlo tu mismo, entrando al conjunto de contenedores **docker** y dale click al botón de **Start** al contenedor de **phpmyadmin** ).*




## Guía para la Creación de Usuarios en phpMyAdmin

Esta sección detalla los pasos para crear **dos usuarios** con diferentes niveles de acceso (**Lectura** y **Escritura / Lectura**) utilizando la interfaz gráfica de **phpMyAdmin**.

### Requisitos Previos
1. Haber desplegado los servicios con Docker Compose.
2. Acceder a la interfaz web de phpMyAdmin en: `http://localhost:9090`.
3. Iniciar sesión como usuario administrador (usuario con privilegios totales configurado en tu archivo `entorno.env`).



### Usuario 1: Permisos de Solo Lectura (`usuario_lectura`)

Este usuario solo podrá consultar información (`SELECT`), sin permisos para modificar, insertar o eliminar datos.

#### Pasos en phpMyAdmin:

   1. En la barra de navegación superior, haz clic en la pestaña **Cuentas de usuarios** (arriba en la barra de herramientas ).

   2. Haz clic en **Agregar cuenta de usuario**.

   3. En la sección **Información de inicio de sesión**:
        * **Nombre de usuario:** `usuario_lectura`
        * **Nombre del host:** Selecciona `Cualquier host` (`%`) o `Local` (`localhost`).
        * **Contraseña:** Ingresa una contraseña #######################.

   4. En la sección **Privilegios globales**:
        * En la columna **Datos**, marca **únicamente** la casilla `SELECT`.

   5. Haz clic en el botón **Continuar** al final de la página para guardar los cambios.



### Usuario 2: Permisos de Lectura y Escritura (`usuario_escritura`)

Este usuario podrá consultar (`SELECT`), insertar (`INSERT`), actualizar (`UPDATE`) y eliminar (`DELETE`) registros dentro de las bases de datos.

#### Pasos en phpMyAdmin:

   1. Ve nuevamente a la pestaña **Cuentas de usuarios**.

   2. Haz clic en **Agregar cuenta de usuario**.

   3. En la sección **Información de inicio de sesión**:

        * **Nombre de usuario:** `usuario_escritura`
        * **Nombre del host:** Selecciona `Cualquier host` (`%`) o `Local` (`localhost`).
        * **Contraseña:** Ingresa una contraseña #######################

   4. En la sección **Privilegios globales**:

   * En la columna **Datos**, marca las siguientes casillas:
        * `SELECT` (Lectura)
        * `INSERT` (Insertar nuevos datos)
        * `UPDATE` (Modificar datos existentes)
        * `DELETE` (Eliminar datos)

   5. Haz clic en el botón **Continuar**  al final de la página para guardar los cambios.
