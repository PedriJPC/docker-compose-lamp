
# Práctica Docker Compose LAMP

**Nombre:** Pedro Jorge Peña  
**Asignatura:** Servicios en Red  
**Curso:** 2.º SMR  
**Fecha:** 26 de noviembre de 2026

## 1. Descripción

El objetivo de esta práctica es desplegar una infraestructura LAMP utilizando Docker Compose.

La infraestructura está formada por Apache, PHP, MySQL, phpMyAdmin y Redis.

## 2. Estructura del proyecto

| Archivo o carpeta | Función |
|---|---|
| docker-compose.yml | Define los servicios de Docker. |
| sample.env | Plantilla de variables de entorno. |
| www/ | Contiene las páginas web. |
| bin/ | Contiene herramientas y scripts auxiliares. |
| config/ | Contiene archivos de configuración. |
| data/ | Almacena datos persistentes. |
| logs/ | Almacena registros de actividad. |
| sql/ | Contiene la exportación de la base de datos. |
| capturas/ | Almacena las evidencias de la práctica. |
| .gitignore | Indica los archivos que Git debe ignorar. |

## 3. Despliegue

Se ha desplegado la infraestructura utilizando Docker Compose.

| Servicio | Función | Puerto interno | Puerto externo |
|---|---|---|---|
| Apache/PHP | Servir páginas web y ejecutar PHP | 80 | 8081 |
| MySQL | Gestionar la base de datos | 3306 | No publicado |
| phpMyAdmin | Administrar MySQL | 80 | 8082 |
| Redis | Almacenamiento en memoria | 6379 | No publicado |

### Diferencia entre imagen y contenedor

Una imagen es una plantilla que contiene los archivos y la configuración de una aplicación. Un contenedor es una instancia de esa imagen que se ejecuta de forma aislada.

### Diferencia entre puerto interno y externo

El puerto interno es el utilizado por el servicio dentro de Docker. El puerto externo permite acceder al servicio desde Windows.

### Funcionamiento de Apache

Apache funciona dentro de un contenedor Docker, por lo que no es necesario instalarlo directamente en Windows.

## 4. Página web

Se ha creado el archivo `www/smr.php`.

La página muestra el nombre del administrador, la fecha, la versión de PHP, el servidor web y el nombre del contenedor.

También incluye un enlace al directorio de servicios.

## 5. Administración de MySQL

Se ha creado la base de datos `smr` y la tabla `servicios`.

La tabla contiene cinco registros:

| Servicio | Puerto |
|---|---:|
| Apache | 80 |
| MySQL | 3306 |
| phpMyAdmin | 80 |
| Redis | 6379 |
| DNS | 53 |

Se ha exportado la base de datos en formato SQL y se ha guardado en `sql/smr.sql`.

## 6. Comunicación entre contenedores

Se ha creado `www/servicios.php` para consultar los registros de MySQL y mostrarlos en una tabla HTML.

PHP utiliza el nombre `database` para conectarse al servicio MySQL dentro de la red de Docker Compose.

Las credenciales se obtienen mediante variables de entorno.

Si MySQL deja de funcionar, la página principal puede seguir funcionando, pero la página de servicios no podrá consultar los datos.

## 7. Ciclo de vida y persistencia

El comando `docker compose stop` detiene los contenedores sin eliminarlos.

El comando `docker compose start` vuelve a iniciarlos.

El comando `docker compose down` detiene y elimina los contenedores y la red creada por Docker Compose.

El comando `docker compose up -d` vuelve a crear y ejecutar los contenedores.

Los archivos PHP se conservan en la carpeta del proyecto y los datos de MySQL se almacenan en el volumen persistente configurado en Docker Compose.

## 8. Evidencias

Se han realizado las siguientes capturas de pantalla:

- `docker.png`: contenedores funcionando en Docker Desktop.
- `servidor.png`: página de información del servidor.
- `mysql.png`: base de datos y tabla `servicios` en phpMyAdmin.
- `servicios.png`: directorio de servicios mostrando los cinco registros.

## 9. Conclusión

Se ha desplegado una infraestructura LAMP utilizando Docker Compose.

Se ha comprobado el funcionamiento de los servicios, creado una página web con PHP, establecido la comunicación con MySQL y verificado la persistencia de los datos.

La práctica ha permitido aprender a desplegar y administrar servicios mediante contenedores Docker.
