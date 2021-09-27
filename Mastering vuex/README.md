## Mastering Vuex

Documentación:  https://vuex.vuejs.org/  
Link Curso:   https://www.vuemastery.com/courses/mastering-vuex/intro-to-vuex


## 1.- Intro to Vuex

Administrar el estado en una aplicación llena de componentes puede resultar difícil  
Cuando hablamos de estado, nos referimos a los datos de los que dependen y procesan sus componentes.  
Cosas como publicaciones de blog, elementos de tareas pendientes, etc

Pero si un componente cambia de estado y un pariente lejano también está usando ese mismo estado, necesitamos comunicar ese cambio. Existe la forma predeterminada de comunicar eventos y transmitir accesorios para compartir datos, pero eso puede volverse demasiado complicado.

Event y Props


![Screenshot](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1578371882429_1.png?alt=media&token=2c411c9f-d5cf-4404-8009-00b73e24a622)

En cambio, podemos consolidar todo nuestro estado en un solo lugar. Una ubicación que contiene el estado actual de toda nuestra aplicación. Una sola fuente de verdad.

**Una única fuente de verdad - Single Source of Truth**  
Esto es lo que proporciona Vuex, y cada componente tiene acceso directo a este estado global.  
Al igual que los datos de la instancia de Vue, este estado es **reactivo**. Cuando un componente actualiza el estado, otros componentes que están usando esos datos son notificados y reciben automáticamente el nuevo valor.

![Screenshot](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1578371889694_2.png?alt=media&token=f9cc01f0-4644-4867-92ad-17ccd6cc7a6e)


Pero la simple consolidación de datos en una única fuente de verdad no resuelve por completo los problemas de gestión del estado.  

¿Qué sucede cuando muchos componentes alteran el Estado de diferentes maneras, desde diferentes lugares?  

Necesitamos algo de estandarización. De lo contrario, los cambios en nuestro estado podrían ser impredecibles e imposibles de rastrear.

**Un patrón de administración de estado**
Esta es la razón por la que Vuex proporciona un patrón de administración de estado completo para una forma simple y estandarizada de realizar cambios de estado. Y si está familiarizado con Vue, Vuex debería verse bastante similar.  


![Screenshot](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1578371892222_3.png?alt=media&token=911a39ae-99b2-4026-9132-71fae035ffc5)

Así como Vue proporciona una instancia raíz de Vue creada con new Vue,    
Vuex ofrece un store creada con  new Vuex.Store.

- Instancia de Vue tiene una propiedad de datos,  el store de Vuex tiene estado.   
- Instancia tiene métodos, que entre otras cosas pueden actualizar datos, el sotre tiene Acciones, que pueden actualizar el estado.
- Instancia tiene computed properties, el store tiene getters, que nos permiten acceder al estado filtrado, derivado o calculado.


data = state  
method = actions  
computer = getters  

La diferencia es que el store tiene mutaciones.  
Las mutaciones se utilizan para confirmar (commit) y (track) realizar un seguimiento de los cambios de estado. 


Como buenas prácticas, podemos usar Acciones para cometer mutaciones, y actualizar el estado directamente.

Desde Vue DevTools, incluso podemos rastrear en el tiempo a través de un registro de cada mutación hasta el estado.

Ahora echemos un vistazo a un ejemplo de Vuex Store.

![Screenshot](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1578371895007_4.png?alt=media&token=27387520-216e-47da-99bd-41e72cebd7bc)


En nuestro **estado** , tenemos una propiedad isLoading, junto con una matriz para todos.  

Debajo tenemos una **mutación** para cambiar nuestro estado isLoading entre verdadero y falso. Y una mutación para establecer nuestro estado con los todos que recibiremos de una llamada API en nuestra acción a continuación.

