# NetworkSentry AI

## Título del Proyecto y Descripción General

**NetworkSentry AI** es una plataforma web para el monitoreo centralizado de redes, DVR/NVR, routers, switches, televisores y cámaras IP distribuidas en diferentes sitios.

La aplicación atiende la dificultad de supervisar múltiples ubicaciones desde herramientas aisladas. Permite consultar el estado de los equipos, revisar el rendimiento y el SLA de las últimas 24 horas, visualizar zonas y transmisiones simuladas, analizar grabaciones, documentar incidencias y aplicar controles asociados a roles de usuario.

El sistema contempla tres perfiles:

- **Super Admin:** administra sitios, zonas, dispositivos, usuarios, canales de alerta y reglas.
- **Técnico SOC:** supervisa equipos, ejecuta diagnósticos y scripts simulados, cambia estados y documenta incidencias.
- **Cliente:** consulta únicamente los sitios que tiene asignados, junto con cámaras, grabaciones y métricas de disponibilidad.

Los datos de demostración se cargan desde `data.json`. Los cambios realizados en el navegador se conservan mediante `localStorage`, mientras que la sesión activa se mantiene mediante `sessionStorage`. Las automatizaciones, terminales, transmisiones y alertas tienen fines didácticos y deben sustituirse por servicios reales antes de un despliegue productivo.

## Tecnologías y Librerías Utilizadas

- **HTML5:** estructura semántica de los portales, formularios, tablas y ventanas modales.
- **CSS3:** diseño responsivo, identidad visual, estados de dispositivos y componentes de interfaz.
- **JavaScript:** lógica de autenticación, navegación, permisos, renderizado dinámico, validaciones y persistencia local.
- **JSON:** almacenamiento inicial de usuarios, sitios, zonas, equipos, incidencias, auditoría y configuración.
- **API Fetch:** carga asíncrona de `data.json`.
- **Web Storage API:** persistencia mediante `localStorage` y `sessionStorage`.
- **Canvas API:** generación dinámica de las vistas simuladas de cámaras.
- **Sin frameworks de frontend:** el proyecto utiliza JavaScript nativo y no requiere React, Angular, Vue u otras librerías.
- **Python/Pandas:** no forman parte de la implementación actual. Python puede utilizarse opcionalmente para levantar un servidor HTTP local.

## Estructura del Repositorio

- **`index.html`:** contiene la estructura principal de la interfaz, incluidos los portales de inicio de sesión, el hub de sitios, los perfiles, los módulos de administración y los modales.
- **`app.js`:** implementa el estado de la aplicación, autenticación, permisos, carga de datos, renderizado, formularios, terminal IA, grabaciones, administración y eventos.
- **`style.css`:** define los estilos generales y responsivos de todos los componentes.
- **`data.json`:** aporta los datos iniciales de demostración: usuarios, sitios, zonas, dispositivos y configuración.
- **`README.md`:** describe el proyecto, su instalación, configuración y uso básico.

## Instrucciones de Instalación y Configuración

### Requisitos previos

- Navegador moderno compatible con JavaScript y Web Storage.
- Editor opcional: Visual Studio Code.
- Para la ejecución recomendada: Python 3.10 o superior.
- Conexión a Internet solo si se utiliza una plataforma de alojamiento; no es necesaria para ejecutar el servidor local.

### Ejecución en una estación de trabajo local

1. Descargue o clone el repositorio.
2. Coloque todos los archivos del proyecto en una misma carpeta.
3. Abra una terminal o PowerShell en esa carpeta.
4. Inicie un servidor HTTP local:

   ```powershell
   python -m http.server 8000
   ```

5. Abra `http://localhost:8000` en el navegador.
6. Seleccione uno de los portales de inicio de sesión.

No se recomienda abrir `index.html` directamente mediante `file://`, porque el navegador puede impedir la carga de `data.json` con `fetch`. En ese caso, el sistema usa un modo de respaldo limitado y, normalmente, solo permite acceder con la cuenta administrativa.

### Datos y persistencia

Al iniciar por primera vez, la aplicación intenta cargar en el siguiente orden:

1. Los datos guardados en `localStorage`.
2. Los datos iniciales de `data.json`.
3. Los datos de respaldo definidos en `app.js` si `data.json` no puede cargarse.

La contraseña inicial almacenada en `data.json` se convierte a un hash didáctico al cargar la aplicación. Las modificaciones de dispositivos, perfiles y configuración continúan en el navegador actual. Para restaurar los datos iniciales:

1. Abra las herramientas de desarrollo del navegador.
2. Acceda a la sección de almacenamiento de la aplicación.
3. Elimine la clave `nsai_v3`.
4. Elimine también `nsai_sess_v3` si desea cerrar la sesión guardada.
5. Recargue la página.

> Nota: este mecanismo es adecuado para demostración académica. No sustituye una base de datos ni un sistema seguro de autenticación y autorización del lado del servidor.

### Cuentas de demostración

| Rol | Usuario | Contraseña | Portal |
|---|---|---|---|
| Super Admin | `admin` | `Sentry#2026` | Personal / Admin |
| Técnico SOC | `tecnico1` | `Soc#Tecnico26` | Personal / Admin |
| Cliente | `cliente1` | `Cliente#2026` | Cliente |
| Cliente | `cliente2` | `Empresa#2026` | Cliente |

### Despliegue en la nube

Al ser una aplicación completamente estática, puede publicarse en GitHub Pages, Netlify, Azure Static Web Apps o un servidor web convencional.

Ejemplo con GitHub Pages:

1. Cree un repositorio y cargue `index.html`, `app.js`, `style.css`, `data.json` y `README.md`.
2. En la configuración del repositorio, abra **Pages**.
3. Seleccione la rama principal y la carpeta raíz `/`.
4. Guarde los cambios y espere la generación del sitio.

Para Netlify o Azure Static Web Apps puede arrastrarse la carpeta del proyecto al panel correspondiente o conectarse el repositorio. No configure un comando de compilación, ya que no existe una etapa de compilación.

## Guía Rápida de Uso

1. Acceda a `http://localhost:8000` o al sitio publicado.
2. Pulse **Portal Cliente** o **Portal Técnico / Admin**.
3. Inicie sesión con una cuenta de demostración.
4. En el hub, utilice los filtros para buscar por nombre, dirección, tipo, equipo o dirección IP.
5. Pulse **Abrir panel** sobre un sitio para consultar sus datos.
6. Navegue por las pestañas disponibles según el rol:
   - consulte dispositivos y estado por zona;
   - revise la imagen en vivo simulada;
   - consulte grabaciones;
   - revise disponibilidad y SLA;
   - acceda al terminal IA;
   - documente incidencias.
7. Como Super Admin, ingrese a **Administración** para crear usuarios, administrar canales y configurar reglas.
8. Como usuario autenticado, ingrese a **Mi perfil** para actualizar datos personales, redes sociales, fotografía y contraseña.
9. Use **Cerrar sesión** al finalizar. La sesión puede cerrarse automáticamente después de 15 minutos de inactividad.
