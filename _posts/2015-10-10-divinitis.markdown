---
layout: post
title: Divinitis
date: '2015-10-10 10:09:00'
share: true
comments: true
---

Estado actual:

<pre class="language-css"><code>border-top-style: inset;
</code></pre>

## Consulta del Dr. Spider
- *¡Doctor, doctor! ¡Ha llegado otro más!*
- *¿Otro más? ¿Otro con **divinitis**?*
- *Creemos que es una epidemia. Todos presentan los mismos síntomas: ganas de hacer las cosas rápido, desconocimiento de estándares...*
- *Hágalo pasar.*

La paciente entra en la consulta. Parece asustada, no sabe muy bién qué está sucediendo. Todo se ve bien, ¿no? ¿Dónde está es el problema?. El Doctor le ofrece sentarse en la camilla.

- *Abra su **código**.*

El Doctor se coloca el *markupendoscopio* que lleva colgado al cuello, y escucha atentamente. Lo que imaginaba, **divinitis** aguda. Nada que no hubiera visto antes.

- *¿Es grave? -pregunta ella, con cara de preocupación-.*
- *No se preocupe -responde el Doctor, poniendo una mano sobre su hombro para tranquilizarla-. Ha estado ingiriendo **Bootstrap**, ¿verdad?*
- *Así es*
- *De acuerdo. Siéntese, y le hago una receta. Tómese 600gr de **Heichtimiel Cinco** después de cada comida, hasta que los síntomas desaparezcan. Si alguna vez siente que va a sufrir una recaída, disuelva en un vaso con agua un sobre de **W3Consortium** hasta que los síntomas remitan. ¿Alguna pregunta?*
- *¿Puedo seguir usando **Bootstrap**?*

El Doctor suelta una estridente carcajada.
- *¡Pues claro, mujer! Sólo tiene que usarlo con conocimiento, como cualquier otro framework.*

---

La *divinitis* es el uso indiscriminado de la etiqueta **div** en los documentos HTML5. No todo es un div. Las equiquetas HTML tienen un significado, representan un elemento dentro de una página. Usar HTML5 hace que un documento sea más legible, que de un vistazo se vea cuál es la estructura de la página, cómo están distribuídos sus elementos.

> The div element has no special meaning at all. It represents its children. It can be used with the class, lang, and title attributes to mark up semantics common to a group of consecutive elements.[W3C Specification](http://www.w3.org/html/wg/drafts/html/master/Overview.html#the-div-element)

En esta página, puedes ver la [lista de elementos HTML5](https://developer.mozilla.org/es/docs/HTML/HTML5/HTML5_lista_elementos).

El objetivo es marcar el texto para que sea más **semántico**, y exprese mejor la estructura de los elementos que está representando.
![html5](/img/content/images/2015/10/html5_doc_sections.gif)
*[Imagen: HTMLgoodies](http://www.htmlgoodies.com/tutorials/html5/new-tags-in-html5.html#fbid=PKv1jfDynGj)*

El problema es que muchos **frameworks** frontend ponen como ejemplo una sintaxis llena de *divs*, y como tendemos al *copy paste*, lo dejamos tal cual (sí, yo también he sufrido de divinitis y aún me estoy curando de los síntomas, sufriendo alguna que otra recaída sin darme cuenta). Aquí dejo un ejemplo de Bootstrap, comparando lo que tiene en la especificación de su web, con cuál sería una solución más semántica.

## Bootstrap

### [Bootstrap Panels](http://getbootstrap.com/components/#panels)
```
<!-- Bootstrap -->
<div class="panel panel-default">
  <div class="panel-heading">
    <h3 class="panel-title">Panel title</h3>
  </div>
  <div class="panel-body">
    Panel content
  </div>
  <div class="panel-footer">Panel footer</div>
</div>
```

Imaginemos que lo que representa el panel es, como en este mismo blog, el contenido de un post. Hay que etiquetar, por lo tanto, el contenido como *article*. El texto será por lo tanto una sección (*section*) del post.

```
<!-- Bootstrap using HTML5 -->
<article class="panel panel-default">
  <header class="panel-heading">
    <h3 class="panel-title">Panel title</h3>
  </header>
  <section class="panel-body">
    Panel content
  </section>
  <footer class="panel-footer">Panel footer</footer>
</article>
```

Mejor, ¿no? ¿Y qué hay de un menú lateral?

### [Simple sidebar](http://startbootstrap.com/template-overviews/simple-sidebar/)
```
<!-- Sidebar -->
<div id="sidebar-wrapper">
    <ul class="sidebar-nav">
        <li class="sidebar-brand">
            <a href="#">Start Bootstrap</a>
        </li>
        <li>
            <a href="#">Dashboard</a>
        </li>
        <li>
            <a href="#">Shortcuts</a>
        </li>
    </ul>
</div>
```

```
<!-- HTML5 Sidebar -->
<aside>
    <nav id="sidebar-wrapper">
        <header>Menu Title</header>
        <ul class="sidebar-nav">
            <li class="sidebar-brand">
                <a href="#">Start Bootstrap</a>
            </li>
            <li>
                <a href="#">Dashboard</a>
            </li>
            <li>
                <a href="#">Shortcuts</a>
            </li>
        </ul>
    </nav>
</aside>
```

Como se puede ver, no hay un *header* por cada página, sino por cada elemento que precise de otro elemento hijo que actúe como 'título', cabecera o introducción al mismo. Es mucho más comprensible: ahora se reconoce a primera vista que se trata de un menú de navegación situado a un lado.

Esto no quiere decir que los divs desaparezcan, ni mucho menos, sino que son utilizados con objetivos distintos que el de contener información estructurada. Sirven para, por ejemplo, ser utilizados como contenedores del grid que estés utilizando en tu framework, o para contener elementos a los que se les va a aplicar un determinado estilo CSS (esto es sólo un ejemplo).