Nuestra **acción** aquí tiene varios pasos. Primero, confirmará la mutación para establecer el estado isLoading en verdadero. Luego, realizará una llamada a la API y, cuando la respuesta regrese, confirmará la mutación para establecer el estado isLoading en falso. Finalmente confirmará la Mutación para establecer el estado de nuestros todos con la respuesta de nuestra API.


Si necesitamos la capacidad de recuperar solo los todos que están etiquetados como hechos, podemos usar un Getter para eso, que recuperará solo el estado específico que queremos.

![Screenshot](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1578371897321_5.png?alt=media&token=1a6cfcd6-5eb0-4d63-b991-f0dbd0c460ea)




Vuex en movimiento
![Screenshot](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1578371900954_6.gif?alt=media&token=a92f02df-8800-4f4a-ac63-6690f9453e66)


## 2.- Mastering Vuex Orientation
Prerequisites for this course include knowledge of:

- Vue CLI
- Vue Router
- Single File .vue Components
- API Calls with Axios

Downloading the App
https://github.com/Code-Pop/real-world-vue/releases/tag/lesson11-vuex-start

Run proyect: 
npm run serve

Install Api Local
npm install -g json-server

Correr Servicio Local: json-server --watch db.json


App Tour - Vue CLI

En la página principal, mostramos una lista de eventos que estamos incorporando con nuestra API. Cuando hago clic en un evento, se nos lleva a la event-showpágina, que muestra los detalles completos de ese evento. Estamos usando Vue Router para la navegación de nuestro sitio, lo que también nos permite navegar entre páginas.


En nuestra carpeta de vistas , tenemos 3 componentes,    
que se cargan cuando navegamos a la ruta en la que viven.

 1.- /src/iews/EventCreate.vue : Pantalla simple

``` html
<template>
    <h1>Create Event</h1>
</template>

```

2.-  /src/views/EventList.vue: es mucho más interesante.

``` js
    <script>
    import EventCard from '@/components/EventCard.vue'
    import EventService from '@/services/EventService.js'
    
    export default {
      components: {
        EventCard
      },
      data() {
        return {
          events: []
        }
      },
      created() {
        EventService.getEvents()
          .then(response => {
            this.events = response.data
          })
          .catch(error => {
            console.log('There was an error:', error.response)
          })
      }
    }
    </script>
```

Aqui, estamos haciendo una llamada a la API para obtener nuestros eventos **EventService.getEvents().**   
Luego, establecemos el valor de nuestro componente events igual a la respuesta de la llamada a la API. También estamos detectando y registrando cualquier error en la consola.

3.- /src/views/EventList.vue
``` html
    <template>
        <div>
        <h1>Events Listing</h1>
        <EventCard v-for="event in events" :key="event.id" :event="event"/>
        </div>
    </template>
```

En nuestra plantilla, usamos v-for para crear un componente EventCard para cada uno de nuestros events, y pasamos el evento como un accesorio para que EventCard pueda usarlo.

 /src/components/EventCard.vue
Recibe el eventobjeto como prop y muestra algunos de sus detalles en la plantilla.


Comprender nuestras llamadas a la API

 /src/views/EventList.vue

 ``` js
   import EventService from '@/services/EventService.js'
    ...
      created() {
        EventService.getEvents()
          .then(response => {
            this.events = response.data
          })
          .catch(error => {
            console.log('There was an error:', error.response)
          })
      }
    ...
```

 /src/services/EventService.js


 
 ``` js
   import EventService from '@/services/EventService.js'
    ...
      created() {
        EventService.getEvents()
          .then(response => {
            this.events = response.data
          })
          .catch(error => {
            console.log('There was an error:', error.response)
          })
      }
    ...
```

Aquí, estamos importando la biblioteca Axios. Si aún no lo ha hecho, puede instalar Axios ejecutando este comando en su terminal:npm install axios.

Luego, estamos creando una única instancia de Axios con apiClient. Cuando lo creamos, le damos un baseURLy establecemos algunas configuraciones predeterminadas.

