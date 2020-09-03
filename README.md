# EDP (Event-driven Programming)

> Aquí se usa contenido de [MDN web docs: Overview of events and handlers](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Overview_of_Events_and_Handlers)

## Intro 

Inicialmente los navegadores esperaban hasta recibir todos los recursos 
asociados a una pagina, los parsearban y procesaban para renderizarla, 
manteniéndose entonces estática hasta que se realizara una petición 
a una nueva URL. En las páginas dinámicas -la mayoría de las que hay hoy en día 
en la web-, los navegadores recorren un bucle que pasa por procesar, pintar, 
presentar contenio y esperar a que se dispare un evento. Y como disparadores de 
eventos se incluyen la carga completa de recursos, la interacción del usuario a 
través del ratón, el pad o el teclado, la finalización de tiempos de 
animaciones, etc. 

El patrón que sigue la programación dirigida se basa en un contrato entre un 
tipo de evento y:
* el nombre (String) utilizado para el evento,
* el tipo de estructura de datos utilizada para acceder a las propiedades del
evento, 
* y el objeto JavaScript que 'emitirá' ese evento.

Y se implementa:
* definiendo una función JavaScript que tome como argumento esa estructura de 
datos acordada, 
* y registrando dicha función utilizando el nombre (String) con el objeto que 
emitirá el evento.

Los navegadores web siguen el patrón de eventos con un enfoque estandarizado. 
Utilizan un ojeto derivado de _EventPrototyope_ como estructura de datos para 
acceder a las propiedades de un evento. Y el método que utilizan para registrar 
las funciones de manejo de eventos (_listeners'_ o 'hendlers') se llama _addEventListener_, que espera 
como argumentos una string con el tipo de evento y la función listener, que es 
la que se encarga de reaccionar al evento. Finalmente, los navegadores definen 
un gran número de objetos emisores de eventos, y una gran variedad de tipos de 
eventos generadoas por éstos.


## Ejemplo

Tenemos el siguiente botón:

```
    <button id="buttonOne">Click here to emit a 'click' event</button>
```

Los elementos de tipo button están destinados a emitir eventos de tipo 'click'.
Entonces, podemos definir primero una función que esté a la escucha de este 
evento:

```
    var example_click_handler = function (event){

            let objKind;
            
            if (event instanceof Event) {
                objectKind = 'EventPrototype';
            }
            else {
                objectKind = 'ObjectPrototype';
            } 

        cosole.log("We got a click event at " + event.timeStamp + " with an argument object derived from: " + objKind );
    };
```

Y, luego, registrar la función con el botón, pudiendo ser en el script utilizando 
el DOM:

```
    var buttonDOMElement = document.querySelector('#buttonOne');
    buttonDOMElement.addEventListener('click', example_click_handler);

```
O bien, en el documento HTML añadiendo la llamada a la función como valor del atributo 
'onclick', aunque no es buena práctica utilizar este segundo enfoque.

```
    <button id="buttonOne" onclick="example_click_handler()">Click here to emit a 'click' event</button>
```

