# Guía de instalación y ejecución en Windows 11

## 1. Objetivo

Esta guía explica cómo descargar, instalar, ejecutar y comprobar el funcionamiento del Gestor de tareas para estudiantes en Windows 11.

Está dirigida a personas que pueden no tener experiencia con Git, Node.js, npm, Vue o Vite. Sigue los pasos en orden y no continúes si un requisito previo presenta errores.

> **Importante:** esta guía se ha preparado a partir de la configuración del repositorio. Antes de afirmar que el procedimiento está validado en Windows 11, debe completarse una instalación de prueba en ese sistema.

## 2. ¿Qué tecnologías utilizaremos?

- **Windows 11:** sistema operativo.
- **Git:** descarga el código del repositorio de GitHub.
- **Node.js:** entorno de ejecución de JavaScript necesario para las herramientas del proyecto.
- **npm:** administra e instala las dependencias.
- **Vue 3:** framework utilizado para construir la interfaz.
- **Vite 8:** herramienta que inicia el servidor de desarrollo y compila la aplicación.
- **Navegador:** permite utilizar la aplicación.

No necesitas instalar Vue globalmente, configurar una base de datos ni instalar Visual Studio Code. Puedes usar un editor de texto si solo quieres ejecutar y probar el proyecto.

## 3. Requisitos previos

Necesitas:

- Una computadora con Windows 11.
- Conexión a Internet para descargar las herramientas y dependencias.
- Permisos suficientes para instalar Git y Node.js si todavía no están instalados.
- Un navegador actualizado.
- Una versión compatible de Node.js.

### Versión de Node.js requerida

El archivo `package.json` de este proyecto declara:

`^22.18.0 || >=24.12.0`

Esto significa que son compatibles:

- Node.js 22.18.0 o posterior dentro de la versión principal 22, sin llegar a la 23.
- Node.js 24.12.0 o cualquier versión posterior que cumpla esa condición.

**Recomendación para una instalación nueva:** utiliza la versión LTS compatible que ofrece la página oficial de Node.js. Comprueba siempre que la versión instalada cumpla el requisito anterior.

No instales Node.js 18 ni una versión anterior de Node.js 22 pensando que cualquier versión sirve: no cumplen el requisito declarado por este proyecto.

- Descarga oficial: https://nodejs.org/en/download/
- Documentación de npm: https://docs.npmjs.com/

## 4. Abrir PowerShell

PowerShell es la terminal donde ejecutaremos los comandos.

1. Abre el menú Inicio de Windows.
2. Escribe `PowerShell`.
3. Abre Windows PowerShell o PowerShell.
4. Escribe los comandos de esta guía y presiona Enter para ejecutarlos.

Cuando un comando termine, normalmente volverás a ver una línea de entrada donde puedes escribir el siguiente.

## 5. Comprobar e instalar Git

### 5.1. Comprobar si Git ya está instalado

Ejecuta:

```powershell
git --version
```

Si aparece algo parecido a `git version 2.x.x.windows.x`, Git está disponible. El número exacto puede ser diferente y no necesitas reinstalarlo solo porque sea distinto.

Si PowerShell indica que `git` no se reconoce como comando, continúa con la instalación.

### 5.2. Instalar Git si hace falta

1. Abre la página oficial: https://git-scm.com/install/windows
2. Descarga el instalador apropiado para tu equipo. En la mayoría de las computadoras con procesador Intel o AMD corresponde la arquitectura x64.
3. Ejecuta el instalador.
4. Si no sabes qué opciones elegir, conserva las opciones predeterminadas.
5. Finaliza la instalación.
6. Cierra todas las ventanas de PowerShell que estuvieran abiertas y abre una nueva. Una terminal ya abierta puede no reconocer las herramientas recién instaladas.
7. Vuelve a ejecutar:

```powershell
git --version
```

Continúa cuando aparezca una versión.

## 6. Comprobar e instalar Node.js y npm

### 6.1. Comprobar Node.js

Ejecuta:

```powershell
node --version
```

Si aparece una versión, por ejemplo `v24.x.x`, comprueba que cumpla los requisitos de la sección 3.

