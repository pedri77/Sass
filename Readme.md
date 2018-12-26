# Sass

Sass es un preprocesador de CSS muy utilizado para el desarrollo FrontEnd. Podemos encontrar la información del mismo en el siguiente enlace:

https://sass-lang.com

![Sass](https://sass-lang.com/assets/img/illustrations/glasses-2087d741.svg)

## Instalación

Documentación oficial: https://sass-lang.com/install

La instalación la podemos hacer de diversas maneras. Una de los usos más extendidos es a través de una aplicación como puede ser [Codekit](http://incident57.com/codekit/) o [Prepros](https://prepros.io/). Aunque existen una gran variedad de aplicaciones que podemos describrir en la docu oficial.

También podemos utilizar el manejador de paquetes npom para su instalación, a través de su repo oficial
<code> npm install -g sass <code>

La opción la decides tú.

## Estructura

La estrcutura de Sass es muy simple. Se trata de un archivos central .scss que contiene todo el contenido, el cual compila a otro archivo .css para poderlo llevar a producción.

El archivo central, normalmente llamado style.scss importa todo el código de los archivos subsidiarios en donde está dividido todoe el código.

Un ejemplo es tener un archivo para los colores llamado "_colors.scss", el guión nos indica que este archivo no va a ser compilado. El archivo style.css a través de @import recoge todo el código de los archivos para reusarlo y compilarlo en uno final llamado sytle.css.

```@import 'colors' ```

Un ejemplo de estrucutura de archivos puede ser la siguiente:

```
Base
Components
Layout
Vendor
style.scss
style.css
```

BEM — Block Element Modifier o Modificador de Bloques de Elementos

Como su nombre indica, BEM distingue claramente 3 conceptos: el Bloque, el Elemento y el Modificador.

Documentación oficial:  https://en.bem.info



## Las variables

Las varibales en Sass se definen con el símbolo $. Estas variables las podemos encontrar definidas en un archivo llamado _variables:

```
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;
body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

Cuando queramos reutilizar una de esas variables, en el ejemplo aterior $primary-color utiulizamos ese mismo nombre y lo usará con el color #333

### Escapar una variable en Sass

Para escapar una variable se usa el comodín <code>#<code>.

Esto es necesario en casos como, por ejemplo, cuando la variable está rodeada por comillas y de no ponerse el escape la variable pasaría como una cadena de caracteres..

```
$size: 10;
div {
content: "#{$size}"
}
```

## Nesting o anidación

```
.btn {
  font-size: 15pt;
  &__icon {
    font-size: .6em;
  }
  &.btn--info {
    background-color: $color-info;
  }
}
```

## Mixins

Los mixins nos ayudan a reducir código, reutilizando declaraciones. La forma de uso es <code>@mixin<code>

```
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}
.box { @include transform(rotate(30deg)); }
```

Otro ejemplo

```
@mixin max-width($max-width: 800px) {
  max-width: $max-width
  margin-left: auto
  margin-right: auto
}
```

En este segundo ejemplo le estamos definiendo un valor por defecto. Si deseamos cambiar ese valor, cuando lo llamemos se lo podemos cambiar de esta forma:

```@mixin max-width(1200px)```

### La directiva Content en los mixins

Una de las características que tienen los mixins es la directiva content. Esta nos permite incluir un bloque de contenido dentro de un mixin.


```
@mixin response-to($width) {
  @media only screen and (min-width: $width) {
    @content;
  }
}
```


La forma en la que usamos esta caracter´stica de los @mixin es así:


```
section {
  background: blue;
  @include response-to(800px) {
    background-color: red;
  };
}
```

# Extend

Los extend se declaran con el símbolo de porcentaje ```%```

Permiten que una declaración herede estilos declarados por otra regla o placeholder. 

```
%btn {
  color: black;
  width: 80px;
}

.btn-info {
  @extend %btn;
  background: blue;
}
```

# Funciones en Sass

En Sass poseemos funciones ya definidas, algunas se pueden utilizar para añadir características a los colores.

```
darken(#ffffff, 25%)
lighten(#ffffff, 25%)
invert(#ffffff)
```

EL enlace a la documentación oficial para ver todas las funciones, lo podemos encontrar [aquí](https://sass-lang.com/documentation/file.SASS_REFERENCE.html#functions)

## Crear funciones

```
@function suma($numero-uno, $numero-dos) {
  @return $numero-uno + $numero-dos;
}

.div {
  padding: suma(10px, 5px);
}
```

## Array
```
$fs: (
  big: 24px,
  normal: 16px,
  small: 14px,
  x-small: 12px
);

p {
  font-size: map-get($fs, normal);
}

small {
  font.size: map-get($fs, x-small);
}
```
## Control del flujo

### EACH

```
$font-weights: normal bold italic;

@each $font in ($font-weights) {
  .#{$font} {font.weight: $font;}
}
```

Obteniendo:

```
.normal {
  font-weight: normal;
}

.bold {
  font-weight: bold;
}

.italic {
  font-weight: italic;
}
```

### FOR

```
@for $i from 1 to 5 {
  .class-#{$i} {
    &:before {
      content: "#{$i}"
    }
  }
}
```

Obtenemos el siguiente resultado:

```
.class-1:before {
  content: "1";
}

.class-2:before {
  content: "2";
}

...

.class-5:before {
  content: "5";
}
```

### IF

```
$background-color: black;

@if $background-color == black {
  p {
    text-color: white;
  }
}
@else {
  p {
    text-color: black;
  }
}
```


## Comprobar nuestro código en linea

Si queremos comprobar nuestro código en linea tenemos un recurso muy interesante a través del siguiente enlace: https://www.sassmeister.com

El comodín ```&``` se usa para hacer referencia al padre.






