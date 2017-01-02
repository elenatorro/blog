---
layout: post
title: Lo que me pasó creando un paquete en npm
date: '2015-12-15 20:59:32'
---

Estado actual:
<pre><code class="language-css">border-top-style: frankenstein;
</code></pre>

No lo he dicho todavía, pero este blog no es un lugar en el que quiera escribir posts al estilo: *'cómo hacer una app usando el stack Rails + AngularJS + Pascal + Foundation + MariaDB + JQuery'*. Aquí cuento mis experiencias de diseño y de desarrollo, y eso es un poco lo que quería escribir hoy. Más que nada, para que la próxima vez que vaya a escribir un paquete npm en concreto, o una pieza reutilizable de software en general, me acuerde de mis errores y no los cometa de nuevo. O al menos, no los cometa tanto.

## ¿Necesito hacer un paquete npm?

Ésa es la primera pregunta que hay que contestarse. Esta mañana leía de camino al trabajo (niños, aunque tengáis coche, usad el transporte público, el planeta os lo agradecerá, y vuestra mente también) un post en el que citaba la siguiente frase de Douglas Crockford: *'Software is the most complex thing that humans have ever created'*. Y me ha explotado un poquito el cerebro, porque instantáneamente he pensado que yo estoy contribuyendo a que haya más cosas complicadas rondando por ahí.

Por eso, antes de publicar una librería que ocupe un espacio en algún servidor de algún sitio muy lejos, me pregunto, ¿merece la pena publicarla? ¿merece la pena un commit en mi cuenta de GitHub, si va a estar ahí, si no la voy a mantener, si a lo mejor ni la voy a usar? Aquí os dejo un [ejemplo](https://github.com/sindresorhus/arrify/blob/master/index.js) de un developer que, por cierto, me parece **brillante**, cuyos proyectos leo para aprender e inspirarme. ¿Hacía falta un paquete en npm para eso?

## ¿De qué depende?

Con esta pregunta me refiero de qué depende literalmente, es decir, de sus **dependencias**. Cuando estás desarrollando una aplicación **tocha**, (es decir, de dimensiones importantes), piensas si de verdad necesitas utilizar y cargar todas las dependencias de una librería. Es un poco el **síndrome Frankenstein**, al final, acabas con un monstruo formado por muchas partes distintas. Pero además, imagínate que para ponerle una mano a tu criatura, te imponen que has de importar *enlace óptimo con muñeca*, *destrezas de pianista* y *uñas limpias*. Al final, acabas con un montón de paquetes, unos que se guardan de no sé dónde, y otros que se cargan no sé cómo, según se le haya ocurrido al developer de turno. Y eso que se supone que como programadores, tenemos en cuenta ['la ortogonalidad, la reversibilidad y el mínimo acoplamiento'](https://pragprog.com/book/tpp/the-pragmatic-programmer).

## ¿Frontend o backend?

Me ha ocurrido que quería hacer un módulo para el frontend de una aplicación, pero que también tenía unas utilidades que podía aplicar para crear una CLI, y entonces he mezclado peras con manzanas y luego, entre que mi paquete dependía de una librería que luego no necesitaba cargar en el frontend y otros jaleos, he decidido refactorizar. Y he arreglado el entuerto. Cosas que pasan al principio y de las que aprendes, vaya.

El caso es que hoy en día puedes manejar librerías y dependencias de muchas maneras. Algunas las importarás dos veces (*DRY alert*), otras se te quedarán desactualizadas y pasarás de ellas... Para esto, puedes valerte de otras librerías para evitar este tipo de problemas. Un proyecto que ha salido recientemente que me gusta mucho es [GreenKeeper](http://greenkeeper.io/).

## ¿Tests? (suena un grillo de fondo)
Escribir tests es hoy en día mi manera más rápida de desarrollar, aunque hace unos meses me diera urticaria pensar en ellos. Para según qué casos, te ahorras hasta hacer un set de 'examples', ¡porque ya está en los tests! Es a la carpeta a la que voy **de cabeza** cuando quiero saber cómo usar una librería.

## ¿Documentación?
Aquí muchos flaqueamos. Me incluyo. Me cuesta escribir documentación. La hago pensando en entenderla yo, más que en que la entiendan los demás. *I'm sorry*. 

## ¿Changelog?
Mi talón de Aquiles, las versiones. Pierdo el control sobre el control de versiones. ¿Cuándo tengo que *upgradear*? Sí, [ya sé que](http://semver.org/):

* MAJOR version when you make incompatible API changes,
* MINOR version when you add functionality in a backwards-compatible manner, and
* PATCH version when you make backwards-compatible bug fixes.

Pero me sigue resultando difícil. Y más aún cuando me doy cuenta de que acabo de publicar una versión que tiene un error que provoca un *facepalm*, y tengo que **crear una nueva versión para arreglarlo**. Y todo esto, tres veces seguidas. Mal Elena. Mal.

![](img/content/images/2015/12/facepalm.jpg)
De esto he aprendido que me lo tengo que pensar **dos veces** antes de actualizar una versión. Y aunque a veces piense: 'es que estoy empezando el proyecto, no necesito comentar cada versión', **obligarme a hacerlo**.

De hecho, fastidia bastante cuando alguien hace un **breaking change** y te das cuenta cuando todo se rompe y tardas bastante rato hasta dar con el [hilo de GitHub](https://github.com/gruntjs/grunt-contrib-imagemin/issues/208) en el que explica lo sucedido.

Al igual que hay librerías para comprobar si las librerías de tu proyecto están actualizadas, hay librerías que te [ayudan a actualizar librerías](https://github.com/bumped), y otras que [te ayudan a hacer releases](https://github.com/semantic-release/semantic-release) (creo que Christopher Nolan podría sacar una peli de esto). Sobre esta última, recomiendo [este vídeo](https://www.youtube.com/watch?v=tc2UgG5L7WM&index=6&list=PLFZ5NyC0xHDaaTy6tY9p0C0jd_rRRl5Zm) de un compañero de clase durante mi Erasmus en Austria.

## Otros posts que hablan sobre el tema:
* [The mess that is npm](http://mikkel.hoegh.org/2011/12/20/trouble-in-node-dot-js-paradise-the-mess-that-is-npm/)
* [Why I hate npm](http://www.jongleberry.com/why-i-hate-npm.html)

## Conclusión

En realidad, npm me gusta, y me gusta mucho. Sólo tengo que ser un poco más ordenada, seguir más las [convenciones](https://en.wikipedia.org/wiki/Convention_over_configuration). Pero eso no quita que, al igual que reciclo en casa y me preocupo por el medio ambiente, pensar que todo lo que está en Internet es también medio ambiente, y que no quiero contribuir a llenarlo de *trash*. 




