# Clon del Sitio Web de la PUCP con WordPress y Docker

**Sistema de réplica académica del portal institucional de la Pontificia Universidad Católica del Perú, desarrollado con WordPress como CMS, tema personalizado, plugin propio y despliegue en contenedores Docker.**

---

## Integrantes

| Nombre | Rol |
|---|---|
| Huamani Vasquez Juan Jose | Desarrollo del tema y configuración Docker |
| Yabar Carazas Melvin Jarred | Plugin personalizado y contenido de base de datos |
| Zela Flores Gabriel Frank | Estructura del CMS y configuración de módulos |
| Chacalla Herrera Roger | Documentación, pruebas y verificación WhatRuns |

---

## Introducción

Este proyecto forma parte del laboratorio del curso de Ingeniería de Software en la Pontificia Universidad Católica del Perú (PUCP). El objetivo principal fue aprender a utilizar un CMS (Content Management System) para construir un sitio web funcional sin necesidad de desarrollar toda la infraestructura desde cero.

Elegimos WordPress como plataforma base por ser el CMS más utilizado en el mundo, con una comunidad activa, amplia documentación y un ecosistema maduro de temas y plugins. La idea del laboratorio fue clonar visualmente el portal institucional de la PUCP, replicando su estructura, diseño y contenido de forma académica, y ejecutar todo el sistema dentro de contenedores Docker para garantizar un entorno reproducible y fácil de desplegar en cualquier máquina.

El resultado es un sitio web funcional que incluye un tema completamente desarrollado desde cero que imita la apariencia oficial de la PUCP, un plugin propio con funcionalidades específicas del campus, contenido precargado mediante un backup SQL, y todo el sistema levantado con un único comando de Docker Compose.

---

## Planteamiento del Problema

El desarrollo de sitios web institucionales desde cero implica un alto costo en tiempo y recursos. Las universidades necesitan publicar contenido constantemente (noticias, eventos, agenda académica, información de admisión) y mantener una identidad visual consistente. Hacerlo de manera manual, sin una plataforma de gestión de contenido, se vuelve inviable a medida que el sitio crece.

Por otro lado, en el entorno académico, los estudiantes de ingeniería muchas veces no tienen experiencia práctica con herramientas que el mercado laboral usa de manera cotidiana, como los CMS. Aprender a instalar, configurar, personalizar y extender WordPress permite entender cómo funciona una arquitectura web modular orientada a contenido.

El problema que abordamos fue: ¿cómo replicar un sitio web institucional real (la PUCP) usando un CMS, un tema personalizado y módulos propios, ejecutado de forma reproducible en cualquier entorno mediante contenedores Docker?

---

## Objetivos

### Objetivo General

Desarrollar una réplica funcional del sitio web institucional de la PUCP utilizando WordPress como CMS, implementando un tema visual personalizado, un plugin propio para funcionalidades del campus, contenido precargado en base de datos, y desplegarlo completamente en contenedores Docker.

### Objetivos Específicos

- Instalar y configurar WordPress como sistema de gestión de contenido dentro de un entorno Docker.
- Diseñar e implementar un tema WordPress personalizado (`PUCP Clone`) que replique la apariencia visual del portal oficial de la PUCP, incluyendo cabecera, navegación, secciones de noticias, agenda, cifras institucionales y pie de página.
- Desarrollar un plugin propio (`PUCP Campus Tools`) que registre un tipo de contenido personalizado para servicios del campus y exponga un shortcode reutilizable.
- Crear y poblar la base de datos con contenido real: noticias, categorías, eventos de agenda y servicios del campus, mediante un archivo SQL de restauración automática.
- Configurar un entorno Docker Compose con dos servicios (WordPress y MariaDB) que permita levantar el proyecto completo con un solo comando.
- Verificar las tecnologías utilizadas por el sitio mediante la extensión WhatRuns y documentar los resultados.
- Documentar todo el proceso en un README detallado que cumpla con los criterios de la rúbrica de evaluación.

---

## Alcance del Proyecto

El proyecto cubre los siguientes aspectos:

- **Sitio público**: página principal con noticias, agenda, sección PUCP en cifras, accesos rápidos y footer. Los visitantes pueden navegar por el contenido sin necesidad de autenticarse.
- **Panel de administración**: acceso a través de `/wp-admin` para gestionar entradas, categorías, servicios del campus, menús y personalización del tema mediante el Customizer de WordPress.
- **Tema personalizado**: desarrollado completamente desde cero, con plantillas PHP para la portada (`front-page.php`), cabecera (`header.php`), pie de página (`footer.php`), entradas individuales (`single.php`) y categorías (`category.php`).
- **Plugin propio**: `PUCP Campus Tools` que agrega un tipo de contenido personalizado (`pucp_servicio`) y un shortcode `[pucp_servicios]` para mostrar servicios del campus en cualquier página.
- **Base de datos**: incluye 12 entradas publicadas, 5 categorías, 3 servicios del campus y la configuración completa del sitio, todo precargado mediante `backup-pucp.sql`.
- **Infraestructura Docker**: dos contenedores (WordPress + MariaDB 10.11) definidos en `docker-compose.yml`.

Lo que **no** está dentro del alcance: integración con APIs externas reales de la PUCP, autenticación de estudiantes, sistema de matrícula ni módulos de pago.

---

## Tecnologías Utilizadas

