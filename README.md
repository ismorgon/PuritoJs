# 🌟 PuritoJs

> El framework JavaScript más limpio, fresquito y potente para el frontend moderno.

PuritoJs es un framework minimalista pero potente que combina la simplicidad con características modernas para crear aplicaciones web de manera elegante y eficiente.

## 📚 Tabla de Contenidos

- [Filosofía](#filosofía)
- [Instalación](#instalación)
- [Single File Components](#single-file-components)
- [Estado Global](#estado-global)
- [Sistema de Señales](#sistema-de-señales)
- [Ejemplos Completos](#ejemplos-completos)

## 🎯 Filosofía

PuritoJs se basa en tres principios fundamentales:

- **Simplicidad**: Sintaxis clara y directa sin configuraciones complejas
- **Elegancia**: Código limpio y legible que se entiende a primera vista
- **Potencia**: Características modernas sin sacrificar la simplicidad

## 🚀 Instalación

```bash
npm install puritojs
```

## 📄 Single File Components (SFC)

### Creando tu Primer Componente

En PuritoJs, los componentes se crean en archivos con extensión `.pjs`. Cada componente es una función que utiliza "funciones mágicas" para definir su estructura, estilos y lógica.

```javascript
// Welcome.pjs
function Welcome() {
  function Render(Welcome) {
    <div>
      <h1>Hola {{name}}</h1>
      <button @click="ping('clicked')">Click me!</button>
    </div>
  }

  function Styles(Welcome) {
    div {
      padding: 20px;
    }
    
    h1 {
      color: blue;
      font-size: 24px;
    }
  }

  function Js(Welcome) {
    const name = "Sofia"
  }

  return Welcome
}
```

### Funciones Mágicas

PuritoJs utiliza tres funciones mágicas principales:

#### 1. Render(ComponentName)
Define la estructura HTML del componente. Soporta interpolación usando `{{}}`.

```javascript
function Render(Component) {
  <div>
    <h1>{{title}}</h1>
    <p>{{description}}</p>
  </div>
}
```

#### 2. Styles(ComponentName)
Define los estilos encapsulados del componente. Los estilos son automáticamente scoped.

```javascript
function Styles(Component) {
  div {
    max-width: 800px;
    margin: 0 auto;
  }
  
  h1 {
    color: #333;
    font-size: 2em;
  }
}
```

#### 3. Js(ComponentName)
Contiene toda la lógica del componente.

```javascript
function Js(Component) {
  const title = "Mi Título"
  const description = "Mi descripción"
  
  function handleClick() {
    // lógica aquí
  }
}
```

### Usando Componentes

Para usar un componente, primero debes importarlo y luego usarlo con la sintaxis de interpolación:

```javascript
import Welcome from "./components/Welcome.pjs"

function App() {
  function Render(App) {
    <div>
      {{$Welcome()}}
    </div>
  }
}
```

## 🌍 Estado Global

PuritoJs maneja el estado global de manera simple y efectiva usando la función mágica `StateGlobal` y el método `mut()`.

### Definiendo Estado Global

```javascript
import { StateGlobal, mut } from "PuritoJs"

function App() {
  function StateGlobal() {
    const userName = mut("Sofia")
    const theme = mut("dark")
  }
}
```

### Características del Estado Global

- **Creación**: `mut()` crea una variable mutable global
- **Acceso**: Las variables son accesibles desde cualquier componente
- **Modificación**: El valor se puede cambiar directamente
- **Eliminación**: Usa `delete nombreVariable` para eliminar del estado global

### Ejemplo de Uso

```javascript
// Header.pjs
function Header() {
  function StateGlobal() {
    const userName = mut("Sofia")  // Si ya existe, solo la referencia
  }

  function Render(Header) {
    <header>
      <h1>Bienvenido {{userName}}</h1>
    </header>
  }
}
```

## 📡 Sistema de Señales

PuritoJs implementa un sistema de señales elegante usando la palabra clave `ping`.

### Emitiendo Señales

En el componente hijo:
```javascript
function Button() {
  function Render(Button) {
    <button @click="ping('clicked', { data: 'Hello!' })">
      Click me
    </button>
  }
}
```

### Escuchando Señales

En el componente padre:
```javascript
function App() {
  function Render(App) {
    <div>
      {{$Button() @clicked="handleClick($event)"}}
    </div>
  }

  function Js(App) {
    function handleClick(event) {
      console.log(event.data) // "Hello!"
    }
  }
}
```

### Características de las Señales

- Sintaxis simple usando `ping`
- Soporte para datos adicionales
- Propagación automática al componente padre
- No requiere configuración adicional

## 📝 Ejemplos Completos

### Formulario con Estado Global y Señales

```javascript
// Form.pjs
import { StateGlobal, mut } from "PuritoJs"

function Form() {
  function StateGlobal() {
    const formData = mut({
      name: "",
      email: ""
    })
  }

  function Render(Form) {
    <form @submit="ping('submitted')">
      <input 
        value={{formData.name}}
        @input="formData.name = $event.target.value"
      />
      <button type="submit">Enviar</button>
    </form>
  }
}

// App.pjs
function App() {
  function Render(App) {
    <div>
      <h1>Formulario</h1>
      {{$Form() @submitted="handleSubmit()"}}
    </div>
  }

  function Js(App) {
    function handleSubmit() {
      console.log('Formulario enviado!')
    }
  }
}
```

## 🤝 Contribución

¡Nos encantaría que contribuyas a PuritoJs! Por favor lee nuestra guía de contribución para empezar.

## 📄 Licencia

PuritoJs está licenciado bajo MIT License.
