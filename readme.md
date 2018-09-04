#Guia de estilos básica 
 
###Estructura de carpetas
-
`/styles`

`/styles/core`

`/styles/lib`

`/styles/components`

`/styles/web-parts`


Dentro de `/styles/core` van los archivos `.sccs` parte del núcleo del proyecto tales como resets, estilos genéricos, mixins, funciones, exteds, etc.


En el caso de integrar librerías externas usar la carpeta `/styles/lib` para su integración.

Dentro de `/styles/web-parts` se incluyen archivos scss para cada sección del sitio (header, footer, etc.). al agregar un nuevo archivo es 
importante escribirlo en ingles y que sea descriptivo.

Dentro de `/styles/components` se incluyen archivos scss para cada componente del sitio. 
al agregar un nuevo archivo es importante escribirlo en ingles y que sea descriptivo.

Por ejemplo para un componente Timeline crear el archivo _timeline.scss y después de eso importarlo en
`/styles/components/index.scss`

#CSS

###Formato
-
* Usar “soft tabs” (2 espacios) de indentación
* Preferentemente usar guiones medios (`-`) en lugar de [camelCase](https://es.wikipedia.org/wiki/CamelCase) en nombres de clases.
  - Guiones bajos (`_`) al adoptar la metodologia BEM son validos simpre y cuando se siga las reglas del mismo.
* No utilizar selectores ID
* Cuando se utilizan varios selectores en una declaración de regla, poner cada selector en una línea
* Poner un espacio antes de la llave de apertura `{` en declaraciones de regla
* En las propiedades, poner un espacio después, y no antes, del caracter `:` (dos puntos)
* Poner las llaves de cierre `}` de las declaraciones de regla en una nueva línea
* Poner líneas en blanco entre las declaraciones de reglas

**Mal**

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```

**Bien**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.un,
.selector,
.por-linea {
  // ...
}
```

### Comentarios

* Preferentemente usar `//` (en Sass) para bloques de comentarios.
* Preferentemente escribir comentarios en una única línea para ello. Evitar los comentarios al final de una línea.
* Escribir comentarios detallados de código que no es auto-documentado:
  - Usos de z-index
  - Compatibilidad o hacks para navegadores específicos

### OOCSS y BEM

Incentivamos el uso de una combinación de OOCSS y BEM por las siguientes razones:

  * Ayuda a crear relaciones claras y estrictas entre CSS y HTML
  * Ayuda a crear componentes reutilizables y que se pueden recomponer.
  * Permite menos anidación y menor especificidad
  * Ayuda a construir hojas de estilos escalables

**OOCSS**, o “CSS Orientado a Objetos” por sus siglas en Inglés, es un enfoque para escribir CSS que le permite pensar en sus hojas de estilo como una colección de “objetos”: reutilizables, con snippets que pueden repetirse fácilmente y se pueden utilizar independientemente a través de un sitio web.

  * [OOCSS Artículo](https://ed.team/blog/css-orientado-objetos-oocss) de edTeam

**BEM**, o “Bloque-Elemento-Modificador”, es una _convención de nomenclatura_ para clases en HTML y CSS. Fue originalmente desarrollado por Yandex con grandes bases de código y escalabilidad en mente, y puede servir como un conjunto sólido de directrices para la aplicación de OOCSS.

  * [Introducción a BEM](https://webdesign.tutsplus.com/es/articles/an-introduction-to-the-bem-methodology--cms-19403) de tutsplus

  ### Selectores ID

Si bien es posible seleccionar elementos por ID en CSS, en general se debe considerar un anti-patrón. Los selectores ID introducen innecesariamente un alto nivel de [especificidad](https://developer.mozilla.org/es/docs/Web/CSS/Especificidad) a sus declaraciones de regla, y no son reutilizables.

### JavaScript hooks

Evitar la vinculación de la misma clase en tu CSS y JavaScript. Combinar los dos a menudo tiene consecuencias negativas, como mínimo, tiempo perdido durante la refactorización cuando un desarrollador debe hacer una referencia cruzada de cada clase que está cambiando, y peor aún, los dessarrolladores temen hacer cambios por miedo a romper la funcionalidad.

Recomendamos crear clases específicas para JavaScript para vincular con CSS, con el prefijo `.js-`:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

### Border

Utilizar `0` en lugar de `none` para especificar que un estilo no tiene borde.

**Mal**

```css
.foo {
  border: none;
}
```

**Bien**

```css
.foo {
  border: 0;
}
```

## Sass

### Sintaxis

* Utilizar la sintaxis `.scss`, nunca la sintaxis `.sass` original
* Ordenar el CSS regular y las declaraciones `@include` lógicamente (ver a continuación)

### Orden de las declaraciones de propiedades

1. Declaraciones de Propiedades

    Listar todas las declaraciones de propiedades estándar en orden alfabetico, todo lo que no sea un `@include` o un selector anidado.

    ```scss
    .btn-green {
      background: green;
      display:flex;
      font-weight: bold;
      z-index:1;
      // ...
    }
    ```

2. Declaraciones `@include`

    Agrupar `@include`s al final hace que sea más fácil de leer el selector entero.

    ```scss
    .btn-green {
      background: green;
      display:flex;
      font-weight: bold;
      z-index:1;
      @include transition(background 0.5s ease);
      // ...
    }
    ```

3. Selectores anidados

    Los selectores anidados, _si es necesario_, van al final, y nada va después de ellos. Añadir espacio en blanco entre las declaraciones y selectores de reglas anidadas, así como entre los selectores adyacentes anidados. Aplicar las mismas directrices anteriores a los selectores anidados.

    ```scss
    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      .icon {
        margin-right: 10px;
      }
    }
    ```
### Variables

Preferentemente utilizar nombres de variable con guiones medios (ej. `$mi-variable`) en lugar de escritura de camello (camelCase) o guiones bajos (snake_case). Es aceptable utilizar como prefijo para nombres de variables que están pensados para ser utilizados solo dentro del mismo archivo con guión bajo (ej., `$_mi-variable`).

### Mixins

Se deben utilizar Mixins para no repetir código ([principio DRY](https://es.wikipedia.org/wiki/No_te_repitas)), agregar claridad o abstraer de complejidad de la misma manera que las funciones. Los Mixins que no aceptan argumentos pueden ser útiles para ello, pero notar que si no está comprimiendo su carga (ej. gzip), esto puede contribuir a la duplicación innecesaria de código en los estilos resultantes.

### Extend

`@extend` debe evitarse ya que tiene un comportamiento poco intuitivo y potencialmente peligroso, específicamente cuando se utiliza con selectores anidados. Incluso extender los selectores placeholder de nivel superior puede causar problemas si el orden de los selectores termina cambiando más tarde (ej. si se encuentran en otros archivos y el orden de los archivos cambia). Gzipping debe manejar la mayor parte de los ahorros que se habría obtenido mediante el uso de `@extend`, y se puede evitar la repetición de código <sup>1</sup> en las hojas de estilos muy bien con mixins.

_<sup>1</sup> Se utiliza el verbo "DRY up" haciendo referencia al principio [DRY (Don't Repeat Yourself)](https://es.wikipedia.org/wiki/No_te_repitas)._

### Anidación

**¡No anidar selectores más de 3 niveles de profundidad!**

```scss
.page-container {
  .content {
    .profile {
      // PARAR!
    }
  }
}
```

Cuando los selectores se vuelven muy largos, probablemente se está escribiendo CSS que es:

* Fuertemente acoplado al HTML (frágil) *—O—*
* Excesivamente específico (poderoso) *—O—*
* No reutilizable

Nuevamente: **¡nunca anidar selectores ID!**

Si tiene que usar un selector ID en primer lugar (debería intentar no hacerlo), nunca deberían anidarse. Si se encuentra haciendo esto, neceista revisar su marcado HTML, o averiguar por qué necesita tanta especificidad. Si está escribiendo HTML y CSS bien formado, **nunca** debería hacer esto.

*Basado en https://github.com/airbnb/css*

