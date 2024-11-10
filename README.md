# 🌟 PuritoJs
El framework JavaScript más limpio, fresquito y potente para el frontend moderno.

## 📚 Tabla de Contenidos
- [Introducción](#introducción)
- [Instalación](#instalación)
- [Componentes](#componentes)
- [Estado Global](#estado-global)
- [Sistema de Señales](#sistema-de-señales)
- [Router](#router)
- [Ejemplos](#ejemplos)

## 🎯 Introducción
PuritoJs es un framework que prioriza la simplicidad y elegancia en el desarrollo frontend. Con una sintaxis clara y consistente, permite crear aplicaciones web modernas sin complicaciones innecesarias.

## 🚀 Instalación
```bash
npm install puritojs
```

## 📦 Componentes

### Estructura Básica
Cada componente se define en un archivo `.pjs` y utiliza funciones mágicas para su estructura:

```javascript
function Welcome() {
  function Render(Welcome) {
    <div>
      <h1>{{$message}}</h1>
      {{$Button()}}
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
    const message = "Hola PuritoJs!"
  }

  return Welcome
}
```

### Uso de Variables y Componentes
- Para mostrar variables: `{{$nombreVariable}}`
- Para usar componentes: `{{$NombreComponente()}}`

## 💾 Estado Global
El estado global se define fuera de los componentes y se puede usar en cualquier parte de la aplicación.

```javascript
// En cualquier archivo .pjs
import { StateGlobal } from "PuritoJs"

function StateGlobal() {
  const user = mut({
    name: "Sofia",
    age: 25
  })
  
  const theme = mut("light")
return StateGlobal
}

function Welcome() {
  function Render(Welcome) {
    <div>
      <h1>Bienvenido {{$user.name}}</h1>
      <p>Tema actual: {{$theme}}</p>
    </div>
  }
}
```

## 📡 Sistema de Señales
Las señales permiten la comunicación entre componentes de forma simple y directa.

### Emitiendo Señales
```javascript
function Button() {
  function Render(Button) {
    <button @click="signal('clicked', { id: 1 })">
      Click me
    </button>
  }
}
```

### Escuchando Señales
```javascript
function App() {
  function Render(App) {
    <div>
      {{$Button() @clicked="handleClick"}}
    </div>
  }

  function Js(App) {
    function handleClick(data) {
      console.log('Button clicked:', data.id)
    }
  }
}
```

## 🛣️ Router

### Configuración
```javascript
// router/index.js
import { CreateRouter } from "PuritoJs"
import Home from "./Views/Home.pjs"
import About from "./Views/About.pjs"

function Routes() {
  {
    route: "/",
    name: "home",
    component: Home
  },
  {
    route: "/about",
    name: "about",
    component: About
  }
}

const Router = CreateRouter(Routes)
export default Router
```

### Montaje
```javascript
// main.js
import { createApp } from "PuritoJs"
import Router from "./router"
import App from "./App.pjs"

const app = createApp(App)
app.use(Router)
app.mount('#app')
```

### Uso del RouterView
```javascript
// App.pjs
function App() {
  function Render(App) {
    <div>
      {{$RouterView()}}
    </div>
  }
}
```

## 📝 Ejemplos

### Componente con Estado Global y Señales
```javascript
// Counter.pjs
function StateGlobal() {
  const count = mut(0)
}

function Counter() {
  function Render(Counter) {
    <div>
      <h2>Contador: {{$count}}</h2>
      <button @click="signal('increment')">+1</button>
      <button @click="signal('decrement')">-1</button>
    </div>
  }
}

// App.pjs
function App() {
  function Render(App) {
    <div>
      {{$Counter() 
        @increment="count++"
        @decrement="count--"
      }}
    </div>
  }
}
```

### Formulario Simple
```javascript
function ContactForm() {
  function Render(ContactForm) {
    <form @submit="handleSubmit">
      <input 
        value={{$formData.name}}
        @input="formData.name = $event.target.value"
      />
      <button type="submit">Enviar</button>
    </form>
  }

  function Js(ContactForm) {
    const formData = {
      name: ''
    }

    function handleSubmit(e) {
      e.preventDefault()
      signal('submit', formData)
    }
  }
}

function App() {
  function Render(App) {
    <div>
      {{$ContactForm() @submit="handleFormSubmit"}}
    </div>
  }

  function Js(App) {
    function handleFormSubmit(data) {
      console.log('Form data:', data)
    }
  }
}
```

### Navegación Básica
```javascript
function Nav() {
  function Render(Nav) {
    <nav>
      <a href="/">Home</a>
      <a href="/about">About</a>
    </nav>
  }
}

function App() {
  function Render(App) {
    <div>
      {{$Nav()}}
      {{$RouterView()}}
    </div>
  }
}
```
