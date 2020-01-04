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

<p>Cheatsheets para desarrolladores experimentados de React que estan empezando con TypeScript</p>

[**Básico**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet#basic-cheatsheet-table-of-contents) |
[**Avanzado**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/blob/master/AVANZADO.md) |
[**Migrando**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/blob/master/MIGRATING.md) |
[**HOC**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/blob/master/HOC.md) |
[中文翻译](https://github.com/fi3ework/blog/tree/master/react-typescript-cheatsheet-cn) |
[¡Contribuir!](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/blob/master/CONTRIBUYENDO.md) |
[¡Preguntas!](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/issues/new)

</div>

---

# HOC Cheatsheet

**Este HOC Cheatsheet** agrupa todo el conocimiento disponible para escribir Componentes de Orden Superior (HOC por las siglas en inglés de higher-order component) con React y Typescript.

- Inicialmente haremos un mapa detallado de la [documentación oficial sobre HOC](https://es.reactjs.org/docs/higher-order-components.html).
- Si bien existen hooks, muchas librerías y bases de código aún necesitan escribir HOC
- Render _props_ podrian ser considerado en el futuro
- El objetivo es escribir HOC que ofrezcan un tipado seguro sin interferir

---

### HOC Cheatsheet Tabla de Contenido

<details>

<summary><b>Expandir Tabla de Contenido</b></summary>

- [Sección 0: Ejemplo completo de un HOC](#Sección-0-Ejemplo-completo-de-un-HOC)
- [Sección 1: Documentación de React sobre HOC en TypeScript](#Sección-1-Documentación-de-React-sobre-HOC-en-TypeScript)
- [Sección 2: Excluyendo Props](#sección-2-Excluyendo-Props)

  </details>

# Sección 0: Ejemplo completo de un HOC

> Este es un ejemplo de un HOC para copiar y pegar. Si ciertos pedazos no tienen sentido para ti, ve a la [Sección 1](#Sección-1-Documentación-de-React-sobre-HOC-en-TypeScript) para obtener un tutorial detallado a través de una traducción completa de la documentación de React en Typescript.

A veces quieres una forma sencilla de pasar _props_ desde otro lugar (ya sea el store global o un provider) y no quieres continuamente pasar los _props_ hacia abajo. Context es excelente para eso, pero entonces los valores desde el context solo pueden ser usado desde tu función `render`. Un HOC proveerá esos valores cómo _props_.

**Los _props_ inyectados**

```ts
interface WithThemeProps {
  primaryColor: string;
}
```

**Uso en el componente**

El objetivo es tener los _props_ disponibles en la interfaz para el componente, pero sustraído para los consumidores del componente cuando estén envuelto en el HoC.

```ts
interface Props extends WithThemeProps {
  children: React.ReactNode;
}

class MyButton extends React.Component<Props> {
  public render() {
    // Renderiza un elemento usando el tema y otros props.
  }

  private someInternalMethod() {
    // Los valores del tema también estan aquí disponibles cómo props.
  }
}

export default withTheme(MyButton);
```

**Consumiendo el componente**

Ahora, al consumir el componente puedes omitir el prop `primaryColor` o anular el que fue proporcionado a través del context.

```tsx
<MyButton>Hello button</MyButton> // Válido
<MyButton primaryColor="#333">Hello Button</MyButton> // Tambien válido
```

**Declarando el HoC**

El HoC actual.

```tsx
export function withTheme<T extends WithThemeProps = WithThemeProps>(
  WrappedComponent: React.ComponentType<T>
) {
  // Intenta crear un buen displayName para React Dev Tools.
  const displayName =
    WrappedComponent.displayName || WrappedComponent.name || "Component";

  // Creando el componente interno. El tipo de prop calculado aquí es donde ocurre la magia.
  return class ComponentWithTheme extends React.Component<
    Optionalize<T, WithThemeProps>
  > {
    public static displayName = `withPages(${displayName})`;

    public render() {
      // Obten los props que quiere inyectar. Esto podría ser hecho con context.
      const themeProps = getThemePropsFromSomeWhere();

      // this.props viene después para que puedan anular los props predeterminados.
      return <WrappedComponent {...themeProps} {...(this.props as T)} />;
    }
  };
}
```

Tenga en cuenta que la aserción `{...this.props as T}` es necesaria debido a un error en TS 3.2 https://github.com/Microsoft/TypeScript/issues/28938#issuecomment-450636046

Para obtener detalles de `Optionalize` consulte la [sección de tipos de utilidad](https://github.com/typescript-cheatsheets/typescript-utilities-cheatsheet#utility-types)

Aquí hay un ejemplo más avanzado de un Componente Dinámico de Orden Superior (HOC por las siglas en inglés de higher-order component) que basa algunos de sus parámetros en los _props_ del componente que está siendo pasado.

```tsx
// Inyecta valores estáticos a un componente de tal manera que siempre son proporcionados.
export function inject<TProps, TInjectedKeys extends keyof TProps>(
  Component: React.JSXElementConstructor<TProps>,
  injector: Pick<TProps, TInjectedKeys>
) {
  return function Injected(props: Omit<TProps, TInjectedKeys>) {
    return <Component {...(props as TProps)} {...injector} />;
  };
}
```

### Usando `forwardRef`

Para una reutilización "verdadera", también debes considerar exponer una referencia para tus HOC. Puedes utilizar `React.forwardRef<Ref, Props>` cómo está documentado en [el cheatsheet básico](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/blob/master/README.md#forwardrefcreateref), pero estamos interesados en más ejemplos del mundo real. [Aquí hay un buen ejemplo en práctica](https://gist.github.com/OliverJAsh/d2f462b03b3e6c24f5588ca7915d010e) de @OliverJAsh.

# Sección 1: Documentación de React sobre HOC en TypeScript

En esta primera sección nos referimos de cerca a [la documentación de React sobre HOC](https://es.reactjs.org/docs/higher-order-components.html) y ofrecemos un paralelo directo en TypeScript.

## Ejemplo de la documentación: [Usa HOCs para preocupaciones transversales](https://es.reactjs.org/docs/higher-order-components.html#usa-hocs-para-preocupaciones-transversales)

<details>

<summary>
<b>Variables a las que se hace referencia en el siguiente ejemplo</b>
</summary>

```tsx
/** Componentes hijos ficticios que pueden recibir cualquiera cosa */
const Comment = (_: any) => null;
const TextBlock = Comment;

/** Data ficticia */
type CommentType = { text: string; id: number };
const comments: CommentType[] = [
  {
    text: "comment1",
    id: 1
  },
  {
    text: "comment2",
    id: 2
  }
];
const blog = "blogpost";

/** simulación de la data */
const DataSource = {
  addChangeListener(e: Function) {
    // Hace algo
  },
  removeChangeListener(e: Function) {
    // Hace algo
  },
  getComments() {
    return comments;
  },
  getBlogPost(id: number) {
    return blog;
  }
};
/** Escriba alias solo para deduplicar */
type DataType = typeof DataSource;
// type TODO_ANY = any;

/** Tipos de utilidad que utilizamos */
type Omit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>;
// type Optionalize<T extends K, K> = Omit<T, keyof K>;

/** Componentes reescritos de la documentación de React que solo utilizan props inyectados */
function CommentList({ data }: WithDataProps<typeof comments>) {
  return (
    <div>
      {data.map((comment: CommentType) => (
        <Comment comment={comment} key={comment.id} />
      ))}
    </div>
  );
}
interface BlogPostProps extends WithDataProps<string> {
  id: number;
  // children: ReactNode;
}
function BlogPost({ data, id }: BlogPostProps) {
  return (
    <div key={id}>
      <TextBlock text={data} />;
    </div>
  );
}
```

[Ver en TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCgeirhgAskBnJOFIuxuMHMJuiHABGrYADsAVkgxIAJsICenVgAkA8gGEK4mEiiZ0rAOrAGAERQwUABV5MAPABUAfHADeFOHFmWUALjhHAG44Gm9fOGB+AHMkMT1gNAoAX2paR0j+BlYYBTBWCExwqzS4a0zlbjs4QsqAdygUMHz5NFxIeLF4BksK8Uw9IllSjQrstgwAVxQAG0iuvQM0AqLxhqaWuDbwCE74AApJlnkYQWjGoW8kA0mZmFsIPjhsXEiYAEoKJAAPSFhnyZiDDAXZwOqmegAZUmQiYaCgwDAMBBYicABoynAfroxLJ+CZzL4HnwnM4MRpnPtPKFaAwonQ8qxZjMIHV+EcBPMBlAyhihJN4OcUJdxrl8jUikZGs05Bp2rs4vAWGB2JYkDMlOCGBABW95rp9AkxNEwRDKv09HFlhKytSpRtZfK9gFkOgYAA6ABSkIAGgBRGZIECKuViJgwKCTDDQezWVwAMjgGjR1LCLEDGAsVgqKABQNOPMw0ECqdoPEe-Hprtkuw1wmkKCOohg+H4RBQNbEdfETGAshWlTQMxQTCY1PT0hgWf8cCp5C8Xh8VkhOqgywCYqQtWnK8ma6QKfnC-LfBdqE7Gvs3p97oAMsAhI0oAoALIoMQoWKyACCMAjD4FZh7GTOA1BAUxYwxAAiJcUCg5wEOpd44AAXlcRwKGQjwjzCcYQE-RIKkYIgAmvO8HyfV930-ORf3-fldH4cEZjmKwAGsci4TcbXtFo5R2PY2FxOAiCYCAZgAN2bfh+xuO4qgrUs2GiFAe26LgT34WoCXoacMTqehEnoCoJCOdSCgRaJxFmTFuK1Yz8Fg-ARKDCApPkF48FMNskAAR0mYAiGDLoxyPbjiX4FC4DI+9H3YKiPy-OiEQYoCQLAiDrGg2D4OcIJqW4yErF0VD3GpRdfACYJqWSfKjyIGA9zELZh1HOAdOnLFvhxPFEGID1+I6RVYzsDEirVVxsIXLZdnDSNoygfZNICCKsPKhcmEmfJFs0946umrw6SYd16HfWRAw0U7jVYKKjpOs6Lqu2J3SEcRZH2I69vWw7DOO8M1VKqaDoqqwAgnTNfH2HdV2WDFdu+uBavW1JKCPLxtiGrozD7F8dS6Ur9mQtC4GhvdlndDtZEu99YnvcM4j0D7fvu3FHpppAvtR6aMYVLoTBYgBVMQQDx+AosJ1DnAR0n93dIK3KQanrrpnFGbuq7zsVp6Obq9aNbZ66CaJqW0YXO6WBgcbdH2IHgdgsH1Unacod8Xd9wxO74dNrxkk59aiFxRm1u9mlKjFcQTSLHkmB4c8I84KJ3U0zJ3VTuApOfGbwEDb53XrcMwRQJRLPoeAxFZMZBFMgvuNMNh+HfBQEbCWDTRYuBw2AduRAZfI0EYNAOOGEOGqa2cEa8exeL4p1FWKFAULcc3iqQd1YOSdxU-dJnE+TkchIUd4N6oE3gc56aUZ9-bQ9HqBmo63w6pR6gACoX7gdRRiOGjTQYJNZ5CnAF+VAvi-GgPANoYZ4D8WCjAFWOloSwnhIiZEoIor2UQXCBESIURzi8DAxUKtDxeBdsuGGSAAjTkcIyY2JNXbkPdLEGABCQqE0wrrcgPw-gQNmvAAAQiyaI1gIDhgQTCLBKCUSlQweI5BODdh4LgAIiAQiREwGIbOGW646FWGofkOGdgAgZRgPYZRqjwwRWyr4eCxt1paNXkwsxwjwxLTsO6PsnxyB7SAA)

</details>

Ejemplo de un HOC de la documentación de React traducido a TypeScript

```tsx
// Estos son los props que serán inyectados por el HOC
interface WithDataProps<T> {
  data: T; // data es genérico
}
// T es el tipo de data
// P son los props del componente envuelto que es inferido
// C es la interfaz real del componente envuelto (utilizado para tomar los defaultProps)
export function withSubscription<T, P extends WithDataProps<T>, C>(
  // este tipo nos permite inferir P, pero toma el tipo de componente envuelto por separado sin que interfiera con la inferencia en P
  WrappedComponent: React.JSXElementConstructor<P> & C,
  // selectData es un functor para T
  // los props son solo de lectura porque son solo lectura dentro de la clase
  selectData: (
    dataSource: typeof DataSource,
    props: Readonly<JSX.LibraryManagedAttributes<C, Omit<P, "data">>>
  ) => T
) {
  // the magic is here: JSX.LibraryManagedAttributes will take the type of WrapedComponent and resolve its default props
  // against the props of WithData, which is just the original P type with 'data' removed from its requirements
  type Props = JSX.LibraryManagedAttributes<C, Omit<P, "data">>;
  type State = {
    data: T;
  };
  return class WithData extends React.Component<Props, State> {
    constructor(props: Props) {
      super(props);
      this.handleChange = this.handleChange.bind(this);
      this.state = {
        data: selectData(DataSource, props)
      };
    }

    componentDidMount = () => DataSource.addChangeListener(this.handleChange);

    componentWillUnmount = () =>
      DataSource.removeChangeListener(this.handleChange);

    handleChange = () =>
      this.setState({
        data: selectData(DataSource, this.props)
      });

    render() {
      // la escritura para difundir this.props es... muy compleja. La mejor manera de hacerlo ahora mismo es escribirlo cómo `any`
      // data todavia sera verificada
      return (
        <WrappedComponent data={this.state.data} {...(this.props as any)} />
      );
    }
  };
  // return WithData;
}

/** Uso de HOC con Componentes */
export const CommentListWithSubscription = withSubscription(
  CommentList,
  (DataSource: DataType) => DataSource.getComments()
);

export const BlogPostWithSubscription = withSubscription(
  BlogPost,
  (DataSource: DataType, props: Omit<BlogPostProps, "data">) =>
    DataSource.getBlogPost(props.id)
);
```

## Ejemplo de documentación: [No mutes el componente original. Usa composición.](https://es.reactjs.org/docs/higher-order-components.html#no-mutes-el-componente-original-usa-composici%C3%B3n)

Es bastante sencillo - asegurate de comprobar los _props_ recibidos cómo `T` [debido al error TS 3.2](https://github.com/Microsoft/TypeScript/issues/28938#issuecomment-450636046).

```tsx
function logProps<T>(WrappedComponent: React.ComponentType<T>) {
  return class extends React.Component {
    componentWillReceiveProps(
      nextProps: React.ComponentProps<typeof WrappedComponent>
    ) {
      console.log("Current props: ", this.props);
      console.log("Next props: ", nextProps);
    }
    render() {
      // Envuelve el componente de entrada en un contenedor sin mutarlo. Muy bien!
      return <WrappedComponent {...(this.props as T)} />;
    }
  };
}
```

## Ejemplo de la documentación: [Pasa los _props_ no relacionados al componente envuelto](https://es.reactjs.org/docs/higher-order-components.html#convenci%C3%B3n-pasa-los-props-no-relacionados-al-componente-envuelto)

No se necesitan consejos específicos de Typescript aquí.

## Ejemplo de la documentación: [Maximizar la componibilidad](https://es.reactjs.org/docs/higher-order-components.html#convenci%C3%B3n-maximizar-la-componibilidad)

los HOC pueden tomar la forma de funciones que retornan Componentes de Orden Superior que devuelven Componentes

la función `connect` de `react-redux` tiene una serie de sobrecargas del que puedes obtener inspiración [fuente](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/bc0c933415466b34d2de5790f7cd6418f676801e/types/react-redux/v5/index.d.ts#L77)

Construiremos nuestro propio `connect` para entender los HOC:

<details>

<summary>
<b>Variables a las que se hace referencia en el siguiente ejemplo:</b>
</summary>

```tsx
/** tipos de utilidad que utilizamos */
type Omit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>;

/** datos ficticios */
type CommentType = { text: string; id: number };
const comments: CommentType[] = [
  {
    text: "comment1",
    id: 1
  },
  {
    text: "comment2",
    id: 2
  }
];
/** componentes ficticios que reciben cualquier cosa */
const Comment = (_: any) => null;
/** Componentes reescritos de la documentación de React que solo utilizan props de datos inyectados **/
function CommentList({ data }: WithSubscriptionProps<typeof comments>) {
  return (
    <div>
      {data.map((comment: CommentType) => (
        <Comment comment={comment} key={comment.id} />
      ))}
    </div>
  );
}
```

</details>

```tsx
const commentSelector = (_: any, ownProps: any) => ({
  id: ownProps.id
});
const commentActions = () => ({
  addComment: (str: string) => comments.push({ text: str, id: comments.length })
});

const ConnectedComment = connect(
  commentSelector,
  commentActions
)(CommentList);
// prop que son inyectadas por el HOC.
interface WithSubscriptionProps<T> {
  data: T;
}
function connect(mapStateToProps: Function, mapDispatchToProps: Function) {
  return function<T, P extends WithSubscriptionProps<T>, C>(
    WrappedComponent: React.ComponentType<T>
  ) {
    type Props = JSX.LibraryManagedAttributes<C, Omit<P, "data">>;
    // Creando el componente interno. El tipo de propiedades calculadas, es donde ocurre la magia
    return class ComponentWithTheme extends React.Component<Props> {
      public render() {
        // Obten los props que desea inyectar. Esto podría hacerse con context
        const mappedStateProps = mapStateToProps(this.state, this.props);
        const mappedDispatchProps = mapDispatchToProps(this.state, this.props);
        // this props viene después de tal modo que anula los predeterminados
        return (
          <WrappedComponent
            {...this.props}
            {...mappedStateProps}
            {...mappedDispatchProps}
          />
        );
      }
    };
  };
}
```

[Ver en el TypeScript Playground](https://www.typescriptlang.org/play/?jsx=2#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgcilQ3wFgAoCtCAOwGd5qQQkaY64BeOAbQF0A3BSq0GcAMK4WbADLAx3ABQBKLgD44iinDgAeACbAAbnAD0aisuHlq9RlNYwAykgA2SDNC6aA+gC44FBoATwAaOAgAdxoABRwwOgCg4NVODUUAb204YH0AqNj4ugA6XIoAX2UhG1F7ZkcAQQxgUW8VdU0s8h0UfX1JerYAxQYoANHgGgBzVI0maXZisABXOgALTLgYJAAPGHGYKHDcgPnHEvdpmDW4Soqq61sxSRoaD23+hzZvWzeMLW6cDObBc7k8R2ywJgTRgLXolkUAwWcgYD0o5FMpi2ayQdCQgSI2PxYCKWwgcAARvjJgArd5IfSU4JEuAACQA8uIKJNtlBMOh8QB1YDXJzLCl0NBQYBgWG0OIQBK6AAqGi6On0KBgKACyuq5QomGWNGatCBtD+MEUIBQYCc2u2yogCoSAQAYsbTTRwjawAAReRgLVoNZOl2JOAek1ymiqdVwIgwZZQGhwI3RuEq8IxOC7bY0fQcYWi8WS6WyuHhlVqcLiNQAnQ6QVQW1gBkDSBvIaIYgwYod2iOZXBNvV7Jx7I6GAj-Hh7wAKScAA1inIKS2oMEALJBFBTBkNGCHYAU5bbOi6cThdkgEW6GLhABEmu1j7UamqjbMWPERC1kymFlJjeKBzXAQc2GKOBlRxIEUFcNBllcLUGTgOdpzbOAcUJeQWUibD8WufEbSmYA0Cw1tWBKScEyQJMUyBZC6A4AcuxgYtQxxFhcz2VhCx7dA+1Yxx7yKNUaJ0FYKVcMjaILJAoHaeMvx0TFIzokMWRJRUOGCCBljgSIgngWl3igmDcOoJDGSpOB9EHQyRRuWxtj2HI7FQfRigkxsnngX0230e0ULnbhfWCx1nSKRRrnkYoGBQ8JYpKbSEjRFTfNqOAAoZAM6CDGAQ1C7LbTygqQzDaLkvih0kCStY4tSuh0oy79sUa0kmFxQJMF5IyoH4uhySIuDUwgIwFOlfRCNg6b+SQ+BB2owEMsTZNUwbVqdF0ZtKM+cC2J8jKMmKU7qqag0Vq2uATtOnKgtq8NLuuxtbuKe6yuDNYnqOxtzF+lqv2extyk-W59SAA)

## Ejemplo de la documentación: [Envuelve el nombre a mostrar para una depuración fácil](https://es.reactjs.org/docs/higher-order-components.html#convenci%C3%B3n-envuelve-el-nombre-a-mostrar-para-una-depuraci%C3%B3n-f%C3%A1cil)

Este es bastante sencillo

```tsx
interface WithSubscriptionProps {
  data: any;
}

function withSubscription<
  T extends WithSubscriptionProps = WithSubscriptionProps
>(WrappedComponent: React.ComponentType<T>) {
  class WithSubscription extends React.Component {
    /* ... */
    public static displayName = `WithSubscription(${getDisplayName(
      WrappedComponent
    )})`;
  }
  return WithSubscription;
}

function getDisplayName<T>(WrappedComponent: React.ComponentType<T>) {
  return WrappedComponent.displayName || WrappedComponent.name || "Component";
}
```

## No escrito: [sección de consideraciones](https://es.reactjs.org/docs/higher-order-components.html#consideraciones)

- No utilice HOCs dentro del método render
- Los métodos estáticos deben ser copiados
- Las Refs no son pasadas

# sección 2: Excluyendo Props

Esto es cubierto en la sección 1 pero aquí nos centraremos en el ya que es un problema muy común. Los HOC a menudo inyectan _props_ a componentes pre-fabricados. El problema que queremos resolver es que el componente envuelto en HOC exponga un tipo que refleje el área de superficie reducida de los _props_ - sin tener que volver a escribir manualmente el HOC cada vez. Esto implica algunos genericos, afortunadamente con algunas utilidades auxiliares.

Digamos que tenemos un componente

```tsx
type DogProps {
  name: string
  owner: string
}
function Dog({name, owner}: DogProps) {
  return <div> Woof: {name}, Owner: {owner}</div>
}
```

Y tenemos un HOC `withOwner` que inyecta el `owner`:
And we have a `withOwner` HOC that injects the `owner`:

```tsx
const OwnedDog = withOwner("swyx")(Dog);
```

Queremos escribir `withOwner` de tal modo que pase por los tipos de cualquier componente cómo `Dog`, en el tipo de `OwnedDog`, menos la propiedad `owner` que inyecta:

```tsx
typeof OwnedDog; // queremos que sea igual a { name: string }

<Dog name="fido" owner="swyx" />; // este debe estar bien
<OwnedDog name="fido" owner="swyx" />; // este debe tener un typeError
<OwnedDog name="fido" />; // este debe estar bien

// y el HOC debe ser reusable por tipos de props totalmente diferentes!

type CatProps = {
  lives: number;
  owner: string;
};
function Cat({ lives, owner }: CatProps) {
  return (
    <div>
      {" "}
      Meow: {lives}, Owner: {owner}
    </div>
  );
}

const OwnedCat = withOwner("swyx")(Cat);

<Cat lives={9} owner="swyx" />; // este debe estar bien
<OwnedCat lives={9} owner="swyx" />; // este debe tener un typeError
<OwnedCat lives={9} />; // este debe estar bien
```

Entonces, cómo escribimos `withOwner`?

1. Obtenemos los tipos del componente: `keyof T`
2. Nosotros `Exclude` las propiedades que queremos encamascarar: `Exclude<keyof T, 'owner'>`, esto te deje con una lista de nombre de propiedades que quieres en el componente envuelto ejm: `name`
3. (Opcional) Utilice los tipo de intersección sí tiene mas para excluir: `Exclude<keyof T, 'owner' | 'otherprop' | 'moreprop'>`
4. Los nombres de las propiedades no son exactamente iguales a las propiedades en sí, los cuales también tienen un tipo asociado. Así que utilizamos esta lista generada de nombre para elegir `Pick` de los _props_ originales: `Pick<keyof T, Exclude<keyof T, 'owner'>>`, this leaves you with the new, filtered _props_, e.g. `{ name: string }`
5. (opcional) En lugar de escribir esto manualmente cada vez, podemos utilizar esta utilidad: `type Omit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>`
6. Ahora escribimos el HOC cómo un función genérica:

```tsx
function withOwner(owner: string) {
  return function<T extends { owner: string }>(
    Component: React.ComponentType<T>
  ) {
    return function(props: Omit<T, "owner">): React.ReactNode {
      return <Component owner={owner} {...props} />;
    };
  };
}
```

_Nota: el de arriba es un ejemplo incompleto y no funcional. PR una solución!_

## Aprende más

Tendremos que extraer las lecciones de aquí en el futuro pero aquí estan:

- https://medium.com/@xfor/typescript-react-hocs-context-api-cb46da611f12
- https://medium.com/@jrwebdev/react-higher-order-component-patterns-in-typescript-42278f7590fb
- https://www.matthewgerstman.com/tech/ts-tricks-higher-order-components/
