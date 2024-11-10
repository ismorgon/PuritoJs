
---
🌟 PuritoJs

Framework frontend JavaScript diseñado para construir aplicaciones modernas y dinámicas con una sintaxis amigable, minimalista y potente.

📚 Tabla de Contenidos

Introducción

Instalación

Características

Componentes

Funciones Mágicas

Estado Global

Sistema de Señales

Router

Desarrollo y Contribuciones

Redes y Soporte

Licencia


🎯 Introducción

PuritoJs es un framework de JavaScript para el frontend moderno que combina simplicidad y eficiencia sin sacrificar rendimiento. Su enfoque modular y ligero permite construir aplicaciones rápidas y dinámicas, manteniendo una sintaxis limpia y directa.

🚀 Instalación

Para instalar PuritoJs en tu proyecto, usa:

npm install puritojs

🌟 Características

PuritoJs se distingue por su estructura simplificada y sus herramientas intuitivas, ofreciendo las siguientes características:

✅ Componentes Single File Components (.pjs): PuritoJs organiza cada componente en un solo archivo .pjs, donde se define la lógica, estilos y renderizado de forma modular.

✅ Estado Global: Permite un estado global flexible, organizado en "slots" para una gestión eficiente de la información compartida entre componentes.

✅ Router: Sistema de rutas dinámico y sencillo para definir, enlazar y gestionar navegación.

✅ Sistema de Señales: Comunicación ágil entre componentes sin necesidad de un sistema complejo de eventos.

❔ Lazy Loading: Implementación futura que permitirá cargar componentes según se necesiten, optimizando el rendimiento.

⚠️ Router (v2): Mejoras como rutas anidadas, manejo de parámetros personalizados y guardianes de ruta.



---

📦 Componentes

PuritoJs utiliza archivos .pjs (Purito JavaScript) para definir cada componente, manteniendo toda su lógica, estilos y renderizado en una única función modular. A diferencia de otros frameworks, los componentes en PuritoJs se construyen como funciones.

Creación de un Componente en .pjs

Para crear un componente en PuritoJs, define un archivo .pjs que contenga la lógica, estilos y HTML del componente. Cada archivo sigue esta estructura básica:

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

En este ejemplo, el componente Welcome se define en su archivo .pjs y se compone de tres funciones mágicas (Render, Styles, y Js) que gestionan sus diferentes aspectos.

Uso de Componentes

Los componentes se invocan como funciones usando su nombre entre {{$nombreComponente()}}. Por ejemplo, para mostrar el componente Welcome en otro componente:

// App.pjs
import { Welcome } from "./Welcome.pjs"

function App() {
  function Render(App) {
    <div>
      {{$Welcome()}}
    </div>
  }
}


---

✨ Funciones Mágicas

Las funciones mágicas en PuritoJs permiten definir la estructura de cada componente de forma modular y sencilla:

1. Render

Render define el HTML del componente. Aquí se escribe el contenido que el componente debe renderizar en la interfaz de usuario.

Ejemplo:

function Render(Welcome) {
  <div>
    <h1>{{$message}}</h1>
  </div>
}

2. Styles

Styles permite definir los estilos CSS específicos del componente. Estos estilos solo afectan al componente en el que se definen.

Ejemplo:

function Styles(Welcome) {
  div {
    padding: 20px;
  }
  
  h1 {
    color: blue;
  }
}

3. Js

Js contiene la lógica interna del componente, como variables, funciones y estados. En esta sección defines el comportamiento y manipulación de datos del componente.

Ejemplo:

function Js(Welcome) {
  const message = "Bienvenido a PuritoJs!"
}

Uso de Variables y Componentes

Variables: Se invocan en Render con {{$nombreVariable}}.

Componentes: Para llamar a un componente en otro componente, se usa {{$NombreComponente()}}.



---

💾 Estado Global

El Estado Global permite compartir datos entre múltiples componentes de manera centralizada. En PuritoJs, el estado global está organizado en "slots", y cada uno tiene una KeyMadre que identifica su grupo de información.

Definición del Estado Global

Define el estado global en un archivo separado, como StateGlobal.pjs, y organízalo en mutables (usando mut) para que sus valores puedan cambiar:

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

Uso del Estado Global

Para acceder a las variables del estado global en un componente:

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


---

📡 Sistema de Señales

Las señales permiten enviar y recibir datos entre componentes sin necesidad de pasar props o estados.

Emisión de Señales

Emite una señal desde un componente usando signal:

// Button.pjs
function Button() {
  function Render(Button) {
    <button @click="signal('clicked', { id: 1 })">
      ¡Haz clic aquí!
    </button>
  }
}

Recepción de Señales

Recibe una señal en otro componente mediante @nombreEvento:

// App.pjs
import { Button } from "./Button.pjs"

function App() {
  function Render(App) {
    <div>
      {{$Button() @clicked="handleClick"}}
    </div>
  }

  function Js(App) {
    function handleClick(data) {
      console.log('Botón clicado, ID:', data.id)
    }
  }
}


---

🛣️ Router

El router en PuritoJs facilita la navegación entre componentes.

Configuración del Router

Define las rutas en un archivo separado, como router/index.js:

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

Montaje del Router

Para montar el router en la aplicación:

// main.js
import { createApp } from "PuritoJs"
import Router from "./router"
import App from "./App.pjs"

const app = createApp(App)
app.use(Router)
app.mount('#app')

Uso de RouterView

Para renderizar componentes según la ruta, usa {{$RouterView()}} en el componente principal (App.pjs):

// App.pjs
function App() {
  function Render(App) {
    <div>
      {{$RouterView()}}
    </div>
  }
}


---

📝 Desarrollo y Contribuciones

Para contribuir a PuritoJs:

1. Fork el proyecto en GitHub.


2. Crea una nueva rama para tu contribución.


3. Reporta errores abriendo un issue.


4. Propón mejoras a través de pull requests.




---

🔗 Redes y Soporte

Para soporte y actualizaciones, síguenos en:

Twitter: @PuritoJs

GitHub: PuritoJs en GitHub

Discord: Únete a nuestra comunidad para discusiones, soporte y colaboración.



---

📜 Licencia

PuritoJs está distribuido bajo la licencia MIT. Esto permite su uso, modificación y distribución libremente. Consulta el archivo LICENSE para más detalles.

