<div align="center">

<h1>React+TypeScript Cheatsheets en Español</h1>

<a href="https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/81">
  <img
    height="90"
    width="90"
    alt="react + ts logo"
    src="https://user-images.githubusercontent.com/6764957/53868378-2b51fc80-3fb3-11e9-9cee-0277efe8a927.png"
    align="left"
  />
</a>

<p>Cheatsheets para desarrolladores expertos en React que comienzan con TypeScript</p>

[**Básico**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es#tabla-de-contenidos-de-la-cheatsheet-básica) |
[**Avanzado**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/blob/master/AVANZADO.md) |
[**Migrando**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/blob/master/MIGRANDO.md) |
[**HOC**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/blob/master/HOC.md) |
[**Inglés**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet) |
[**中文翻译**](https://github.com/fi3ework/blog/tree/master/react-typescript-cheatsheet-cn) |
[Contribuir](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/blob/master/CONTRIBUYENDO.md) |
[Preguntas](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/issues/new)

---

:wave: Este repositorio es mantenido por [@laurosilvacom](https://twitter.com/laurosilvacom), [@aromanarguello](https://twitter.com/aromanarguello), [@rainerxmf ](https://twitter.com/rainerxmf), [@dantehemerson](https://twitter.com/dantehemerson), y [@hanslgarcia](https://twitter.com/HansLGarcia) . ¡Estamos tan contentos de que quieras probar TypeScript con React! Si ves que algo esta mal, ¡abre un [_Issue_](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/issues/new)! :+1:

---

</div>

[![All Contributors](https://img.shields.io/github/contributors/typescript-cheatsheets/react-typescript-cheatsheet?color=orange&style=flat-square)](/COLABORADORES.md)

## All React + TypeScript Cheatsheets

- **La cheatsheet básica** ([`/README.md`](/README.md#basic-cheatsheet-table-of-contents)) se enfoca en ayudar a los desarrolladores de React a comenzar a usar TS en **aplicaciones** de React
  - Enfoque en buenas prácticas (según nuestra opinión) y ejemplos que se puedan copiar y pegar.
  - Explica en la marcha el uso y configuración de algunos tipos básicos de TS.
  - Responde las preguntas más frecuentes.
  - El objetivo es lograr volverse efectivo con TS sin aprender _demasiado_ TS.
- **La cheatsheet avanzada** ([`/AVANZADO.md`](/AVANZADO.md)) ayuda a mostar y explicar usos avanzados de los tipos genéricos para personas que escriben tipos reutilizables en utilidades/funciones/render props/components de orden superior y **bibliotecas** de TS+React.
  - También tiene consejos y trucos variados para usuarios avanzados.
  - Consejos para contribuir a DefinitelyTyped
  - El objetivo es _aprovechar al máximo_ TypeScript.
- **La cheatsheet de migración** ([`/MIGRATING.md`](/MIGRATING.md)) ayuda a agrupar consejos para migrar incrementalmente una base de código grande de JS o Flow, **de personas que lo han hecho**.
  - No intentamos convencer a las personas a hacer el cambio, solo ayudar a aquellos que ya se han decidido.
  - ⚠️Esta es una nueva cheatsheet, toda ayuda es bienvenida.
- **La cheatsheet HOC** ([`/HOC.md`](/HOC.md)) enseña específicamente a las personas a escribir componentes de orden superior (HOC por sus siglas en inglés) con ejemplos.
  - Es necesario estar familiarizado con la [Genericidad](https://www.typescriptlang.org/docs/handbook/generics.html).
  - ⚠️Esta es una nueva cheatsheet, toda ayuda es bienvenida.

---

### Tabla de contenidos de la Cheatsheet básica

<details>

<summary><b>Expandir tabla de contenidos</b></summary>

- [Sección 1: Configuración](#sección-1-configuración)
  - [Prerrequisitos](#prerrequisitos)
  - [Herramientas de inicio de React + TypeScript](#herramientas-de-inicio-de-react--typescript)
  - [Importar React](#importar-react)
- [Sección 2: Comienzo](#sección-2-comienzo)
  - [Componentes de función](#componentes-de-función)
  - [Hooks](#hooks)
  - [Componentes de clase](#componentes-de-clase)
  - [Tipos de defaultProps](#tipos-de-defaultprops)
  - [¿Tipos o interfaces?](#tipos-o-interfaces)
  - [Ejemplos básicos de Prop Types](#ejemplos-básicos-de-prop-types)
  - [Ejemplos útiles de tipos de props en React](#ejemplos-útiles-de-tipos-de-props-en-react)
  - [getDerivedStateFromProps](#getderivedstatefromprops)
  - [Formularios y Eventos](#formularios-y-eventos)
  - [Contexto](#contexto)
  - [forwardRef/createRef](#forwardrefcreateref)
  - [Portales](#portales)
  - [Barreras de error](#barreras-de-error)
  - [Concurrent React/React Suspense](#concurrent-reactreact-suspense)
- [Manual básico de resolución de problemas: Tipos](#manual-básico-de-resolución-de-problemas-tipos)
  - [Tipos de unión y seguro de tipo](#tipos-de-unión-y-seguro-de-tipo)
  - [Tipos opcionales](#tipos-opcionales)
  - [Tipos Enum](#tipos-enum)
  - [Aserción de tipo](#aserción-de-tipo)
  - [Simulación de tipos nominales](#simulación-de-tipos-nominales)
  - [Tipos de intersección](#tipos-de-intersección)
  - [Tipos de unión](#tipos-de-unión)
  - [Sobrecarga de tipos de función](#sobrecarga-de-tipos-de-función)
  - [Uso de tipos inferidos](#uso-de-tipos-inferidos)
  - [Uso de tipos parciales](#uso-de-tipos-parciales)
  - [¡Los tipos que necesito no fueron exportados!](#los-tipos-que-necesito-no-fueron-exportados)
- [Manual de resolución de problemas: Imágenes y otros archivos que no son TS/TSX](#manual-de-resolución-de-problemas-imágenes-y-otros-archivos-que-no-son-tstsx)
- [Manual de resolución de problemas: Operadores](#manual-de-resolución-de-problemas-operadores)
- [Manual de resolución de problemas: Utilitarios](#manual-de-resolución-de-problemas-utilitarios)
- [Manual de resolución de problemas: ESLint](#manual-de-resolución-de-problemas-eslint)
- [Manual de resolución de problemas: tsconfig.json](#manual-de-resolución-de-problemas-tsconfigjson)
- [Manual de resolución de problemas: Errores en tipos oficiales](#manual-de-resolución-de-problemas-errores-en-tipos-oficiales)
- [Bases de código de React + TypeScript recomendadas para aprender](#bases-de-código-de-react--typescript-recomendadas-para-aprender)
- [Herramientas e integración en editores](#herramientas-e-integración-en-editores)
- [Linting](#linting)
- [Otros recursos sobre React + TypeScript](#otros-recursos-sobre-react--typescript)
- [Charlas recomendadas sobre React + TypeScript](#charlas-recomendadas-sobre-react--typescript)
- [Hora de realmente aprender TypeScript](#hora-de-realmente-aprender-typescript)
- [Aplicación de ejemplo](#aplicación-de-ejemplo)
- [¡Mi pregunta no está respondida aquí!](#mi-pregunta-no-está-respondida-aquí)
  - [Contribuidores](#contribuidores)

</details>

# Sección 1: Configuración

## Prerrequisitos

1. Buena comprensión de [React](https://reactjs.org)
2. Estar familiarizado con con los [tipos de TypeScript básicos](https://www.typescriptlang.org/docs/handbook/basic-types.html) ([La guía de 2ality](http://2ality.com/2018/04/type-notation-typescript.html) es de ayuda)
3. Haber leído la [sección sobre TypeScript en la documentación oficial de React](https://es.reactjs.org/docs/static-type-checking.html#typescript).
4. Haber leído [la sección de React del nuevo Typescript playground](http://www.typescriptlang.org/play/index.html?jsx=2&esModuleInterop=true&e=181#example/typescript-with-react) (opcional: además haga los 40+ ejemplos debajo de la sección de ejemplos [del playground](http://www.typescriptlang.org/play/index.html))

Esta guía siempre asumirá que estás iniciando con la última versión de Typescript. Las notas para versiones anteriores se encontrarán en etiquetas expandibles `<details>`.

## Herramientas de inicio de React + TypeScript

1. [Create React App v2.1+ con Typescript](https://facebook.github.io/create-react-app/docs/adding-typescript): `npx create-react-app my-app --template typescript`

- Solíamos recomendar `create-react-app-typescript` pero ahora está [desaconsejado](https://www.reddit.com/r/reactjs/comments/a5919a/createreactapptypescript_has_been_archived_rip/). [consulta las instrucciones para la migración](https://vincenttunru.com/migrate-create-react-app-typescript-to-create-react-app/)

2. [La guía de Basarat](https://github.com/basarat/typescript-react/tree/master/01%20bootstrap) para una **configuración manual** de React + TypeScript + Webpack + Babel

- En particular, asegúrate de tener `@types/react` y `@types/react-dom` instalados ([Lee más acerca del proyecto DefinitelyTyped si no estás familiarizado](https://definitelytyped.org/)).
- También hay muchos _boilerplates_ de React + Typescript, por favor consulta [nuestra lista de recursos debajo](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet#recommended-react--typescript-codebases-to-learn-from).

## Importar React

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
```

En [TypeScript 2.7+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-7.html), puedes correr TypeScript con `--allowSyntheticDefaultImports` (o añadir `"allowSyntheticDefaultImports": true` a tsconfig) para importar como se hace normalmente en jsx:

```tsx
import React from "react";
import ReactDOM from "react-dom";
```

<details>

<summary>Explicación</summary>

¿Por qué `allowSyntheticDefaultImports` sobre `esModuleInterop`? [Daniel Rosenwasser](https://twitter.com/drosenwasser/status/1003097042653073408) ha dicho que es mejor para webpack/parcel. Para consultar más argumentos en el debate visita <https://github.com/wmonk/create-react-app-typescript/issues/214>

¡Por favor haz un PR o [abre un _issue_](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new) con tus sugerencias!

</details>

# Sección 2: Comienzo

## Componentes de función

Pueden escribirse como funciones normales que pueden tomar un argumento `props` y retornar un elemento JSX.

```tsx
type AppProps = { message: string }; /* también se puede usar una interfaz */
const App = ({ message }: AppProps) => <div>{message}</div>;
```

<details>

<summary><b>¿Y dónde queda `React.FC`/`React.FunctionComponent`?</b></summary>

También puedes escribir componentes con `React.FunctionComponent` (o la forma abreviada `React.FC`):

```tsx
const App: React.FC<{ message: string }> = ({ message }) => (
  <div>{message}</div>
);
```

Algunas diferencias con la versión "normal de función":

- Proporciona chequeo de tipos y autocompletamiento para propiedades estáticas como `displayName`, `propTypes`, y `defaultProps` - **Sin embargo**, actualmente existen problemas conocidos cuando se usa `defaultProps` con `React.FunctionComponent`. Consulta [este _issue_ para los detalles](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/87) (navega hacia nuestra sección sobre `defaultProps` para las recomendaciones sobre la declaración de tipos).

- Proporciona un definición implícita de `children` (ver debajo); sin embargo existen algunos problemas con el tipo implícito `children` (p.ej. [DefinitelyTyped#33006](https://github.com/DefinitelyTyped/DefinitelyTyped/issues/33006)), y podría considerarse de todas formas ser explícito en los componentes que consumen `children`.

```tsx
const Title: React.FunctionComponent<{ title: string }> = ({
  children,
  title
}) => <div title={title}>{children}</div>;
```

- _En el futuro_, podría marcar props automáticamente como `readonly`, aunque es discutible si el objeto props se desestructura en la lista de parámetros.

- `React.FunctionComponent` es explícito sobre el tipo de retorno, mientras la forma normal de función es implícita (o de lo contrario necesita anotaciones adicionales).

En la mayoría de los casos no importa mucho qué sintaxis se use, pero la sintaxis de `React.FC` es ligeramente más verbosa sin proporcionar una clara ventaja, por lo que se le da precedencia a la sintaxis "normal de función".

</details>

<details>
<summary><b>Problemas menores</b></summary>

Estos patrones no se permiten:

**Renderizado condicional**

```tsx
const MyConditionalComponent = ({ shouldRender = false }) =>
  shouldRender ? <div /> : false; // no hagas esto tampoco en JS
const el = <MyConditionalComponent />; // lanza un error
```

Esto ocurre por limitaciones en el compilador, los componentes de función no pueden retornar otra cosa que no sea una expresión JSX o `null`, de lo contrario se queja con un mensaje de error críptico qeu dice que el otro tipo no es asignable a `Element`.

```tsx
const MyArrayComponent = () => Array(5).fill(<div />);
const el2 = <MyArrayComponent />; // lanza un error
```

**Array.fill**

Desafortunadamente con simplemente anotar el tipo de la función no se resolverá, por lo que si realmente necesitas retornar otros tipos exóticos con los que React es compatible, necesitarás realizar una aserción de tipo:

```tsx
const MyArrayComponent = () => (Array(5).fill(<div />) as any) as JSX.Element;
```

[Consulta aquí el comentario de @ferdaber](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/57).

</details>

## Hooks

Los Hooks están incluidos [en `@types/react` desde la versión v16.8 en adelante](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/a05cc538a42243c632f054e42eab483ebf1560ab/types/react/index.d.ts#L800-L1031).

**useState**

La inferencia de tipo funciona muy bien la mayoría de las veces:

```tsx
const [val, toggle] = React.useState(false); // se infiere que `val` es un booleao, `toggle` solo toma booleanos
```

Consulta también la sección sobre el [Uso de tipos inferidos](#using-inferred-types) si necesitas usar un tipo complejo y te has apoyado en la inferencia para hacerlo.

Sin embargo, muchos hooks son inicializados con valores por defecto de tipo null o semejantes y puede que te preguntes como proporcionar tipos. Declara explícitamente el tipo y utiliza un tipo de unión:

```tsx
const [user, setUser] = React.useState<IUser | null>(null);

// later...
setUser(newUser);
```

**useRef**

Cuando utilices `useRef`, tienes dos opciones al crear un contenedor de la ref que no tiene un valor inicial:

```ts
const ref1 = useRef<HTMLElement>(null!);
const ref2 = useRef<HTMLElement | null>(null);
```

La primera opción hará que `ref1.current` sea de solo lectura y se usa para pasarla a los atributos incorporados `ref` que React manejará (porque React maneja la actualización del valor `current` por ti).

La segunda opción hará que `ref2.current` sea mutable, y se usa para "variables de instancia" que quieres manejar tú mismo.

**useEffect**

Al utilizar `useEffect`, asegúrate de no retornar otra cosa que no sea una función o `undefined`, de otra forma tanto TypeScript como React se quejarán. Esto puede ser sútil al usar funciones flecha:

```ts
function DelayedEffect(props: { timerMs: number }) {
  const { timerMs } = props;
  // mal! setTimeout retorna implícitamente un número porque la función flecha no está envuelta en llaves
  useEffect(
    () =>
      setTimeout(() => {
        /* do stuff */
      }, timerMs),
    [timerMs]
  );
  return null;
}
```

**useRef**

```tsx
function TextInputWithFocusButton() {
  // inicializa con null, pero dile a TypeScript que estamos buscando un HTMLInputElement
  const inputEl = React.useRef<HTMLInputElement>(null);
  const onButtonClick = () => {
    // Los chequeos estrictos de null requieren que verifiquemos si inputEl y current existen.
    // ¡Pero una vez que current existe, es de tipo HTMLInputElement, por lo que
    // tiene el método focus! ✅
    if (inputEl && inputEl.current) {
      inputEl.current.focus();
    }
  };
  return (
    <>
      {/* Adicionalmente, inputEl solo puede ser usada en elementos input. ¡Sí! */}
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgIilQ3wFgAoCzAVwDsNgJa4AVJADxgElaxqYA6sBgALAGIQ01AM4AhfjCYAKAJRwA3hThwA9DrjBaw4CgA2waUjgB3YSLi1qp0wBo4AI35wYSZ6wCeYEgAymhQwGDw1lYoRHCmEBAA1oYA5nCY0HAozAASLACyADI8fDAAoqZIIEi0MFpwaEzS8IZllXAAvIjEMAB0MkjImAA8+cWl-JXVtTAAfEqOzioA3A1NtC1wTPIwirQAwuZoSV1wql1zGg3aenAt4RgOTqaNIkgn0g5ISAAmcDJvBA3h9TsBMAZeFNXjl-lIoEQ6nAOBZ+jddPpPPAmGgrPDEfAUS1pG5hAYvhAITBAlZxiUoRUqjU6m5RIDhOi7iIUF9RFYaqIIP9MlJpABCOCAUHJ0eDzm1oXAAGSKyHtUx9fGzNSacjaPWq6Ea6gI2Z9EUyVRrXV6gC+DRtVu0RBgxuYSnRIzm6O06h0ACpIdlfr9jExSQyOkxTP5GjkPFZBv9bKIDYSmbNpH04ABNFD+CV+nR2636kby+BETCddTlyo27w0zr4HycfC6L0lvUjLH7baHY5Jas7BRMI7AE42uYSUXed6pkY6HtMDulnQruCrCg2oA)

Ejemplo creado por [Stefan Baumgartner](https://fettblog.eu/typescript-react/hooks/#useref)

**useReducer**

Puedes usar [Uniones discriminadas](https://www.typescriptlang.org/docs/handbook/advanced-types.html#discriminated-unions) para las acciones del reductor. No olvides definir el tipo de retorno del reductor, de lo contrario Typescript lo inferirá.

```tsx
type AppState = {};
type Action =
  | { type: "SET_ONE"; payload: string }
  | { type: "SET_TWO"; payload: number };

export function reducer(state: AppState, action: Action): AppState {
  switch (action.type) {
    case "SET_ONE":
      return {
        ...state,
        one: action.payload // `payload` es de tipo string
      };
    case "SET_TWO":
      return {
        ...state,
        two: action.payload // `payload` es de tipo number
      };
    default:
      return state;
  }
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/C4TwDgpgBAgmYGVgENjQLxQN4F8CwAUKJLAMbACWA9gHZTqFRQA+2UxEAXFAEQICiAFQD6AeQBy-HgG4oYZCAA2VZABNuAZ2AAnCjQDmUfASass7cF14CRggOqiZchcrXcaAVwC2AIwjajaUJCCAAPMCptYCgAMw8acmo6bQhVD1J-AAotVCs4RBQ0ABooZETabhhymgBKSvgkXOxGKA0AdwpgUgALKEyyyloAOg4a5pMmKFJkDWg+ITFJHk4WyagU4A9tOixVtaghw5zivbXaKwGkofklFVUoAHoHqAADG9dVF6gKDVadPX0p0Ce2ms2sC3sjhWEzWGy2OyBTEOQ2OECKiPYbSo3Euw3ed0ezzeLjuXx+UE8vn8QJwQRhUFUEBiyA8imA0P26wgm22f1ydKYxhwQA)

**Hooks personalizados**

Si estás retornando un _array_ en tu Hook personalizdo, querrás evitar la inferencia de tipo dado que Typescript inferirá un tipo de unión (cuando lo que realmente quieres son diferentes tipos en cada posición del _array_). En cambio, utiliza [aserciones const de TS 3.4](https://devblogs.microsoft.com/typescript/announcing-typescript-3-4/#const-assertions):

```tsx
export function useLoading() {
  const [isLoading, setState] = React.useState(false);
  const load = (aPromise: Promise<any>) => {
    setState(true);
    return aPromise.finally(() => setState(false));
  };
  return [isLoading, load] as const; // infiere [boolean, typeof load] en lugar de (boolean | typeof load)[]
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?target=5&jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCpAD0ljkwFcA7DYCZuRgZyQBkIKACbBmAcwAUASjgBvCnDhoO3eAG1g3AcNFiANHF4wAyjBQwkAXTgBeRMRgA6HklPmkEzCgA2vKQG4FJRV4b0EhWzgJFAAFHBBNJAAuODjcRIAeFGYATwA+GRs8uSDFIzcLCRgoRiQA0rgiGEYoTlj4xMdMUR9vHIlpW2Lys0qvXzr68kUAX0DpxqRm1rgNLXDdAzDhaxRuYOZVfzgAehO4UUwkKH21ACMICG9UZgMYHLAkCEw4baFrUSqVARb5RB5PF5wAA+cHen1BfykaksFBmQA)

De esta forma, cuando desestructuras realmente obtienes el tipo adecuado dependiendo de la posición de la desestructuración.

<details>
<summary><b>Alternativa: Aserción de un tipo de retorno de tupla</b></summary>

Si [tienes problemas con las aserciones const](https://github.com/babel/babel/issues/9800), también puedes hacer aserciones o definir los tipos de retorno de la función:

```tsx
export function useLoading() {
  const [isLoading, setState] = React.useState(false);
  const load = (aPromise: Promise<any>) => {
    setState(true);
    return aPromise.finally(() => setState(false));
  };
  return [isLoading, load] as [
    boolean,
    (aPromise: Promise<any>) => Promise<any>
  ];
}
```

Una función utilitaria que automáticamente asigne los tipos también puede ser de ayuda si escribes muchos Hooks personalizados:

```ts
function tuplify<T extends any[]>(...elements: T) {
  return elements;
}

function useArray() {
  const numberValue = useRef(3).current;
  const functionValue = useRef(() => {}).current;
  return [numberValue, functionValue]; // type is (number | (() => void))[]
}

function useTuple() {
  const numberValue = useRef(3).current;
  const functionValue = useRef(() => {}).current;
  return tuplify(numberValue, functionValue); // type is [number, () => void]
}
```

</details>

Nota, sin embargo, que el equipo de React recomienda que los Hooks personalizados que retornan más de dos valores deberían usar objetos reales en lugar de tuplas.

Lecturas adicionales sobre Hooks + Typescript:

- https://medium.com/@jrwebdev/react-hooks-in-typescript-88fce7001d0d
- https://fettblog.eu/typescript-react/hooks/#useref

Si estás escribiendo una biblioteca de Hooks de React, no olvides que deberías exponer tus tipos para que los usuarios los usen.

Ejemplos de bibliotecas con Hooks de React + Typescript

- https://github.com/mweststrate/use-st8
- https://github.com/palmerhq/the-platform
- https://github.com/sw-yx/hooks

[Algo que añadir? Abre un _issue_](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new).

## Componentes de clase

Dentro de Typescript, `React.Component` es un tipo genérico (alias `React.Component<PropType, StateType>`), por lo que quieres añadirle parámetros (opcionales) de prop y estado:

```tsx
type MyProps = {
  // usar `interface` también está bien
  message: string;
};
type MyState = {
  count: number; // así
};
class App extends React.Component<MyProps, MyState> {
  state: MyState = {
    // segunda anotación opcional para una mejor inferencia de tipos
    count: 0
  };
  render() {
    return (
      <div>
        {this.props.message} {this.state.count}
      </div>
    );
  }
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCmATzCTgFlqAFHMAZzgF44BvCuHAD0QuAFd2wAHYBzOAANpMJFEzok8uME4oANuwhwIAawFwQSduxQykALjjsYUaTIDcFAL4fyNOo2oAZRgUZW4+MzQIMSkYBykxEAAjFTdhUV1gY3oYAAttLx80XRQrOABBMDA4JAAPZSkAE05kdBgAOgBhXEgpJFiAHiZWCA4AGgDg0KQAPgjyQSdphyYpsJ5+BcF0ozAYYAgpPUckKKa4FCkpCBD9w7hMaDgUmGUoOD96aUwVfrQkMyCKIxOJwAAMZm8ZiITRUAAoAJTzbZwIgwMRQKRwOGA7YDRrAABuM1xKN4eW07TAbHY7QsVhsSE8fAptKWynawNinlJcAGQgJxNxCJ8gh55E8QA)

No olvides que puedes exportar/importar/extender estos tipos/interfaces para su reutilización.

<details>
<summary><b>¿Por qué anotar `state` dos veces?</b></summary>

No es estrictamente necesario antotar la propiedad de clase `state`, pero permite una mejor inferencia de tipos cuando se accede a `this.state` y también al inicializar el estado.

Esto ocurre porque funcionan de dos formas diferentes, el segundo parámetro del tipo genérico permitirá que `this.setState()` funcione correctamente, porque ese método viene de la clase base, pero al inicializar `state` dentro del componente sobreescribe la implementación base por lo que te tienes que asegurar de decirle al compilador que en realidad no estás haciendo nada distinto.

[Consulta el comentario de @ferdaber aquí](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/57).

</details>

<details>
  <summary><b>No hay necesidad de anotar con <code>readonly</code></b></summary>

A menudo ves código en ejemplos que incluyen `readonly` para marcar las props y el estado como inmutables:

```tsx
type MyProps = {
  readonly message: string;
};
type MyState = {
  readonly count: number;
};
```

Esto no es necesario, porque `React.Component<P,S>` ya los marca como inmutables. ([¡Consulta el PR y el debate!](https://github.com/DefinitelyTyped/DefinitelyTyped/pull/26813))

</details>

**Métodos de clase**: Hazlo como de costumbre, pero solo recuerda que cualquier argumento para tus funciones también debe tener tipos:

```tsx
class App extends React.Component<{ message: string }, { count: number }> {
  state = { count: 0 };
  render() {
    return (
      <div onClick={() => this.increment(1)}>
        {this.props.message} {this.state.count}
      </div>
    );
  }
  increment = (amt: number) => {
    // así
    this.setState(state => ({
      count: state.count + amt
    }));
  };
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCtAGxQGc64BBMMOJADxiQDsATRsnQwAdAGFckHrxgAeAN5wQSBigDmSAFxw6MKMB5q4AXwA0cRWggBXHjG09rIAEZIoJgHwWKcHTBTccAC8FnBWtvZwAAwmANw+cET8bgAUAJTe5L6+RDDWUDxwKQnZcLJ8wABucBA8YtTAaADWQfLpwV4wABbAdCIGaETKdikAjGnGHiWlFt29ImA4YH3KqhrGsz19ugFIIuF2xtO+sgD0FZVTWdlp8ddH1wNDMsFFKCCRji5uGUFe8tNTqc4A0mkg4HM6NNISI6EgYABlfzcFI7QJ-IoA66lA6RNF7XFwADUcHeMGmxjStwSxjuxiAA)

**Propiedades de clase**: Si necesitas declarar propiedades de clase para un uso posterior, simplemente declaralas como `state`, pero sin asignación:

```tsx
class App extends React.Component<{
  message: string;
}> {
  pointer: number; // así
  componentDidMount() {
    this.pointer = 3;
  }
  render() {
    return (
      <div>
        {this.props.message} and {this.pointer}
      </div>
    );
  }
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCtAGxQGc64BBMMOJADxiQDsATRsnQwAdAGFckHrxgAeAN4U4cEEgYoA5kgBccOjCjAeGgNwUAvgD44i8sshHuUXTwCuIAEZIoJuAHo-OGpgAGskOBgAC2A6JTg0SQhpHhgAEWA+AFkIVxSACgBKGzjlKJiRBxTvOABeOABmMzs4cziifm9C4ublIhhXKB44PJLlOFk+YAA3S1GxmzK6CpwwJdV1LXM4FH4F6KXKp1aesdk-SZnRgqblY-MgA)

[¿Algo que añadir? Abre un issue](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new).

## Tipos de defaultProps

Para Typescript 3.0+, la inferencia de tipos [debe funcionar](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html), sin embargo [algunos casos extremos aún son problemáticos](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/61). Simplemente asigna tus tipos como de costumbre, excepto que no uses `React.FC`.

```tsx
// ////////////////
// componentes de función
// ////////////////
type Props = { age: number } & typeof defaultProps;
const defaultProps = {
  who: "Johny Five"
};

const Greet = (props: Props) => {
  /*...*/
};
Greet.defaultProps = defaultProps;
```

Para los **componentes de clase**, hay [un par de formas de hacerlo](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/pull/103#issuecomment-481061483) (incluido el uso del tipo utilitario `Pick`) pero la recomendación es "revertir" la definición de las props:

```tsx
type GreetProps = typeof Greet.defaultProps & {
  age: number;
};

class Greet extends React.Component<GreetProps> {
  static defaultProps = {
    name: "world"
  };
  /*...*/
}

// ¡Hay chequeo de tipos! ¡No se requieren aserciones de tipo!
let el = <Greet age={3} />;
```

<details>
  <summary>¿Por qué React.FC interfiere con las defaultProps?</summary>

Puedes chequear los debates aquí:

- https://medium.com/@martin_hotell/10-typescript-pro-tips-patterns-with-or-without-react-5799488d6680
- https://github.com/DefinitelyTyped/DefinitelyTyped/issues/30695
- https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/87

Esto es solo el estado actual y podría ser solucionado en el futuro.

</details>

<details>
 <summary>Typescript 2.9 y versiones anteriores</summary>

Para Typescript 2.9 y versiones anteriores, hay más de una forma de hacerlo, pero el mejor consejo que hemos visto hasta ahora es:

```ts
type Props = Required<typeof MyComponent.defaultProps> & {
  /* additional props here */
};

export class MyComponent extends React.Component<Props> {
  static defaultProps = {
    foo: "foo"
  };
}
```

Nuestra recomendación anterior usaba la funcionalidad `Partial type` de Typescript, que significa que la interfaz actual cumplirá con una versión parcial de la interfaz envuelta. ¡De esa forma podemos extender defaultProps sin ningún cambio en los tipos!

```ts
interface IMyComponentProps {
  firstProp?: string;
  secondProp: IPerson[];
}

export class MyComponent extends React.Component<IMyComponentProps> {
  public static defaultProps: Partial<IMyComponentProps> = {
    firstProp: "default"
  };
}
```

El problema con este enfoque es que causa complejos problemas con la inferencia de tipos en conjunto con `JSX.LibraryManagedAttributes`. Básicamente ocasiona que el compilador piensa que cuando se crea una expresión JSX con ese componente, todas sus props son opcionales.

[Consulta el comentario de @ferdaber aquí](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/57).

</details>

[¿Algo que añadir? Abre un issue](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new).

## ¿Tipos o interfaces?

Las interfaces (`interface`) son diferentes de los tipos (`type`) en TypeScript, pero tienen usos muy similares en lo que concierne a los casos de usos comunes en React. Esta es una regla útil:

- siempre usa `interface` para las definiciones de API pública cuando se está escribiendo una biblioteca o las definiciones de tipos de ambiente de una biblioteca de terceros.

\_ considera usar `type` para las props y estado de tus componentes de React, porque tiene más restricciones.

Los tipos son útiles para los tipos de unión (p. ej. `type MyType = TypeA | TypeB`) mientras las interfaces son mejores para declarar formas de dicionario y luego `implementarlas` o `extenderlas`.

<details>
  <summary>
    <b>Tabla útil para tipos vs. interfaces</b>
  </summary>
Es un tema con muchos matices, no te preocupes demasiado por esto. He aquí un gráfico útil:

![https://pbs.twimg.com/media/DwV-oOsXcAIct2q.jpg](https://pbs.twimg.com/media/DwV-oOsXcAIct2q.jpg) (fuente: [Karol Majewski](https://twitter.com/karoljmajewski/status/1082413696075382785))

</details>

[¿Algo que añadir? Abre un issue](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new).

## Ejemplos básicos de Prop Types

```tsx
type AppProps = {
  message: string;
  count: number;
  disabled: boolean;
  /** ¡array de un tipo! */
  names: string[];
  /** literales de string que especifican valores exactos de string, con un tipo de unión que los une */
  status: "waiting" | "success";
  /** cualquier objeto siempre y cuando no utilices sus propiedades (noi es común) */
  obj: object;
  obj2: {}; // casi igual que `object`, exactamente los mismo que `Object`
  /** un objeto con propiedades definidas (preferido) */
  obj3: {
    id: string;
    title: string;
  };
  /** ¡array de objetos! (común) */
  objArr: {
    id: string;
    title: string;
  }[];
  /** cualquier función siempre y cuando no la invoques (no recomendado) */
  onSomething: Function;
  /** función que no toma ni devuelve nada (MUY COMÚN) */
  onClick: () => void;
  /** función con una prop nombrada (MUY COMÚN) */
  onChange: (id: number) => void;
  /** sintaxis alternativa de tipo función que toma un evento (MUY COMÚN) */
  onClick(event: React.MouseEvent<HTMLButtonElement>): void;
  /** una prop opcional (!MUY COMÚN!) */
  optional?: OptionalType;
};
```

Nota que hemos usado `/** commentarios */` con estilo TSDoc para cada prop. Puedes y te recomendamos dejar comentarios descriptivos en los componentes reutilizables. Para un ejemplo más completo y comentarios, consulta nuestra sección de [comentar componentes](/AVANZADO.md#componentes-comentados) en la guía avanzada.

## Ejemplos útiles de tipos de props en React

```tsx
export declare interface AppProps {
  children1: JSX.Element; // mal, no tiene en cuenta los arreglos
  children2: JSX.Element | JSX.Element[]; // más o menos, no acepta funciones
  children3: React.ReactChildren; // a pesar del nombre, no es para nada apropieado; es un utilitario
  children4: React.ReactChild[]; // mejor
  children: React.ReactNode; // el mejor, acepta todo
  functionChildren: (name: string) => React.ReactNode; // tipo recomendado para render prop del tipo función como hijo
  style?: React.CSSProperties; // para pasar props de estilo
  onChange?: React.FormEventHandler<HTMLInputElement>; // ¡Eventos de formulario! el parámetro genérico es el tipo de event.target
  props: Props & React.PropsWithoutRef<JSX.IntrinsicElements["button"]>; // para imitar todas las props de un elemento button sin su ref
}
```

<details>
 <summary><b>¿JSX.Element vs. React.ReactNode?</b></summary>

Citando a [@ferdaber](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/57): Una explicación más técnica consiste en que un nodo válido de React no es lo mismo que lo que retorna `React.createElement`. Sin importar el componente que se termina renderizando, `React.createElement` siempre retorna un objeto, que es la interfaz `JSX.Element`, pero `React.ReactNode` es el conjunto de todos los posibles valores de retorno de un componente.

- `JSX.Element` -> Valor de retorno de `React.createElement`
- `React.ReactNode` -> Valor de retorno de un componente
  </details>

[Más discusiones: Where ReactNode does not overlap with JSX.Element](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/129)

[¿Algo que añadir? Abre un issue](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new).

## getDerivedStateFromProps

Antes de que comiences a usar `getDerivedStateFromProps`, por favor consulta la [documentación](https://es.reactjs.org/docs/react-component.html#static-getderivedstatefromprops) y [Probablemente no necestas estado derivado](https://es.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html). El estado derivado puede conseguirse facilmente utilizando Hooks, los que también pueden ayudar a configurar fácilmente la memoización.

Aquí hay algunas formas en las que puedes anotar `getDerivedStateFromProps`

1. Si has establecido explícitamente los tipos de tu estado derivado y quieres asegurarte de que el valor de retorno de `getDerivedStateFromProps` lo cumple.

```tsx
class Comp extends React.Component<Props, State> {
  static getDerivedStateFromProps(
    props: Props,
    state: State
  ): Partial<State> | null {
    //
  }
}
```

2. Cuando quieres que el valor de retorno de la función determine tu estado.

```tsx
class Comp extends React.Component<
  Props,
  ReturnType<typeof Comp["getDerivedStateFromProps"]>
> {
  static getDerivedStateFromProps(props: Props) {}
}
```

3. Cuando quieres estado derivado con otros campos de estado y memoización

```tsx
type CustomValue = any;
interface Props {
  propA: CustomValue;
}
interface DefinedState {
  otherStateField: string;
}
type State = DefinedState & ReturnType<typeof transformPropsToState>;
function transformPropsToState(props: Props) {
  return {
    savedPropA: props.propA, // guardar para memoización
    derivedState: props.propA
  };
}
class Comp extends React.PureComponent<Props, State> {
  constructor(props: Props) {
    super(props);
    this.state = {
      otherStateField: "123",
      ...transformPropsToState(props)
    };
  }
  static getDerivedStateFromProps(props: Props, state: State) {
    if (isEqual(props.propA, state.savedPropA)) return null;
    return transformPropsToState(props);
  }
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoUSWOYAZwFEBHAVxQBs5tcD2IATFHQAWAOnpJWHMuQowAnmCRwAwizoxcANQ4tlAXjgoAdvIDcFYMZhIomdMoAKOMHTgBvCnDhgXAQQAuVXVNEB12PQtyAF9La1t7NGUAESRMKyR+AGUYFBsPLzgIGGFbHLykADFgJHZ+II0oKwBzKNjyBSU4cvzDVPTjTJ7lADJEJBgWKGMAFUUkAB5OpAhMOBgoEzpMaBBnCFcZiGGAPijMFmMMYAhjdc3jbd39w+PcmwAKXwO6IJe6ACUBXI3iIk2mwO83joKAAbpkXoEfC46KJvmA-AAaOAAehxcBh8K40DgICQIAgwAAXnkbsZCt5+LZgPDsu8kEF0aj0X5CtE2hQ0OwhG4VLgwHAkAAPGzGfhuZDoGCiRxTJBi8C3JDWBb-bGnSFwNC3RosDDQL4ov4ooGeEFQugsJRQS0-AFRKHrYT0UQaCpwQx2z3eYqlKDDaq1epwABEAEYAEwAZhjmIZUNEmY2Wx2UD2KKOw1drgB6f5fMKfpgwDQcGaE1STVZEZw+Z+xd+cD1BPZQWGtvTwDWH3ozDY7A7aP82KrSF9cIR-gBQLBUzuxhY7HYHqhq4h2ceubbryLXPdFZiQA)

## Formularios y Eventos

Si el rendimiento no es un problema, tener los manejadores de eventos en línea es la forma más fácil dado que simplemente puedes usar [la inferencia de tipos y el tipado contextual](https://www.typescriptlang.org/docs/handbook/type-inference.html#contextual-typing):

```tsx
const el = (
  <button
    onClick={event => {
      /* ... */
    }}
  />
);
```

Pero si necesitas definir tus manejadores de eventos de forma separada, las herramientas del IDE pueden ser útiles en este caso, dado que las definiciones de @type vienen con muchos tipos. Escribe lo que estás buscando y usualmente el autocompletamiento te ayudará. Aquí se muestra el caso de `onChange` para un evento de formulario:

```tsx
class App extends React.Component<
  {},
  {
    // sin props
    text: string;
  }
> {
  state = {
    text: ""
  };

  // anotar el tipo en la parte DERECHA de =
  onChange = (e: React.FormEvent<HTMLInputElement>): void => {
    this.setState({ text: e.currentTarget.value });
  };
  render() {
    return (
      <div>
        <input type="text" value={this.state.text} onChange={this.onChange} />
      </div>
    );
  }
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCtAGxQGc64BBMMOJADxiQDsATRsnQwAdAGFckHrxgAeCnDgBvAL4AaBcs2KA9Drg8IcMDjB1tcblwBccOjCjAeAcwDcmlRQB8W8ovso3HAAvL6KilYwtgBE0R7ulH5wepYAnmBOznAQPIgAkgDiABIAKnAAFij8dsB8SNmYIZo5YpUu9aEAFEi2QhgiAGLQIACiAG4ysqUAsgAyeTxgAK4wI9RIIDJeAJS2YxC1IT5KFjDlwHQidEgwAMowgUidSpacUewiaEtQRDwwJSgoM4biIxihqEt6iptglFCpYXBfnUoJ1tmFwkQYN9cp0LIpZHxgGMvHjwrInMt4DB0khgtFItE4GCIbSlGcLlcHtwRJEVNkeK0qsDgmzzpcWm1gXydCSkuE4LIdITiRYYR4KCogA)

En lugar de anotar los tipos de los argumentos y los valore de retorno con `React.FormEvent<>` y `void`, alternativamente puedes aplicar los tipos al manejador de eventos mismo (_contribución de @TomasHubelbauer_):

```tsx
  // anotar el tipo en la parte IZQUIERDA de =
  onChange: React.ChangeEventHandler<HTMLInputElement> = (e) => {
    this.setState({text: e.currentTarget.value})
  }
```

<details>

<summary><b>¿Por qué dos formas de hacer lo mismo?</b></summary>

El primer método utiliza una firma inferida para el método `(e: React.FormEvent<HTMLInputElement>): void` y la segunda fuerza un tipo del delegado proporcioanado por `@types/react`. O sea que `React.ChangeEventHandler<>` es simplemente un tipo "bendecido" por `@types/react`, mientras puedes ver el método inferido como más... _hecho artesanalmente_. De cualquier forma es un buen patrón a conocer. [Mira nuestro PR de Github PR para más información](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/pull/24).

</details>

**Tipado de onSubmit, con componentes no controlados en un formulario**

Si no te importa mucho el tipo del evento, simplemente puedes utilizar React.SyntheticEvent. Si tu formulario objetivo tiene _inputs_ con nombres personalizados a los que quisieras acceder, puedes utilizar la extensión de tipos:

```tsx
<form
  ref={formRef}
  onSubmit={(e: React.SyntheticEvent) => {
    e.preventDefault();
    const target = e.target as typeof e.target & {
      email: { value: string };
      password: { value: string };
    };
    const email = target.email.value; // typechecks!
    const password = target.password.value; // typechecks!
    // etc...
  }}
>
  <div>
    <label>
      Email:
      <input type="email" name="email" />
    </label>
  </div>
  <div>
    <label>
      Password:
      <input type="password" name="password" />
    </label>
  </div>
  <div>
    <input type="submit" value="Log in" />
  </div>
</form>
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCtCAOwGctoRlM4BeRYmAOgFc6kLABQBKClVoM4AMSbs4o9gD4FFOHAA8mJmrhFMbAN7aozJJgC+u2gGVeAIxDAYRoUgBcndDxsBPGjAAFkgwwGgAogBuSAEiynCGuupI3GBE0QEAIuYovAA2MKIA3Elw1PTwMChQAOYh8ilVtfUodHAwvmBIEKyN1XXwAGQJpckgKMB5noZwkSh5vB5wDFDANDVwFiXk6rtwYK10AO7QACbTs-OLnitrG1ulDzu75VJI45PyTQPc7xN53DmCyQRTgAHowe1Okg0ME0ABrOgAQlKr3gBzoxzOX36IVShxOUFOgKuIPBkI6XVhMMRKOe6ghcBCaG4rN0Fis5CUug0p2AkW59M0eRQ9iQeUFe3U4Q+U1GmjWYF4lWhbAARH9Jmq4DQUCAkOrNXltWDJbsNGCRWKJTywXyBTz7Wb1BoreLnbsAAoEs7ueUaRXKqFddUYrFE7W6-Whn0R8Eei1um3PC1Ox38hOBlUhtV0BxOGDaoGLdUAGQgGzWJrNqYzFAtJhAgpEQA)

Por supuesto, si estás construyendo algún tipo de formulario de consideración, [deberías usar Formik](https://jaredpalmer.com/formik), que está escrito en TypeScript.

## Contexto

Usar `React.createContext` y [getters de contexto](https://kentcdodds.com/blog/application-state-management-with-react/) para hacer un `createCtx` **sin `defaultValue`, pero sin tener que chequear por `undefined`**:

```tsx
// Crea un contexto sin un valor por defecto inicial
// sin tener que hacer chequeos de undefined todo el tiempo
function createCtx<A>() {
  const ctx = React.createContext<A | undefined>(undefined);
  function useCtx() {
    const c = React.useContext(ctx);
    if (!c) throw new Error("useCtx must be inside a Provider with a value");
    return c;
  }
  return [useCtx, ctx.Provider] as const; // haz que TypeScript infiera una tupla, no un arreglo de tipos de unión
}

// uso

export const [useCtx, SettingProvider] = createCtx<string>(); // Se especifica el tipo, ¡pero sin necesidad de especificar el valor de antemano!
export function App() {
  const key = useCustomHook("key"); // Se obtiene un valor de un hook, debe estar en un componente
  return (
    <SettingProvider value={key}>
      <Component />
    </SettingProvider>
  );
}
export function Component() {
  const key = useCtx(); // ¡Aún se puede usar sin chequeos de null!
  return <div>{key}</div>;
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCtCAOwGd4BXOpAYWZlwAkIIBrOAF44ACj5IAngC44DKMBoBzAJRCAfHADeFOHGr14AbQYoYSADSykMAMoxTSALpDExGADpmSOw5GaAvso6cEQwjFA0svZmhuISjhT+FAD0yXpEDnq0ZgAe8ADuwDAAFnA0EHCMYNjZcAAmSJgojAA2MABqKC2MSClphSUQjPDFKABuCopwnPUVjDQNmApIdXrFSGgCXS3T69OgveSY8xjAtOmoZqwwOQA8AIJqIqra5Lr6DHo3LsjoHmgZK7ZJB5B5wAA+lQWjWWdSe80WsOUAG5gscaKdzl5rjlnlpgu9aJ80D83J4WKxgXkRBgciiCXBgJhRABCNCqEo4fJlJDcgCiUBwUBEACJsd8QBw4AAjJCM+jABpwFBwAAKOAmDSgcAGpRVYy6PRF9LeuhC1nCkTQqNNSVNoUtcEM4pyllp7nVEE1SCgzhQdCyBmRcFScBAKHEcAAKhIwN4AcAwPAFJgfcrplUWhYyhB4ChIihBSgJHAIMz5mdIjBY0g6IkKH1KnQUIpDhQQZBYIHPs6KTdLDZrDBJp7vb6XADLmwbrc5JMniiQ2k6HG0EyS9W45ZpcMczyVtMKiuNuu4AbunKqjUaDAWe2cp2sCdh+d7mAwHjXoSDHA4i5sRw3C8HwopxMawahq2eZnoaco1HgKrFMBliSp8sryum1DgLQSA3sEDoRKIDK3IOMDDkoo6Kmm549IImhxP4agMrotyUthNC4fAyRMaaLHJKR5GKJRWo8boJp2h20BPhiL6RGxkAcTen7BB88B-sILrPBBaRoPmUTAC0OxeDqRRIbuNCtDsaDrJsd72hahG3HUwBjGo9GSP4tzJM5rk2v4QA)

Usando `React.createContext` y `useContext` para hacer un `createCtx` con _setters_ de contexto al estilo [`unstated`](https://github.com/jamiebuilds/unstated):

```tsx
export function createCtx<A>(defaultValue: A) {
  type UpdateType = React.Dispatch<React.SetStateAction<typeof defaultValue>>;
  const defaultUpdate: UpdateType = () => defaultValue;
  const ctx = React.createContext({
    state: defaultValue,
    update: defaultUpdate
  });
  function Provider(props: React.PropsWithChildren<{}>) {
    const [state, update] = React.useState(defaultValue);
    return <ctx.Provider value={{ state, update }} {...props} />;
  }
  return [ctx, Provider] as const; // alternativamente, [typeof ctx, typeof Provider]
}

// uso

const [ctx, TextProvider] = createCtx("someText");
export const TextContext = ctx;
export function App() {
  return (
    <TextProvider>
      <Component />
    </TextProvider>
  );
}
export function Component() {
  const { state, update } = React.useContext(TextContext);
  return (
    <label>
      {state}
      <input type="text" onChange={e => update(e.target.value)} />
    </label>
  );
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCpAD0ljkwFcA7DYCZuNIlGJAYRjUAPAEEAfAAoAJkkwpGAGxgA1FIsZIAXHFEBKOAG8KcODACeYJHACqYabyQAVS9YC8iYjAB0AEWAAzmC8aAAWwsjoPgDKSDDRMI6ibBzCFlYQmHCy8kqq6pri4gDcJlwcAfA5Csp2Dnw6dY4uVnAekgZu4tlyNfkaSKXkpmgV8BjUbZ5R3tyofPwcfNQwksbDpnCVjjrVeWoDADRlpoz2Oz25ted8ZQC+ekOmTKww7JwACjgAbsCyUJIwDgwAEdJEMN4vhAQQB1YAwUL8ULARTSIjMYSGO7iAzrTblZiVOAAbW2fEOcDO9SQAF0puCfIwAkgEo4ZL19gUkI8TnAiDBGFBOMIJpCfn8kFA4N8uW5DIYtolyZSbtY7ncjN4tUDoQENQB6Er3Mr8wWcYkTClQ37-OkoAIEyrFOD6-VwdR8IW8YDfJCKcwU4npJCZLhCCnB0PWiVQGkUO4UCiuykBFAAcyQifIo0J8At4bgThoMGjtqmc0cgmokgARAFcM5izWeeQaHRxmNC8XFsxlvAPBMhm3oFgWClOKIwGAOkYTXEzXBJLzhEWVqXJeJeaZhItwBwkL2XZuNtv9auS+L-sfTC2E63aCOGGO3hw4LvIMwD6tcWUc0SFWSSAUlSjhwBqHgMt4TICEsxaSOePZ9i2pimkKi7LooKAAEZ+te+JGIBd74XAwjAMwYCMPAwZuDWfY1nAHBIigzAZnK7jdCBfCSEg3iJFAGY+DKAx6AaeGnphOGKHht5AA)

Un [versión basada en useReducer](https://gist.github.com/sw-yx/f18fe6dd4c43fddb3a4971e80114a052) también puede resultar útil.

<details>

<summary><b>Contexto mutable usando un envoltorio de componente de clase</b></summary>

_Contribuido por: [@jpavon](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/pull/13)_

```tsx
interface ProviderState {
  themeColor: string;
}

interface UpdateStateArg {
  key: keyof ProviderState;
  value: string;
}

interface ProviderStore {
  state: ProviderState;
  update: (arg: UpdateStateArg) => void;
}

const Context = React.createContext({} as ProviderStore); // type assertion on empty object

class Provider extends React.Component<{}, ProviderState> {
  public readonly state = {
    themeColor: "red"
  };

  private update = ({ key, value }: UpdateStateArg) => {
    this.setState({ [key]: value });
  };

  public render() {
    const store: ProviderStore = {
      state: this.state,
      update: this.update
    };

    return (
      <Context.Provider value={store}>{this.props.children}</Context.Provider>
    );
  }
}

const Consumer = Context.Consumer;
```

</details>

[¿Algo que añadir? Abre un issue](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new).

## forwardRef/createRef

Consulta la sección de [Hooks](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/blob/master/README.md#hooks) para `useRef`.

`createRef`:

```tsx
class CssThemeProvider extends React.PureComponent<Props> {
  private rootRef = React.createRef<HTMLDivElement>(); // así
  render() {
    return <div ref={this.rootRef}>{this.props.children}</div>;
  }
}
```

`forwardRef`:

```tsx
type Props = { children: React.ReactNode; type: "submit" | "button" };
export type Ref = HTMLButtonElement;
export const FancyButton = React.forwardRef<Ref, Props>((props, ref) => (
  <button ref={ref} className="MyClassName" type={props.type}>
    {props.children}
  </button>
));
```

Si estás obteniendo las props de un componente que pasa las refs, usa [`ComponentPropsWithRef`](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/a05cc538a42243c632f054e42eab483ebf1560ab/types/react/index.d.ts#L770).

Más información: https://medium.com/@martin_hotell/react-refs-with-typescript-a32d56c4d315

También puede que quieras hacer [Renderizado condicional con `forwardRef`](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/167).

[¿Algo que añadir? Abre un issue](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new).

## Portales

Uso de `ReactDOM.createPortal`:

```tsx
const modalRoot = document.getElementById("modal-root") as HTMLElement;
// asumiento que tu archivo html tiene un div con id 'modal-root';

export class Modal extends React.Component {
  el: HTMLElement = document.createElement("div");

  componentDidMount() {
    modalRoot.appendChild(this.el);
  }

  componentWillUnmount() {
    modalRoot.removeChild(this.el);
  }

  render() {
    return ReactDOM.createPortal(this.props.children, this.el);
  }
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoUSWRYmAEQHkBZObXAo9GAWgBNcZchTQQAdgGd4ICHxQAbBBAjwAvHAFoAriCRiYAOgDmSGAFF5SXfoBCATwCSfABQAiGXPk8cK1wEo4FAk4AAkAFWYAGQsrPRgAbgoAeiTAiQkdYDEjOCy4OwgtKDgACxgQeTZgS1KgwI1gADc4AHdgGBLcvgIPBW9lGHxE4XIkAA9qeDR5IODmWQU4cZg9PmDkbgMAYVxIMTi4AG8KOCX5AC5QiOjLazUNCG07gzQuFZi7tz4m-2GTuFE4HEcXowD48y0+mcAWO5FOp16igGBhQYDAqy2JWqLg6wAkBiQ8j8w1OAF8KP9AXs4gB1aryACqYhkkJg0KO-wRCyRKgMRBkjSQmOxzlx+MJxP+5JGpyIYj4SCg7Nh8LgRBgRTEtG4TGYLzeSAACtAYApRVj8WAcGB8WgsfI+HKADRwMUEokkuDS0lAA)

<details>

<summary><b>Contexto del ejemplo</b></summary>

Este ejemplo está basado en el ejemplo [Event Bubbling Through Portal](https://es.reactjs.org/docs/portals.html#event-bubbling-through-portals) de la documentación de React.

</details>

## Barreras de error

_No escrito aún._

[¿Algo que añadir? Abre un issue](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new).

## Concurrent React/React Suspense

_No escrito aún._ observa <https://github.com/sw-yx/fresh-async-react> para más sobre React Suspense y Time Slicing.

[¿Algo que añadir? Abre un issue](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new).

# Manual básico de resolución de problemas: Tipos

> ⚠️ ¿Has leído la [página de preguntas frecuentes de TypeScript](https://github.com/microsoft/TypeScript/wiki/FAQ)?) !Tu respuesta podría estar allí!

¿Te encuentras ante extraños errores de tipo? No estás solo. Esta es la parte más difícil de usar TypeScript con React. Sé paciente (después de todo estás aprendiendo un nuevo lenguaje). Sin embargo, mientras mejor te vuelvas en esto, ¡menos tiempo estarás trabajando _en contra_ del compilador y más tiempo estará el compilador trabajando _para_ ti!

Intenta evitar asignar el tipo `any` tanto como te sea posible para experimentar los máximos beneficios de TypeScript. En cambio, intentemos familiarizarnos con algunas estrategias comunes para resolver esos problemas.

## Tipos de unión y seguro de tipo

Los tipos de unión son útiles para resolver algunos de estos problemas con el tipado:

```tsx
class App extends React.Component<
  {},
  {
    count: number | null; // así
  }
> {
  state = {
    count: null
  };
  render() {
    return <div onClick={() => this.increment(1)}>{this.state.count}</div>;
  }
  increment = (amt: number) => {
    this.setState(state => ({
      count: (state.count || 0) + amt
    }));
  };
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCtAGxQGc64BBMMOJADxiQDsATRsnQwAdAGFckHrxgAeCnDgBvAL4AaBcs2K0EAK48YALjg89IAEZIocAD6m91agG44AejdxqwANZI4MAAWwHSaKhQAfFrkinQwKNxwALzRijr6hiZmTmHOmkT81gAUAJSpaUQwelA8cLJ8wABucBA8Yt5oPklKpclRQSEiwDxoRCAyRQCMJSoRSgN0InEJSCK6BjAqsm4NjRF5MXDhh8OjSOOGyXBFKCDGDpbWZUlRStoBwYt0SDAAyvHcIrLRIva5vQ5pODrTLXYGraHwWz2AAMZQA1HBbjB3ioSiUDooVAcVEA)

**Seguro de tipo**: A veces los tipos de unión resuelven el problema en un área, pero crean otro debajo en la cadena. Si `A` y `B` son ambos tipos de objeto, `A | B` no es "o bien A o bien B", es "A o B (o ambos)", lo que causa alguna confusión si esperabas que fuera lo primero. Aprende como escribir chequeos, seguros, y aserciones (también consulta la sección de renderizado condicional debajo). Por ejemplo:

```ts
interface Admin {
  role: string;
}
interface User {
  email: string;
}

// Método 1: usar la palabra clave `in`
function redirect(user: Admin | User) {
  if ("role" in user) {
    // Usa el operador `in` para seguros de tipo desde TS 2.7+
    routeToAdminPage(user.role);
  } else {
    routeToHomePage(user.email);
  }
}

// Método 2: Seguro de tipo personalizado, hace lo mismo en versiones anteriores de TS o donde `in` no es suficiente
function isAdmin(user: Admin | User): user is Admin {
  return (user as any).role !== undefined;
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoC4AOxiSk3STgEEATEGuAbwrjhwAbJAC44AZxhQaAcwDcFAL5Va9RmmYBVcfR584SECmCCxk6dXlKKFTAFdqGYBGoCIdugBUI7TtQAKKDJIABTiwDLUwJjA9ACUeuT80XBhEVExugC8OQR2OlAIEML4CbxJ-AJIMHZQrvi+NGQVinDWlOT2jjDOrjgeSN4AErhIgcFpkdGxUGX6KZMZM3A5WQSGxoKliZVVNXUEIyBIYEFIzfzK5FcUAPS3cACy1QAWEGxwAIxi+cwABjQ-nAANZIACeAHdoGxbA4nC4qmxgEQMCFflAxI1XAAfODaeI7ODREIAIiESBJRNc6LKcHucF+cBgL3+gLgEDA9BQMGgcEwvJgYM5MjsKCgbHEEhoGjgngAynAAEwAOgA7ABqfT8fpeHwcGjjULo5XkuIKFoGQQ6Qna9y6o5jM5ogrKjYmM36K43cj057M95KsRofI8vCCzlwEVitgAGjgbAgSElzOY4hQxyZL1kVPZgjYunlcAAbvRwi5JbyISyiHAAdQgcBxLQDNR3DIXrDur0ieIsc76Jj9Ti8QU4j8Cj3WEPCUR9q5+1A4ChJShqGC4ibiswAIS5Bz5mLUJAw65AA)

El método 2 también se conoce como [Seguros de tipo definidos por el usuario](https://www.typescriptlang.org/docs/handbook/advanced-types.html#user-defined-type-guards) y puede ser muy útil para obtener un código legible. Así es como TS mismo refina tipos con `typeof` e `instanceof`.

Si necesitas, en cambio, cadenas de `if...else` o la sentencia `switch`, debería "simplemente funcionar", pero busca [Uniones discriminadas](https://www.typescriptlang.org/docs/handbook/advanced-types.html) si necesitas ayuda. (Ve también: [El escrito de Basarat](https://basarat.gitbooks.io/typescript/docs/types/discriminated-unions.html)). Es útil para asignar tipos en `useReducer` o Redux.

## Tipos opcionales

Si un componente tiene una prop opcional, añade un signo de interrogación y asigna durante las desestructuración (o usa defaultProps).

```tsx
class MyComponent extends React.Component<{
  message?: string; // así
}> {
  render() {
    const { message = "default" } = this.props;
    return <div>{message}</div>;
  }
}
```

También puedes usar un carácter `!` para asegurar que algo no es undefined, pero no se recomienda.

_Something to add? [File an issue](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new) with your suggestions!_

## Tipos Enum

Las Enums en TypeScript se convierten por defecto a números. Usualmente querrás usarlas en cambio como _strings_:

```tsx
export enum ButtonSizes {
  default = "default",
  small = "small",
  large = "large"
}
```

Uso:

```tsx
export const PrimaryButton = (
  props: Props & React.HTMLProps<HTMLButtonElement>
) => <Button size={ButtonSizes.default} {...props} />;
```

Una alternativa más simple a los enum es simplemente declarar _strings_ como una unión:

```tsx
export declare type Position = "left" | "right" | "top" | "bottom";
```

Esto es útil, porque TypeScript lanzará errores cuando escribas mal un _string_ para tus props.

## Aserción de tipo

En ocasiones que TypeScript no tiene la razón y que el tipo que estás usando es más restringido que lo que cree, o que los tipos de unión necesitan una aserción con un tipo más especifico para trabajar con otras APIs, para ello hazlo con la palabra clave `as`. Esto le dice al razón que tienes la razón.

```tsx
class MyComponent extends React.Component<{
  message: string;
}> {
  render() {
    const { message } = this.props;
    return (
      <Component2 message={message as SpecialMessageType}>{message}</Component2>
    );
  }
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCmATzCTgGU61gUAbAWSQGduUBzJABVa9ALwFuMKMAB2-fAG4KFOTCRRM6egAUcYbnADeFOHBA8+ggFxwpM+XAA+cAK6yAJkkxykH5eQAvirkaBCyUnAAwriQskiyMABMtsjoMAB0AGJRADx6EAYAfHASABRG5pYCSIEAlKUlZaZwuR7AAG5FLWa5ABYAjEVGFrw1gbkA9IPd5L2T7V0UdSFobCi8cBzUMeDhCfBIAB7qnoZpGBm7cQe5JnNVYzZ20nL8AYEl92ZEnhplDW+ZjgYQi8Eqoys9ECpTgMD6wG4GTA+m4AWBcCIMFcUFkcGaDwxuWu+0SSUeULEI2qgjgG0YzFYnBpwlEn2pT1qUxJ8TJswxdXRcGCQSAA)

Nota que no puedes hacer aserciones a tu forma a cualquier cosa (básicamente es solo para refinar tipos). Por tanto no es lo mismo que hacer "casting" a un tipo.

También puedes hacer una aserción de que una propiedad no es null al acceder a ella:

```ts
element.parentNode!.removeChild(element) // ! antes del punto
myFunction(document.getElementById(dialog.id!)! // ! después de acceder a la propiedad
let userID!: string // aserción de asignación definitiva... ten cuidado!
```

Por supuesto, intenta realmente manejar el caso null en lugar de hacer la aserción. :)

## Simulación de tipos nominales

El tipado estructural de TS es útil, hasta que es inconveniente. Sin embargo puedes simular el tipado nominal usando [`marca de tipo`](https://basarat.gitbooks.io/typescript/docs/tips/nominalTyping.html):

```ts
type OrderID = string & { readonly brand: unique symbol };
type UserID = string & { readonly brand: unique symbol };
type ID = OrderID | UserID;
```

Podemos crear estos valores con el patrón de objeto acompañante:

```ts
function OrderID(id: string) {
  return id as OrderID;
}
function UserID(id: string) {
  return id as UserID;
}
```

Ahora TypeScript no permitirá que uses el ID incorrecto en un lugar determinado:

```ts
function queryForUser(id: UserID) {
  // ...
}
queryForUser(OrderID("foobar")); // Error, Argument of type 'OrderID' is not assignable to parameter of type 'UserID'
```

En el futuro podrás uar la palabra clave `unique` para marcar el tipo. [Consulta este PR](https://github.com/microsoft/TypeScript/pull/33038).

## Tipos de intersección

Añadir dos tipos juntos puede ser útil, por ejemplo cuando se supone que tu componente refleje las props de un componente nativo como `button`:

```tsx
export interface Props {
  label: string;
}
export const PrimaryButton = (
  props: Props & React.HTMLProps<HTMLButtonElement> // se añaden mis Props junto con las props de button provistas por @types/react
) => <Button {...props} />;
```

También puedes usar tipos de intersección para hacer subconjuntos reutilizables de props para componentes similares:

```tsx
type BaseProps = {
   className?: string,
   style?: React.CSSProperties
   name: string // used in both
}
type DogProps = {
  tailsCount: number
}
type HumanProps = {
  handsCount: number
}
export const Human: React.FC<BaseProps & HumanProps> = // ...
export const Dog: React.FC<BaseProps & DogProps> = // ...
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCmATzCTgCEUBnJABRzGbgF44BvCnGFoANi2YA5FCCQB+AFxxmMKMAB2AcwA0Q4Suqj5S5OhgA6AMIBlaxwh1YwJMz1x1MpEpVqtcAPT+cACurAAmcBpwAEYQMAAWFAC+VLT0ACIQmvZcvAJ6MCjAosyWEMHqMErqwSDRSFDJqXRwABK1KOo53HyC5MLxnWGl5ZXVtfWN5CnkSAAekLBwaBDqKm0d6ibEFgBilgA8TKzdcABkGyCd3QB8eQAUAJS8d-d6B2HAAG4BNxSPFAo80W8BWa3gmU02zM5n2RxY7E43AukNuD2ePFe70+P38f3IjyAA)

Asegúrate de no confundir los tipos de intersección (que son operaciones **y**) con los tipos de unión (que son operaciones **o**).

## Tipos de unión

Esta sección aún no se ha escrito. (¡Por favor contribuye!). Mientras tanto, consulta nuestro [comentario sobre los casos de uso de los tipos de unión](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/blob/master/README.md#union-types-and-type-guarding).

La cheatsheet AVANZADA también tiene información sobre los tipos discriminados de unión, que son útiles cuando TypeScript no parece estar reduciendo tu tipo de unión como esperas.

## Sobrecarga de tipos de función

Específicamente en lo concerniente a las funciones, puede que necesites sobreescribir en lugar de hacer una unión de tipos. La forma más común en que se escriben los tipos de función es la forma abreviada:

```ts
type FunctionType1 = (x: string, y: number) => number;
```

Pero esto no te permite hacer niguna sobrecarga. Si tienes la implementación, puedes poner los tipos detrás de cada elemento con la palabra clave `function`:

```ts
function pickCard(x: { suit: string; card: number }[]): number;
function pickCard(x: number): { suit: string; card: number };
function pickCard(x): any {
  // implementation with combined signature
  // ...
}
```

Sin embargo, si no tienes ninguna implementación y solo estás escribiendo un archivo de definición `d.ts`, esto tampoco ayudará. En este caso puedes renunciar a las formas abreviadas y escribirlo a la antigua. La clave es recordar que en lo que concierne a TypeScript, `las funciones son solo objetos invocables sin llaves`:

```ts
type pickCard = {
  (x: { suit: string; card: number }[]): number;
  (x: number): { suit: string; card: number };
  // no hay necesidad de una firma combinada en esta forma
  // también puedes añadir tipos a las propiedades estáticas de funciones aquí ej. `pickCard.wasCalled`
};
```

Nota que cuando implementes la función sobrecargada en sí, la implementación necesitará declarar la firma combinada de la llamada que estás manejando, no lo inferirá por ti. Puedes ver ejemplos fácilmente de sobrecargas en las APIs del DOM, p. ej. `createElement`.

[Lee más sobre la sobrecarga en el manual.](https://www.typescriptlang.org/docs/handbook/functions.html#overloads)

## Uso de tipos inferidos

Apoyarse en la inferencia de tipos de TypeScript es genial... hasta que te das cuenta de que necesiotas un tipo que fue inferido, y tienes que volver y declarar explícitamente los tipos o interfaces y así puedas exportarlos para su reutilización.

Afortunadamente, con `typeof`, no tienes que hacerlo. Simplemente úsalo sobre cualquier valor:

```tsx
const [state, setState] = React.useState({
  foo: 1,
  bar: 2
}); // el tipo state se infirió como {foo: number, bar: number}

const someMethod = (obj: typeof state) => {
  // obteniendo el tipo del estado aún cuando fue inferido
  // algún código usando obj
  setState(obj); // funciona
};
```

## Uso de tipos parciales

Trabajar con porciones del estado o las props es común en React. Nuevamente, no necesitas realmente ir y redefinir explícitamente tus tipos si utilizas el tipo genérico `Partial`:

```tsx
const [state, setState] = React.useState({
  foo: 1,
  bar: 2
}); // el tipo inferido de state es {foo: number, bar: number}

// NOTA: La mezcla de estado anterior en realidad no se recomienda con React.useState
// aquí solo estamos demostrando como usar Partial
const partialStateUpdate = (obj: Partial<typeof state>) =>
  setState({ ...state, ...obj });

// luego...
partialStateUpdate({ foo: 2 }); // funciona
```

<details>
  <summary>
    Advertencias menores al usar <code>Partial</code>
  </summary>

Nota que hay algunos usuarios de TS que no están de acuerdo con usar `Partial` como se comporta hoy. Mira [sútiles problemas del ejemplo anterior aquí](https://twitter.com/ferdaber/status/1084798596027957248), y consulta este largo debate sobre [por qué @types/react usa Pick en lugar de Partial](https://github.com/DefinitelyTyped/DefinitelyTyped/issues/18365).

</details>

## ¡Los tipos que necesito no fueron exportados!

Esto puede ser molesto, ¡pero hay forma de obtener los tipos!

- Obtener los tipos de las props de un componente: `React.ComponentProps` y `typeof`, y opcionalemente `Omit` para omitir cualquier tipo solapado.

```tsx
import { Button } from "library"; // ¡Pero no exporta ButtonProps! ¡Ay, no!
type ButtonProps = React.ComponentProps<typeof Button>; // !No hay problema! ¡Obtén el tuyo propio!
type AlertButtonProps = Omit<ButtonProps, "onClick">; // modifícalo
const AlertButton: React.FC<AlertButtonProps> = props => (
  <Button onClick={() => alert("hello")} {...props} />
);
```

También puedes usar [`ComponentPropsWithoutRef`](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/a05cc538a42243c632f054e42eab483ebf1560ab/types/react/index.d.ts#L774) (en lugar de ComponentProps) y [`ComponentPropsWithRef`](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/a05cc538a42243c632f054e42eab483ebf1560ab/types/react/index.d.ts#L770) (si tu componente específicamente pasa las refs)

- Obtener el tipo de retorno de una función: utiliza `ReturnType`:

```tsx
// dentro de alguna biblioteca - el tipo de retorno { baz: number } se infiere, pero no se exporta
function foo(bar: string) {
  return { baz: 1 };
}

//  dentro de tu aplicación, si necesitas { baz: number }
type FooReturn = ReturnType<typeof foo>; // { baz: number }
```

De hecho, puedes obtener virtualmente cualquier cosa que sea pública: [mira esta publicación de Ivan Koshelev](http://ikoshelev.azurewebsites.net/search/id/11/Pragmatic-uses-of-TypeScript-type-system-My-type-of-type)

```ts
function foo() {
  return {
    a: 1,
    b: 2,
    subInstArr: [
      {
        c: 3,
        d: 4
      }
    ]
  };
}

type InstType = ReturnType<typeof foo>;
type SubInstArr = InstType["subInstArr"];
type SubIsntType = SubInstArr[0];

let baz: SubIsntType = {
  c: 5,
  d: 6 // ¡Se chequea correctamente el tipo!
};

// Podrías escribirlo en una sola línea,
// pero por favor asegúrate de que sea legible hacia adelante
// (lo puedes entender al leerlo una vez de izquierda a derecha sin saltos)
type SubIsntType2 = ReturnType<typeof foo>["subInstArr"][0];
let baz2: SubIsntType2 = {
  c: 5,
  d: 6 // ¡Se chequea correctamente el tipo!
};
```

# Manual de resolución de problemas: Imágenes y otros archivos que no son TS/TSX

Utiliza [mezcla de declaraciones](https://www.typescriptlang.org/docs/handbook/declaration-merging.html):

```ts
// declaration.d.ts
// en cualquier lugar de tu proyecto, NO el mismo nombre de cualquiera de tus archivos .ts/tsx
declare module "*.png";

// importación en un archivo tsx
import * as logo from "./logo.png";
```

Nota que `tsc` no puede empaquetar estos archivos por ti, tendrás que usar Webpack o Parcel.

Issue relacionado: https://github.com/Microsoft/TypeScript-React-Starter/issues/12 y [StackOverflow](https://stackoverflow.com/a/49715468/4216035)

# Manual de resolución de problemas: Operadores

- `typeof` y `instanceof`: consulta de tipos usadas para refinar
- `keyof`: obtiene llaves de un objeto
- `O[K]`: búsqueda de una propiedad
- `[K in O]`: tipos mapeados
- `+` o `-` o `readonly` o `?`: modificadores de adición, substracción, solo lectura y opcionalidad
- `x ? Y : Z`: Tipos condicionales para tipos genéricos, alias de tipo y tipos de parámetros de función
- `!`: Aserción de no nulidad para tipos que pueden ser nulos
- `=`: Valor por defecto del tipo paramétrico genérico en tipos genéricos
- `as`: aserción de tipo
- `is`: protección de tipo para tipos de retorno de funciones

Los tipos condicionales son un tema difícil de comprender, por lo que aquí hay algunos recursos extra:

- Explicación completa paso a paso https://artsy.github.io/blog/2018/11/21/conditional-types-in-typescript/
- _Bail out_ y otros temas avanzados https://github.com/sw-yx/ts-spec/blob/master/conditional-types.md

# Manual de resolución de problemas: Utilitarios

Todos estos están incorporados, [mira el código en es5.d.ts](https://github.com/microsoft/TypeScript/blob/2c458c0d1ccb96442bca9ce43aa987fb0becf8a9/src/lib/es5.d.ts#L1401-L1474):

- `ConstructorParameters`: una tupla de los tipos de los parámetros del constructor
- `Exclude`: excluye un tipo de otro tipo
- `Extract`: selecciona un subtipo que es asignable a otro tipo
- `InstanceType`: el tipo de instancia que obtienes al hacer `new` a `new` a un constructor de clase
- `NonNullable`: excluye `null` y `undefined` de un tipo
- `Parameters`: una tupla de los tipos de los parámetros de una función
- `Partial`: Hace que todas las propiedades en un objeto sean opcionales
- `Readonly`: Hace que todas las propiedades en un objeto sean de solo lectura
- `ReadonlyArray`: Hace un arreglo inmutable del tipo dado
- `Pick`: Un subtipo de un tipo de objeto con un subconjunto de sus llaves
- `Record`: Un mapeo de un tipo de llave a un tipo de valor
- `Required`: Hace todas que todas las propiedades de un objeto sean requeridas
- `ReturnType` El tipo de retorno de una función

# Manual de resolución de problemas: ESLint

**Nota: TSLint está en modo de mantenimiento y ESLint es el camino a seguir para TypeScript. [Puedes convertir TSlint a ESlint con esta herramienta](https://github.com/typescript-eslint/tslint-to-eslint-config).**

Esta sección necesita escribirse, pero probablemente puedes encontrar un buen punto para comenzar en la [configuración de ESLint de Wes Bos](https://github.com/wesbos/eslint-config-wesbos) (que viene con una [introducción en YouTube](https://www.youtube.com/watch?v=lHAeK8t94as)).

¡Luego, revisa las secciones sobre [Prettier](/AVANZADO.md#prettier) y [Linting](/AVANZADO.md#linting) cheatsheet AVANZADA!

# Manual de resolución de problemas: tsconfig.json

Puedes encontrar [todas las opciones del compilador en la documentación de TypeScript](https://www.typescriptlang.org/docs/handbook/compiler-options.html). Esta es la configuración que utilizo en APLICACIONES (no para bibliotecas; para bibliotecas puede que quieras ver las configuraciones que usamos en `tsdx`):

```json
{
  "compilerOptions": {
    "incremental": true,
    "outDir": "build/lib",
    "target": "es5",
    "module": "esnext",
    "lib": ["dom", "esnext"],
    "sourceMap": true,
    "importHelpers": true,
    "declaration": true,
    "rootDir": "src",
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "allowJs": false,
    "jsx": "react",
    "moduleResolution": "node",
    "baseUrl": "src",
    "forceConsistentCasingInFileNames": true,
    "esModuleInterop": true,
    "suppressImplicitAnyIndexErrors": true,
    "allowSyntheticDefaultImports": true,
    "experimentalDecorators": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "build", "scripts"]
}
```

Por favor abre un issue y expresa tu opinión sobre si existen mejores elecciones a recomendar para React.

Banderas seleccionadas y por qué nos gustan:

- `esModuleInterop`: deshabilita imports de espacios de nombre (`import * as foo from "foo"`) y habilita imports al estilo de CJS/AMD/UMD (`import fs from "fs"`)
- `strict`: `strictPropertyInitialization` te obliga a inicializar las propiedades de clase o declarar explícitamente que pueden no estar definidas. Puedes evitarlo usando una aserción de asignación definitiva.
- `"typeRoots": ["./typings", "./node_modules/@types"]`: Por defecto, TypeScript busca en `node_modules/@types` y directorios ancestros para buscar declaraciones de tipos de terceros. Podrías querer sobreescribir esta resolución por defecto de manera tal de que pudieras poner todas tus declaraciones globales de tipos en un directorio especial `typings`.

La velocidad de la compilación crece linealmente con el tamaño de la base de código. Para proyectos grandes, querrás usar [Referencias de proyecto](https://www.typescriptlang.org/docs/handbook/project-references.html). Mira nuestra cheatsheet [AVANZADA](AVANZADO.md) para comentarios.

# Manual de resolución de problemas: Errores en tipos oficiales

Si te encuentras errores en los tipos de tu biblioteca oficial, puedes copiarlos localmente y decirle a TypeScript que utilice tu versión local usando el campo "paths". En tu `tsconfig.json`:

```json
{
  "compilerOptions": {
    "paths": {
      "mobx-react": ["../typings/modules/mobx-react"]
    }
  }
}
```

[Gracias a @adamrackis for el consejo.](https://twitter.com/AdamRackis/status/1024827730452520963)

Si solo quieres añadir una interfaz, o añadir miembros que faltan a una interfaz existente, no necesitas copiar todo el paquete de tipos. En cambio, puedes utilizar la [mezcla de declaraciones](https://www.typescriptlang.org/docs/handbook/declaration-merging.html):

```tsx
// my-typings.ts
declare module "plotly.js" {
  interface PlotlyHTMLElement {
    removeAllListeners(): void;
  }
}

// MyComponent.tsx
import { PlotlyHTMLElement } from "plotly.js";

const f = (e: PlotlyHTMLElement) => {
  e.removeAllListeners();
};
```

No siempre tienes que implementar el módulo, puedes simplementer importar el módulo como `any` para un inicio rápido:

```tsx
// my-typings.ts
declare module "plotly.js"; // cada uno de estas importaciones son `any`
```

Dado que no tienes que explícitamente exportarlo, se conoce como [declaración de módulo de ambiente](https://www.typescriptlang.org/docs/handbook/namespaces-and-modules.html#pitfalls-of-namespaces-and-modules). puedes hacer una declaración de módulo de ambiente en un archivo `.ts` en modo de script (sin imports o exports), o en un archivo `.d.ts` en cualquier lugar de tu proyecto.

También puedes hacer declaraciones de variables de ambiente y de tipos de ambiente:

```ts
// tipo utilitario de ambiente
type ToArray<T> = T extends unknown[] ? T : T[];
// variable de ambiente
declare let process: {
  env: {
    NODE_ENV: "development" | "production";
  };
};
process = {
  env: {
    NODE_ENV: "production"
  }
};
```

También puedes ver ejemplos de ellos en las declaraciones de tipos incorporadas en el campo `lib` de `tsconfig.json`

# Bases de código de React + TypeScript recomendadas para aprender

- https://github.com/jaredpalmer/formik
- https://github.com/jaredpalmer/react-fns
- https://github.com/palantir/blueprint
- https://github.com/Shopify/polaris
- https://github.com/NullVoxPopuli/react-vs-ember/tree/master/testing/react
- https://github.com/artsy/reaction
- https://github.com/benawad/codeponder (¡con [programación en vivo!](https://www.youtube.com/watch?v=D8IJOwdNSkc&list=PLN3n1USn4xlnI6kwzI8WrNgSdG4Z6daCq))
- https://github.com/artsy/emission (React Native)
- [@reach/ui's community typings](https://github.com/reach/reach-ui/pull/105)

_Boilerplates_ de React:

- [@jpavon/react-scripts-ts](https://github.com/jpavon/react-scripts-ts) react-scripts alternativos con todas las funcionalidades de TypeScript usando [ts-loader](https://github.com/TypeStrong/ts-loader)
- [webpack config tool](https://webpack.jakoblind.no/) es una herramienta visual para la cración de proyectos de webpack con React y TypeScript
- <https://github.com/innFactory/create-react-app-material-typescript-redux> plantilla lista para usarse con [Material-UI](https://material-ui.com/), enrutamiento y Redux

_Boilerplates_ de React Native: _contribución de [@spoeck](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/pull/20)_

- https://github.com/GeekyAnts/react-native-seed
- https://github.com/lopezjurip/ReactNativeTS
- https://github.com/emin93/react-native-template-typescript
- <https://github.com/Microsoft/TypeScript-React-Native-Starter>

# Herramientas e integración en editores

- VSCode
  - Extensión de VSCode de swyx: https://github.com/sw-yx/swyx-react-typescript-snippets
  - amVim: https://marketplace.visualstudio.com/items?itemName=auiworks.amvim
- VIM
  - https://github.com/Quramy/tsuquyomi
  - ¿nvim-typescript?
  - https://github.com/leafgarland/typescript-vim
  - peitalin/vim-jsx-typescript
  - NeoVim: https://github.com/neoclide/coc.nvim
  - otros discusiones: https://mobile.twitter.com/ryanflorence/status/1085715595994095620

## Linting

> ⚠️ Nota que [TSLint ahora está en mantenimiento y deberías intentar usar ESLint en su lugar](https://medium.com/palantir/tslint-in-2019-1a144c2317a9). Si está interesado en los consejos de TSLint, consulte este PR desde [@azdanov](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/pull/14). El resto de esta sección solo se centra en ESLint.

> ⚠️ Este es un tema en evolución. `typescript-eslint-parser` ya no se mantiene y [el trabajo ha comenzado recientemente sobre`typescript-eslint` en la comunidad ESLint](https://eslint.org/blog/2019/01/future-typescript-eslint) para lleve ESLint con TSLint.

Siga los documentos de TypeScript + ESLint en https://github.com/typescript-eslint/typescript-eslint:

```
yarn add -D @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint
```

agregue un script `lint` a su`package.json`:

```json
  "scripts": {
    "lint": "eslint 'src/**/*.ts'"
  },
```

y en `.eslintrc.json` adecuado:

```json
{
  "env": {
    "es6": true,
    "node": true,
    "jest": true
  },
  "extends": "eslint:recommended",
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint"],
  "parserOptions": {
    "ecmaVersion": 2017,
    "sourceType": "module"
  },
  "rules": {
    "indent": ["error", 2],
    "linebreak-style": ["error", "unix"],
    "quotes": ["error", "single"],
    "no-console": "warn",
    "no-unused-vars": "off",
    "@typescript-eslint/no-unused-vars": [
      "error",
      { "vars": "all", "args": "after-used", "ignoreRestSiblings": false }
    ],
    "no-empty": "warn"
  }
}
```

Esto está tomado de [el `tsdx` PR](https://github.com/palmerhq/tsdx/pull/70/files) que es para **bibliotecas**.

Más opciones de `.eslintrc.json` se pueden desear para **aplicaciones**:

```json
{
  "extends": [
    "airbnb",
    "prettier",
    "prettier/react",
    "plugin:prettier/recommended",
    "plugin:jest/recommended",
    "plugin:unicorn/recommended"
  ],
  "plugins": ["prettier", "jest", "unicorn"],
  "parserOptions": {
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "env": {
    "es6": true,
    "browser": true,
    "jest": true
  },
  "settings": {
    "import/resolver": {
      "node": {
        "extensions": [".js", ".jsx", ".ts", ".tsx"]
      }
    }
  },
  "overrides": [
    {
      "files": ["**/*.ts", "**/*.tsx"],
      "parser": "typescript-eslint-parser",
      "rules": {
        "no-undef": "off"
      }
    }
  ]
}
```

Puede leer una [guía de configuración más completa de TypeScript + ESLint aquí](https://blog.matterhorn.dev/posts/learn-typescript-linting-part-1/) de Matterhorn, en particular consulte https://github.com/MatterhornDev/learn-typescript-linting.

Si está buscando información sobre Prettier, consulte [Prettier](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/blob/master/ADVANCED.md#prettier).

# Otros recursos sobre React + TypeScript

- !Yo! <https://twitter.com/swyx>
- <https://github.com/piotrwitek/react-redux-typescript-guide> - **MUY MUY RECOMENDADO**, escribí este repo antes de conocer sobre este, este tien muchas cosas que no cubro, incluyendo **REDUX** y **JEST**.
- [Ultimate React Component Patterns with TypeScript 2.8](https://levelup.gitconnected.com/ultimate-react-component-patterns-with-typescript-2-8-82990c516935)
- [Basarat's TypeScript gitbook has a React section](https://basarat.gitbooks.io/typescript/content/docs/jsx/react.html) con un [curso de Egghead.io](https://egghead.io/courses/use-typescript-to-develop-react-applications) también.
- [Palmer Group's Typescript + React Guidelines](https://github.com/palmerhq/typescript) así como también otros trabajos de Jared como [disco.chat](https://github.com/jaredpalmer/disco.chat)
- [Sindre Sorhus' TypeScript Style Guide](https://github.com/sindresorhus/typescript-definition-style-guide)
- [TypeScript React Starter Template by Microsoft](https://github.com/Microsoft/TypeScript-React-Starter) Una plantilla de inicio para TypeScript y React con un README detallado donde se describe cómo usarlos juntos. Nota: esto parece ya no actualizarse frecuentemente.
- [Curso intermedio sobre React de Brian Holt en Frontend Masters (de pago)](https://frontendmasters.com/courses/intermediate-react/converting-the-app-to-typescript/) - Sección sobre convertir una aplicación a TypeScript
- Conversión a TypeScript:
  - [CLI de conversión de React a TypeScript de Lyft](https://github.com/lyft/react-javascript-to-typescript-transform)
  - [Publicación de Gustav Wengel - Conversión de una base de código en React a TypeScript](http://www.gustavwengel.dk/converting-typescript-to-javascript-part-1)
  - [Guía de conversión de React a Typescript de Microsoft](https://github.com/Microsoft/TypeScript-React-Conversion-Guide#typescript-react-conversion-guide)
- [¿Tú?](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new).

# Charlas recomendadas sobre React + TypeScript

- ¡Por favor ayuda a contribuir con esta nueva sección!

# Hora de realmente aprender TypeScript

Lo creas o no, apenas hemos introducido TypeScript en esta cheatsheet. Hay un mundo complejo de loǵica de tipos genéricos al que eventualmente te enfrentarás, sin embargo se trata menos de lidiar con React que simplemente mejorar en TypeScript, y por eso está fuera de este ámbito. Pero al menos ahora ya puedes ser productivo en React :)

Vale la pena menicionar algunos recursos para inciarse:

- La sección de los 40+ ejemplos [del playground](http://www.typescriptlang.org/play/index.html), escrito por @Orta
- El resumen de TS de Anders Hejlsberg's: https://www.youtube.com/watch?v=ET4kT88JRXs
- Marius Schultz: https://blog.mariusschulz.com/series/typescript-evolution con un [curso de Egghead.io](https://egghead.io/courses/advanced-static-types-in-typescript)
- La explicación profunda de Basarat: https://basarat.gitbooks.io/typescript/
- Rares Matei: [El curso de Egghead.io](https://egghead.io/courses/practical-advanced-typescript) Advanced Typescript es muy bueno para las funcionalidades más nuevas de TypeScript y aplicaciones prácticas de la lógica de tipos (p. ej. hacer recursivamente todas las propiedades de un tipo como `readonly`).

# Aplicación de ejemplo

- [React TypeScript Todo Example 2019 Mid](https://github.com/ryota-murakami/react-typescript-todo-example-2019)

# ¡Mi pregunta no está respondida aquí!

- Consulta la [cheatsheet avanzada](/AVANZADO.md)
- [Abre un issue](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/new).

## Contribuidores

Este proyecto sigue la especificación de [all-contributors](https://github.com/all-contributors/all-contributors). Mira [CONTRIBUTORS.md](/CONTRIBUTORS.md) para la lista completa. ¡Contribuciones de cualquier tipo son bienvenidas!
