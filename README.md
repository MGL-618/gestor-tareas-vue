# Gestor de tareas para estudiantes

Aplicación web desarrollada con Vue 3 y Vite para organizar las actividades académicas de un estudiante.

## Funcionalidades

- Crear, editar y eliminar tareas.
- Marcar tareas como pendientes o completadas.
- Filtrar tareas por su estado.
- Organizar actividades por materia, prioridad y fecha de entrega.
- Consultar estadísticas de las tareas.
- Conservar los datos en el navegador mediante localStorage.
- Interfaz adaptable a diferentes tamaños de pantalla.

## Tecnologías

- Vue 3
- JavaScript
- Vite
- HTML y CSS
- localStorage

## Requisitos

- Git.
- Node.js compatible con la versión indicada en `package.json`.
- npm, incluido con Node.js.

## Instalación

Clona el repositorio:

```bash
git clone https://github.com/MGL-618/gestor-tareas-vue.git
```

Entra en la carpeta del proyecto:

```bash
cd gestor-tareas-vue
```

Instala las dependencias:

```bash
npm install
```

Inicia el servidor de desarrollo:

```bash
npm run dev
```

Abre en el navegador la dirección local que muestre la terminal, normalmente `http://localhost:5173/`.

## Compilación para producción

Para generar la versión de producción:

```bash
npm run build
```

Los archivos generados se guardan en la carpeta `dist/`.

## Almacenamiento de datos

Las tareas se guardan en el almacenamiento local del navegador. Por lo tanto, los datos no se sincronizan automáticamente entre diferentes navegadores o computadoras.

## Autoría

Proyecto académico de Programación Web, desarrollado como práctica de Vue 3.
