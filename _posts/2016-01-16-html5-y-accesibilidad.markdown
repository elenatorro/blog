---
layout: post
title: HTML5 y Accesibilidad
date: '2016-01-16 09:36:05'
---

Estado actual:
<pre><code class="language-css">border-top-style: accessible;
</code></pre>

Unas semanas atrás escribí un [post](http://bordertopstyle.com/divinitis/) sobre la tendencia que tenemos los programadores web en escribir código HTML e inundar la web de *divs*. Esto afecta a la **accesibilidad** de las páginas y aplicaciones web, y la gente que hay detrás y permanece en la sombra está esforzándose para que los navegadores sean más accesibles. Y personalmente, este es un tema que, a pesar de que me interesa muchísimo, no lo aplico todo lo que debería (cosa que está cambiando).

Este post surge a raíz de la conferencia [Novedades en HTML5 accesible para la gestión de recursos multimedia](https://canal.uned.es/mmobj/index/id/47135), parte del II Workshop "Tecnología y Accesibilidad" UNED - Fundación Vodafone. He llegado hasta esta charla a través de la asignatura 'Usabilidad y Accesibilidad' que estoy cursando en el Máster. El ponente es [Chaals McCathie Nevile](https://twitter.com/chaals), un Australiano que trabaja en Yandex, el buscador más usado en Rusia, y que ha trabajado para la [W3C](https://www.w3.org/People/Charles/).

He recopilado lo que más me ha interesado y que creo que puede resultar interesante para los que quieran saber hacia donde están conducidos estos avances.

## Video y Audio
Mola mucho que no tengas que utilizar pluggins de terceros como había que hacer antaño para incluir vídeo y audio en la web. HTML5 incluye estos tags para hacerlo todo más sencillo y adaptable.

Además, son elementos bastante *customizables*, porque tienen la opción de añadir los [controles](https://developer.mozilla.org/es/docs/Web/HTML/Usando_audio_y_video_con_HTML5) (play, pause, stop...) de la manera que el desarrollador desee.

Sin embargo, aún faltan cosillas. Por ejemplo, no existe una manera de incluir una transcripción a un vídeo, y que ésta se sincronice con el contenido del vídeo, lo cual sería un gran avance en términos de accesibilidad.

## ARIA

Son las siglas de 'Accessible Rich Internet Applications'. Se trata de una serie de atributos que se pueden añadir a los elementos HTML. Estos atributos se comunican con las APIs de accesibilidad que tienen los distintos navegadores, haciendo que el uso de los tags sea más semántico, proporcionando más información a los navegadores.

Cuando desarrollamos elementos webs, hemos de dotar a estos de un contenido extra, de una explicación, de datos que hagan ese elemento más accesible. Así, los navegadores interpretan la información de un elemento y la pueden utilizar en tecnologías de asistencia para, por ejemplo, personas con dificultades o discapacidades.

![](/img/content/images/2016/01/accessibleelement.png)
Imagen: [W3C](https://www.w3.org/TR/wai-aria/introduction#at_support)

He hecho un breve esquema a partir de la [documentación que ofrece el W3C](https://www.w3.org/TR/wai-aria/usage).

* roles: 
  * define un elemento de interfaz de usuario
* estados y propiedades: aria-*
  * el nombre del atributo empieza con "aria-" para reducir la posibilidad de que coincida con otros atributos existentes.
  * ejemplos:
     * aria-checked
     * aria-haspopup
     * aria-labelledby
  * [tabla de estados y propiedades soportados](https://www.w3.org/TR/wai-aria/appendices#a_schemata)

Aquí vemos unos ejemplos de código:
```
<li role="menuitemcheckbox" aria-checked="true">
  <img src="checked.gif" role="presentation" alt="">
  <!-- note: additional scripts required to toggle image source -->
  Sort by Last Modified
</li>
```

```
<div role="slider" aria-valuenow="1" 
	aria-valuemin="1" aria-valuemax="7"
	aria-valuetext="Sunday">
</div>
```

Existen unas [directivas](http://w3c.github.io/aria-in-html/) que seguir a la hora de utilizar ARIA en HTML5. También se consultar el siguiente [diagrama de clases](https://www.w3.org/TR/wai-aria/rdf_model.png) que explica más sobre los roles y su herencia.

La documentación es muy **extensa**, pero creo que merece la pena estudiarla con atención.

## longdesc

HTML4 tenía una propiedad conocida como **longdesc**, cuyo propósito era el de añadir información adicional a una imagen. Cuando no sólo basta con el atributo **alt**, y se necesita una descripción más detallada.

Buscando información al respecto, he encontrado este [post de Olga Carreras](http://olgacarreras.blogspot.com.es/2015/01/longdesc-soporte-y-alternativas-wcag-20.html) en el que explica este atributo y sus alternativas en HTML5. Básicamente, el uso de este atributo conllevaba cumplir una serie de reglas, sin embargo, 'un 0.13% incluían el atributo LONGDESC. De este porcentaje solo un 1% tenían un LONGDESC adecuado.' Este post es **muy interesante**, ya que en él podemos encontrar:

* Cómo usar correctamente el atributo longdesc
* Soporte del atributo en los distintos navegadores
* Soporte del atributo en **lectores de pantalla**.

También explica como usar [ARIA de manera alternativa](https://www.w3.org/TR/2014/NOTE-WCAG20-TECHS-20140916/ARIA15) para este mismo propósito. Me ha encantado este post.

## El problema de accessKey y JavaScript

Como podemos leer en [Mozilla Developer Network](https://developer.mozilla.org/es/docs/Web/HTML/Atributos_Globales/accesskey): 'El atributo **global accesskey** provee un indicio para generar un atajo de teclado para el elemento actual . Este atributo consiste en una lista de caracteres separada por espacios (un único punto de código Unicode). El explorador usa el primero que existe en la distribución del teclado de la computadora .' Es decir, ofrece la posibilidad de extender la interacción con el DOM sin necesidad de escribir un script.

El uso de este atributo conlleva muchos [problemas](http://john.foliot.ca/more-reasons-why-we-dont-use-accesskeys/).

Chaals nos habla en su charla de que **no usemos JavaScript** para definir interacciones en este atributo, ya que estos hacen que el User Agent (ver esquema anterior) no interactúe como es debido. Para combatir este mal uso del atributo, tiene un [repositorio en GitHub](https://github.com/chaals/accesskey) en el que propone un cambio del uso de accesskey en HTML. En este [ejemplo](http://chaals.github.io/accesskey/tests/accesskey-cyrillic-latin-manual.html) se comprueban los problemas del uso de accesskey mediante un test en distintos navegadores.


## Nuevas tecnologías y adaptación accesible

En una de las preguntas, un chico preguntaba acerca de la inclusión de la accesibilidad en tecnologías que usamos hoy en día como **AngularJS**, **Polymer** o **React**.

La respuesta de Chaals es que se está intentando dar una solución a estas tecnologías, en las cuales 'todo lo que no se ve, no existe'. Se van mostrando y ocultando partes, y sólo lo que está enfrente del usuario existe y se puede interactuar con él. Según él, los ingenieros **no incluyen accesibilidad** en estas tecnologías, pero **sí que es posible** incluir accesibilidad (mientras otras más antiguas como JQuery, del cual reniego a menudo, sí que lo hacen, aunque no ha dado más referencias sobre este tema.)

Leyendo la especificación de ARIA de W3C he encontrado este [apartado sobre contenido dinámico](https://www.w3.org/TR/2013/WD-wai-aria-practices-20130307/#docmgt), que creo que responde en cierto modo a la pregunta anterior, y veo que es un tema **muy interesante**. La accesibilidad en aplicaciones dinámicas y SPAs.

Imagen de portada: [Swing](http://simpledesktops.com/browse/desktops/2013/jul/26/swing/)