Si el comando no se reconoce o la versión no es compatible, instala Node.js.

### 6.2. Instalar Node.js

1. Abre https://nodejs.org/en/download/
2. Selecciona una versión LTS que cumpla los requisitos de la sección 3.
3. Descarga el instalador para Windows. En la mayoría de los equipos Intel o AMD será el instalador `.msi` x64.
4. Ejecuta el instalador y acepta la licencia.
5. Conserva las opciones predeterminadas, incluida la opción de agregar Node.js al PATH, si aparece.
6. Finaliza la instalación.
7. Cierra PowerShell y abre una ventana nueva.
8. Comprueba la instalación:

```powershell
node --version
```

La versión mostrada debe ser compatible con este proyecto.

### 6.3. Comprobar npm

Ejecuta:

```powershell
npm --version
```

Debe aparecer un número de versión. npm se instala normalmente junto con Node.js mediante el instalador oficial.

Si `node` funciona, pero `npm` no se reconoce:

1. Cierra y vuelve a abrir PowerShell.
2. Ejecuta `npm --version` de nuevo.
3. Si sigue fallando, revisa la instalación de Node.js y su configuración del PATH. Repara o reinstala Node.js desde la página oficial si es necesario.

**No continúes hasta que Git, Node.js y npm respondan correctamente.**

## 7. Elegir dónde guardar el proyecto

El comando `git clone` crea la carpeta del proyecto dentro de la ubicación actual de PowerShell. Para evitar perderla entre otras carpetas, recomendamos crear una carpeta propia dentro de tu perfil de usuario.

Ejecuta:

```powershell
New-Item -ItemType Directory -Force "$HOME\proyectos"
Set-Location "$HOME\proyectos"
Get-Location
```

Estos comandos crean la carpeta `proyectos` dentro de tu perfil, entran en ella y muestran la ruta actual.

Puedes utilizar otra ubicación si lo prefieres. Lo importante es saber dónde descargaste el repositorio.

## 8. Descargar el repositorio desde GitHub

Comprueba que estás en la carpeta donde quieres guardar el proyecto. Después ejecuta:

```powershell
git clone https://github.com/MGL-618/gestor-tareas-vue.git
```

El repositorio es público; no necesitas iniciar sesión en GitHub para clonarlo.

Este comando descarga el código y crea una carpeta llamada `gestor-tareas-vue`.

### Entrar en la carpeta del proyecto

Ejecuta:

```powershell
Set-Location .\gestor-tareas-vue
Get-Location
```

La ruta mostrada debe terminar en `proyectos\gestor-tareas-vue`, si seguiste la ubicación recomendada.

Comprueba los archivos:

```powershell
Get-ChildItem
```

Entre los archivos y carpetas debes encontrar `package.json`, `package-lock.json`, `README.md`, `GUIA-INSTALACION-WINDOWS.md` y `src`.

Si la carpeta ya existe y Git indica que no puede clonar en ella, no borres nada automáticamente. Es posible que el proyecto ya esté descargado. Comprueba la ubicación y entra en la carpeta existente.

## 9. Instalar las dependencias del proyecto

Asegúrate de estar dentro de `gestor-tareas-vue`. Puedes verificarlo con:

```powershell
Get-Location
```

Después ejecuta:

```powershell
npm ci
```

### ¿Qué hace este comando?

Instala las dependencias definidas para el proyecto usando `package-lock.json`, el archivo que registra las versiones resueltas. Esto ayuda a que diferentes integrantes del equipo instalen un conjunto coherente de dependencias.

La primera instalación puede tardar varios minutos. Necesitas conexión a Internet.

Espera hasta que termine y vuelva a aparecer la línea de entrada de PowerShell. Si aparecen mensajes de advertencia, no necesariamente significa que la instalación haya fallado; revisa si npm termina con un error.

No necesitas repetir la instalación cada vez que abras la aplicación. Normalmente se hace al descargar el proyecto por primera vez o cuando necesitas reconstruir las dependencias.

### Si `npm ci` falla

