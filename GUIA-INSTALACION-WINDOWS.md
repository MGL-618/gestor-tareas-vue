# Guía de instalación y ejecución en Windows 11

## 1. Objetivo

Esta guía explica cómo preparar una computadora con Windows 11 para descargar, instalar y ejecutar el Gestor de tareas para estudiantes, desarrollado con Vue 3 y Vite.

Los pasos están pensados para una computadora que puede no tener las herramientas necesarias instaladas.

## 2. Tecnologías que utilizaremos

- **Windows 11:** sistema operativo de la computadora.
- **Git:** permite descargar el proyecto desde GitHub.
- **Node.js:** proporciona el entorno para ejecutar las herramientas de desarrollo.
- **npm:** instala las dependencias que necesita el proyecto.
- **Vue 3:** framework utilizado para construir la interfaz.
- **Vite:** servidor de desarrollo que permite ejecutar la aplicación en el navegador.
- **Brave, Chrome, Edge o Firefox:** navegador para visualizar la aplicación.

No es necesario instalar Vue globalmente ni instalar una base de datos. Tampoco se requiere Visual Studio Code para ejecutar el proyecto.

## 3. Abrir PowerShell

1. Abre el menú Inicio de Windows.
2. Escribe `PowerShell`.
3. Abre Windows PowerShell o PowerShell.
4. Ejecuta los comandos de esta guía en esa terminal.

En los siguientes pasos, cada herramienta se comprobará antes de instalarla.

## 4. Comprobar si Git está instalado

Ejecuta:

```powershell
git --version
```

### Si Git está instalado

Aparecerá un resultado parecido a:

```text
git version 2.x.x.windows.x
```

El número exacto puede ser diferente. Si aparece una versión, continúa con la sección 5.

### Si aparece un error

Si Windows indica que `git` no se reconoce como comando, instala Git for Windows.

1. Abre la página oficial: https://git-scm.com/install/windows
2. Descarga el instalador correspondiente a tu computadora. En la mayoría de los equipos con procesador Intel o AMD será la versión x64.
3. Ejecuta el instalador.
4. Si no sabes qué opciones elegir, conserva las opciones predeterminadas.
5. Termina la instalación.
6. Cierra PowerShell y abre una ventana nueva.
7. Ejecuta nuevamente:

```powershell
git --version
```

Continúa cuando aparezca una versión de Git.

## 5. Comprobar si Node.js está instalado

Ejecuta:

```powershell
node --version
```

Este comando muestra la versión instalada de Node.js.

### Si Node.js está instalado

El proyecto requiere una versión compatible con alguna de estas condiciones:

- Node.js 22.18.0 o posterior dentro de la rama 22.
- Node.js 24.12.0 o posterior.

Para una instalación nueva, recomendamos Node.js 24 LTS.

Si tienes una versión compatible, continúa con la sección 6.

### Si Node.js falta o es incompatible

1. Abre la página oficial: https://nodejs.org/en/download
2. Selecciona la versión **LTS**.
3. Descarga el instalador para Windows con extensión `.msi` y la arquitectura correspondiente a tu equipo. Para la mayoría de las computadoras Intel o AMD será x64.
4. Ejecuta el instalador.
5. Acepta la licencia y conserva las opciones predeterminadas, incluida la opción de agregar Node.js al PATH.
6. Termina la instalación.
7. Cierra PowerShell y vuelve a abrirlo.
8. Ejecuta:

```powershell
node --version
```

Comprueba que la versión instalada sea compatible con los requisitos anteriores.

## 6. Comprobar si npm está instalado

Ejecuta:

```powershell
npm --version
```

npm se instala junto con Node.js mediante el instalador oficial.

### Si aparece una versión

Por ejemplo, `10.x.x` u otra versión compatible con la instalación de Node.js, continúa con la sección 7.

### Si npm no se reconoce

1. Cierra PowerShell y abre una terminal nueva.
2. Ejecuta de nuevo `npm --version`.
3. Si sigue sin reconocerse, revisa que Node.js se haya instalado correctamente y que su carpeta esté incluida en la variable PATH de Windows.
4. Si es necesario, repara o reinstala Node.js usando el instalador oficial.

No continúes hasta que `node --version` y `npm --version` funcionen.

## 7. Descargar el proyecto desde GitHub

Cuando Git esté instalado, ejecuta en PowerShell:

```powershell
git clone https://github.com/MGL-618/gestor-tareas-vue.git
```

Este comando descarga una copia del repositorio público a la carpeta actual de PowerShell.

Después entra en la carpeta del proyecto:

```powershell
cd gestor-tareas-vue
```

Comprueba que estás dentro de la carpeta correcta:

```powershell
Get-Location
```

La ruta mostrada debe terminar en `gestor-tareas-vue`.