| Tecnología | Versión | Propósito |
|---|---|---|
| WordPress | Latest (6.x) | CMS principal del proyecto |
| PHP | 8.x | Lenguaje de programación del backend de WordPress |
| MariaDB | 10.11 | Motor de base de datos relacional |
| Apache | 2.x | Servidor web incluido en la imagen oficial de WordPress |
| Docker | 24+ | Contenedorización del entorno completo |
| Docker Compose | v2 | Orquestación de los servicios WordPress y MariaDB |
| jQuery | 3.x | Biblioteca JavaScript incluida en WordPress |
| Bootstrap | 3.3.7 | Framework CSS para el layout y componentes del tema |
| Google Fonts | — | Tipografías Montserrat y Roboto usadas en el tema |
| Akismet | Incluido | Plugin de protección contra spam en comentarios |
| WhatRuns | Extensión | Herramienta de verificación de tecnologías del sitio |

### Detalles tecnológicos relevantes

**WordPress** es el CMS sobre el que corre todo el proyecto. Gestiona el contenido, los usuarios, los temas, los plugins y las URLs amigables. La versión usada es la imagen oficial `wordpress:latest` disponible en Docker Hub.

**PHP** es el lenguaje en el que está escrito WordPress y nuestro tema/plugin. Todo el backend, desde las consultas a la base de datos hasta el renderizado de las vistas, pasa por PHP.

**MariaDB 10.11** es el motor de base de datos elegido por compatibilidad total con WordPress y MySQL. Se ejecuta como un servicio separado en Docker y almacena todas las tablas del sistema (`wp_posts`, `wp_users`, `wp_options`, etc.).

**Apache** es el servidor web que viene preconfigurado dentro de la imagen oficial de WordPress. Maneja las peticiones HTTP y sirve los archivos PHP a través del módulo `mod_rewrite` para las URLs amigables.

**Docker Compose** permite definir y ejecutar ambos servicios (WordPress y MariaDB) de manera coordinada, con variables de entorno, volúmenes persistentes y dependencias entre contenedores.

**Bootstrap 3.3.7** se referencia desde el CDN de la PUCP original, lo cual nos permitió heredar parte del sistema de grillas y componentes que usa el sitio real.

---

## Arquitectura del Sistema

El proyecto sigue una arquitectura **Cliente-Servidor con CMS monolítico**, típica de WordPress:

```
┌─────────────────────────────────────────────────────┐
│                   Navegador (Cliente)                │
│         http://localhost:8085                        │
└───────────────────┬─────────────────────────────────┘
                    │ HTTP
┌───────────────────▼─────────────────────────────────┐
│           Contenedor Docker: wordpress_app           │
│  ┌─────────────────────────────────────────────┐    │
│  │              Apache + PHP                   │    │
│  │  ┌──────────────────────────────────────┐   │    │
│  │  │           WordPress Core             │   │    │
│  │  │  ┌────────────┐  ┌────────────────┐  │   │    │
│  │  │  │ Tema PUCP  │  │ Plugin Campus  │  │   │    │
│  │  │  │   Clone    │  │    Tools       │  │   │    │
│  │  │  └────────────┘  └────────────────┘  │   │    │
│  │  └──────────────────────────────────────┘   │    │
│  └─────────────────────────────────────────────┘    │
│           Puerto: 8085 → 80                          │
└───────────────────┬─────────────────────────────────┘
                    │ MySQL Protocol (3307→3306)
┌───────────────────▼─────────────────────────────────┐
│           Contenedor Docker: wordpress_db            │
│              MariaDB 10.11                           │
│         Base de datos: wordpress                     │
│    (inicializada con backup-pucp.sql)                │
└─────────────────────────────────────────────────────┘
```

Internamente, WordPress sigue el patrón **Template Hierarchy** para el renderizado de vistas, que es una variante del patrón MVC donde:

- **Modelo**: WordPress se conecta a MariaDB a través de la clase `$wpdb` y funciones como `WP_Query`, `get_posts()`, `get_option()`, etc.
- **Vista**: los archivos de plantilla PHP del tema (`front-page.php`, `single.php`, `category.php`, `header.php`, `footer.php`) se encargan de renderizar el HTML.
- **Controlador**: el núcleo de WordPress actúa como controlador, interpretando la URL, determinando qué plantilla cargar y qué datos inyectar.

El plugin `PUCP Campus Tools` se integra a esta arquitectura mediante los hooks de WordPress (`add_action`, `add_shortcode`), sin modificar el núcleo.

---

## Estructura del Proyecto

