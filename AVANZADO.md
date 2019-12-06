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
  - [`as` props (pasando un componente para ser renderizado](#as-props-pasando-un-componente-para-ser-renderizado)
  - [Componentes genéricos](#componentes-genéricos)
  - [Escribiendo un componente que acepta diferentes accesorios](#escribiendo-un-componente-que-acepta-diferentes-accesorios)
  - [Props: uno u otro pero no ambos](#props-uno-u-otro-pero-no-ambos)
  - [Props: debe pasar ambos](#props-debe-pasar-ambos)
  - [Props: opcionalmente, puedes pasar uno solo si se pasa el otro](#props-opcionalmente-puedes-pasar-uno-solo-si-se-pasa-el-otro)
  - [Omitir atributo de un tipo](#omitir-atributo-de-un-tipo)
  - [Type Zoo](#type-zoo)
  - [Extracción de tipos de Prop de un componente](#extracción-de-tipos-de-prop-de-un-componente)
  - [Manejo de excepciones](#manejo-de-excepciones)
  - [Bibliotecas de Terceros](#bibliotecas-de-terceros)
- [Sección 2: Patrones útiles por versión de TypeScript](sección-2-patrones-útiles-por-versión-de-typeScript)

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

[Gracias @eps1lon](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/pull/69) por esto.

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

// Tenga en cuenta que <T se extiende desconocido> antes de la definición de la función.
// No puedes usar solo `<T>` ya que confundirá al analizador TSX ya sea una etiqueta JSX o una Declaración Genérica.
// También puedes usar <T,> https://github.com/microsoft/TypeScript/issues/15713#issuecomment-499474386
const List = <T extends unknown>(props: Props<T>) => {
  const { items, renderItem } = props;
  const [state, setState] = React.useState<T[]>([]); // Puedes usar el tipo T en el alcance de la función Lista.
  return (
    <div>
      {items.map(renderItem)}
      <button onClick={() => setState(items)}>Clone</button>
      {JSON.stringify(state, null, 2)}
    </div>
  );
};
```

Lo mismo para usar clases: (Crédito: al [gist](https://gist.github.com/karol-majewski/befaf05af73c7cb3248b4e084ae5df71) de [Karol Majewski](https://twitter.com/WrocTypeScript/status/1163234064343736326)).

```tsx
interface Props<T> {
  items: T[];
  renderItem: (item: T) => React.ReactNode;
}

interface State<T> {
  items: T[];
}

class List<T> extends React.PureComponent<Props<T>, State<T>> {
  // Puedes usar el tipo T dentro de la clase Lista.
  state: Readonly<State<T>> = {
    items: []
  };
  render() {
    const { items, renderItem } = this.props;
    // Puedes usar el tipo T dentro de la clase Lista.
    const clone: T[] = items.slice(0);
    return (
      <div>
        {items.map(renderItem)}
        <button onClick={() => this.setState({ items: clone })}>Clone</button>
        {JSON.stringify(this.state, null, 2)}
      </div>
    );
  }
}
```

Aunque no puedes utilizar los parámetros de tipo genérico para miembros estáticos:

```tsx
class List<T> extends React.PureComponent<Props<T>, State<T>> {
  // Los miembros estáticos no pueden hacer referencia a los parámetros de tipo de clase.ts(2302)
  static getDerivedStateFromProps(props: Props<T>, state: State<T>) {
    return { items: props.items };
  }
}
```

Para solucionar esto, debe convertir tu función estática en una función inferida de tipo:

```tsx
class List<T> extends React.PureComponent<Props<T>, State<T>> {
  static getDerivedStateFromProps<T>(props: Props<T>, state: State<T>) {
    return { items: props.items };
  }
}
```

### Componentes genéricos con children

`children` generalmente no se define como parte del tipo de _props_. A menos que `children` se defina explícitamente como parte del tipo `props`, un intento de usar `props.children` en JSX o en el cuerpo de la función fallará:

```tsx
interface WrapperProps<T> {
  item: T;
  renderItem: (item: T) => React.ReactNode;
}

/* La propiedad 'children' no existe en el tipo 'WrapperProps <T>'. */
const Wrapper = <T extends {}>(props: WrapperProps<T>) => {
  return (
    <div>
      {props.renderItem(props.item)}
      {props.children}
    </div>
  );
};

/*
Type '{ children: string; item: string; renderItem: (item: string) => string; }' no es asignable a tipo 'IntrinsicAttributes & WrapperProps<string>'.
 La propiedad 'children' no existe en el tipo'IntrinsicAttributes & WrapperProps<string>'.
*/

const wrapper = (
  <Wrapper item="test" renderItem={item => item}>
    {test}
  </Wrapper>
);
```

[View in the TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoC4AOxiSk3STgHUoUwx6AFHMAZwA8AFQB8cAN4U4cYHRAAuOMIDc0uEWoATegEl5SgBRyki5QEo4AXnHJ0MAHR2MAOQg615GWgAWwADZamkrOjqFuHhQAvhQUAPQAVHC8EFywAJ4EvgFBSNT4cFoQSPxw1BDwSAAewPzwENRwMOlcBGwcaSkCIqL4DnAJcRRoDXWs7Jz01nAicNV02qUSUaKGYHz8Su2TUF1CYpY2kupEMACuUI2G6jKCWsAAbqI3MpLrqfwOmjpQ+qZrGwcJhA5hiXleMgk7wEDmygU0YIhgji9ye6nMniinniCQowhazHwEjgcNy1CUdSgNAA5ipZAY4JSaXTvnoGcYGUzqNTDuIubS4FECrUyhU4Ch+PxgNTqCgAEb+ZgwCBNAkEXS0KnUKVoACCMBgVLlZzopQAZOMOjwNoJ+b0HOouvRmlk-PC8gUiiVRZUamMGqrWvgNYaaDr9aHjaa4Bbtp0bXa+hRBrFyCNtfBTfArHBDLyZqjRAAJJD+fwqrPIwvDUbwADuEzS02u4MEcamwKsACIs12NHkfn8QFYJMDrOJgSsXhIs4iZnF21BnuQMUA)

Para evitar eso, agregue `children` a la definición de`WrapperProps` (posiblemente reduzca su tipo, según sea necesario):

```tsx
interface WrapperProps<T> {
  item: T;
  renderItem: (item: T) => React.ReactNode;
  children: string; // El componente solo aceptará una sola cadena strig child
}

const Wrapper = <T extends {}>(props: WrapperProps<T>) => {
  return (
    <div>
      {props.renderItem(props.item)}
      {props.children}
    </div>
  );
};
```

o envuelva el tipo de los props en `React.PropsWithChildren` (this is what `React.FC<>` does):

```tsx
interface WrapperProps<T> {
  item: T;
  renderItem: (item: T) => React.ReactNode;
}

const Wrapper = <T extends {}>(
  props: React.PropsWithChildren<WrapperProps<T>>
) => {
  return (
    <div>
      {props.renderItem(props.item)}
      {props.children}
    </div>
  );
};
```

## Escribiendo un componente que acepta diferentes accesorios

Los componentes, y JSX en general, son análogos a las funciones. Cuando un componente puede renderizarse de manera diferente en función de sus _props_, es similar a cómo se puede sobrecargar una función para tener múltiples _llamadas_. Del mismo modo, puede sobrecargar las _llamadas_ de un componente de función para enumerar todas sus diferentes "versiones".

Un caso de uso muy común para esto es representar algo como un botón o un ancla, en función de si recibe un atributo `href`.

```tsx
type ButtonProps = JSX.IntrinsicElements["button"];
type AnchorProps = JSX.IntrinsicElements["a"];

// opcionalmente use un type guard personalizado
function isPropsForAnchorElement(
  props: ButtonProps | AnchorProps
): props is AnchorProps {
  return "href" in props;
}

function Clickable(props: ButtonProps | AnchorProps) {
  if (isPropsForAnchorElement(props)) {
    return <a {...props} />;
  } else {
    return <button {...props} />;
  }
}
```

Ni siquiera necesitan ser props completamente diferentes, siempre que tengan al menos una diferencia en las propiedades:

```tsx
type LinkProps = Omit<JSX.IntrinsicElements["a"], "href"> & { to?: string };

function RouterLink(props: LinkProps | AnchorProps) {
  if ("to" in props) {
    return <a {...props} />;
  } else {
    return <Link {...props} />;
  }
}
```

<details>
  <summary><b>Enfoque: Componentes Genéricos</b></summary>

Aquí hay una solución de ejemplo, vea la discusión adicional para otras soluciones. _gracias a [@jpavon](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/12#issuecomment-394440577)_

```tsx
interface LinkProps {}
type AnchorProps = React.AnchorHTMLAttributes<HTMLAnchorElement>;
type RouterLinkProps = Omit<NavLinkProps, "href">;

const Link = <T extends {}>(
  props: LinkProps & T extends RouterLinkProps ? RouterLinkProps : AnchorProps
) => {
  if ((props as RouterLinkProps).to) {
    return <NavLink {...(props as RouterLinkProps)} />;
  } else {
    return <a {...(props as AnchorProps)} />;
  }
};

<Link<RouterLinkProps> to="/">Mi enlace</Link>; // bien
<Link<AnchorProps> href="/">Mi enlace</Link>; // bien
<Link<RouterLinkProps> to="/" href="/">
  Mi enlace
</Link>; // error
```

</details>

<details>
  <summary><b>Enfoque: Composición</b></summary>

Si desea renderizar condicionalmente un componente, a veces es mejor usar [React's composition model](https://reactjs.org/docs/composition-vs-inheritance.html) para tener componentes más simples y comprender mejor los _tipos_.

```tsx
type AnchorProps = React.AnchorHTMLAttributes<HTMLAnchorElement>
type RouterLinkProps = Omit<AnchorProps, 'href'>

interface Button {
  as: React.ComponentClass | 'a'
}

const Button: React.FunctionComponent<Button> = (props) => {
  const {as: Component, children, ...rest} = props
  return (
    <Component className="button" {...rest}>{children}</Component>
  )
}

const AnchorButton: React.FunctionComponent<AnchorProps> = (props) => (
  <Button as="a" {...props} />
)

const LinkButton: React.FunctionComponent<RouterLinkProps> = (props) => (
  <Button as={NavLink} {...props} />
)

<LinkButton to="/login">Iniciar sesión</LinkButton>
<AnchorButton href="/login">Iniciar sesión</AnchorButton>
<AnchorButton href="/login" to="/test">Iniciar sesión</AnchorButton> // Error: la propiedad 'a' no existe en el tipo...
```

</details>

También es posible que desee utilizar Uniones discriminadas, consulte [Expressive React Component APIs with Discriminated Unions](https://blog.andrewbran.ch/expressive-react-component-apis-with-discriminated-unions/).

Aquí hay una breve intuición para **Tipos de Unión Discriminada**:

```ts
type UserTextEvent = { value: string; target: HTMLInputElement };
type UserMouseEvent = { value: [number, number]; target: HTMLElement };
type UserEvent = UserTextEvent | UserMouseEvent;
function handle(event: UserEvent) {
  if (typeof event.value === "string") {
    event.value; // string
    event.target; // HTMLInputElement | HTMLElement (!!!!)
    return;
  }
  event.value; // [number, number]
  event.target; // HTMLInputElement | HTMLElement (!!!!)
}
```

Even though we have narrowed based on `event.value`, the logic doesn't filter up and sideways to `event.target`. This is because a union type `UserTextEvent | UserMouseEvent` could be BOTH at once. So TypeScript needs a better hint. The solution is to use a literal type to tag each case of your union type:

```ts
type UserTextEvent = {
  type: "TextEvent";
  value: string;
  target: HTMLInputElement;
};
type UserMouseEvent = {
  type: "MouseEvent";
  value: [number, number];
  target: HTMLElement;
};
type UserEvent = UserTextEvent | UserMouseEvent;
function handle(event: UserEvent) {
  if (event.type === "TextEvent") {
    event.value; // string
    event.target; // HTMLInputElement
    return;
  }
  event.value; // [number, number]
  event.target; // HTMLElement
}
```

Para simplificar esto, también puede combinar esto con el concepto de _**User-Defined Type Guards**_.

```ts
function isString(a: unknown): a is string {
  return typeof a === "string";
}
```

[Lea más sobre User-Defined Type Guards en esta guia](https://www.typescriptlang.org/docs/handbook/advanced-types.html#user-defined-type-guards).

## Props: uno u otro pero no ambos

Use la palabra clave `in`, la sobrecarga de funciones y los tipos de unión para crear componentes que tengan uno u otro conjunto de props pero no ambos:

```tsx
type Props1 = { foo: string };
type Props2 = { bar: string };

function MyComponent(props: Props1 | Props2) {
  if ("foo" in props) {
    // props.bar // error
    return <div>{props.foo}</div>;
  } else {
    // props.foo // error
    return <div>{props.bar}</div>;
  }
}
const UsageComponent: React.FC = () => (
  <div>
    <MyComponent foo="foo" />
    <MyComponent bar="bar" />
    {/* <MyComponent foo="foo" bar="bar"/> // invalid */}
  </div>
);
```

[View in the TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCmATzCTgAUcwBnARjgF44BvOTCBABccFjCjAAdgHM4AXwDcVWvSYRWAJi684AIxRQRYiTPlLK5TAFdJGYBElwAstQDCuSJKSSYACjDMLCJqrBwAPoyBGgCUvBRwcMCYcL4ARAIQqYmOAeossTzxCXAA9CVwuawAdPpQpeVIUDhQRQlEMFZQjgA8ACbAAG4AfDyVLFUZct0l-cPmCXJwSAA2LPSF5MX1FYETgtuNza1w7Z09syNjNQZTM4ND8-IUchRoDmJwAKosKNJI7uAHN4YCJkOgYFUAGKubS+WKcIYpIp9e7HbouAGeYH8QScdKCLIlIZojEeIE+PQGPG1QnEzbFHglABUcHRbjJXgpGTxGSytWpBlSRO2UgGKGWwF6cCZJRe9OmFwo0QUQA)

Lectura adicional: [cómo prohibir pasar `{}` si tiene un tipo `NoFields`](http://www.javiercasas.com/articles/typescript-impossible-states-irrepresentable)

## Props: debe pasar ambos

```tsx
type OneOrAnother<T1, T2> =
  | (T1 & { [K in keyof T2]?: undefined })
  | (T2 & { [K in keyof T1]?: undefined });

type Props = OneOrAnother<{ a: string; b: string }, {}>;

const a: Props = { a: "a" }; // error
const b: Props = { b: "b" }; // error
const ab: Props = { a: "a", b: "b" }; // ok
```

Gracias [diegohaz](https://twitter.com/kentcdodds/status/1085655423611367426)

## Props: opcionalmente, puedes pasar uno solo si se pasa el otro

Supongamos que desea un componente de texto que se acorta si se pasa el accesorio `truncate` pero se expande para mostrar el texto completo cuando se pasa el accesorio`expanded` (por ejemplo, cuando el usuario hace clic en el texto).

Desea permitir que se pase `expanded` solo si también se pasa `truncate`, porque no hay uso para `expanded` si el texto no esta acortado.

Puede hacerlo mediante function overloads:

```tsx
type CommonProps = {
  children: React.ReactNode;
  miscProps?: any;
};

type NoTruncateProps = CommonProps & { truncate?: false };

type TruncateProps = CommonProps & { truncate: true; expanded?: boolean };

// Function overloads acepta ambos tipos de props NoTruncateProps y TruncateProps
function Text(props: NoTruncateProps): JSX.Element;
function Text(props: TruncateProps): JSX.Element;
function Text(props: CommonProps & { truncate?: boolean; expanded?: boolean }) {
  const { children, truncate, expanded, ...otherProps } = props;
  const classNames = truncate ? ".truncate" : "";
  return (
    <div className={classNames} aria-expanded={!!expanded} {...otherProps}>
      {children}
    </div>
  );
}
```

Usando el componente de texto:

```tsx
const App: React.FC = () => (
  <>
    {/* todos estos typecheck */}
    <Text>not truncated</Text>
    <Text truncate>truncated</Text>
    <Text truncate expanded>
      truncate-able but expanded
    </Text>
    {/* TS error: Property 'truncate' is missing in type '{ children: string; expanded: true; }' but required in type '{ truncate: true; expanded?: boolean | undefined; }'. */}
    <Text expanded>truncate-able but expanded</Text>
  </>
);
```

## Omitir atributo de un tipo

Nota: [Omitir se agregó como una utilidad de primera clase en TS 3.5](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittk)! 🎉

A veces, cuando se cruzan tipos, queremos definir nuestra propia versión de un atributo. Por ejemplo, quiero que mi componente tenga una `etiqueta`, pero el tipo con el que me estoy cruzando también tiene un atributo `etiqueta`. Aquí se explica cómo extraer ese tipo:

```tsx
export interface Props {
  label: React.ReactNode; // esto entrará en conflicto con la etiqueta InputElement
}

// esto viene incorporado con TS 3.5
type Omit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>;

// uso
export const Checkbox = (
  props: Props & Omit<React.HTMLProps<HTMLInputElement>, "label">
) => {
  const { label } = props;
  return (
    <div className="Checkbox">
      <label className="Checkbox-label">
        <input type="checkbox" {...props} />
      </label>
      <span>{label}</span>
    </div>
  );
};
```

Cuando su componente define múltiples accesorios, aumentan las posibilidades de esos conflictos. Sin embargo, puede indicar explícitamente que todos sus campos deben eliminarse del componente subyacente utilizando el operador `keyof`:

```tsx
export interface Props {
  label: React.ReactNode; // entra en conflicto con la etiqueta de InputElement
  onChange: (text: string) => void; // entra en conflicto con onChange de InputElement
}

export const Textbox = (
  props: Props & Omit<React.HTMLProps<HTMLInputElement>, keyof Props>
) => {
  // implementar el componente Textbox ...
};
```

## Type Zoo

Como puede ver en el ejemplo anterior de Omitir, también puede escribir una lógica significativa en sus tipos. [type-zoo](https://github.com/pelotom/type-zoo) es un buen conjunto de herramientas de operadores que puede desear consultar (incluye Omitir), así como [tipos de utilidad](https://github.com/piotrwitek/utility-types)(especialmente para aquellos que migran desde Flow).

## Extracción de tipos de Prop de un componente

_(Contribuido por [@ferdaber](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/issues/63))_

Hay muchos lugares donde desea reutilizar algunas piesas de props debido a _props drilling_, para que pueda exportar el tipo de accesorios como parte del módulo o extraerlos (de cualquier manera funciona).

La ventaja de extraer los tipos de props es que no necesitas exportar todo. Y el componente fuente se propagará a todos los componentes consumidores.

```ts
import { ComponentProps, JSXElementConstructor } from "react";

// va un paso más allá y se resuelve con las propiedades propTypes y defaultProps
type ApparentComponentProps<
  C extends keyof JSX.IntrinsicElements | JSXElementConstructor<any>
> = C extends JSXElementConstructor<infer P>
  ? JSX.LibraryManagedAttributes<C, P>
  : ComponentProps<C>;
```

También puede usarlos para escribir controladores de eventos personalizados si no están escritos en los propios sitios de llamadas
(es decir, en línea con el atributo JSX):

```tsx
// my-inner-component.tsx
export function MyInnerComponent(props: {
  onSomeEvent(
    event: ComplexEventObj,
    moreArgs: ComplexArgs
  ): SomeWeirdReturnType;
}) {
  /* ... */
}

// my-consuming-component.tsx
export function MyConsumingComponent() {
  // event y moreArgs se escriben contextualmente junto con el valor de retorno
  const theHandler: Props<typeof MyInnerComponent>["onSomeEvent"] = (
    event,
    moreArgs
  ) => {};
  return <MyInnerComponent onSomeEvent={theHandler} />;
}
```

## Manejo de Excepciones

Puede proporcionar buena información cuando suceden cosas malas.

```ts
class InvalidDateFormatError extends RangeError {}
class DateIsInFutureError extends RangeError {}

/**
 * // opcional docblock
 * @throws {InvalidDateFormatError} El usuario ingresó la fecha incorrectamente
 * @throws {DateIsInFutureError} El usuario ingresó la fecha en el futuro
 *
 */
function parse(date: string) {
  if (!isValid(date))
    throw new InvalidDateFormatError("no es un formato de fecha válido");
  if (isInFuture(date))
    throw new DateIsInFutureError("la fecha es en el futuro");
  // ...
}

try {
  // llamar a parse(date)) en alguna parte
} catch (e) {
  if (e instanceof InvalidDateFormatError) {
    console.error("formato de fecha inválido", e);
  } else if (e instanceof DateIsInFutureError) {
    console.warn("la fecha es en el futuro", e);
  } else {
    throw e;
  }
}
```

[View in TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCtAGxQGc64BJAOwDcVrgATAERRhIAYtBACAolBxQ4SAB6CW3RghQsA5kknS4AbwC+VWgzj9BTOqyEBXGNaLboshUiUq1mxzIMUKmaywYwBAscMB0AGqcPAAU3AJIAFxwdDBQwBoAlHoUcHBEdlCh8YJwAPxwadZIcMmYnHRIANwUhpTk-oEwwaHhVrb2SHEJyanpWTnkeWghqXAlSAByEADucAC8cCxIa2ZDmS1TcDMsc2j2RCwwextbO6YJw4KZuXCvBfah51Ku1wkAdJoYAAVUD7OAAPnmCWWK0BSBBYJiB1avnIAHoAFSY3KYuDo9FwCBgbohTjzCBoABG1EpAGtcXAAAIwAAWOBWjF0rA4XD4CREUDEMC8+jgwNZNWsjRkvyQRG40NKGRmPww1AAnoyWezVly9hZ+oUtFJoGKJVKZbIrvKkIqFmFQv5jbjcei-AEgiE4GAUFBGk8kik0hl1NldK9gJg4DEAIThKJ8wOZF5HPJsjl3NY86L8wSC4VeGIAIhYEHgKDgvJ4SpqmFEAmLKKOUZjfRYNmNyeyGdWWYe5ksHYGDlNUBLDvCjsqkrgzsGTcOeQJcH+a9R7TSGsmy8JaE41B9foDC2ydFwO0lRFaxwEaFZMaQ4cj0ZiNQyqTUaCQEGjOb5ewFhIY7PmmxyzBA1BIP88rSCWGTVvaCRzg2MDFgANLIzZ5GKSDUI0YSvu+pwwF+P7RgaQ6doMXigXk0wQVB-wrH6LATshU4ZHOI5IBhWFLnAuH4TUEZgb2azNK8bT6EAA)

Simplemente lanzar una excepción está bien, sin embargo, sería bueno hacer que TypeScript recuerde al consumidor de tu código para manejar tu excepción. Podemos hacerlo simplemente volviendo en lugar de lanzar:

```ts
function parse(
  date: string
): Date | InvalidDateFormatError | DateIsInFutureError {
  if (!isValid(date))
    return new InvalidDateFormatError("no es un formato de fecha válido");
  if (isInFuture(date))
    return new DateIsInFutureError("la fecha es en el futuro");
  // ...
}

// ahora el consumidor * tiene * para manejar los errores
let result = parse("mydate");
if (result instanceof InvalidDateFormatError) {
  console.error("invalid date format", result.message);
} else if (result instanceof DateIsInFutureError) {
  console.warn("date is in future", result.message);
} else {
  /// usa el resultado de forma segura
}

// alternativamente, puede manejar todos los errores
if (result instanceof Error) {
  console.error("error", result);
} else {
  /// usa el resultado de forma segura
}
```

También puede describir excepciones con tipos de datos de propósito especial (no diga mónadas ...) como los tipos de datos `Try`,`Option` (o `Maybe`) y`Either`:

```ts
interface Option<T> {
  flatMap<U>(f: (value: T) => None): None
  flatMap<U>(f: (value: T) => Option<U>): Option<U>
  getOrElse(value: T): T
}
class Some<T> implements Option<T> {
  constructor(private value: T) {}
  flatMap<U>(f: (value: T) => None): None
  flatMap<U>(f: (value: T) => Some<U>): Some<U>
  flatMap<U>(f: (value: T) => Option<U>): Option<U> {
    return f(this.value)
  }
  getOrElse(): T {
    return this.value
  }
}
class None implements Option<never> {
  flatMap<U>(): None {
    return this
  }
  getOrElse<U>(value: U): U {
    return value
  }
}

// ahora puedes usarlo como:
let result = Option(6) // Algunos <número>
              .flatMap(n => Option(n*3)) // Algunos <número>
              .flatMap(n = new None) // Nada
              .getOrElse(7)

// or:
let result = ask() // Opción<string>
              .flatMap(parse) // Option<Date>
              .flatMap(d => new Some(d.toISOString()) // Opción<string>
              .getOrElse('cadena de análisis de error')
```

## Bibliotecas de Terceros

A veces, DefinitelyTyped se puede equivocar o no puede abordar su caso de uso. Puedes declarar tu propio archivo con el mismo nombre de interfaz. Typecript fusionará interfaces con el mismo nombre.

# Sección 2: Patrones útiles por versión de TypeScript
