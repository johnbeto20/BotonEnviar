# Boton de Enviar

Este es un boton diseñado desde cero, me llama la atención realizar estos diseños propuestos desde animaciones y pasarlos a un formato limpio en HTML y CSS.

1. Para la construcción de este elemento es necesario tener un boton en html,

````html
<button class="btn" id="boton">Enviar!</button>
````

2. Luego le aplico los estilos al gusto.

![imagen boton](https://raw.githubusercontent.com/johnbeto20/pildoritas-css-botonSend/master/img_Readme/btn-enviar.jpg)

3. Conseguiremos dos imagenes (en png o SVG) donde mostraremos el icono principal y el icono final.

Imagen principal

![imagen inicial](https://raw.githubusercontent.com/johnbeto20/pildoritas-css-botonSend/master/img_Readme/ico-send.jpg)

Imagen final

![imagen final](https://raw.githubusercontent.com/johnbeto20/pildoritas-css-botonSend/master/img_Readme/ico-done.jpg)

4. tenemos que tener en cuenta que la estructura de nuestro botón podría cambiar, entonces maquetamos acorde a lo que queremos controlar, con una separación, 'esa es la clave'.

````html
<button class="btn" id="btn">
    <div class="cont-image">
        <img id="icoFligh" src="ico-fligh.svg" alt="icono enviar"/>
    </div>
    <div class="cont-image-check" id="icoCheck">
        <img src="ico-check.svg" alt="icono final">
    </div>
    <span class="btn__text">Enviar</span>
    <span class="btn__text-2">Done</span>
</button>
````
5. Ajustamos por estilos la parte principal, la imagen que lo contiene la clase: **"class="cont-image"** y el texto que lo contiente la siguiente clase: **"class="btn__text"**, así tendríamos algo así:

![imagen enviar final](https://raw.githubusercontent.com/johnbeto20/pildoritas-css-botonSend/master/img_Readme/boton-enviar-finish.jpg)

## Animar el icono del avioncito.

Para esta parte hay un detalle coqueto donde utilicé un **:after** y un **:before** dentro del contenedor con la clase: **cont-image**

````css
.cont-image:after, .cont-image:before {
    display: block;
    content: "";
    width: 10px;
    height: 4px;
    border-radius: 2px;
    background: #fff;
    position: absolute;
    top: 12px;
    right: 100%;
}
````
quedaría algo así, pero le agregamos una **opacidad** de **0** para no mostrarlo al principio.
![imagen lineas del avion](https://raw.githubusercontent.com/johnbeto20/pildoritas-css-botonSend/master/img_Readme/image-avion-con-lineas.jpg)

Aparte agregamos las animaciónes respectivas, esto ya sería como queremos animarlo (En el repositorio estará la base de animación inicial):

````css
.active .cont-image img {
    animation: goMove 1s ease-in forwards;
}

.active .cont-image:after, .active .cont-image:before {
    animation: opacityLines 0.8s ease-in forwards;
}

.active .btn__text {
    animation: recorText .1s ease-in forwards .7s;
}
````

## Animar la parte donde se ejecuta la acción final... el chulito.

Para esto la clave esta en manejar el **delay** en las animaciones, o utilizar el "animationEnd" en javascript apenas se termine la animación principal aplicada, pero sería a tu gusto, ya que esta animación final comienza justo cuando la inicial ni siquiera ha terminado, entonces como inicia a destiempo utilicé el **delay**.

````css
.active .cont-image-check img {
    animation: moveCheck .5s ease-in forwards;
}

.active .btn__text-2 {
    animation: recorText .1s ease-in forwards 1.4s reverse;
}

.btn.active {
    animation: transformCircle 1s ease-in forwards .5s;
}
````

y en javascript agregué que cuando se inicie la animación se muestre el icono final. 

````javascript
btn.addEventListener("animationstart", function(){
    setTimeout(function(){
        icoCheck.style.display ="inline-block"
    },950)
})
````

## Animar el contenedor

Este me pareció retador, ya que tuve que modificarlo para que los elementos por dentro no se alteraran por la estructura:

````css

.btn.active {
    animation: transformCircle 1s ease-in forwards .5s;
}

@keyframes transformCircle {
    0% {
        width: 200px;
        padding: 0 45px;
    }
    25% {
        width: 70px;
        padding: 0;
    }
    75% {
        width: 70px;
        padding: 0;
        background-color: var(--color-btn);
    }
    100% {
        background-color: var(--color-ok);
        width: 200px;
        padding: 0 45px;
    }
}
````

## Uniendo las partes.

6. despues de tener todo construido a nuestro gusto es momento de agregar las animaciones para que todo se ejecute en cadena, ¿se acuerdan que mis clases tienen un **.active**: al principio, bueno, es la funcioncita de javascript para que el botón se active
```javascript

var icoFligh = document.getElementById("icoFligh")
var btn = document.getElementById("btn")
var icoCheck = document.getElementById("icoCheck")

btn.addEventListener("click", function() {
    this.classList.add("active");
})

````

Al ejecutarlo las animaciones comenzarán a funcionar, pueden ver el [Demo aquí](https://johnbeto20.github.io/pildoritas-css-botonSend/)

En conclusión:

* Fijarnos en que tan detallado queremos que sea nuestra animación. 
* Utilicemos los **delay** para seguir una secuencia.
* el **transform** es un buen aliado.

Si lo ven, son experimentos de como podría ser una construcción de este botón, si encuentran otra forma diferente de hacerlo sería aagradable compartir el conocimiento.

espero que sea de utilidad.