1. Lee el mensaje de error completo.
2. Confirma que estás dentro de `gestor-tareas-vue`.
3. Comprueba que existen `package.json` y `package-lock.json`.
4. Revisa tu conexión a Internet y vuelve a intentar solo si el error indica un problema temporal de red.

Si npm informa que `package.json` y `package-lock.json` no coinciden, no borres el archivo de bloqueo como primera solución. El repositorio debe corregirse y publicarse con ambos archivos sincronizados. Conserva el mensaje de error para diagnosticarlo.

## 10. Iniciar la aplicación

Desde la carpeta del proyecto, ejecuta:

```powershell
npm run dev
```

Vite iniciará el servidor de desarrollo. Si todo funciona, aparecerá una dirección similar a:

```text
Local: http://localhost:5173/
```

El puerto puede ser diferente si el 5173 ya está ocupado. Utiliza la dirección exacta que muestre tu terminal.

### Abrir la aplicación en el navegador

1. Selecciona y copia la dirección que aparece junto a `Local`.
2. Abre Brave, Chrome, Edge o Firefox.
3. Pega la dirección en la barra de direcciones y presiona Enter.

Mientras utilizas la aplicación, deja abierta la ventana de PowerShell. El servidor se ejecuta en ella; cerrarla detendrá el servidor.

### Detener el servidor

Cuando quieras cerrar la aplicación:

1. Regresa a la ventana de PowerShell donde se está ejecutando Vite.
2. Presiona `Ctrl + C`.
3. Si la terminal muestra una solicitud de confirmación, sigue las indicaciones que aparezcan. No todas las sesiones muestran esa pregunta.

Para volver a iniciar la aplicación más adelante, abre PowerShell, entra en la carpeta del proyecto y ejecuta `npm run dev`.

## 11. Probar las funcionalidades

Con la aplicación abierta, realiza estas pruebas:

1. Crea una tarea.
2. Edita una tarea existente.
3. Marca una tarea como completada y después vuelve a dejarla pendiente.
4. Filtra las tareas por estado.
5. Elimina una tarea.
6. Recarga la página y comprueba si las tareas guardadas siguen apareciendo.

Si alguna prueba falla, anota qué hiciste, qué esperabas que ocurriera y qué sucedió realmente.

### Cómo se guardan los datos

La aplicación utiliza `localStorage` del navegador. Las tareas se guardan localmente en el navegador y perfil donde se utilizó la aplicación.

Por eso, los datos no se sincronizan automáticamente entre computadoras, perfiles de navegador o navegadores diferentes. Borrar los datos del sitio en el navegador puede eliminar las tareas guardadas.

## 12. Comprobar la compilación de producción (opcional)

Esta prueba no es necesaria para iniciar la aplicación, pero ayuda a verificar que el proyecto puede compilarse.

Detén el servidor con `Ctrl + C` si sigue activo. Desde la carpeta del proyecto, ejecuta:

```powershell
npm run build
```

Si la compilación termina correctamente, Vite generará los archivos de producción en la carpeta `dist`.

Que la compilación funcione es una comprobación adicional; para utilizar la aplicación durante el desarrollo, el comando habitual sigue siendo `npm run dev`.

## 13. Solución de problemas frecuentes

### 13.1. `git` no se reconoce

Git no está instalado correctamente o PowerShell no encuentra su ubicación.

- Instala Git desde https://git-scm.com/install/windows.
- Cierra y vuelve a abrir PowerShell.
- Ejecuta `git --version` de nuevo.

### 13.2. `node` o `npm` no se reconocen

Node.js puede faltar, haberse instalado incorrectamente o no estar disponible en el PATH de la terminal.

- Cierra y vuelve a abrir PowerShell.
- Ejecuta `node --version` y `npm --version`.
- Si persiste el problema, revisa o repara la instalación desde https://nodejs.org/en/download/.

### 13.3. La versión de Node.js no es compatible

Comprueba la salida de `node --version` y compárala con los requisitos de la sección 3. Instala una versión compatible de Node.js si es necesario.