También puedes comprobar que se encuentran los archivos principales:

```powershell
Get-ChildItem
```

Deben aparecer, entre otros, `package.json`, `package-lock.json`, `README.md` y la carpeta `src`.

## 8. Instalar las dependencias

Desde la carpeta `gestor-tareas-vue`, ejecuta:

```powershell
npm install
```

Este comando lee los archivos de configuración del proyecto e instala las dependencias necesarias, incluidas Vue y Vite.

La primera instalación puede tardar varios minutos, según la conexión a Internet.

Espera hasta que termine y vuelva a aparecer el indicador de PowerShell. Si npm muestra un error, consulta la sección 11 antes de continuar.

No necesitas ejecutar `npm install` cada vez que quieras abrir la aplicación. Normalmente solo es necesario al descargar el proyecto por primera vez o cuando cambian sus dependencias.

## 9. Iniciar la aplicación

En la misma carpeta, ejecuta:

```powershell
npm run dev
```

Vite iniciará un servidor de desarrollo. En la terminal aparecerá una dirección local parecida a:

```text
Local: http://localhost:5173/
```

Abre esa dirección en tu navegador.

Si Vite muestra otra dirección o puerto, utiliza exactamente la dirección que aparece en la terminal.

Mientras el servidor esté ejecutándose, no cierres esa ventana de PowerShell.

Para detenerlo, vuelve a la terminal y presiona `Ctrl + C`.

## 10. Probar las funciones

Una vez abierta la aplicación, comprueba las siguientes acciones:

1. Crear una tarea.
2. Editar una tarea existente.
3. Marcar una tarea como completada y volver a dejarla pendiente.
4. Filtrar las tareas por estado.
5. Eliminar una tarea.
6. Recargar la página y comprobar si las tareas guardadas siguen apareciendo.

Los datos se guardan en el almacenamiento local del navegador. Por tanto, no se sincronizan automáticamente entre computadoras o entre diferentes navegadores.

## 11. Solución de problemas frecuentes

### Error: `git` no se reconoce

Git no está instalado o Windows no encuentra su ubicación.

- Instala Git for Windows desde https://git-scm.com/install/windows.
- Cierra y vuelve a abrir PowerShell.
- Ejecuta `git --version` otra vez.

### Error: `node` o `npm` no se reconoce

Node.js no está instalado correctamente o la terminal no ha actualizado la variable PATH.

- Comprueba la instalación de Node.js.
- Cierra y vuelve a abrir PowerShell.
- Ejecuta `node --version` y `npm --version`.
- Si continúa el error, repara la instalación desde la página oficial de Node.js.

### Error de versión de Node.js

Si una herramienta indica que la versión de Node.js no es compatible, instala una versión que cumpla los requisitos de la sección 5 y vuelve a comprobar `node --version`.

### Error durante `npm install`

- Comprueba que tienes conexión a Internet.
- Confirma que estás dentro de la carpeta `gestor-tareas-vue`.
- Comprueba que `package.json` y `package-lock.json` existen.
- Lee el mensaje de error completo antes de intentar otras soluciones.

No borres archivos de configuración ni el archivo `package-lock.json` como primera solución.

### El navegador no abre la aplicación

- Comprueba que `npm run dev` sigue ejecutándose.
- Utiliza la dirección que Vite muestra en la terminal.
- Si el puerto 5173 está ocupado, Vite puede ofrecer otro puerto. Abre la dirección indicada.
- Si aparece un error en la terminal, conserva el mensaje para poder diagnosticarlo.

### La página abre, pero una función no funciona

Comprueba primero que no haya errores en la terminal. Después recarga la página y repite la prueba. Si el problema continúa, registra los pasos para reproducirlo y el mensaje de error.

## 12. Compilar la aplicación para producción

Como comprobación adicional, desde la carpeta del proyecto ejecuta:

```powershell
npm run build
```

Este comando genera una versión de producción en la carpeta `dist`.

Si termina sin errores, significa que Vite pudo compilar el proyecto. Para esta práctica, la ejecución durante el desarrollo se realiza con `npm run dev`.

## 13. Resumen de comandos

Una vez instalados Git y Node.js, la secuencia habitual para descargar y ejecutar el proyecto es:

```powershell
git clone https://github.com/MGL-618/gestor-tareas-vue.git
cd gestor-tareas-vue
npm install
npm run dev
```

La primera vez se deben completar todas las comprobaciones de las secciones anteriores. En ocasiones posteriores, si el proyecto ya está descargado y las dependencias instaladas, normalmente bastará con abrir PowerShell en la carpeta del proyecto y ejecutar `npm run dev`.

## 14. Repositorio

Código fuente: https://github.com/MGL-618/gestor-tareas-vue
