---
layout: post
title: BumBum CSS Animation
date: '2015-11-07 18:51:50'
---

Hoy no tocaba post, pero me ha parecido buena idea rescatar un antiguo *codepen* que hice el pasado enero para compensar tanta **morralla** que inunda mi blog últimamente, como el [extenso post]() sobre la fase de planificación en el diseño centrado en el usuario. Que sí, que la teoría mola, pero también me apetece mostrar un poco de código de vez en cuando.

Ahora que están tan de moda los corazoncitos (twitter ha cambiado recientemente su *fav* por *like*) Voy a simular el bum bum (sí, es la mejor onomatopeya que se me ha ocurrido) de un corazón con CSS. La idea es mostrar:

1. Cómo definir una transformación.
2. Cómo definir una animación.
3. Cómo funcionan los keyframes.
4. Ejemplo final.


**LET'S DO IT**

## Transformaciones
Para definir una transformación en CSS, basta con lo siguiente:
<pre><code class="language-css">.shape {
 transform: scale(2)
};
</code></pre>

Es lo que estás pensando: va a escalar el doble (a hacer el doble más grande) el elemento que tenga esa clase. **Easy**.
Llegados a este punto, tenemos que tener en cuenta que las animaciones en cada navegador son, como el que dice, **de su padre y de su madre**, por lo que no hay que olvidar incluir los **vendor prefixes**:
<pre><code class="language-css">.shape {
  -webkit-transform: scale(2);
  -moz-transform: scale(2);
  -ms-transform: scale(2);
  -o-transform: scale(2);
  transform: scale(2);
};
</code></pre>

> En css3 hay nuevas propiedades que están todavía en estado experimental. Los navegadores tienen varias maneras de interpretar el css, y varios niveles de soporte para los estandartes W3C

[Más sobre vendor prefixes](http://w3.unpocodetodo.info/css3/prefijos.php)

## Animaciones

Viene la parte que más me gusta. Ojo, que aquí también hay que tener en cuenta los vendor prefixes. La sintaxis de la animación es la siguiente:

* Variables

<pre><code class="language-css">.shape {
 animation-name: *keyframename*|none|initial|inherit;
 animation-duration: *time*|initial|inherit;
 animation-timing-function: linear|ease|ease-in|ease-out|cubic-bezier(n,n,n,n)|initial|inherit;
 animation-delay: *time*|initial|inherit;
 animation-direction: normal|reverse|alternate|alternate-reverse|initial|inherit;
 animation-iteration-count: *number*|infinite|initial|inherit;
 animation-fill-mode: none|forwards|backwards|both|initial|inherit;
 animation-play-state: paused|running|initial|inherit;
}
</code></pre>
Dichas variables se pueden poner en la misma línea, siguiendo el orden anterior, o de manera individual.

<pre><code class="language-css">.shape {
  animation: 'animation-name' || 
             'animation-duration' || 
             'animation-timing-function' || 
             'animation-delay' ||
             'animation-iteration-count' || 
             'animation-direction' || 
             'animation-fill-mode'
};
</code></pre>

Para nuestro bombeante corazón que utilizaré como ejemplo, queremos que haga lo siguiente:

* Que lata a cada segundo
* Que el tipo de animación sea (timing-function) linear
* Que esté bombeando de manera infinita (*qué bonito*)

<pre><code class="language-css">.shape {
  -webkit-animation: beat 1s linear infinite;
  -moz-animation: beat 1s linear infinite;
  -ms-animation: beat 1s linear infinite;
  -o-animation: beat 1s linear infinite;
  animation: beat 1s linear infinite;
};
</code></pre>

* 'beat' es el nombre de nuestra animación. Aquí es donde vienen nuestros amigos los **keyframes**.

Básicamente, un keyframe es un punto en la línea temporal de una animación en la que el objeto animado cambia de estado. En CSS, sigue el siguiente esquema:

<pre><code class="language-css">@keyframes nombre-animación {
  porcentaje {
    transform: transformación(valor);
  }
};
</code></pre>

Por ejemplo, imaginemos que tenemos una animación de cuatro segundos. En el keyframe identificado en el 25%, provocará que se produzca una transformación en el primer segundo. 50% en el segundo segundo (valga la redundancia), 75% en el tercer segundo y 100% en el cuarto segundo.

Para hacer el bum bum del corazón, digamos que hará falta algo así:

- Corazón está en tamaño normal
- Corazón crece muy rápido
- Corazón vuelve a tamaño normal muy rápido
- Corazón vuelve a crecer muy rápido
- Corazón vuelve poco a poco a tamaño normal y se queda así un rato

Para conseguir lo anterior, he establecido los siguientes porcentajes:

- Corazón está en tamaño normal (-)
- Corazón crece (10%)
- Corazón vuelve a tamaño normal (20%)
- Corazón crece (30%)
- Corazón vuelve a tamaño normal poco a poco (-)

Como vemos, el bum bum ocurrirá de manera muy rápida entre el 10% y el 30% del segundo en el que ocurrirá la animación.

<pre><code class="language-css">@keyframes beat {
  10% {
    transform: scale(1.2);
  }

  20% {
    transform: scale(1);
  }

  30% {
    transform: scale(1.2);
  }
}
</code></pre>

En mi caso, he puesto una escala de 1.2 porque no me gustaba que quedara demasiado exagerado. Evidentemente, hay que incluir también los vendor prefixes en los keyframes. Éste es el resultado del corazón bombeante:

<p data-height="268" data-theme-id="20780" data-slug-hash="qOKzqL" data-default-tab="result" data-user="elenatorro" class='codepen'>See the Pen <a href='http://codepen.io/elenatorro/pen/qOKzqL/'>qOKzqL</a> by Elena Torró (<a href='http://codepen.io/elenatorro'>@elenatorro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

En este ejemplo, los corazones (el interior y el exterior) están creados con CSS (no son iconos o imágenes), pero puedes aplicarlos al elemento que quieras.

Para no tener que escribir tantas veces los vendor prefixes, existen varios mixins (funciones) en preprocesadores CSS que te harán esta tarea mucho más sencilla, y que recomiendo utilizar para evitar duplicar tanto codigo o que se te escape algún vendor sin querer.

Espero que te haya gustado este post y que vayas poniendo muchos corazoncitos por ahí.

Más info en:

* [W3Schools](http://www.w3schools.com/cssref/css3_pr_animation.asp)
* [CSS-Tricks](https://css-tricks.com/snippets/css/keyframe-animation-syntax/)
* [W3C](https://drafts.csswg.org/css-animations/)
