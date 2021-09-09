## Mastering Vuex

Documentación:  https://vuex.vuejs.org/  
Link Curso:   https://www.vuemastery.com/courses/mastering-vuex/intro-to-vuex


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
