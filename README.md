# Introducción a React

En este tutorial vamos a escribir nuestra primera aplicación en react sin necesidad de usar un bundler, como por ejemplo, Webpack.

## Preparación
Para empezar debemos crear un archivo index.html, en el que debemos agregar el siguiente tag para usar la cdn.

```html  
<script src="https://unpkg.com/react@16.14.0/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16.14.0/umd/react-dom.development.js"></script>
```

Luego crearemos un archivo index.js en el mismo directorio, y lo agregaremos al documento con el siguiente tag:

```html 
<script src="./index.js" defer></script>
```

## Crear y renderizar un elemento

### Crear un elemento

En nuestro index.js, crearemos un elemento de react con ```React.createElement```, una función similar a ```document.createElement```.
En este caso, crearemos un div:

```javascript
const div = React.createElement('div', {
  children: "Hola mundo!"
})
```

### Renderizar un elemento
Para renderizar nuestro elemento debemos hacer uso no de React, sino de React-DOM, la librería que importamos en nuestro segundo script tag.
Para esto usaremos ```ReactDOM.render()```, una función que recibe como argumentos nuestro elemento y el punto en el que montarlo.

```javascript
ReactDOM.render(div, document.body)
```

## Problema
¿Que pasaría si en lugar de renderizar texto dentro de nuestro elemento, quisieramos que hubiera otro elemento? como un párrafo, por ejemplo.
Tendríamos que usar ```React.createElement()``` dos veces, de la siguiente forma:

```javascript
const div = React.createElement('div', {
  children: React.createElement('p', {
    children: "Hola Mundo!"
  })
})
```

Como podemos ver, leer un arbol de elementos creados de esta forma puede ser difícil, sobretodo si nuestra aplicación es más compleja que esta.

## Solución
Por este problema es que el equipo de React creó una sintáxis llamada JSX, que es muy parecida a HTML. Con esta, el código de arriba se equivale a lo siguiente:

```jsx
const div = <div><p>Hola Mundo!</p></div>
```

Pero esto no es javascript, y no podemos escribirlo esperando que nuestro navegador lo interprete como queremos. Para esto vamos a agregar un último script tag:

```html
<script src="https://unpkg.com/babel-standalone@6.26.0/babel.min.js"></script>
```
Con este, estamos importando Babel, un compilador que va a interpretar nuestro código JSX y ejecutará su equivalente javascript. Pero para esto debemos agregar un atributo a nuestro script tag reemplazando

```html 
<script src="./index.js" defer></script>
```
por 

```html 
<script type="text/babel" src="./index.js" defer></script>
```
