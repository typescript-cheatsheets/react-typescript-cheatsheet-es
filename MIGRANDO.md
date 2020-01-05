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
[**Avanzado**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/blob/master/AVANZADO.md) |
[**Migrando**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/blob/master/MIGRATING.md) |
[**HOC**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/blob/master/HOC.md) |
[**Inglés**](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet) |
[**中文翻译**](https://github.com/fi3ework/blog/tree/master/react-typescript-cheatsheet-cn) |
[Contribuir](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/blob/master/CONTRIBUYENDO.md) |
[Preguntas](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet-es/issues/new)

</div>

---

# Migrando (a TypeScript) Cheatsheet

Este Cheatsheet recopila consejos y utilidades de casos de estudios reales de equipos que mueven bases de código significativas de JS plano o Flow a Typescript. Esto no intenta _convencer_ a la gente para que lo haga, pero recopilamos las pocas estadísticas que ofrecen las empresas después de su experiencia de migración.

> ⚠️ Este Cheatsheet es extremadamente nuevo y podría usar toda la ayuda que podamos obtener. Consejos sólidos, resultados, y contenido actualizado son bienvenidos.

## Prerrequisitos
Leer la [Guía oficial de TypeScript para migrar desde JS](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html) y también deberías estar familiarizado con la [Guía de conversión de React](https://github.com/Microsoft/TypeScript-React-Conversion-Guide#typescript-react-conversion-guide).

## Enfoques de conversión general

- Nivel 0: No uses TypeScript, usa JSDoc
  - Mira nuestra [seccion de JSDoc](#JSDoc)
- Nivel 1A: JavaScript mayoritario, TypeScript cada vez más estricto
  - como recomienda la [guía oficial de TS](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)
  - usa `allowJS` (Experiencias: [clayallsop][clayallsop], [pleo][pleo])
- Nivel 1B: Renombrar todo a TypeScript desde el principio
  - "[Just rename all .js files to .ts](https://twitter.com/jamonholmgren/status/1089241726303199232)"?
  - usa lo mas simple, la configuración mas mínima para comenzar
- Nivel 2: TypeScript estricto
  - usa [`dts-gen`](https://github.com/Microsoft/dts-gen) de Microsoft para generar archivos `.d.ts` para tus archivos sin tipo. [Esta respuesta de SO](https://stackoverflow.com/questions/12687779/how-do-you-produce-a-d-ts-typings-definition-file-from-an-existing-javascript) tiene mas información sobre el tema.
  - usa la palabra clasve `declare` para declaraciones de ambiente - mira la [declaración de fusión](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet#troubleshooting-handbook-bugs-in-official-typings) para parchear declaraciones de biblioteca en línea.

Varios consejos/enfoques que las empresas exitosas han tomado

- `@ts-ignore` en errores del compilador para librerias sin typedefs.
- elije ESLint sobre TSLint (fuente: [ESLint](https://eslint.org/blog/2019/01/future-typescript-eslint) y [TS Roadmap](https://github.com/Microsoft/TypeScript/issues/29288)). [Puedes convertir TSlint a ESlint con esta herramienta](https://github.com/typescript-eslint/tslint-to-eslint-config).
- El nuevo código siempre de escribirse en TypeScript. Sin excepciones. Para el código existente: Si tu tarea requiere cambiar el código JavaScript, debes volverlo a escribir. (Source: [Hootsuite][hootsuite])

<details>
<summary>
<b>
Consejos para Webpack
</b>
</summary>

- webpack loader: `awesome-typescript-loader` vs `ts-loader`? (Hay un cierto desacuerdo en la comunidad sobre esto - pero lee [awesome's point of view](https://github.com/s-panferov/awesome-typescript-loader#differences-between-ts-loader))
- configuración de Webpack:

```js
module.exports = {

resolve: {
-    extensions: ['.js', '.jsx']
+    extensions: ['.ts', '.tsx', '.js', '.jsx']
},

// Soporte para source maps ('inline-source-map' también funciona)
devtool: 'source-map',

// Añadir el loader para archivos .ts.
module: {
  loaders: [{
-       test: /\.jsx?$/,
-       loader: 'babel-loader',
-       exclude: [/node_modules/],
+       test: /\.(t|j)sx?$/,
+       loader: ['awesome-typescript-loader?module=es6'],
+       exclude: [/node_modules/]
+   }, {
+       test: /\.js$/,
+       loader: 'source-map-loader',
+       enforce: 'pre'
  }]
}
};
```

Nota especial sobre `ts-loader` y librerias de terceros: https://twitter.com/acemarke/status/1091150384184229888

</details>

## JSDoc

- https://github.com/Microsoft/TypeScript/wiki/JsDoc-support-in-JavaScript
- El código base de webpack usa JSDoc con linting de TS https://twitter.com/TheLarkInn/status/984479953927327744 (un truco loco: https://twitter.com/thelarkinn/status/996475530944823296)

Problemas a tener en cuenta:

- `object` se convierte a `any` por alguna razón.
- Si tiene un error en el JSDoc, no recibes ningún warning/error. TS just silently doesn't type annotate the function.
- [El casteo puede ser detallado](https://twitter.com/bahmutov/status/1089229349637754880)

(_gracias [Gil Tayar](https://twitter.com/giltayar/status/1089228919260221441) y [Gleb Bahmutov](https://twitter.com/bahmutov/status/1089229196247908353) por compartir el comentario anterior_)

## Desde JS

### Conversión automatizada de JS a TS

- [TypeStat](https://github.com/JoshuaKGoldberg/TypeStat) ([usado por Codecademy](https://mobile.twitter.com/JoshuaKGoldberg/status/1159090281314160640))
- [TypeWiz](https://github.com/urish/typewiz)
- [js-to-ts-converter](https://github.com/gregjacobs/js-to-ts-converter)

### Conversión manual de JS a TS 

la estrategia de "Solo renombra"

- OSX/Linux: `find src -name "*.js" -exec sh -c 'mv"$0" "${0%.js}.tsx"' {} \;`

Puede cargar archivos de TypeScript con webpack o usar el compilador `tsc` para compilar sus archivos TS en JS uno al lado del otro. El `tsconfig.json` básico es:

```json
{
  "compilerOptions": {
    "allowJs": true
  }
}
```

Luego querrás habilitarlo para validar JS:

```json
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": true
  }
}
```

Si tiene una base de código grande y arroja demasiados errores a la vez, puedes optar por excluir archivos problemáticos con `//@ts-nocheck` o en su lugar desactivar `checkJs` y agregar una directiva `// @ ts-check` en la parte superior de cada archivo JS normal.

TypeScript debería arrojar algunos errores atroces aquí que deberían ser fáciles de solucionar.

Una vez que haya terminado, trague la píldora roja apagando los `any` implícitos:

```js
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": true,
    "noImplicitAny": true // o "strict": true
  }
}
```

Esto generará un montón de errores de tipo y puedes comenzar a convertir archivos a TS u (opcionalmente) usar [anotaciones JSDoc](https://www.typescriptlang.org/docs/handbook/type-checking-javascript-files.html) en tu JS.


Una práctica común es usar alias de tipo TODO para `any`, para que puedas hacer un seguimiento de lo que necesita hacer luego.

```ts
type TODO_TYPEME = any;
export function myFunc(foo: TODO_TYPEME, bar: TODO_TYPEME): number {
  // ...
}
```

Gradualmente agrega [mas banderas de modo `strict`](https://www.typescriptlang.org/docs/handbook/compiler-options.html) como `noImplicitThis`, `strictNullChecks`, y así sucesivamente hasta que finalmente pueda correr por completo en modo estricto sin que queden archivos js:

```js
{
  "compilerOptions": {
    "strict": true
  }
}
```

**Más recursos**

- [Adopting TypeScript at Scale - AirBnB's conversion story and strategy](https://www.youtube.com/watch?v=P-J9Eg7hJwE)
- [Migrating a `create-react-app`/`react-scripts` app to TypeScript](https://facebook.github.io/create-react-app/docs/adding-typescript) - don't use `react-scripts-ts`
- [Migrating an EJECTED CRA app to TS](https://spin.atomicobject.com/2018/07/04/migrating-cra-typescript/)
- [Lyft's JS to TS migration tool](https://github.com/lyft/react-javascript-to-typescript-transform) (includes PropTypes migration)
- [Hootsuite][hootsuite]
- [Storybook's migration (PR)](https://github.com/storybooks/storybook/issues/5030)
- [How we migrated a 200K+ LOC project to TypeScript and survived to tell the story][coherentlabs] - Coherent Labs - using `grunt-ts`, jQuery and Kendo UI

Contenido antiguo que posiblemente esté desactualizado

- [Incrementally Migrating JS to TS][clayallsop] (old)
- [Microsoft's TypeScript React Conversion Guide][mstsreactconversionguide] (old)

## Desde Flow

- Try flow2ts: `npx flow2ts` - doesn't work 100% but saves some time ([mira este y otros tips de @braposo](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet/pull/79#issuecomment-458227322) at TravelRepublic)
- [Incremental Migration to TypeScript on a Flowtype codebase][entria] at Entria
- [MemSQL's Studio's migration](https://davidgom.es/porting-30k-lines-of-code-from-flow-to-typescript/) - blogpost con muchos tips útiles
- Retail-UI's Codemod: https://github.com/skbkontur/retail-ui/tree/master/packages/react-ui-codemodes/flow-to-ts
- Quick-n-dirty [Flow to TS Codemod](https://gist.github.com/skovhus/c57367ce6ecbc3f70bb7c80f25727a11)
- [Ecobee's brief experience](https://mobile.twitter.com/alanhietala/status/1104450494754377728)
- [Migrating a 50K SLOC Flow + React Native app to TypeScript](https://blog.usejournal.com/migrating-a-flow-react-native-app-to-typescript-c74c7bceae7d)

## Resultados

- El número de despliegues de producción se duplicó para [Hootsuite][hootsuite]
- Se encontraron globals accidentales para [Tiny][tiny]
- Se encontraron llamadas a funciones incorrectas para [Tiny][tiny]
- Se encontró un código de error poco utilizado que no se probó [Tiny][tiny]

## Estudios Académicos de Migración

- [To Type or Not to Type: Quantifying Detectable Bugs in JavaScript](http://earlbarr.com/publications/typestudy.pdf)

> Nuestro hallazgo central es que ambos sistemas de tipos estáticos encuentran un porcentaje importante de errores públicos: tanto Flow 0.30 como TypeScript 2.0 detectan con éxito el 15%.

## Diversas historias de migración de compañías notables y fuentes abiertas


- [Adopting TypeScript at Scale - AirBnB's conversion story and strategy](https://www.youtube.com/watch?v=P-J9Eg7hJwE)
- [Lyft](https://eng.lyft.com/typescript-at-lyft-64f0702346ea)
- [Google](http://neugierig.org/software/blog/2018/09/typescript-at-google.html)
- [Tiny][tiny] - [Talk from ForwardJS here](https://www.slideshare.net/tiny/porting-100k-lines-of-code-to-typescript)
- [Slack](https://slack.engineering/typescript-at-slack-a81307fa288d) ([podcast](https://softwareengineeringdaily.com/2017/08/11/typescript-at-slack-with-felix-rieseberg/))
- [Priceline](https://medium.com/priceline-labs/trying-out-typescript-part-1-15a5267215b9)
- Dropbox - [Talk at React Loop](https://www.youtube.com/watch?v=veXkJq0Z2Qk)

Código abierto

- [Jest's migration (PR)](https://github.com/facebook/jest/pull/7554#issuecomment-454358729)
- [Expo's migration (issue)](https://github.com/expo/expo/issues/2164)
- [Google Workbox migration](https://github.com/GoogleChrome/workbox/pull/2058)
- [Atlassian's migration (PR)](https://github.com/atlassian/react-beautiful-dnd/issues/982)
- [Yarn's migration (issue)](https://github.com/yarnpkg/yarn/issues/6953)
- [React Native CLI](https://github.com/react-native-community/cli/issues/683)
- [Next.js](https://nextjs.org/blog/next-9)
- [Redux](https://github.com/reduxjs/redux/pull/3536)

## Enlaces

[hootsuite]: https://medium.com/hootsuite-engineering/thoughts-on-migrating-to-typescript-5e1a04288202 "Thoughts on migrating to TypeScript"
[clayallsop]: https://medium.com/@clayallsopp/incrementally-migrating-javascript-to-typescript-565020e49c88 "Incrementally Migrating JavaScript to TypeScript"
[pleo]: https://medium.com/pleo/migrating-a-babel-project-to-typescript-af6cd0b451f4 "Migrating a Babel project to TypeScript"
[mstsreactconversionguide]: https://github.com/Microsoft/TypeScript-React-Conversion-Guide "TypeScript React Conversion Guide"
[entria]: https://medium.com/entria/incremental-migration-to-typescript-on-a-flowtype-codebase-515f6490d92d "Incremental Migration to TypeScript on a Flowtype codebase"
[coherentlabs]: https://hashnode.com/post/how-we-migrated-a-200k-loc-project-to-typescript-and-survived-to-tell-the-story-ciyzhikcc0001y253w00n11yb "How we migrated a 200K+ LOC project to TypeScript and survived to tell the story"
[tiny]: https://go.tiny.cloud/blog/benefits-of-gradual-strong-typing-in-javascript/ "Benefits of gradual strong typing in JavaScript"