Como se señaló anteriormente, json-server es el archivo db.json como nuestra "base de datos" simulada, que contiene todos nuestros eventos. Entonces, cuando visitamos localhost:3000/events, podemos ver todos los eventos que viven en el archivo db.json . Y debido a que json-server es una API REST completamente falsa, podemos OBTENER eventos de él y POST eventos en él, etc

## 3.- State & Getters{}

- Accesing state  (accediento al estado)
- Getters for derived state 
- Mapping to computed properties

Accediento a State (estados)
in main.js
    import store form './store'

En instancia de vue, agregar, store (injected into all componentes)

``` js
new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')
```

store.js
- AGREGAMOS ESTADOS (states)


 ``` js
  export default new Vuex.Store({
  state: {
    user: { id: '45421537', name: 'Jorge Callalle' },
  },
  mutations: {},
  actions: {}
})

```
- MOSTRAMOS ESTADOS  (State)
  
  $store:  hace que sea accesible globalmente, se puede inyectar en cada componente


 ``` js
<template>
  <div>
    <h1>Create Event - {{ $store.state.user.name }}</h1>
    <p>This event was created by  {{ userName }} with id: {{ userId }}</p>
  </div>
</template>

<script>

export default {
  computed: {
    userName() {
      return this.$store.state.user.name
    },
    userId() {
      return this.$store.state.user.id
    }
  }
}
</script>

```

The mapState Helper
Puede volverse repetitivo tener múltiples propiedades calculadas, cada una de las cuales devuelve este. 
$ Store.state.something.   
Para simplificar las cosas, podemos usar el ayudante mapState, que genera propiedades calculadas para nosotros.

 ``` js
import { mapState } from 'vuex'

export default {
  computed: mapState ({
    userName: state => state.user.name,
    userId: state => state.user.id,
    categories: state => state.categories
  })

```

Podemos simplificar mapState, pasando un array de los valores de state.


Object Spread Operator


Getters
_____________________________
Accediento al Estado con Getter


Si bien podemos acceder al estado de la tienda directamente, a veces queremos acceder al estado derivado. En otras palabras, es posible que deseemos procesar el estado de alguna manera cuando accedamos a él.

Por ejemplo, en lugar de acceder a las categorías de nuestro estado, es posible que queramos saber cuántas categorías hay. En otras palabras, es posible que queramos saber la longitud de la matriz de categorías.

Desde dentro de nuestro componente, podríamos decir:

    this.$store.state.categories.length

Pero, ¿qué pasa si varios componentes necesitan usar este mismo valor? Al crear un Vuex Getter, podemos evitar la duplicación de código innecesaria. Además, dado que los Getters se almacenan en caché, esta opción también es un poco más eficaz.

``` js
 getters: {
    catLength: state => {
      return state.categories.length
    }
  },

  computed: {
  catLength() {
    return this.$store.getters.catLength
  },
}
```

Passing getters to Getters

Si necesitáramos obtener el estado que queremos procesar junto con otro Getter, podemos pasar getters como segundo argumento a un Getter. Esto nos permite acceder a otro Getter desde dentro del Getter que estamos creando. Lo sé, eso suena un poco confuso.

Pero para un ejemplo simple, digamos que tenemos una variedad de todos en nuestro estado.

``` js
 todos: [
          { id: 1, text: '...', done: true },
          { id: 2, text: '...', done: false },
          { id: 3, text: '...', done: true },
          { id: 4, text: '...', done: false }
        ]
```

Podríamos tener un Getter que obtenga una matriz de todos los que están etiquetados como hechos.

``` js
  doneTodos: (state) => {
    return state.todos.filter(todo => todo.done)
  }
```

Y podemos usar este Getter dentro de otro Getter si queremos saber cuántos todos quedan por completar.


``` js
 activeTodosCount: (state, getters) => {
      return state.todos.length - getters.doneTodos.length
    }
```