```
PUCP/
├── docker-compose.yml              # Orquestación de contenedores (WordPress + MariaDB)
├── backup-pucp.sql                 # Dump SQL con todo el contenido precargado
├── .gitignore                      # Exclusiones de Git (uploads, cache, logs, db_data/)
├── README.md                       # Documentación principal del proyecto
├── docs/
│   ├── checklist-rubrica.md        # Checklist de cumplimiento de la rúbrica
│   └── evidencia-whatruns.md       # Instrucciones para verificar tecnologías con WhatRuns
└── wordpress/                      # Instalación completa de WordPress
    ├── wp-config.php               # Configuración principal de WordPress
    ├── wp-config-docker.php        # Configuración adaptada para variables de entorno Docker
    ├── wp-config-sample.php        # Plantilla de configuración de WordPress
    ├── index.php                   # Punto de entrada de WordPress
    ├── .htaccess                   # Reglas de reescritura para URLs amigables (Apache)
    ├── wp-admin/                   # Panel de administración de WordPress (núcleo)
    ├── wp-includes/                # Núcleo de WordPress (clases, funciones, APIs)
    └── wp-content/
        ├── themes/
        │   ├── pucp-clone/         # ★ Tema personalizado (nuestro desarrollo)
        │   │   ├── style.css           # Hoja de estilos principal + metadata del tema
        │   │   ├── functions.php       # Soporte del tema, enqueue de assets, customizer
        │   │   ├── front-page.php      # Plantilla de la página principal
        │   │   ├── header.php          # Cabecera: barra superior + navegación
        │   │   ├── footer.php          # Pie de página con menús y enlaces
        │   │   ├── single.php          # Vista de entrada individual
        │   │   ├── category.php        # Listado de entradas por categoría
        │   │   ├── index.php           # Plantilla fallback
        │   │   ├── pucp-original.html  # HTML original de referencia del sitio de la PUCP
        │   │   └── assets/
        │   │       └── images/         # Imágenes del tema (noticias, eventos, portada)
        │   │           ├── conversatorio-ia.jpg
        │   │           ├── coro-femenino.jpg
        │   │           ├── Creonograma.jpg
        │   │           ├── Estudiantes-Profesores.jpeg
        │   │           ├── festival-cultural.jpg
        │   │           ├── intercambio-estudiantil.jpg
        │   │           ├── juegos-postgrado.jpg
        │   │           ├── Laboratorio.jpg
        │   │           ├── open-pucp.jpg
        │   │           ├── peru-democratico.jpg
        │   │           └── pregrado.jpg
        │   └── twentytwentyfive/   # Tema oficial de WordPress (incluido por defecto)
        └── plugins/
            ├── pucp-campus-tools/  # ★ Plugin personalizado (nuestro desarrollo)
            │   └── pucp-campus-tools.php  # Registro de CPT, shortcode y estilos inline
            ├── akismet/            # Plugin anti-spam incluido con WordPress
            └── hello.php           # Plugin "Hello Dolly" incluido por defecto
```

---

## Funcionalidades del Sistema

### 1. Sitio web público (frontend)

#### Página principal (`front-page.php`)
La portada del sitio replica fielmente la estructura del portal oficial de la PUCP:

