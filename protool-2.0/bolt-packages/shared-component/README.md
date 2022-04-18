# Shared component

What should be a basic shared component looks like?



In protool 2.0, we have defined a component as the structure below:

```
component
|
|--styles--base.scss
|    |-----_en_ZA.scss
|    |-----_es_MX.scss
|
|--l10n--en_ZA.ts
|    |---es_mx.ts
|
|--__test__---index.test.tsx
|
|--index.tsx
|
|--utils.ts
|
|--config.ts

```

As protool at very beginning is designed for multi-tenant, So the style and the language is different, so for a component:

1. &#x20;different and reusable styles  ---- styles folder
2. different languages support  ----- l10n folder
3. UT  ----- test folder
4. main component structure ----`index.ts` file or other support files
5. &#x20;the utils to support he component working ---- `utils.ts`
6. some configure files&#x20;



This is the header component

![](<../../../.gitbook/assets/image (3).png>)





As this is the basic block of the whole system, so I will explain the detail it in several other topic:

1. [i18next](i18next.md)
2. [SCSS vs module css](scss-vs-module-css.md)
3. [Functional Component ](functional-component.md)

