# Boton de Enviar

![imagen boton](https://raw.githubusercontent.com/johnbeto20/BotonEnviar/main/img_Readme/elemento-animado.gif)

Este es un boton diseñado desde cero, me llama la atención realizar estos diseños propuestos desde animaciones y pasarlos a un formato limpio en HTML y CSS.

1. Para la construcción de este elemento es necesario tener un <b>botón</b> en html, pero antes, este botón debe estar dentro de un <b>contenedor</b> que va a contener nuestros elementos.

````html
<div class="button">
    <button class="btn" id="boton">Enviar!</button>
    <!--Acá van los elementos que vamos a mostrar de a poquito.-->
</div>
````

Luego le aplico los estilos al gusto, pero hay unos clave para que pueda funcionar lo que queremos lograr.

````css
/*El contenedor puede tener un alto y un alto según como se necesite, y con una posición relativa.*/
.button {
    position: relative;
    width: 190px;
    height: 60px;
}

/*El botón debe estar en una posición absoluta.*/
.button button {
    position: absolute;
}

/*El reflow y repaint lo aplicas a tu gusto ;) */

````

![imagen boton](https://raw.githubusercontent.com/johnbeto20/BotonEnviar/main/img_Readme/paso-1.png)

2. tenemos que tener en cuenta que la estructura de nuestro botón podría cambiar, entonces maquetemos acorde a lo que queremos controlar, con una separación <b>"esa es la clave"</b>.

````html
<div class="button">
    <button id="start">...</button>
    <span id="fligh" class="icon-fligh">...</div>
    <div id="answer" class="answer">...</div>
</div>
````

3. agregamos los elementos que nos hacen falta, que sería, el icono del avioncito de papel, y el mensaje que dice "enviado", acompañado de un icono de confirmación.

````html
<!--Icono del avioncito en SVG con clase icon-fligh-->
<span id="fligh" class="icon-fligh">
    <svg viewBox="0 0 72 59.7">
        <g id="Group_3_1_" transform="translate(-186 -162.933)">
            <path id="Path_1_1_" class="st1" d="M186,162.9l72,19.5l-72,33.1l6.1-25.8l26.6-4.6l-26.6-1.5L186,162.9z"/>
            <path id="Path_2_1_" class="st1" d="M202.4,211.6l28.7-12.4l-28.7,23.5L202.4,211.6z"/>
        </g>
    </svg>
</span>
<!--Frase con el texto de validación con un icono en SVG con la clase answer-->
<div id="answer" class="answer">
    <span class="icon-after">
        <svg viewBox="0 0 38.7 28.9">
            <path id="Path_3_1_" class="st0" d="M3,16.5l9,9.3L35.7,3"/>
        </svg>
    </span>
    <span class="text-after">Enviado</span>
</div>
````

Imagene de los elementos

![imagen elementos](https://raw.githubusercontent.com/johnbeto20/BotonEnviar/main/img_Readme/paso-2.png)

4. Ahora vamos a colocar answer y el botón con **position: absolute** para manejar los elementos que vamos a mover libremente.

````css
.button .icon-fligh {
    position: absolute;
}

.button button {
    position: absolute;
}

````

![imagen boton elementos ocultos](https://raw.githubusercontent.com/johnbeto20/BotonEnviar/main/img_Readme/paso-3.png)

5. Para la clase answer vamos a realizar un modo donde podamos mantener el texto oculto, ya que haremos que le texto se muestre como una mascara.

````css
.button .answer {
    overflow: hidden;
    width: 0;
}
````

Para l icono del check con clase **icon-after** lo utilizaremos en SVG.
````html
<span class="icon-after">
    <svg viewBox="0 0 38.7 28.9">
        <path id="Path_3_1_" class="st0" d="M3,16.5l9,9.3L35.7,3"/>
    </svg>
</span>
````

Y aplicaremos estilos visuales para generar su linea

````css
.button .st0 {
    fill: none;
    stroke: #00FF11;
    stroke-width: 6;
    stroke-linecap: round;
    stroke-linejoin: round;
    stroke-miterlimit: 4;
}
````

Para el icono tendríamos que colocarlo en pocisión absolute, para tener un mejor control sobre él, y centrarlo de esta manera y adicional reducir el tamaño por medio de estilos.

````css

.button .icon-fligh {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    width: 60px;
    height: 50px;
    width: 60px;
    height: 50px;
}

````

## construyamos las animaciones

6. ya  sabemos que elementos se van a animar, ahora construyamos por partes esas animaciones, revisemos la animación y veamos los elementos, a partir de eso podemos generar nuestras animaciones.

````css
/*Animación para nuestro boton, usamos un "transform" para moverlo a la dirección que se necesita*/
@keyframes moveBtn {
    0% {
        transform: translate(0, 0);
        opacity: 1;
    }
    100% {
        transform: translate(-150px, 0);
        opacity: 0;
    }
}

/*activando la animación, agregandoselo a una clase que lo realize, esta clase se la agregaremos por medio de javascript*/
.moveBtn {
    animation: moveBtn 1s ease forwards;
}

/*Animación para nuestro avioncito, usamos un "transform" para moverlo a la dirección que se necesita*/
@keyframes movefligh {
    0% {
        transform: translate(0, 0);
        opacity: 1;
    }
    100% {
        transform: translate(200px, 0);
        opacity: 0;
    }
}

/*activando la animación, agregandoselo a una clase que lo realize, esta clase se la agregaremos por medio de javascript*/
.movefligh {
    animation: movefligh 1s ease forwards;
}

/*¿se acuerdan de la mascara realizada con el overflow y el width?, Bueno... esto lo vamos a animar*/
@keyframes maskLetter {
    0% {
        width: 0;
    }
    100% {
        width: 120px;
    }
}

/*activando la animación, agregandoselo a una clase que lo realize, esta clase se la agregaremos por medio de javascript*/
.maskLetter {
    animation: maskLetter 0.5s ease forwards;
    animation-delay: 0.05s;
}

/*Acá estamos utilizando un recurso para SVG en CSS que nos permite dibujar las lineas y generar un efecto de trazo, lo ideal es que el stroke-dasharray separe entre lineas el elemento y también su ampliación, y el stroke-dashoffset define desde donde inicia el efecto, sabiendo esto sólo animaremos el stroke-dashoffset para moverlo de un estado a otro*/
@keyframes draw {
    0% {
        stroke-dasharray: 50;
        stroke-dashoffset: 50;
    }
    100% {
        stroke-dashoffset: 0;
    }
}

/*activando la animación, agregandoselo a una clase que lo realize, esta clase se la agregaremos por medio de javascript*/
.draw {
    animation: draw 1s ease forwards;
    animation-delay: 0.25s;
}
````

es bueno tener esto por separado para saber que vamos a utilizar

## vamos para el Javascript.

7. En el javascipt llamamos a los elementos con los que vamos a interactuar **"a los elementos también les agregué un id con el mismo nombre, esto con el fin de que utilicemos los id para temas de programación y las clases para la parte de estilos"**.

````javascript
const btn = document.getElementById("start");
const Fligh = document.getElementById("fligh");
const Answer = document.getElementById("answer");
const Line = document.getElementById("Path_3_1_");
````

8. llamamos al activador de la acción que es el **btn**
````javascript
btn.addEventListener("click", function() {})
````

9. dentro de la función aplicamos el llamado a las clases que agregamos para las animaciones, ¿Las recuerdan?

````javascript
btn.addEventListener("click", function() {
    this.classList.add("moveBtn")
    this.addEventListener('animationend', () => {
        Fligh.classList.add("movefligh");
        Answer.classList.add("maskLetter");
        Answer.addEventListener('animationend', () => {
            Line.classList.add("draw");
        });;
    });
})
````

el **animationend** lo estoy utilizando para identificar que pasa cuando la animación termine, cuando termine ejecuto la otra animación para los demas elementos, esto con el fin de tener un orden de secuenda de mis elementos a animar.

Al ejecutarlo las animaciones comenzarán a funcionar, pueden ver el [Demo aquí](https://johnbeto20.github.io/BotonEnviar/)

En conclusión:

* Fijarnos en que tan detallado queremos que sea nuestra animación. 
* el **transform** es un buen aliado.

Si lo ven, son experimentos de como podría ser una construcción de este botón, si encuentran otra forma diferente de hacerlo sería aagradable compartir el conocimiento.

espero que sea de utilidad.
