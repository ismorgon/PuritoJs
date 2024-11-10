
# 🌟 PuritoJs

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Twitter: PuritoJs](https://img.shields.io/twitter/follow/PuritoJs?style=social)](https://twitter.com/PuritoJs)

Framework frontend JavaScript diseñado para construir aplicaciones modernas y dinámicas con una sintaxis amigable, minimalista y potente.

---

## 📚 Tabla de Contenidos

- [🎯 Introducción](#-introducción)
- [🚀 Instalación](#-instalación)
- [🌟 Características](#-características)
- [📦 Componentes](#-componentes)
- [✨ Funciones Mágicas](#-funciones-mágicas)
- [💾 Estado Global](#-estado-global)
- [📡 Sistema de Señales](#-sistema-de-señales)
- [🛣️ Router](#️-router)
- [📝 Desarrollo y Contribuciones](#-desarrollo-y-contribuciones)
- [🔗 Redes y Soporte](#-redes-y-soporte)
- [📜 Licencia](#-licencia)

---

## 🎯 Introducción

**PuritoJs** es un framework de JavaScript para el frontend moderno que combina simplicidad y eficiencia sin sacrificar rendimiento. Su enfoque modular y ligero permite construir aplicaciones rápidas y dinámicas, manteniendo una sintaxis limpia y directa.

[🔝 Volver al inicio](#-tabla-de-contenidos)

---

## 🚀 Instalación

Para instalar PuritoJs en tu proyecto, usa:

```bash
npm install puritojs
```

[🔝 Volver al inicio](#-tabla-de-contenidos)

---

## 🌟 Características

PuritoJs se distingue por su estructura simplificada y sus herramientas intuitivas, ofreciendo las siguientes características:

- ✅ Componentes `Single File Components (.pjs)`: PuritoJs organiza cada componente en un solo archivo `.pjs`, donde se define la lógica, estilos y renderizado de forma modular.
- ✅ **Estado Global**: Permite un estado global flexible, organizado en "slots" para una gestión eficiente de la información compartida entre componentes.
- ✅ **Router**: Sistema de rutas dinámico y sencillo para definir, enlazar y gestionar navegación.
- ✅ **Sistema de Señales**: Comunicación ágil entre componentes sin necesidad de un sistema complejo de eventos.
- ❔ **Lazy Loading**: Implementación futura que permitirá cargar componentes según se necesiten, optimizando el rendimiento.
- ⚠️ **Router (v2)**: Mejoras como:
  - Rutas anidadas
  - Manejo de parámetros personalizados
  - Guardianes de ruta

[🔝 Volver al inicio](#-tabla-de-contenidos)

---

## 📦 Componentes

PuritoJs utiliza archivos `.pjs` (Purito JavaScript) para definir cada componente, manteniendo toda su lógica, estilos y renderizado en una única función modular.

### Creación de un Componente en `.pjs`

Para crear un componente en PuritoJs, define un archivo `.pjs` que contenga la lógica, estilos y HTML del componente:

```javascript
// Welcome.pjs

function Welcome() {
  function Render(Welcome) {
    <div>
      <h1>{{$message}}</h1>
      <p>¡Bienvenido a PuritoJs!</p>
    </div>
  }

  function Styles(Welcome) {
    div {
      padding: 20px;
    }

    h1 {
      color: blue;
    }
  }

  function Js(Welcome) {
    const message = "Hola desde PuritoJs"
  }

  return Welcome
}
```

### Uso de Componentes

Los componentes se invocan como funciones usando `{{$nombreComponente()}}`. Para mostrar el componente `Welcome` en otro componente:

```javascript
// App.pjs
import { Welcome } from "./Welcome.pjs"

function App() {
  function Render(App) {
    <div>
      {{$Welcome()}}
    </div>
  }
}
```

[🔝 Volver al inicio](#-tabla-de-contenidos)

---

## ✨ Funciones Mágicas

Las funciones mágicas en PuritoJs permiten definir la estructura de cada componente de forma modular y sencilla:

- **Render**: Define el HTML del componente.
- **Styles**: Define los estilos CSS específicos del componente.
- **Js**: Contiene la lógica interna del componente.

### Ejemplos

```javascript
function Render(Welcome) {
  <div>
    <h1>{{$message}}</h1>
  </div>
}

function Styles(Welcome) {
  div {
    padding: 20px;
  }
  h1 {
    color: blue;
  }
}

function Js(Welcome) {
  const message = "Bienvenido a PuritoJs!"
}
```

[🔝 Volver al inicio](#-tabla-de-contenidos)

---

## 💾 Estado Global

El Estado Global permite compartir datos entre múltiples componentes de manera centralizada. Organiza el estado en "slots", cada uno identificado con una `KeyMadre`.

### Definición del Estado Global

Define el estado global en un archivo separado, como `StateGlobal.pjs`:

```javascript
// StateGlobal.pjs
import { StateGlobal } from "PuritoJs"

function StateGlobal() {
  const user = mut({
    name: "Marcos",
    age: 30
  })
  
  const theme = mut("dark")

  return StateGlobal
}
```

### Uso del Estado Global

Accede a las variables del estado global en un componente:

```javascript
// Welcome.pjs
import { StateGlobal } from "./StateGlobal.pjs"

function Welcome() {
  function Render(Welcome) {
    <div>
      <h1>Bienvenido, {{$user.name}}</h1>
      <p>Tema actual: {{$theme}}</p>
    </div>
  }
}
```

[🔝 Volver al inicio](#-tabla-de-contenidos)

---

## 📡 Sistema de Señales

Las señales permiten enviar y recibir datos entre componentes sin necesidad de pasar props o estados.

### Emisión y Recepción de Señales

```javascript
// Emite una señal
<button @click="signal('clicked', { id: 1 })">¡Haz clic aquí!</button>

// Recibe una señal
{{$Button() @clicked="handleClick"}}
```

[🔝 Volver al inicio](#-tabla-de-contenidos)

---

## 🛣️ Router

El router en PuritoJs facilita la navegación entre componentes.

### Configuración y Montaje del Router

Define las rutas en `router/index.js` y móntalo en la app principal:

```javascript
// router/index.js
import { CreateRouter } from "PuritoJs"
import Home from "./Views/Home.pjs"
import About from "./Views/About.pjs"

function Routes() {
  return [
    { route: "/", name: "home", component: Home },
    { route: "/about", name: "about", component: About }
  ]
}

const Router = CreateRouter(Routes)
export default Router
```

```javascript
// main.js
import { createApp } from "PuritoJs"
import Router from "./router"
import App from "./App.pjs"

const app = createApp(App)
app.use(Router)
app.mount('#app')
```

### Uso de `RouterView`

Para renderizar según la ruta, usa `{{$RouterView()}}` en el componente principal (`App.pjs`):

```javascript
function App() {
  function Render(App) {
    <div>
      {{$RouterView()}}
    </div>
  }
}
```

[🔝 Volver al inicio](#-tabla-de-contenidos)

---

## 📝 Desarrollo y Contribuciones

Para contribuir a PuritoJs:

1. **Fork el proyecto** en GitHub.
2. **Crea una nueva rama** para tu contribución.
3. **Reporta errores** abriendo un `issue`.
4. **Propón mejoras** a través de `pull requests`.

[🔝 Volver al inicio](#-tabla-de-contenidos)

---

## 🔗 Redes y Soporte

Para soporte y actualizaciones, síguenos en:

- **Twitter**: [@PuritoJs](https://twitter.com/PuritoJs)
- **GitHub**: [PuritoJs en GitHub](https://github.com/usuario/PuritoJs)
- **Discord**: Únete a nuestra comunidad para discusiones, soporte y colaboración.

[🔝 Volver al inicio](#-tabla-de-contenidos)

---

## 📜 Licencia

PuritoJs está distribuido bajo la licencia MIT. Esto permite su uso, modificación y distribución libremente. Consulta el archivo [LICENSE](LICENSE) para más detalles.

[🔝 Volver al inicio](#-tabla-de-contenidos)
