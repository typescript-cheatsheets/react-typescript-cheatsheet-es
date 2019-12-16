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

- Inicialmente haremos un mapa detallado de la [documentación oficial sobre HOC](https://reactjs.org/docs/higher-order-components.html).
- Si bien existen hooks, muchas librerias y bases de código aún necesitan escribir HOC
- Render props podrian ser considerado en el futuro
- El objetivo es escribir HOC que ofrezcan un tipado seguro sin interferir

---

### HOC Cheatsheet Tabla de Contenido

<details>

<summary><b>Expandir Tabla de Contenido</b></summary>

- [Sección 0: Ejemplo completo de un HOC](#section-0-full-hoc-example)
- [Sección 1: Documentación de React sobre HOC en TypeScript](#section-1-react-hoc-docs-in-typescript)
- [Sección 2: Excluyendo Props](#section-2-excluding-props)

  </details>

# Sección 0: Ejemplo completo de un HOC

> Este es un ejemplo de un HOC para copiar y pegar. Si ciertos pedazos no tienen sentido para ti, ve a la [Sección 1](#section-1-react-hoc-docs-in-typescript) para obtener un tutorial detallado a través de una traducción completa de la documentación de React en Typescript.

A veces quieres una forma sencilla de pasar props desde otro lugar (ya sea el store global o un provider) y no quieres continuamente pasar los props hacia abajo. Context es excelente para eso, pero entonces los valores desde el context solo pueden ser usado desde tu función `render`. Un HOC proveerá esos valores como props.

**Los props inyectados**

```ts
interface WithThemeProps {
  primaryColor: string;
}
```

**Uso en el componente**

El objetivo es tener los props disponibles en la interfaz para el componente, pero sustraído para los consumidores del componente cuando estén envuelto en el HoC.

```ts
interface Props extends WithThemeProps {
  children: React.ReactNode;
}

class MyButton extends React.Component<Props> {
  public render() {
    // Renderiza un elemento usando el tema y otros props.
  }

  private someInternalMethod() {
    // Los valores del tema tambien estan aqui disponibles como props.
  }
}

export default withTheme(MyButton);
```

**Consumiendo el componente**

Ahora, al consumir el componente puedes omitir el prop `primaryColor` o anular el que fue proporcionado a través del context.

```tsx
<MyButton>Hello button</MyButton> // Valido
<MyButton primaryColor="#333">Hello Button</MyButton> // Tambien valido
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

  // Creando el component interno. El tipo de prop calculado aqui es donde ocurre la magia.
  return class ComponentWithTheme extends React.Component<
    Optionalize<T, WithThemeProps>
  > {
    public static displayName = `withPages(${displayName})`;

    public render() {
      // Obten los props que quiere inyectar. Esto podria ser hecho con context.
      const themeProps = getThemePropsFromSomeWhere();

      // this.props viene despues para que puedan anular los props predeterminados.
      return <WrappedComponent {...themeProps} {...(this.props as T)} />;
    }
  };
}
```
Tenga en cuenta que la aserción `{...this.props as T}` es necesaria debido a un error en TS 3.2 https://github.com/Microsoft/TypeScript/issues/28938#issuecomment-450636046

Para obtener detalles de `Optionalize` consulte la [sección de tipos de utilidad](https://github.com/typescript-cheatsheets/typescript-utilities-cheatsheet#utility-types)


Aquí hay un ejemplo más avanzado de un Componente Dinámico de Orden Superior (HOC por las siglas en inglés de higher-order component) que basa algunos de sus parametros en los props del componente que está siendo pasado.

```tsx
// Inyecta valores estaticos a un componente de tal manera que siempre son proporcionados.
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
Para una reutilización "verdadera", tambien debes considerar exponer una referencia para tus HOC. Puedes utilizar `React.forwardRef<Ref, Props>` como está documentado en [el cheatsheet basico](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/blob/master/README.md#forwardrefcreateref), pero estamos interesados en más ejemplos del mundo real. [Aquí hay un buen ejemplo en práctica](https://gist.github.com/OliverJAsh/d2f462b03b3e6c24f5588ca7915d010e) de @OliverJAsh.