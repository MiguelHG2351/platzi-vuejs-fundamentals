# platzi-vuejs-fundamentals
Curso de introducción  a Vue.js Platzi

## Desarrollo basado en componentes

No esta solo relacionado a web es un concepto de arquitectura de software, que nos permite dividir una aplicación en piezas pequeñas y reutilizables. Abstraer todas las partes del software e interacturan entre sí a través de una interfaz.

![](./readme_files/components.jpg)
![](./readme_files/interfaz.jpg)

## Componentes UI

Cada vez que vemos una página web vemos algo como esto, una interfaz de usuario, que esta compuesta por componentes, que a su vez son piezas de software que se pueden reutilizar.

![](./readme_files/components2.jpg)


## Two way data binding

Es la forma en la que los componentes se comunican entre sí, es decir, cuando un componente cambia de estado, los demás componentes se enteran y se actualizan.

Two Way Data Binding es un patrón MVVM (model - view - view - model) donde se enlazan dos elementos en dos direcciones (cuando cambia uno cambia el otro). Sirve para tener los datos sincronizados con el DOM sin hacer esfuerzos adicionales.

![](./readme_files/two-way-data-binding.jpg)

### Vista

Aquí tenemos el HTML. La vista se encarga de decirle al estado que hay cambios, a lo cual el estado va a reaccionar y mandar una nueva vista. Todo lo que el usuario puede interacturar

### Estado

Aquí tenemos el estado de la aplicación. El estado es un objeto que contiene la información de la aplicación. El estado se encarga de decirle a la vista que hay cambios, a lo cual la vista va a reaccionar y mandar un nuevo estado. Un botón puede tener un estado de activo o inactivo, un input puede tener un estado de texto escrito o no escrito.

### Usuario

El usuario es el que interactúa con la aplicación. El usuario va a interactuar con la vista, a lo cual la vista va a reaccionar y mandar un nuevo estado.

![MVVM](./readme_files/mvvm.jpg)

## Configuración de Vue.js

Antes de empezar necesitamos el cdn de Vue.js

```html
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

Con el cdn podemos empezar a trabajar con Vue.js agregando nuestro código debajo del cdn

```html
    <script>
        const app = Vue.createApp({
            data: {
                message: 'Hello Vue.js'
            }
        }).mount('#app')
    </script>
```

Al final nos quedaria algo como esto

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Vue.js</title>
</head>
<body>
    <div id="app">
        <h1>{{ message }}</h1>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        const app = Vue.createApp({
            data: {
                message: 'Hello Vue.js'
            }
        }).mount('#app')
    </script>
</body>
</html>
```

## Interpolación

Es la forma en la que podemos mostrar información en el HTML, en Vue.js podemos usar la sintaxis de doble llave para mostrar información en el HTML.

```html
    <h1>{{ message }}</h1>
```

## Directivas

Son atributos especiales que comienzan con v- y nos permiten modificar el comportamiento de un elemento en el DOM.

### v-text

Nos permite mostrar texto en el HTML [[ref]](https://vuejs.org/api/built-in-directives.html#v-for)

```html
    <h1 v-text="message"></h1>
```

En este caso no necesitamos usar la interpolación, ya que v-text nos permite mostrar texto en el HTML

```js
const vm = Vue.createApp({
    data() {
        return {
            text: 'Hola vue',
        }
    },
    template:`
        <div v-text="text">
        </div>
    `,
}).mount('#app')
```

En caso que queramos insertar html en el template podemos usar la directiva v-html

```js
const vm = Vue.createApp({
    data() {
        return {
            text: '<h1>Hola vue</h1>',
        }
    },
    template:`
        <div v-html="text">
        </div>
    `,
}).mount('#app')
```

## Atributos reactivos

Son directivas que nos permiten modificar el comportamiento de un elemento en el DOM, por ejemplo, podemos usar la directiva v-bind para modificar el atributo src de una imagen.

```html
    <img v-bind="{'alt': alt, 'width': width, 'src': img}"/>
    <img :attr="img" :alt="alt" :width="width"/>
```

En javascript lo veriamos de la siguiente forma

```js
const vm = Vue.createApp({
    data() {
        return {
            img: 'https://vuejs.org/images/logo.png',
            alt: 'Vue.js',
            width: 200,
        }
    },
    template:`
        <div>
            <img v-bind="{'alt': alt, 'width': width, 'src': img}"/>
            <img :attr="img" :alt="alt" :width="width"/>
        </div>
    `,
}).mount('#app')
```

También podemos pasar un objeto como argumento de la directiva v-bind

```js
    const vm = Vue.createApp({
        data() {
          return {
            images: {
              attr: "src",
              textoalternativo: "alt",
              texto: "Myimagen",
              img: "https://i.picsum.photos/id/0/5616/3744.jpg?hmac=3GAAioiQziMGEtLbfrdbcoenXoWAW-zlyEAMkfEdBzQ",
              size: "width",
              width: "250",
            },
          };
        },
        template: `
            <img :[images.attr]="images.img" :[images.size]="images.width" :[images.textoalternativo]="images.texto" />
            `,
    }).mount("#app");
```
