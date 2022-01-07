# Motivaciones

> Porque

## Indice

  - [Javascript orientado a React](#javascript-orientado-a-react)
    - [Declarando variables](#declarando-variables)
      - [**Var**](#var)
      - [**Const**](#const)
      - [**Let**](#let)
    - [Exports](#exports)
    - [Imports](#imports)
    - [Funciones](#funciones)
      - [Function declaration](#function-declaration)
      - [Function expression](#function-expression)
      - [Arrow function](#arrow-function)
      - [Parametros de función](#parametros-de-funcion)
    - [;](#)
    - [Timers](#timers)
    - [Convenciones](#convenciones)
    - [Asincronismo](#asincronismo)
    - [Desestructuración](#desestructuración)
    - [Objetos](#objetos)
    - [Arrays](#arrays)
    - [Buenas practicas](#buenas-practicas)
    - [Programación funcional](#programación-funcional)
    - [Condicionales](#condicionales)
    - [Breve introduccion a node.js](#breve-introduccion-a-nodejs)
      - [Instalación](#instalación)
      - [nvm](#nvm)
      - [npm](#npm)
      - [pnpm](#pnpm)
  - [Github](#github)
    - [`git init`](#git-init)
    - [`git add`](#git-add)
    - [`git clone`](#git-clone)
    - [`git push`](#git-push)
    - [`git remote`](#git-remote)
    - [`git checkout`](#git-checkout)
    - [`git branch`](#git-branch)
  - [Sass](#sass)
    - [Uso con CRA](#uso-con-cra)
    - [Convenciones](#convenciones-1)
    - [Metodologias](#metodologias)
    - [Funciones y Mixins](#funciones-y-mixins)
    - [Complementando con css-vars](#complementando-con-css-vars)
  - [React](#react)
    - [Iniciar un proyecto](#iniciar-un-proyecto)
    - [Convenciones](#convenciones-2)
    - [Uso de librerias externas](#uso-de-librerias-externas)
      - [Bootstrap](#bootstrap)
      - [Material Ui](#material-ui)
      - [Classnames](#classnames)
      - [Craco](#craco)
      - [React-icons](#react-icons)
    - [Componentes](#componentes)
    - [React router dom](#react-router-dom)
    - [Props](#props)
    - [Ciclo de vida](#ciclo-de-vida)
    - [useContext](#usecontext)
    - [useState](#usestate)
    - [useEffect](#useeffect)
    - [useReducer](#usereducer)
    - [useRef](#useref)
    - [useMemo](#usememo)
    - [Eventos](#eventos)
    - [useCallback](#usecallback)
    - [useLayoutEffect](#uselayouteffect)
    - [useImperativeHandle](#useimperativehandle)
    - [Custom hooks](#custom-hooks)
    - [Proptypes](#proptypes)
    - [Deploy](#deploy)
      - [vercel](#vercel)
      - [heroku](#heroku)
      - [netlify](#netlify)
    - [Styleguidist](#styleguidist)
    - [Patrones avanzados](#patrones-avanzados)
    - [React.lazy](#reactlazy)
    - [Testing con react-testing-library](#testing-con-react-testing-library)
    - [Redux](#redux)
    - [Virtual Dom](#virtual-dom)
  - [Typescript en react](#typescript-en-react)
    - [Tipos](#tipos)
    - [Interfaces](#interfaces)
    - [Genericos](#genericos)
    - [Ventajas](#ventajas)
  - [VSCode 2022](#vscode-2022)
    - [Plugins](#plugins)
    - [Temas](#temas)
    - [Configs](#configs)

## Javascript orientado a React


<br />

### Declarando variables
[volver al indice](#indice)
<hr />

#### **Var**

Era el unico modo para declarar una variable, pero presentaba varios inconvenientes. Muchos programas antiguos la utilizan pero no es lo recomendable.

```js
var foo = "bar";
/* Las variables declaradas con 'var' tienen un scope global
 a menos que fuese declarada dentro de una funcion */
```

#### **Const**

Es la forma en que declaramos variables constantes en javascript. Datos sobre `const`:

- Tiene un alcance de bloque, quiere decir que solo existe en el bloque que fue creada

```js
const funcionFoo = () => {
  const foo = "bar";
  return foo;
};
funcionFoo();

console.log(foo); /*Mostraria un error de referencias pues esta fuera de su scope,
si quisieramos usar ese valor deberiamos asignar el resultado de la funcion a otra variable. /*
```

- Solo pueden declararse una vez _(Dentro de su mismo scope)_

```js
const foo = 1;
const foo = 3;
//Muestra un error que te dice que 'foo' ya ha sido declarado
```

- No puede cambiarse su valor y por lo tanto necesitas inicializarla

```js
const foo = 1;
foo = "bar";
//Muestra un error de asignación
```

_Los arrays y objetos declarados con const pueden ser modificados de ciertas formas_

#### **Let**

> Variables ¿variables?

Al igual que [**Const**](#const), **let** se utiliza en las aplicaciones modernas para declarar variables y tiene alcance de bloque. Datos sobre `let`:

- Solo existe en su contexto:

```js
if (esVerdad) {
  let foo = "bar";
}
console.log(foo); //undefined
```

- Solo puede declararse una vez en un mismo scope

```js
let foo = "bar";
let foo = 2;
//Identifier 'foo' has already been declared.
```

- Puede variar su valor y por lo tanto no necesita inicializarse

```js
let foo;
foo = "bar";

console.log(foo); //'bar'
```

**_TIP_**

> Puedes declarar varias variables usando una sola vez let _No lo recomiendo si no se hace de la forma adecuada_ -> Ver buenas practicas

```js
//Sin inicializar
let foo, bar, stuart;
//Inicializando
let foo = "hello",
  bar = "world",
  stuart = "little";
```

### Exports
[volver al indice](#indice)
<hr />

Con **export** podemos exportar funciones, objetos o tipos de datos para que despues puedan ser importados con [imports](#imports)

<br />

Básicamente existen dos tipos de exportaciones:

- Export sencillo

```js
export const foo = "bar";

export let foo = "bar";

export class Clase {}

//Usando algo declarado previamente

const pin = 1234;

export { pin };
```

Este tipo de export es obligatorio importarlo con el nombre correspondiente. _Se le puede agregar un alias_

[//]: <> (TODO agregar link al alias)

- Export por default

```js

export default function(){...}

export default class Clase(){ }

const foo = 'bar';

export default foo;

```

_Las variables no pueden usar `export default` directamente_

_Solo puede existir un export por defecto por archivo_

**_TIP_**

> Si uno quiere usar una estructura de archivos basado en indices es interesante conocer que se puede re-exportar desde otro archivo.

```js
//Re-exportamos bar.
export { bar } from "./bar.js";
//Esto seria equivalente
import { bar } from "./bar.js";
export { bar };
```

_bar fue re-exportado de forma sencilla y deben ser importados con ese nombre y con el tipo de `import` adecuado._

[//]: <> (TODO agregar link al alias y al import)

### Imports
[volver al indice](#indice)
<hr />

Con **import** podemos importar funciones, objetos o tipos de datos que fueron efectivamente exportados con [export](#exports)

- Importando export por defecto de un modulo

```js
import foo from "./bar.js";
//Le asignamos un nombre a esa importación, no necesariamente el mismo que tenia en el archivo
import superiorFoo from "./bar.js";
//Si queremos importar algo más ademas de lo exportado por defecto
import foo, { bar } from "./bar.js";
```

- Importando los export sencillos

```js
import { foo } from "bar.js";
```

Anatomia de estos import:

- `import` &nbsp; _Declaración de importación estática_
- `{foo}` &nbsp; _Modulo a importar, debe ir entre llaves y ademas haber sido exportado con ese nombre en especifico, ej:_ `export {foo}`
- `from` &nbsp; _Desde_
- `'bar.js'` ruta al archivo

### Funciones
[volver al indice](#indice)
<hr />

#### Function declaration

Se _declara_ una funcion con la palabra reservada `function`

```js
function multiply(a, b) {
  return a * b;
}
```

#### Function expression

Se almacena la funcion en una variable, su principal ventaja y desventaja a la vez es que no puede ser usada hasta ser declarada, por lo tanto evitamos comportamientos inesperados.

```js
multiply(2, 3); // No definida
const multiply = function (a, b) {
  return a * b;
};
multiply(2, 3); // 6
```

#### Arrow function

Las `arrow functions` siempre son anonimas, tambien se pueden asignar a una variable o usarse como callback. `() => {}`

```js
const multiply = (a, b) => {
  return a * b;
};

multiply(2, 3); //6

/* El retorno en las arrow function puede ser implicito
siempre que se vaya a retornar algo inmediatamente
y no se vaya a agregar otra logica */

const multiply = (a, b) => a * b;

multiply(2, 3); // 6

/* Si solo recibe un parametro se pueden omitir
los parentesis */

const upName = (name) => name.toUpperCase();
upName("Fulano"); // 'FULANO'

/* Y son muy utiles para usar como callback */

otraFuncion(() => console.log('Hola'));

//otraFuncion solo espera un callback como parametro

/* Si solo se quiere retornar un objeto, este
se envuelve con parentesis */

const objectG = () => ({ title: "El hijo del consul", precio: 300 });

objectG(); //{title: 'El hijo del consul', precio: 300}
```

#### Parametros de función

Una función es una porcion de codigo que es independiente al resto
del programa, algo asi como una "plantilla" para usarla posteriormente.
Estas reciben ( o no ) parametros , estos parametros son variables y
pueden llamarse con cualquier nombre (*siempre que no sean palabras reservadas*).
```js
//Parametros de addTwoNumbers => n1 , n2
const addTwoNumbers = (n1, n2) => n1 + n2
//Funciona exactamente igual pero los llamamos number1 y number2
const addTwoNumbers = (number1, number2) => number1 + number2
/* Para constatar se pueden llamar de cualquier forma, 
seria confuso pero posible por que no sabemos si se van a 
concatenar strings o sumar numeros o agendar una fiesta */
const addTwoNumbers = (tequila, casita) => tequila + casita
```
Al llamar la funcion los parametros se pasan en el orden que se establecieron al crear la funcion
```js
addTwoNumbers(2,4) //6
//2 seria n1 y 6 n2
```
Si quisieramos que el orden no importara, podemos establecer que los parametros sean un objeto. (Ver desestructuración )

[//]: <> (TODO agregar link a desestructuración)

```js
const addTwoNumbers = ({numero1, numero2}) => numero1 + numero2
addTwoNumbers({numero1: 2, numero2: 4}) //6
```

### ;

<hr />

### Timers

<hr />

### Convenciones

<hr />

### Asincronismo

<hr />

### Desestructuración

<hr />

### Objetos

<hr />

### Arrays

<hr />

### Buenas practicas

<hr />

### Programación funcional

<hr />

### Condicionales

<hr />

### Breve introduccion a node.js

<hr />

#### Instalación

#### nvm

#### npm

#### pnpm

## Github

[volver al indice](#indice)

### `git init`

<hr />

### `git add`

<hr />

### `git clone`

<hr />

### `git push`

<hr />

### `git remote`

<hr />

### `git checkout`

<hr />

### `git branch`

<hr />

## Sass

### Uso con CRA

<hr />

### Convenciones

<hr />

### Metodologias

<hr />

### Funciones y Mixins

<hr />

### Complementando con css-vars

<hr />

[volver al indice](#indice)

<hr />

## React

[volver al indice](#indice)

### Iniciar un proyecto

<hr />

### Convenciones

<hr />

### Uso de librerias externas

<hr />

#### Bootstrap

#### Material Ui

#### Classnames

#### Craco

#### React-icons

### Componentes

<hr />

### React router dom

<hr />

### Props

<hr />

### Ciclo de vida

<hr />

### useContext

<hr />

### useState

<hr />

### useEffect

<hr />

### useReducer

<hr />

### useRef

<hr />

### useMemo

<hr />

### Eventos

<hr />

### useCallback

<hr />

### useLayoutEffect

<hr />

### useImperativeHandle

<hr />

### Custom hooks

<hr />

### Proptypes

<hr />

### Deploy

<hr />

#### vercel

#### heroku

#### netlify

### Styleguidist

<hr />

### Patrones avanzados

<hr />

### React.lazy

<hr />

### Testing con react-testing-library

<hr />

### Redux

<hr />

### Virtual Dom

<hr />

## Typescript en react

[volver al indice](#indice)

### Tipos

<hr />

### Interfaces

<hr />

### Genericos

<hr />

### Ventajas

<hr />

## VSCode 2022

[volver al indice](#indice)

### Plugins

### Temas

### Configs
