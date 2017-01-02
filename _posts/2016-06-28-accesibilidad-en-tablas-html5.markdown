---
layout: post
title: Accesibilidad en Tablas HTML5
date: '2016-06-28 21:56:03'
---

<pre><code class="language-css">border-top-style: aria-labelledby;
</code></pre>

El tema del tag `<table>` y la accesibilidad web ha sido discutido en varias ocasiones. En este post no voy a hablar de por qué no utilizar tablas para maquetar contenido web, sino de las tablas en sí mismas. Últimamente me ha tocado estar trabajando con tablas, y me han surgido muchas dudas al respecto. ¿Qué buenas prácticas existen a la hora de utilizar tablas en HTML5? ¿Cómo conseguir que el contenido sea accesible? ¿Qué herramientas existen para interaccionar con tablas?

En el post de hoy quiero introducir el tema de la accesibilidad web en las tablas: no hablar de tablas en general, ya que éste es un tema increíblemente extenso. Me voy a centrar en tres aspectos concretos, a pesar de que hay muchos más, ya que son los primeros con los que me he encontrado: 

* el tag `<colgroup>`
* los roles que se pueden aplicar a una tabla
* selección de tablas: checkboxes y atributos ARIA.

Soy bastante *newbie* en el tema de accesibilidad, así que voy poco a poco, leyendo mucho y **fijándome en qué hacen otros**. Además, he de confesar que me lo estoy pasando pipa con los **lectores de pantalla**. Ya publiqué un post breve sobre [HTML5 y Accesibilidad](http://bordertopstyle.com/html5-y-accesibilidad/), por si quieres hacer un repaso rápido antes de seguir.

Bien, vayamos por partes. Concretamente, por las **partes de una tabla**. En [este tutorial](https://www.w3.org/WAI/tutorials/tables/) del W3C encontramos una detallada lista de los tipos de tabla, así como las partes que puede tener una tabla. Conviene echarle un ojo por encima para continuar con el post, si no estamos familiarizados con las tablas.

## Ejemplo base

En este post, el código HTML de referencia es el siguiente:

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>HTML 5 Accesible Table</title>
    <link rel="stylesheet" href="style.css" media="screen" title="stylesheet">
</head>

<body>
    <table class="table" role="presentation">
        <colgroup>
            <col class="column-select">
            <col class="column-name">
            <col class="column-surname">
        </colgroup>
        <thead>
            <tr>
                <th scope="col">Selected Row</th>
                <th scope="col">Name</th>
                <th scope="col">Surname</th>
            </tr>
        </thead>
        <tbody role="grid" aria-multiselectable="true">
            <tr role="row" id="row-1">
                <td role="gridcell">
                    <input type="checkbox" aria-labelledby="row-1" name="selected-row-1" value="0" id="check-1" checked>
                </td>
                <td role="gridcell">Elena</td>
                <td role="gridcell">Torro</td>
            </tr>
            <tr role="row" id="row-2">
                <td role="gridcell">
                  <input type="checkbox" aria-labelledby="row-2" name="selected-row-2" value="1" id="check-2">
                </td>
                <td role="gridcell">Alvaro</td>
                <td role="gridcell">Torro</td>
            </tr>
        </tbody>
    </table>
</body>

</html>

```

## `<colgroup>`

Esta etiqueta que desconocía por completo es de gran utilidad. Me surgió la necesidad de añadir ciertas clases a las distintas **columnas** de una tabla, y acudí de cabeza a tocar el **CSS**. ERROOOOR. Para aplicar estilos concretos, conviene utilizar las etiquetas `<colgroup>` y `<col>`. Como se aprecia en el código de referencia, gracias a estas etiquetas podemos aplicar un estilo específico a cada columna. Esto es **mega útil**. En este caso, quiero que mi tabla tenga una primera columna más estrecha que las demás, que utilizaré para colocar el checkbox que seleccionará la fila.

## Roles

Algunos tips de roles en tablas:

* Si usamos th, no es necesario utilizar role="colheader"
* Si el tag `<tbody>`tiene el rol `grid`, esto nos permitirá que también pueda tener el atributo aria `aria-multiselectable`. Un grid es un control **interactivo** que contiene celdas o contenido tabular ordenado en filas y columnas. Es decir, no se limita sólo a las tablas.
* Se puede ver si un rol puede ser problemático, como es el caso de `role="presentation"` en las tablas: http://www.powermapper.com/tests/screen-readers/tables/table-role-presentation/

## Seleccionar filas

Hay ciertas interacciones que por convención se utilizan generalmente en información dispuesta en forma de tabla. Por ejemplo, el manager de Wordpress o la bandeja de correo de Gmail. En mi caso, he estado mirando cómo la bandeja de Gmail ha manejado el tema de la selección de filas, y lo he reflejado en el código de referencia (de manera MUY simplificada). Como se puede apreciar, cada fila tiene un identificador `id`. Así, se puede identificar qué fila se selecciona mediante el checkbox.

En mi caso, estoy usando el lector de pantalla *ChromeVox* para el navegador Chrome. Como dato sin utilidad, le he puesto la voz 'Diego' porque es la que menos ansiedad me produce. Lo que pasa cuando me coloco sobre la primera celda de selección, en la que hay un checkbox, Diego me dice:

* *'Elena Torro. Cell selected.'*

Y en la segunda:

* *'Alvaro Torro. Cell not selected.'*

Y al hacer click en ambos checkboxes, respectivamente:

* *'Elena Torro. Checkbox not checked.'*
* *'Alvaro Torro. Checkbox checked.'*

Pero **OJO**. Si en la celda en la que tengo el nombre y el apellido tuviera un `aria-label`, es decir:

```html
<td role="gridcell" aria-label="Name">Elena</td>
<td role="gridcell" aria-label="Surname">Torro</td>
```

entonces dirá el contenido de este atributo:

* *'Name Surname. Checkbox not checked.'*

**Problema**: `aria-checked'. Éste atributo ARIA nos ayuda a saber si el checkbox está marcado o no. El problema es que, si queremos cambiar su estado, hemos de utilizar JavaScript cuando el usuario haga click en el checkbox para cambiar este atributo. Al utilizar el lector de pantalla, éste hace primero caso al aria-checked, ya esté marcado o no. Sin embargo, al omitir el atributo, el lector de pantalla lee el input correctamente. ¿Alguien conoce una solución? **#INeedHelp**.

Para los que os adentréis en algún link de la bibliografía, o bien busquéis más sobre el tema en Internet, veréis que la documentación sobre los atributos ARIA y sus aplicaciones es, cuanto menos, extensa. Coged un café y poneos cómodos si vais a empezar a leer algo. Como siempre digo, ¡el **feedback** es bienvenido!

# Bibliografía
* [https://www.w3.org/WAI/tutorials/tables/](https://www.w3.org/WAI/tutorials/tables/)
* [https://www.w3.org/TR/html5/tabular-data.html#the-colgroup-element](https://www.w3.org/TR/html5/tabular-data.html#the-colgroup-element)
* [https://www.w3.org/TR/html5/dom.html#allowed-aria-roles,-states-and-properties](https://www.w3.org/TR/html5/dom.html#allowed-aria-roles,-states-and-properties)

* Imagen de portada: [Agon Wallpaper](http://static.simpledesktops.com/uploads/desktops/2013/09/11/agon_wallpaper.png)