### 13.4. PowerShell indica que no puede ejecutar `npm.ps1`

Puede aparecer un mensaje que indique que la ejecución de scripts está deshabilitada o que no se puede cargar `npm.ps1`.

Primero, no cambies la política de seguridad de Windows. Prueba a utilizar el ejecutable de npm para Windows:

```powershell
npm.cmd ci
```

Para iniciar el servidor, utiliza:

```powershell
npm.cmd run dev
```

Si necesitas compilar:

```powershell
npm.cmd run build
```

Estos comandos permiten invocar `npm.cmd` explícitamente. Si también fallan, conserva el mensaje de error y revisa la instalación de Node.js.

### 13.5. `npm ci` falla

- Comprueba la conexión a Internet.
- Confirma que estás dentro de la carpeta `gestor-tareas-vue`.
- Comprueba que existen `package.json` y `package-lock.json`.
- Lee el mensaje completo y distingue entre un problema de red, permisos, versión de Node.js o archivos de dependencias incompatibles.

No borres `package-lock.json` ni ejecutes comandos de limpieza destructivos sin conocer la causa.

### 13.6. El navegador no abre la aplicación

- Comprueba que `npm run dev` sigue ejecutándose.
- Copia la dirección que Vite muestra junto a `Local`.
- Si aparece otro puerto, utiliza el que indica Vite.
- Si aparece un error en la terminal, guarda el texto para diagnosticarlo.

### 13.7. El puerto predeterminado está ocupado

Vite puede iniciar el servidor en otro puerto y mostrar una dirección diferente. Abre esa dirección. No supongas que siempre será `http://localhost:5173/`.

### 13.8. La aplicación abre, pero una función no funciona

- Recarga la página y repite la prueba.
- Comprueba si la terminal muestra errores.
- Anota los pasos para reproducir el problema y el resultado esperado.
- Si el problema continúa, comparte el mensaje de error sin eliminar archivos del proyecto.

### 13.9. Cerré PowerShell y no encuentro el proyecto

Si seguiste la ubicación recomendada, el proyecto está en:

`$HOME\proyectos\gestor-tareas-vue`

En una nueva ventana de PowerShell puedes volver a esa carpeta con:

```powershell
Set-Location "$HOME\proyectos\gestor-tareas-vue"
```

Si elegiste otra ubicación, sustituye la ruta por la carpeta donde clonaste el repositorio.

### 13.10. Git indica que la carpeta ya existe al clonar

No repitas `git clone` dentro de una carpeta de proyecto ya creada. Entra en la carpeta existente y comprueba que corresponde al repositorio correcto.

Si necesitas volver a descargar el proyecto desde cero, primero asegúrate de que no tienes archivos propios que quieras conservar.

## 14. Uso habitual después de la instalación inicial

Cuando Git y Node.js ya estén instalados y el repositorio esté descargado, normalmente bastará con:

1. Abrir PowerShell.
2. Entrar en la carpeta del proyecto.
3. Ejecutar `npm run dev`.
4. Abrir en el navegador la dirección mostrada por Vite.
5. Detener el servidor con `Ctrl + C` al terminar.

No necesitas clonar el repositorio ni reinstalar las dependencias cada vez que quieras utilizarlo.

Si actualizas el proyecto y cambian sus dependencias, sigue las instrucciones del equipo para instalar las dependencias actualizadas.

## 15. Referencias oficiales

- Repositorio del proyecto: https://github.com/MGL-618/gestor-tareas-vue
- Git para Windows: https://git-scm.com/install/windows
- Descargas de Node.js: https://nodejs.org/en/download/
- Documentación de npm: https://docs.npmjs.com/
- Guía oficial de Vite: https://vite.dev/guide/
- Políticas de ejecución de PowerShell: https://learn.microsoft.com/es-es/powershell/module/microsoft.powershell.security/set-executionpolicy

## 16. Estado de validación

La compilación de producción se ha comprobado en el entorno Fedora del desarrollador. La instalación y ejecución descritas para Windows 11 deben validarse en una computadora con ese sistema antes de considerar la guía probada de extremo a extremo.
