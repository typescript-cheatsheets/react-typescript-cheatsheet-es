<div align="center">

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

[**Básico**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet#basic-cheatsheet-table-of-contents) |
[**Avanzado**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/blob/master/ADVANCED.md) |
[**Migrando**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/blob/master/MIGRATING.md) |
[**HOC**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/blob/master/HOC.md) |
[中文翻译](https://github.com/fi3ework/blog/tree/master/react-typescript-cheatsheet-cn) |
[¡Contribuir!](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/blob/master/CONTRIBUYENDO.md) |
[¡Preguntas!](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/issues/new)

</div>

---


# Cheatsheet Avanzado

**Esta Cheatsheet Avanzada** ayuda a mostrar y explicar el uso avanzado de tipos genéricos para personas que escriben utilidades/funciones de tipo reutilizable/props de render/componentes de orden superior y **bibliotecas** TS+React.

- También tiene varios consejos y trucos para usuarios profesionales.
- Consejos para contribuir a DefinitelyTyped
- El objetivo es _aprovechar al máximo_ TypeScript.

**Creación de bibliotecas React + TypeScript**

La mejor herramienta para crear bibliotecas React + TS en este momento es [`tsdx`](https://github.com/palmerhq/tsdx). Ejecute `npx tsdx create` y seleccione la opción "react". Puede ver la [Guía del usuario de React](https://github.com/palmerhq/tsdx/issues/5) para obtener algunos consejos sobre las mejores prácticas y optimizaciones de la biblioteca React + TS para la producción.

- Asegúrese de consultar también la [guía de `basarat`'s](https://basarat.gitbooks.io/typescript/content/docs/quick/library.html) para la configuración de la biblioteca tsconfig.
- Desde el mundo angular, consulte https://github.com/bitjson/typescript-starter

---

### Tabla de contenido para Cheatsheet Avanzado

<details>

<summary><b>Expandir tabla de contenido</b></summary>

- [Sección 0: Tipos de utilidad](#Sección-0-tipos-de-utilidad)
- [Sección 1: Componentes reutilizables / Utilidades de tipos](#Sección-1-Componentes-reutilizablesutilidades-de-tipos)
    - [Componentes de orden superior](#de-orden-superior-componentes-hocs)
    - [Render Props](#render-props)
    - [Componentes de Representación Condicional](#componentes-de-representación-condicional)
    - [`as` props (pasando un componente para ser renderizado](as-props-pasando-un-componente-para-ser-renderizado)


</details>


# Sección 0: Tipos de utilidad


Asumiremos el conocimiento de los tipos de utilidad cubiertos en la guía de [`typescript-utilities-guide`](https://github.com/typescript-cheatsheets/typescript-utilities-guide) del proyecto hermano. Busque bibliotecas incluidas allí también para sus necesidades de escritura.

# Sección 1: Guías Avanzadas

## Componentes de orden superior

**Ahora hay una hoja de [Cheatsheet de HOC](./HOC.md) dedicada que puede consultar para obtener algo de práctica sobre HOC.**

## Render Props

A veces querrás escribir una función que pueda tomar un elemento React o una cadena o algo más como Prop. El mejor tipo para usar en tal situación es `React.ReactNode` que se adapta a cualquier lugar normal, bueno, React Node encajaría:

```tsx
export interface Props {
  label?: React.ReactNode;
  children: React.ReactNode;
}
export const Card = (props: Props) => {
  return (
    <div>
      {props.label && <div>{props.label}</div>}
      {props.children}
    </div>
  );
};
```

Si está utilizando una función como render prop con `props.children`: 

```tsx
export interface Props {
  children: (foo: string) => React.ReactNode;
}
```

[Algo para agregar? Presentar un problema](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/issues/new).

## Componentes de Representación Condicional

Usar [type guards](https://basarat.gitbooks.io/typescript/docs/types/typeGuard.html#user-defined-type-guards)!

```tsx
// Props de botón
type ButtonProps = React.ButtonHTMLAttributes<HTMLButtonElement> & {
  href?: undefined;
};

// Anchor props
type AnchorProps = React.AnchorHTMLAttributes<HTMLAnchorElement> & {
  href?: string;
};

// Opciones de entrada / salida
type Overload = {
  (props: ButtonProps): JSX.Element;
  (props: AnchorProps): JSX.Element;
};

// Guard para verificar si existe href en props
const hasHref = (props: ButtonProps | AnchorProps): props is AnchorProps =>
  "href" in props;

// Componente
const Button: Overload = (props: ButtonProps | AnchorProps) => {
  // renderizado de anchor
  if (hasHref(props)) return <a {...props} />;
  // renderizado de botón
  return <button {...props} />;
};

// Uso
function App() {
  return (
    <>
      {/* 😎 Todo bien */}
      <Button target="_blank" href="https://www.google.com">
        Test
      </Button>
      {/* 😭 Error, `disabled` no existe en el elemento de anlaze */}
      <Button disabled href="x">
        Test
      </Button>
    </>
  );
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoAekrgCEBXGGCAOzjBzAGcKYBPMEjqNmLAAqcucALyJiMAHQMmrABIAVALIAZAIJMowAEaMkXADwady0QFEANkhBIWMAHxwAZHADeFOHAAFkSYAPwAXHD0LAAmSJjALEgxANwUAL5p5BTUcLosaIHQ7JK8AkL5hdASENwycuiKlUVQVnoGxqYWbc3QDk4u7l6+-kEhEXBcMIYsAOZZmRQ5NACSLGCMlBCMG-C1MMCsPOT8gnAA8gBuSFD2ECgx9X7kAQAUHLVckTasNdwAlJEAFIAZQAGgp+s5XFk3h9uJFelA-lxAXBQRCoYMFlllnAAOL0FBQR7MOCFJBoADWcGAmDG8TgSAAHsAplJEiVPhQ0Ed4IEUFxVCF6u9JN8RL9JHAAD55AotFFo+EcqRIlEyNyjABEwXi2tpbBVuKoNAAwrhIElXDy+cIVCxIlcbncHqKVRKHRq5erJP9NSMXnBcigFcUiLEbqM6XBXgKhSExZ9-v6iDB6FA2OYUL4FHmVelg25YcGaCYHXAI3EoKM0xms+XRLn85JC5RixkTbkAKpcFCzJAUTDRDCHNi6MBgV7+54BOuZ2OjALmLVBgIBHyUABUcEAvBuAOD28vZ7HBZhAII8t5R0kv1+YfmwYMSBzBpNqAPpGeyhqkGvWYN9AiYBFqAAd3AhQzwgWZHAUXkQG1Vd12QuB1DMGBb2XSgHyQlDNx3XdAFo9uBbCgHAoAAGjgAADGI2RQL9kmouAYggMxXCZVkpjgVg4FDKooCZRxoXgK8bzXO8HxY+jGMef832ZRDMPXNCpmU8xsMlFhcKw3D-gWIA)

## `as` props (pasando un componente para ser renderizado)

`ElementType` es bastante útil para cubrir la mayoría de los tipos que se pueden pasar a createElement, p.ej.

```tsx
function PassThrough(props: { as: React.ElementType<any> }) {
  const { as: Component } = props;

  return <Component />;
}
```

[Gracias  @eps1lon](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/pull/69) por esto.


## Componentes genéricos

Del mismo modo que puede crear funciones y clases genéricas en TypeScript, también puede crear componentes genéricos para aprovechar el sistema de tipos para la seguridad de _tipos_ reutilizables. Tanto Props como State pueden aprovechar los mismos _tipos_ genéricos, aunque probablemente tenga más sentido para Props que para State. Luego puede usar el tipo genérico para anotar los _tipos_ de cualquier variable definida dentro del alcance de su función / clase.

```tsx
interface Props<T> {
  items: T[];
  renderItem: (item: T) => React.ReactNode;
}
function List<T>(props: Props<T>) {
  const { items, renderItem } = props;
  const [state, setState] = React.useState<T[]>([]); // Puede usar el tipo T en el alcance de la función Lista.
  return (
    <div>
      {items.map(renderItem)}
      <button onClick={() => setState(items)}>Clone</button>
      {JSON.stringify(state, null, 2)}
    </div>
  );
}
```

A continuación, puede utilizar los componentes genéricos y obtener una buena seguridad de _tipos_ mediante la inferencia de _tipos_:

```tsx
ReactDOM.render(
  <List
    items={["a", "b"]} // tipo de 'string' inferido
    renderItem={item => (
      <li key={item}>
        {item.toPrecision(3)} // Error: la propiedad 'toPrecision' no existe en
         escriba 'string'.
      </li>
    )}
  />,
  document.body
);
```

A partir de [TS 2.9](#typescript-29), también puede proporcionar el parámetro de _tipo_ en su JSX para optar por la inferencia de _tipos_:

```tsx
ReactDOM.render(
  <List<number>
    items={["a", "b"]} // Error: el tipo 'string' no es asignable para escribir 'number'.
    renderItem={item => <li key={item}>{item.toPrecision(3)}</li>}
  />,
  document.body
);
```

También puede usar genéricos usando el estilo de función de flecha de grande:

```tsx
interface Props<T> {
  items: T[];
  renderItem: (item: T) => React.ReactNode;
}
