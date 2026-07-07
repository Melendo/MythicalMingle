# Mythical Mingle
Mythical Mingle es una plataforma web interactiva y nostálgica que revive la clásica tradición de coleccionar álbumes de cromos. A través de la apertura de sobres virtuales, trivias educativas para ganar monedas y el intercambio de cromos con amigos, los usuarios pueden completar colecciones temáticas en un entorno digital moderno y social.

# Descripción detallada
En la actualidad, gran parte de nuestras interacciones diarias se realizan a través de pantallas, lo que ha disminuido los momentos de socialización tradicionales. Mythical Mingle nace con la misión de adaptar y trasladar al mundo virtual una de las actividades más entrañables y sociales de la infancia: comprar sobres en el quiosco, pegar cromos en un álbum físico, lidiar con los cromos repetidos e intercambiarlos con amigos en el patio de la escuela.

La plataforma no solo ofrece entretenimiento y coleccionismo digital, sino que añade un fuerte componente educativo. Cada colección de cromos cuenta con preguntas y cuestionarios temáticos que permiten a los usuarios poner a prueba sus conocimientos, aprender datos de valor y obtener monedas virtuales para seguir comprando sobres en la tienda del juego.

El público objetivo de Mythical Mingle es sumamente amplio:
- **Adultos nostálgicos** que deseen revivir la ilusión de completar colecciones y compartir esta tradición.
- **Niños y jóvenes** que busquen un pasatiempo interactivo, divertido y con un valor formativo y pedagógico gracias a los cuestionarios didácticos de cada colección.
- **Coleccionistas en general** interesados en conectar con otras personas para forjar amistades y socializar mediante el intercambio y el juego colectivo.

## Índice
- [Requisitos Previos](#requisitos-previos)
- [Instalación](#instalación)
- [Configuración](#configuración)
- [Ejecución y Uso](#ejecución-y-uso)
- [Arquitectura y Stack Tecnológico](#arquitectura-y-stack-tecnológico)
- [Contribuciones](#contribuciones)
- [Licencia y Créditos](#licencia-y-créditos)

## Requisitos Previos
Antes de comenzar con la instalación, asegúrate de cumplir con los siguientes requisitos de entorno y software:
- **Sistema Operativo recomendado:** Linux / macOS / Windows
- **Runtime o Lenguaje:** Node.js (v18.0.0+ o v20.11.1+ recomendado)
- **Gestor de paquetes:** npm (v9.0.0+ o v10.0.0+)
- **Base de Datos:** MySQL Server (v8.0+) o compatible

## Instalación
Sigue estos pasos para clonar el repositorio e instalar las dependencias locales:

1. Clonar el repositorio:
```bash
git clone https://github.com/Melendo/MythicalMingle.git
cd MythicalMingle
```

2. Instalar las dependencias del proyecto:
```bash
npm install
```

## Configuración
El proyecto utiliza variables de entorno para gestionar la conexión a la base de datos MySQL y el puerto del servidor.

1. Duplica el archivo de ejemplo para crear tu configuración de entorno:
```bash
cp .env.example .env
```

2. Edita los valores del archivo `.env` según corresponda con tu entorno local:
```ini
PORT=3000
HOST=localhost
USER=tu_usuario_mysql
PASSWORD=tu_contraseña_mysql
```

### Variables de Entorno
| Variable | Descripción | Valor por Defecto | Requerido |
| :--- | :--- | :--- | :---: |
| `PORT` | Puerto de escucha de la aplicación Express | `3000` | Sí |
| `HOST` | Dirección del servidor de base de datos MySQL | `localhost` | Sí |
| `USER` | Nombre de usuario para la conexión a la base de datos | `root` | Sí |
| `PASSWORD` | Contraseña del usuario de la base de datos MySQL | `-` | Sí |

### Inicialización de la Base de Datos
El proyecto requiere una base de datos MySQL llamada `mm_db`. Puedes configurarla importando el archivo SQL incluido en la raíz del proyecto:
```bash
# Accede a MySQL y crea la base de datos
mysql -u tu_usuario_mysql -p -e "CREATE DATABASE mm_db;"

# Importa el esquema y los datos iniciales
mysql -u tu_usuario_mysql -p mm_db < mm_db.sql
```

## Ejecución y Uso

### Entorno de Desarrollo
Para levantar el servidor web local con Node.js:
```bash
npm start
```
La aplicación estará disponible en: `http://localhost:3000`

### Ejecución con Docker
Si prefieres ejecutar el proyecto de forma aislada en un contenedor Docker, puedes compilarlo y levantarlo utilizando el `Dockerfile` provisto:

1. Construir la imagen Docker:
```bash
docker build -t mythicalmingle .
```

2. Ejecutar el contenedor vinculando el puerto y pasando las variables del archivo `.env`:
```bash
docker run -d -p 3000:3000 --env-file .env mythicalmingle
```

### Pruebas (Testing)
El proyecto cuenta con una suite de pruebas unitarias y de integración desarrolladas con **Jest** y **Supertest**. Para ejecutarlas, corre:
```bash
npm run test
```

## Arquitectura y Stack Tecnológico
El proyecto sigue el patrón de diseño Modelo-Vista-Controlador (MVC) y utiliza un diseño modular para gestionar las rutas y operaciones del lado del servidor:

- **Backend / Core:** Node.js con Express para el servidor web y la lógica de negocio, `express-session` con almacenamiento persistente en la base de datos (`express-mysql-session`) para el manejo seguro de sesiones de usuario, y `multer` para la gestión en memoria de imágenes subidas.
- **Frontend / Motor de Vistas:** HTML5, CSS3 vanilla (con hojas de estilo dedicadas para cada módulo, ej. `album.css`, `tienda.css`, `animacionSobre.css`), plantillas EJS para el renderizado del lado del servidor y Bootstrap v5.3.2 para estilos y diseño adaptativo.
- **Base de Datos / Almacenamiento:** MySQL para persistir las entidades (usuarios, monedas, colecciones, categorías, cromos, álbumes personales y cuestionarios didácticos).
- **Pruebas (Testing):** Jest como motor de pruebas y Supertest para pruebas de integración sobre los endpoints HTTP de Express.
- **Contenedores / DevOps:** Docker (Dockerfile optimizado basado en Node Alpine).

## Contribuciones
Si deseas contribuir al desarrollo de este proyecto, por favor sigue los siguientes pasos:
1. Haz un Fork del repositorio.
2. Crea una nueva rama para tu funcionalidad (`git checkout -b feature/nueva-funcionalidad`).
3. Realiza tus cambios y haz un commit claro siguiendo convenciones (`git commit -m 'Añade nueva funcionalidad'`).
4. Sube los cambios a tu rama (`git push origin feature/nueva-funcionalidad`).
5. Abre una Pull Request explicando detalladamente los cambios realizados.

## Licencia y Créditos


### Créditos y Agradecimientos
- Desarrollado por [Melendo](https://github.com/Melendo), [AlvaroDelCampoUCM](https://github.com/AlvaroDelCampoUCM), [Valeria Corina](https://github.com/valeriacorinapl), [Pedro Cuadra](https://github.com/pedrocuadracarri), [Pablo Zapico](https://github.com/pzapico23), [Iván Alcalde](https://github.com/IAlcCamDev).
