# ProjectsApp

Aplicación de gestión de proyectos y tareas desarrollada con Vue 3 y TypeScript.

## Tecnologías Utilizadas

- Vue 3
- TypeScript
- Vite
- DaisyUI
- Pinia

## Configuración Recomendada del IDE

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (y deshabilitar Vetur).

## Soporte de TypeScript para Importaciones `.vue`

TypeScript no puede manejar la información de tipos para importaciones `.vue` por defecto, por lo que reemplazamos el CLI `tsc` con `vue-tsc` para la verificación de tipos. En los editores, necesitamos [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) para que el servicio de lenguaje TypeScript sea consciente de los tipos `.vue`.

## Configuración del Proyecto

```sh
npm install
```

### Compilar y Hot-Reload para Desarrollo

```sh
npm run dev
```

### Verificación de Tipos, Compilación y Minificación para Producción

```sh
npm run build
```
