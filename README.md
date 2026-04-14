# Config Server

Este servicio es un **Servidor de Configuración de Spring Cloud**. Su función principal es centralizar la gestión de la configuración para todos los demás microservicios en el sistema. Al externalizar la configuración, se logra una mayor flexibilidad y gestionabilidad del entorno, permitiendo cambios de configuración sin necesidad de redesplegar los microservicios.

## Características Principales

- **Centralización de la Configuración:** Evita la necesidad de tener archivos de configuración dispersos en cada microservicio. Los microservicios cliente obtienen su configuración de este servidor al arrancar.
- **Perfil Nativo (`native`):** Está configurado para usar el perfil `native` de Spring Cloud Config. Esto significa que sirve los archivos de configuración directamente desde el classpath del proyecto, específicamente desde la carpeta `src/main/resources/config`.

## Configuración de Microservicios

Dentro del directorio `src/main/resources/config`, se encuentran los archivos de configuración para cada microservicio:

- `activityservice.yaml`: Configuración para el servicio de actividades.
- `gateway.yaml`: Configuración para el API Gateway, incluyendo las rutas a los demás servicios y la configuración de seguridad.
- `iaservice.yaml`: Configuración para el servicio de inteligencia artificial.
- `userservice.yaml`: Configuración para el servicio de usuarios.

Cuando un microservicio (por ejemplo, `userservice`) se inicia, se pone en contacto con el `configserver` y solicita su configuración. El `configserver` busca un archivo que coincida con el nombre de la aplicación (`spring.application.name`) del microservicio cliente y se lo proporciona.

## Dependencias Clave

- `spring-cloud-config-server`: La dependencia fundamental que habilita la funcionalidad del servidor de configuración.
- `spring-boot-starter-parent`: Versión `3.5.13`.
- **Java:** Versión `21`.

## Configuración (`application.yaml`)

- **Puerto:** Se ejecuta en el puerto `8888`.
- **Nombre de la Aplicación:** `configserver`.
- **Búsqueda de Archivos:** Busca los archivos de configuración en la ruta del classpath: `/config`.
