# i18next/react

As Protool 2.0 is design for both MX and ZA at very beginning. To render different language for the component is one of the problem to be considered. But it is cool that React tech stack get some solution about language part.



Let me first show the folder of l10n:

![](<../../../.gitbook/assets/image (6) (1) (1).png>)

Each page has it's own translate folder and some common translate is put into common file. The common file is also the default `namespace` for translate function.



For each file:

![](<../../../.gitbook/assets/image (7) (1).png>)

It imports the language from the required component.&#x20;



The technology we used is:

### i18next

i18next is the project to solve the problem for js. It support plurals, interpolation very well.

more details : [https://www.i18next.com/](https://www.i18next.com/)



But actually, we are not direct use `i18next` but use [`i18next-react`](https://react.i18next.com/)&#x20;

### i18next-react

This is the react version of i18next and I need to mention that it support server side rendering and change language well.

```javascript
const initialL10n = (
    namespace: string,
    translation: TranslationType,
    language: Languages,
): i18nType => {
    const resources = {
        [language]: {
            common,
            [namespace]: translation,
        },
    };

    if (!i18n.isInitialized) {
        i18n.use(initReactI18next).init({
            resources,
            lng: language,
            ns: [Namespace.common, namespace],
            defaultNS: Namespace.common,
            interpolation: {
                escapeValue: false,
                format: formatVal,
            },
            react: {
                useSuspense: false,
                defaultTransParent: 'div',
                transSupportBasicHtmlNodes: true,
                transKeepBasicHtmlNodesFor: ['br', 'strong', 'i', 'b'],
            },
        });
    } else {
        i18n.addResourceBundle(language, namespace, translation);
    }

    return i18n;
};
```

This is the util function for initial the language for the page and it also support switch the page (add resource).

