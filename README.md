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

[volver al indice](#indice)
<br />

 ### Declarando variables 


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
if(esVerdad){ 
  let foo = 'bar'
}
console.log(foo) //undefined
```
- Solo puede declararse una vez en un mismo scope

```js
let foo = 'bar'
let foo = 2 
  //Identifier 'foo' has already been declared.
```

- Puede variar su valor y por lo tanto no necesita inicializarse

```js
let foo;
foo = 'bar';

console.log(foo) //'bar'
```
<span style="color: red;"> **_TIP_** </span>

> Puedes declarar varias variables usando una sola vez let  *No lo recomiendo si no se hace de la forma adecuada* -> Ver buenas practicas 

```js
  //Sin inicializar
  let foo,bar,stwart;
  //Inicializando
  let foo='hello', bar='world', stwart='little';
```


### Exports

<hr />

Con **export** podemos exportar funciones, objetos o tipos de datos para que despues puedan ser importados con [imports](#imports)

<br />

Básicamente existen dos tipos de exportaciones:

- Export sencillo

```js
export const foo = 'bar';

export let foo = 'bar';

export class Clase{}

//Usando algo declarado previamente

const pin =  1234;

export { pin }

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

<hr />

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
