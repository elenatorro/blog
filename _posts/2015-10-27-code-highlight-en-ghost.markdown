---
layout: post
title: Code Highlight en Ghost
date: '2015-10-27 21:51:30'
---

<pre><code class="language-css">border-top-style: sleepy;
</code></pre>

## POST EXPRESS
¿Quieres que tus posts con bloques de código queden mucho más *bonicos*?


Lo primero, es bajarse alguna librería de *por ahí* (no soy vaga, soy práctica) que edite el estilo del código. Yo he pillado [Prism](http://prismjs.com/),que la ha hecho [Lea Verou](https://twitter.com/LeaVerou) y para mi gusto tiene todo lo que necesito: una librería simple, fácil de usar y fácil de instalar. Puedes descargártela, consultarla en [github](https://github.com/PrismJS/prism) o instalarla con **bower**:
<pre class="language-bash"><code>$ bower install prism
</code></pre>

El siguiente paso es incluir en tu blog el script (prism.js), el estilo principal (prism.css) y el tema que más te mole (yo lo he dejado tal cual, fíjate si soy *express*).

Después, cada vez que vayas a meter un bloque de código, en lugar de hacerlo con la sintaxis de markdown (poniendo estas tres comas ``` al principio y al final del bloque), usaremos HTML **a pelo**. 

```
<pre class="language-css"><code>
.myClass {
  border-top-style: sleepy;
}
</code></pre>
```

Y *voilá*. Pero **hay un pequeño problema**. Y es que claro, por defecto, si quieres incluir código HTML, no puedes hacerlo así porque markdown **lo renderiza**. Por lo tanto, cuando quieras escribir con un lenguaje de marcado, he hecho lo que se conoce como un *workaround* (también llamado popularmente **ñapa**), que ha sido la mejor solución que se me ha ocurrido. Y es incluir la siguiente función en javascript:

<pre><code class="language-javascript">var item;
var element;
  for (item in document.getElementsByTagName('code')) {
   element = document.getElementsByTagName('code')[item];
   if (!element.className) {
    element.className = 'language-html';
   }
  };
};
</code></pre>

En resumen, coge todos los bloques de código que tengas en el post y, si no les has asignado una clase del tipo language-loquesea, te añade por defecto HTML.

¿Tienes una solución mejor? ¡Cuéntamela!

Imagen de portada: [Inside Out](http://simpledesktops.com/browse/desktops/2015/jul/07/inside-out/)