- **Barra superior**: links de acceso rápido (Intranet, Agenda, Mapa del campus, Trabaja con nosotros) y selector de idioma.
- **Cabecera con logo PUCP**: navegación principal con los menús de Pregrado, Posgrado, Investigación, Vida universitaria y Comunidad.
- **Sección de noticias destacadas**: carrusel con las últimas noticias publicadas, mostrando imagen, categoría, título y enlace. Las imágenes se obtienen del metadato `_pucp_image_url` de cada entrada, con fallback a una imagen predeterminada del servidor de la PUCP.
- **Sección PUCP en Cifras**: datos estadísticos de la universidad (año de fundación 1917, ranking QS #1 en Perú, #11 en Latinoamérica, 31,516 estudiantes, 66 carreras, 175 programas de posgrado, 535 investigadores RENACYT). Todos estos valores son configurables desde el Customizer de WordPress.
- **Sección de agenda**: muestra las entradas de la categoría "Agenda", con formato de fecha y descripción del evento.
- **Accesos rápidos (Servicios del Campus)**: renderizados mediante el shortcode `[pucp_servicios]` del plugin propio, mostrando tarjetas de Biblioteca PUCP, Campus Virtual y Servicios al Estudiante.
- **Pie de página**: menús de navegación secundarios con links a secciones institucionales, redes sociales, información de contacto y logo de la PUCP.

#### Entradas individuales (`single.php`)
Muestra cada noticia o entrada con su imagen destacada, categoría, fecha, título y contenido completo. Incluye navegación a entradas anteriores y siguientes.

#### Listado por categoría (`category.php`)
Muestra las entradas filtradas por categoría (Actualidad, Campus y comunidad, Institucional, Agenda, Admisión), con paginación incluida.

### 2. Plugin PUCP Campus Tools

El plugin registra un **Custom Post Type (CPT)** llamado `pucp_servicio` con las siguientes características:

- Visible en el panel de administración bajo el menú "Servicios PUCP".
- Soporta título, editor y extracto.
- Expuesto en la REST API de WordPress (`show_in_rest: true`).
- URL amigable: `/servicios-pucp/`.
- Ícono de dashicon personalizado en el menú de administración.

Además registra el **shortcode `[pucp_servicios]`** que acepta el parámetro `limit` (por defecto 3) y renderiza una grilla CSS con las tarjetas de servicios publicados. Si no hay servicios cargados, muestra tres tarjetas predeterminadas (Biblioteca PUCP, Campus Virtual, Admisión).

Los estilos del plugin se inyectan de forma inline para no depender de archivos CSS externos, garantizando que funcionen incluso en entornos sin acceso a CDN.

### 3. Tema PUCP Clone

#### Funcionalidades del tema (functions.php)
- **Soporte de WordPress**: `title-tag`, `post-thumbnails`, `html5` semántico.
- **Menús registrados**: Menú Principal, Barra Superior y Menú Footer, todos gestionables desde el panel de administración.
- **Carga de assets**: Google Fonts (Montserrat + Roboto), Bootstrap 3.3.7, hojas de estilo y scripts del portal original de la PUCP referenciados por CDN, jQuery integrado de WordPress.
- **Helper de imágenes (`pucp_get_post_image_url`)**: función que resuelve la imagen de cada entrada buscando primero en el metadato `_pucp_image_url`, luego en la imagen destacada de WordPress, y finalmente en una imagen de fallback en el servidor de la PUCP.
- **Customizer de WordPress**: sección "PUCP en Cifras" con controles para editar todos los datos estadísticos directamente desde el panel de personalización visual del CMS, sin tocar código.

### 4. Panel de administración

Accesible en `http://localhost:8085/wp-admin` con credenciales `admin / admin`. Permite:

- Gestionar entradas (crear, editar, publicar, categorizar).
- Administrar los servicios del campus (Custom Post Type `pucp_servicio`).
- Configurar menús de navegación.
- Personalizar cifras institucionales desde el Customizer.
- Gestionar plugins y temas instalados.
- Configurar opciones generales del sitio.

### 5. Contenido precargado

El archivo `backup-pucp.sql` carga automáticamente al iniciar el contenedor de MariaDB:

- **12 entradas** publicadas: noticias, eventos culturales y de agenda distribuidos entre mayo y junio de 2026.
- **5 categorías**: Actualidad, Campus y comunidad, Institucional, Agenda, Admisión.
- **3 servicios del campus**: Biblioteca PUCP, Campus Virtual, Servicios al Estudiante.
- **Configuración completa**: URL del sitio, nombre del blog, tema activo, plugin activo, idioma español (es_ES), estructura de permalinks.
- **Usuario administrador**: login `admin` con contraseña `admin`.

---

## Flujo General del Sistema

Cuando un visitante accede a `http://localhost:8085`, el flujo es el siguiente:

1. **Docker** redirige el puerto 8085 del host al puerto 80 del contenedor `wordpress_app`.
2. **Apache** recibe la petición HTTP y la enruta a través de las reglas de `.htaccess`.
3. **WordPress** carga `index.php`, que incluye `wp-blog-header.php`, iniciando el ciclo de carga.
4. WordPress consulta la base de datos en MariaDB (contenedor `wordpress_db`) usando las credenciales definidas en `wp-config.php` mediante variables de entorno Docker.
5. Según la URL, WordPress determina qué plantilla del tema cargar: si es la raíz, usa `front-page.php`; si es una entrada, usa `single.php`; si es una categoría, usa `category.php`.
6. La plantilla llama a funciones de WordPress (`the_loop`, `WP_Query`, `get_template_part`) para obtener el contenido y renderizarlo en HTML.
7. El tema carga los estilos (Google Fonts, Bootstrap, CSS del tema) y los scripts (jQuery, Bootstrap JS) mediante `wp_enqueue_scripts`.
8. El plugin `PUCP Campus Tools` está activo y sus hooks (`init`, `wp_enqueue_scripts`) se ejecutan en cada petición, registrando el CPT y los estilos.
9. En las páginas donde aparece el shortcode `[pucp_servicios]`, WordPress lo procesa antes de renderizar el contenido y lo reemplaza con la grilla de servicios.
10. El HTML completo se envía al navegador del usuario.

Para el panel de administración (`/wp-admin`), el flujo es similar pero WordPress carga las vistas del panel en lugar de las del tema.

---

## Base de Datos

### Motor utilizado

**MariaDB 10.11** — compatible con MySQL, ejecutada en el contenedor `wordpress_db` con el volumen `db_data` para persistencia.

### Configuración de conexión

| Parámetro | Valor |
|---|---|
| Host | `db:3306` (nombre del servicio Docker) |
| Base de datos | `wordpress` |
| Usuario | `wordpress` |
| Contraseña | `wordpress` |
| Root password | `rootpassword` |
| Puerto externo | `3307` (mapeado al 3306 interno) |
| Charset | `utf8mb4` |
| Collation | `utf8mb4_unicode_ci` |

### Tablas del sistema

WordPress crea automáticamente las siguientes tablas con el prefijo `wp_`:

| Tabla | Descripción |
|---|---|
| `wp_posts` | Almacena entradas, páginas, menús, revisiones y CPTs (incluyendo `pucp_servicio`) |
| `wp_postmeta` | Metadatos de cada post (en nuestro caso `_pucp_image_url`) |
| `wp_terms` | Términos de taxonomías (categorías, etiquetas) |
| `wp_term_taxonomy` | Relaciona términos con sus taxonomías |
| `wp_term_relationships` | Relaciona posts con términos |
| `wp_users` | Usuarios del sistema |
| `wp_usermeta` | Metadatos de usuarios (roles, preferencias) |
| `wp_options` | Configuración global del sitio (URL, tema activo, plugins, etc.) |
| `wp_comments` | Comentarios de las entradas |
| `wp_commentmeta` | Metadatos de comentarios |
| `wp_links` | Blogroll (legado) |
| `wp_termmeta` | Metadatos de términos |

### Contenido cargado en la base de datos

**Categorías (wp_terms + wp_term_taxonomy):**

| ID | Nombre | Slug | Descripción |
|---|---|---|---|
| 1 | Actualidad | actualidad | Noticias generales |
| 2 | Campus y comunidad | campus-y-comunidad | Vida universitaria |
| 3 | Institucional | institucional | Comunicados institucionales |
| 4 | Agenda | agenda | Eventos y actividades |
| 5 | Admisión | admision | Información para postulantes |

**Entradas publicadas (wp_posts):**

| ID | Título | Categoría | Fecha |
|---|---|---|---|
| 1 | Juegos Interfacultades 2026 | Campus y comunidad | 25/05/2026 |
| 2 | Magnifica humanitas: el llamado del Papa León XIV | Actualidad | 25/05/2026 |
| 3 | Estudiantes y autoridades consiguen un acuerdo basado en el diálogo | Institucional | 21/05/2026 |
| 4 | Perú democrático: responsabilidad común | Agenda | 26/05/2026 |
| 5 | Coro Femenino PUCP \| Temporada Vox Laudis | Agenda | 28/05/2026 |
| 6 | Admisión PUCP: carreras y modalidades de ingreso | Admisión | 27/05/2026 |
| 7 | Nuevos laboratorios impulsan la investigación interdisciplinaria | Institucional | 29/05/2026 |
| 8 | Feria de proyectos estudiantiles reúne innovación y compromiso social | Campus y comunidad | 30/05/2026 |
| 9 | Nuevas oportunidades de intercambio internacional | Actualidad | 31/05/2026 |
| 10 | Conversatorio con especialistas sobre inteligencia artificial | Agenda | 03/06/2026 |
| 11 | Open PUCP: conoce nuestras carreras y servicios | Agenda | 06/06/2026 |
| 12 | Festival cultural universitario en el campus | Agenda | 12/06/2026 |

**Servicios del campus (Custom Post Type `pucp_servicio`):**

| ID | Título | Extracto |
|---|---|---|
| 20 | Biblioteca PUCP | Recursos académicos y bases de datos |
| 21 | Campus Virtual | Servicios digitales para estudiantes y docentes |
| 22 | Servicios al Estudiante | Bienestar y acompañamiento universitario |

### ORM y acceso a datos

WordPress no usa un ORM tradicional. En su lugar, utiliza la clase global `$wpdb` y funciones de alto nivel como `WP_Query`, `get_posts()`, `get_option()`, `get_post_meta()`. El acceso a datos desde nuestro plugin se realiza mediante `WP_Query`:

```php
$services = new WP_Query(array(
    'post_type'      => 'pucp_servicio',
    'posts_per_page' => absint($atts['limit']),
    'post_status'    => 'publish',
));
```

### Backup y restauración

El archivo `backup-pucp.sql` es un dump completo que incluye instrucciones `DROP TABLE IF EXISTS` seguidas de `CREATE TABLE` e `INSERT INTO`. Cuando Docker Compose levanta el contenedor de MariaDB por primera vez, detecta el archivo en `/docker-entrypoint-initdb.d/` y lo importa automáticamente, inicializando la base de datos con todo el contenido del proyecto.

---

## Instalación y Configuración

### Requisitos previos

Antes de ejecutar el proyecto, asegúrate de tener instalado:

- **Docker Desktop** (Windows/macOS) o **Docker Engine + Docker Compose** (Linux). Versión mínima recomendada: Docker 24.x.
- **Git** para clonar el repositorio.
- Un **navegador web** moderno (Chrome, Firefox, Edge).
- (Opcional para verificación) La extensión **WhatRuns** instalada en el navegador.

Verifica que Docker esté funcionando:

```bash
docker --version
docker compose version
```

### Paso 1: Clonar el repositorio

```bash
git clone https://github.com/userly03/wordpress-webpucp.git
cd wordpress-webpucp
```

### Paso 2: Levantar el proyecto con Docker Compose

Desde la raíz del proyecto (donde está `docker-compose.yml`), ejecuta:

```bash
docker compose up -d
```

Este comando realiza lo siguiente:

1. Descarga las imágenes `wordpress:latest` y `mariadb:10.11` de Docker Hub (solo la primera vez).
2. Crea el contenedor `wordpress_app` (WordPress + Apache) mapeando el puerto `8085`.
3. Crea el contenedor `wordpress_db` (MariaDB) con el volumen `db_data` para persistencia.
4. Monta la carpeta `./wordpress` del repositorio dentro del contenedor en `/var/www/html`, por lo que el tema y el plugin ya están disponibles desde el inicio.
5. Al inicializar la base de datos por primera vez, MariaDB importa automáticamente `backup-pucp.sql` desde `/docker-entrypoint-initdb.d/`.

Espera unos 30-60 segundos a que MariaDB esté lista y WordPress termine de configurarse.

### Paso 3: Verificar que los contenedores estén activos

```bash
docker compose ps
```

Deberías ver ambos contenedores en estado `running`:

```
NAME              IMAGE              STATUS
wordpress_app     wordpress:latest   Up
wordpress_db      mariadb:10.11      Up
```

### Paso 4: Abrir el sitio en el navegador

```
http://localhost:8085
```

Deberías ver la réplica de la página principal de la PUCP con las noticias, agenda y servicios cargados.

### Paso 5: Acceder al panel de administración (opcional)

```
http://localhost:8085/wp-admin
```

- **Usuario**: `admin`
- **Contraseña**: `admin`

### Solución de problemas comunes

**Si ves la página por defecto de WordPress o el instalador de WordPress** en lugar del sitio con contenido, significa que MariaDB levantó con un volumen anterior (sin el SQL importado). Solución:

```bash
docker compose down -v
docker compose up -d
```

El flag `-v` elimina los volúmenes persistentes, lo que fuerza una reimportación del `backup-pucp.sql`.

**Si prefieres importar el SQL manualmente:**

```bash
docker exec -i wordpress_db mysql -u wordpress -pwordpress wordpress < backup-pucp.sql
```

**Si el puerto 8085 ya está en uso** en tu máquina, cambia el mapeo en `docker-compose.yml`:

```yaml
ports:
  - "8090:80"   # Cambia 8085 por cualquier puerto libre
```

Y luego accede a `http://localhost:8090`.

### Variables de entorno

Las variables de entorno están definidas directamente en `docker-compose.yml`. No se usa un archivo `.env` externo. Estas son las variables configuradas:

| Variable | Valor | Descripción |
|---|---|---|
| `WORDPRESS_DB_HOST` | `db:3306` | Host de la base de datos |
| `WORDPRESS_DB_USER` | `wordpress` | Usuario de la BD |
| `WORDPRESS_DB_PASSWORD` | `wordpress` | Contraseña de la BD |
| `WORDPRESS_DB_NAME` | `wordpress` | Nombre de la BD |
| `MYSQL_DATABASE` | `wordpress` | Base de datos a crear en MariaDB |
| `MYSQL_USER` | `wordpress` | Usuario de MariaDB |
| `MYSQL_PASSWORD` | `wordpress` | Contraseña del usuario MariaDB |
| `MYSQL_ROOT_PASSWORD` | `rootpassword` | Contraseña del root de MariaDB |

WordPress lee estas variables desde `wp-config-docker.php` mediante la función `getenv_docker()`, que también soporta el patrón `_FILE` para Docker Secrets.

---

## Ejecución del Proyecto

### Comandos principales

| Comando | Descripción |
|---|---|
| `docker compose up -d` | Levanta el proyecto en background |
| `docker compose down` | Detiene y elimina los contenedores (mantiene volúmenes) |
| `docker compose down -v` | Detiene, elimina contenedores **y volúmenes** (resetea la BD) |
| `docker compose ps` | Muestra el estado de los contenedores |
| `docker compose logs wordpress` | Muestra los logs del contenedor de WordPress |
| `docker compose logs db` | Muestra los logs de MariaDB |
| `docker compose restart` | Reinicia todos los servicios |

### Importación manual del SQL

```bash
docker exec -i wordpress_db mysql -u wordpress -pwordpress wordpress < backup-pucp.sql
```

### Acceso a la shell del contenedor WordPress

```bash
docker exec -it wordpress_app bash
```

### Acceso a la shell de MariaDB

```bash
docker exec -it wordpress_db mysql -u wordpress -pwordpress wordpress
```

### Verificación de tecnologías con WhatRuns

1. Levanta el proyecto con `docker compose up -d`.
2. Abre `http://localhost:8085` en Chrome o Firefox.
3. Haz clic en el ícono de la extensión WhatRuns en la barra del navegador.
4. WhatRuns detectará automáticamente las tecnologías utilizadas. Deberías ver:
   - WordPress
   - PHP
   - jQuery
   - Apache
   - Tema personalizado: PUCP Clone
5. Toma una captura de pantalla como evidencia para la rúbrica.

---

## Capturas o Evidencias

Las imágenes del proyecto están ubicadas en:

```
wordpress/wp-content/themes/pucp-clone/assets/images/
```

Para agregar capturas de pantalla del sitio funcionando, crea una carpeta `docs/capturas/` en la raíz del proyecto y coloca ahí las imágenes:

```
docs/
├── capturas/
│   ├── 01-portada.png           # Vista de la página principal
│   ├── 02-noticias.png          # Sección de noticias
│   ├── 03-agenda.png            # Sección de agenda
│   ├── 04-wp-admin.png          # Panel de administración
│   ├── 05-plugin-servicios.png  # Custom Post Type en el admin
│   ├── 06-docker-ps.png         # docker compose ps con contenedores activos
│   └── 07-whatruns.png          # Captura de WhatRuns con tecnologías detectadas
├── checklist-rubrica.md
└── evidencia-whatruns.md
```

Referencia en el README con:

```markdown
![Portada del sitio](docs/capturas/01-portada.png)
![WhatRuns](docs/capturas/07-whatruns.png)
```

---

## Explicación Técnica

### Cómo funciona el tema PUCP Clone

El tema está construido siguiendo la jerarquía de plantillas de WordPress. La plantilla principal es `front-page.php`, que se carga cuando la página de inicio está configurada como "últimas entradas" (que es nuestro caso, definido en `wp_options` con `show_on_front = posts`).

Dentro de `front-page.php`, el tema realiza múltiples `WP_Query` independientes para obtener las noticias por categoría, los eventos de agenda y el contenido de la sección destacada. Cada sección del HTML corresponde a un bloque funcional del sitio real de la PUCP:

1. El encabezado carga `header.php`, que construye la barra superior y la navegación principal usando `wp_nav_menu()` con el menú registrado `primary`.
2. La sección de noticias itera el loop de WordPress con `have_posts()` / `the_post()`.
3. La función `pucp_get_post_image_url()` resuelve la imagen de cada entrada consultando el metadato `_pucp_image_url` de `wp_postmeta`. Si el valor es una ruta relativa (como `assets/images/juegos-postgrado.jpg`), la concatena con la URL del directorio del tema usando `get_stylesheet_directory_uri()`. Si es una URL absoluta, la usa directamente.
4. La sección "PUCP en Cifras" usa `get_theme_mod()` para leer los valores configurados en el Customizer, con defaults sensatos definidos en `pucp_customize_register()`.
5. El footer carga `footer.php` con los menús secundarios y links institucionales.

### Cómo funciona el plugin PUCP Campus Tools

El plugin se carga automáticamente porque está marcado como activo en `wp_options` (campo `active_plugins`). Al iniciarse WordPress, llama a `do_action('init')`, que ejecuta la función `pucp_tools_register_service_type()` y registra el tipo de contenido personalizado `pucp_servicio`.

El shortcode `[pucp_servicios limit="3"]` funciona así: cuando WordPress encuentra ese texto en el contenido de una página o entrada, llama a la función `pucp_tools_shortcode()`, que ejecuta un `WP_Query` buscando posts de tipo `pucp_servicio` en estado `publish`. El resultado se construye con `ob_start()` / `ob_get_clean()` para capturar el HTML generado y retornarlo como string al contenido de la página.

Los estilos del plugin se registran e inyectan como CSS inline (usando `wp_add_inline_style()`) en el hook `wp_enqueue_scripts`, lo que los hace independientes de cualquier archivo externo y garantiza que funcionen sin configuración adicional.

### Cómo funciona Docker Compose

El archivo `docker-compose.yml` define dos servicios:

**Servicio `wordpress`**: usa la imagen oficial `wordpress:latest`, que incluye Apache + PHP + WordPress preconfigurado. Monta la carpeta local `./wordpress` en `/var/www/html` del contenedor, lo que significa que cualquier cambio en los archivos del tema o plugin se refleja inmediatamente sin reconstruir la imagen. Depende del servicio `db` (definido con `depends_on`) para asegurar que MariaDB esté disponible antes de iniciar.

**Servicio `db`**: usa `mariadb:10.11`. La clave del funcionamiento automático es el volumen de montaje `./backup-pucp.sql:/docker-entrypoint-initdb.d/backup-pucp.sql:ro`. MariaDB, al iniciar por primera vez (cuando `db_data` está vacío), ejecuta automáticamente todos los archivos `.sql`, `.sh` y `.sql.gz` que encuentre en `/docker-entrypoint-initdb.d/`, importando así toda la base de datos sin intervención manual.

El volumen `db_data` persiste los datos de la base de datos entre reinicios del contenedor. Al hacer `docker compose down -v`, este volumen se elimina, forzando una reimportación del SQL en el próximo inicio.

---

## Retos Encontrados

Durante el desarrollo del proyecto encontramos varios problemas que nos tomó tiempo resolver:

**1. La base de datos no se importaba automáticamente.** Al principio, cuando levantábamos Docker Compose, WordPress cargaba correctamente pero la base de datos estaba vacía (veíamos el instalador de WordPress o la página por defecto). Descubrimos que esto pasaba porque el volumen `db_data` ya existía de una instalación anterior de MariaDB, y Docker no vuelve a ejecutar los scripts de inicialización si el volumen ya tiene datos. La solución fue hacer `docker compose down -v` para eliminar el volumen y forzar la reimportación del SQL.

**2. Las imágenes del tema no cargaban.** Configuramos las imágenes de las noticias como rutas relativas (por ejemplo, `assets/images/juegos-postgrado.jpg`) en el metadato `_pucp_image_url`, pero inicialmente el tema las mostraba como rutas rotas. Tuvimos que implementar la función `pucp_get_post_image_url()` que detecta si el valor es una URL absoluta o relativa, y en el caso de una ruta relativa, la concatena con `get_stylesheet_directory_uri()` para construir la URL completa correcta.

**3. El tema no se activaba automáticamente.** La primera vez que levantamos el proyecto sin el `backup-pucp.sql`, WordPress usaba su tema por defecto (Twenty Twenty-Five) en lugar del nuestro. La solución fue incluir en el SQL los registros de `wp_options` que configuran `template`, `stylesheet` y `current_theme` con los valores del tema `pucp-clone`.

**4. Conflictos de puertos.** El puerto 3306 de MariaDB ya estaba en uso en nuestras máquinas por instalaciones locales de MySQL. Resolvimos esto mapeando el puerto externo al 3307 (`3307:3306`) en el `docker-compose.yml`.

**5. La reescritura de URLs no funcionaba.** Las URLs amigables mostraban error 404 porque el módulo `mod_rewrite` de Apache no estaba habilitado o el archivo `.htaccess` no se aplicaba correctamente. La imagen oficial de WordPress ya maneja esto internamente, pero tuvimos que asegurarnos de que el `.htaccess` del directorio `wordpress/` estuviera incluido en el repositorio.

**6. Configurar el Customizer de WordPress.** Nos costó entender cómo funciona el sistema de `add_setting` y `add_control` del Customizer. Tuvimos que leer la documentación de WordPress y hacer varias pruebas hasta que los valores editados desde el panel se reflejaran correctamente en la vista pública del sitio.

---

## Conclusiones

Este laboratorio fue una experiencia muy enriquecedora que nos permitió entender cómo funciona en la práctica el desarrollo web basado en CMS, que es algo que en los cursos teóricos se menciona mucho pero pocas veces se aborda de manera tan completa.

Aprender a usar WordPress no solo como usuario final sino como desarrolladores —creando un tema desde cero y extendiendo sus funcionalidades con un plugin propio— nos dio una comprensión mucho más profunda de su arquitectura interna: la jerarquía de plantillas, el sistema de hooks, el loop de WordPress, las WP_Query y el Customizer son conceptos que ahora entendemos con claridad porque los usamos directamente en código.

La parte de Docker fue especialmente valiosa. Antes del laboratorio, algunos de nosotros solo conocíamos Docker de manera superficial. Entender cómo levantar dos servicios coordinados, cómo funciona la inicialización automática de la base de datos y cómo los volúmenes gestionan la persistencia nos dio una habilidad que sabemos que vamos a necesitar en el entorno profesional.

También fue interesante trabajar con un caso real: clonar el sitio de la PUCP no es solo copiar un diseño, sino entender cómo está estructurado, qué recursos usa (Bootstrap, jQuery, Google Fonts) y cómo replicarlos dentro de WordPress de manera limpia y mantenible.

Finalmente, el proceso de documentar todo en este README nos hizo reflexionar sobre aspectos del proyecto que no habíamos pensado de manera explícita: la arquitectura, el flujo de datos, las decisiones técnicas tomadas. Documentar es parte del trabajo de ingeniería, y este laboratorio lo refuerza de buena manera.

---

## Recomendaciones

- **No usar credenciales por defecto en producción.** Las credenciales `admin/admin` y las contraseñas de base de datos `wordpress/wordpress` son adecuadas para un entorno de laboratorio local, pero nunca deben usarse en un servidor accesible desde internet. Siempre se deben usar contraseñas fuertes y únicas.

- **Usar un archivo `.env`** para externalizar las variables de entorno sensibles en lugar de hardcodearlas en `docker-compose.yml`. Esto facilita cambiar configuraciones sin modificar el archivo de orquestación directamente.

- **Hacer backups regulares del SQL.** Si se agrega contenido nuevo al sitio a través del panel de administración, ese contenido solo existe en el volumen de Docker. Para persistirlo en el repositorio, hay que exportar un nuevo dump: `docker exec wordpress_db mysqldump -u wordpress -pwordpress wordpress > backup-pucp.sql`.

- **Mantener el tema y el plugin bajo control de versiones.** La carpeta `wordpress/wp-content/themes/pucp-clone/` y `wordpress/wp-content/plugins/pucp-campus-tools/` son el código que realmente desarrollamos. Todo lo demás (el núcleo de WordPress) es una dependencia que podría gestionarse con WP-CLI en lugar de incluirse en el repositorio.

- **Explorar el uso de WP-CLI** para automatizar tareas: activar temas, importar contenido, limpiar caché, etc. Se puede usar directamente en el contenedor de WordPress con `docker exec -it wordpress_app wp --allow-root theme list`.

---

## Mejoras Futuras

Si tuviéramos más tiempo para continuar el proyecto, estas son las mejoras que consideramos más importantes:

- **Internacionalización real**: implementar un selector de idioma funcional que cambie el contenido del sitio entre español e inglés, aprovechando el soporte multilingüe de WordPress.

- **Integración con la API REST de WordPress**: el plugin ya expone el CPT `pucp_servicio` en la REST API (`show_in_rest: true`). Una mejora sería crear una sección del sitio que consuma esta API con JavaScript (Fetch API) para cargar los servicios de manera dinámica sin recargar la página.

- **Autenticación de usuarios**: implementar un sistema de login para estudiantes y docentes que les permita acceder a contenido exclusivo (horarios, notas, trámites), usando el sistema de roles y capacidades de WordPress.

- **Optimización de imágenes**: actualmente las imágenes se sirven directamente sin compresión ni formatos modernos (WebP). Integrar un plugin de optimización de imágenes mejoraría el rendimiento del sitio.

- **Despliegue en la nube**: configurar un despliegue en Railway, Render o AWS con HTTPS, dominio personalizado y variables de entorno seguras, para que el sitio sea accesible públicamente.

- **Sistema de caché**: instalar y configurar un plugin de caché (como W3 Total Cache o WP Super Cache) para mejorar el rendimiento en producción, ya que actualmente cada petición genera una consulta a la base de datos.

- **Formulario de contacto**: agregar un formulario funcional para que los visitantes puedan comunicarse con la institución, usando el plugin Contact Form 7 o desarrollando uno propio.

- **Cobertura de testing**: implementar pruebas automatizadas con PHPUnit para el plugin `PUCP Campus Tools`, verificando que el shortcode renderice correctamente y que el CPT se registre con los atributos esperados.

---

## Referencias

- WordPress. (2024). *WordPress Developer Resources*. https://developer.wordpress.org/
- WordPress. (2024). *Theme Handbook*. https://developer.wordpress.org/themes/
- WordPress. (2024). *Plugin Handbook*. https://developer.wordpress.org/plugins/
- WordPress. (2024). *WP_Query class reference*. https://developer.wordpress.org/reference/classes/wp_query/
- WordPress. (2024). *Theme Customization API*. https://developer.wordpress.org/themes/customize-api/
- Docker. (2024). *Docker Documentation*. https://docs.docker.com/
- Docker. (2024). *Docker Compose file reference*. https://docs.docker.com/compose/compose-file/
- Docker Hub. (2024). *WordPress official image*. https://hub.docker.com/_/wordpress
- Docker Hub. (2024). *MariaDB official image*. https://hub.docker.com/_/mariadb
- MariaDB Foundation. (2024). *MariaDB Server Documentation*. https://mariadb.com/kb/en/
- Bootstrap. (2024). *Bootstrap 3 Documentation*. https://getbootstrap.com/docs/3.3/
- Google Fonts. (2024). *Montserrat & Roboto font families*. https://fonts.google.com/
- PUCP. (2024). *Portal oficial de la Pontificia Universidad Católica del Perú*. https://www.pucp.edu.pe/
- WhatRuns. (2024). *WhatRuns - Discover What Runs a Website*. https://www.whatruns.com/
- PHP Group. (2024). *PHP Manual*. https://www.php.net/manual/es/
- Pressman, R. S. (2014). *Ingeniería del Software: Un enfoque práctico* (7.ª ed.). McGraw-Hill.

---

*Laboratorio desarrollado en el marco del curso de Ingeniería de Software — PUCP 2026-1.*
