---
layout: post
title: La Ley de Fitts
date: '2016-01-07 13:55:18'
---

# ¿Qué es la Ley de Fitts?
Estado actual: <pre><code class="language-css">border-top-style: calculated;
</code></pre>

No todo en el mundo del diseño de interfaces son colores, formas, patrones o diseño responsive. También hay un **lado técnico** que no se ve a primera vista, pero que ahí está.

Por eso, en mi post de hoy, voy a comentaros qué es la **Ley de Fitts**. [Paul Fitts](https://en.wikipedia.org/wiki/Paul_Fitts) era un psicólogo de Ohio que nació hace más de 100 años. Con esto vengo a decir que el diseño y la psicología del diseño no es una **moda reciente**, sino que ya tiene unos cuantos añitos a sus espaldas. Este hombre tuvo una gran repercusión en el ámbito que hoy conocemos como "Human-Computer Interaction", o Interacción Hombre-Máquina. (HCI)

Publicó en 1945 un artículo titulado **"The information capacity of the human motor system in controlling the amplitude of movement"**. En este estudio, Fitts obtiene la manera de predecir el tiempo que una persona necesita para alcanzar un objetivo, dado un tamaño de dicho objetivo y una distancia a éste. Hay que ver cómo nos gusta a las personas calcularlo todo y encontrar maneras de medir las cosas. Total, que en el campo del HCI esto se ha convertido en un *must-know*, y se aplica en el diseño de interfaces. ¿Cuánto tarda un usuario en hacer click utilizando el ratón en un botón en concreto, situado en una posición [x,y] de la aplicación que está usando?

La conclusión de Fitts es que se tarda más en alcanzar un objetivo que está más lejos, y que también se tarda más si el objetivo es más pequeño. Sí, vale, esto es bastante **obvious**. Pero alguien tenía que decirlo, y ése fue Fitts.

Hasta aquí todo es bastante sencillo. Pero claro, no todos los sistemas son iguales. Por ejemplo, el tiempo que voy a tardar en dibujar una línea recta con un **bolígrafo** desde la esquina superior izquierda de mi libreta hasta un punto en el centro de la misma, va a depender de varios factores: el tipo de tinta del bolígrafo, la rugosidad del papel, la velocidad a la que yo dibujo la línea... Si tuviéramos que trazar la misma distancia hacia un punto con las mismas dimensiones, utilizando un ratón en una aplicación de dibujo, los factores determinantes serían distintos: la velocidad de pintado de píxeles de la aplicación, lo bien que se me dé utilizar el ratón, la velocidad a la que haya configurado éste...

![](img/content/images/2016/01/fittslaw.gif)
![](img/content/images/2016/01/fitss2.gif)

Las imágenes anteriores las he obtenido de [este artículo](http://www.particletree.com/features/visualizing-fittss-law/), que lo ilustra y explica bastante bien.

La fórmula simple de la ecuación propuesta por Fitts es la siguiente:

> Índice de Dificultad = log2( 2 Distancia / Ancho del objetivo )

A esta fórmula hay que añadir las variables que comentaba anteriormente. Un poco más desarrollada, la cosa queda tal que así:

> Tiempo de alcance del objetivo = a + b * Índice de Dificultad

Siendo **a** la constante del tiempo de reacción, y **b** la constante del tiempo que el sistema nervioso humano necesita para **procesar un bit**. Esta ley resulta de gran utilidad para, por ejemplo, [diseños de menús desplegables](http://www.sigchi.org/chi97/proceedings/paper/ja.htm)

Esta parte *nerd* del diseño me gusta bastante. Son detalles que muchas veces no tengo en cuenta a la hora de desarrollar una interfaz. Es interesante ver cómo han ido evolucionando los estudios a lo largo del tiempo, cómo se están aplicando al desarrollo de aplicaciones hoy en día.

Artículos relacionados:

* https://msdn.microsoft.com/en-us/library/ms993291.aspx
* http://www.yorku.ca/mack/hci1992.pdf
* http://www.simonwallner.at/ext/fitts/
* http://www.sigchi.org/chi97/proceedings/paper/ja.htm
