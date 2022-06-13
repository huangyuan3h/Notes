# Eslint

In Javascript or Typescript area, [`eslint`](https://eslint.org/) currently is still the best tool to do coding standard check.&#x20;



### airbnb vs google vs standard

Normally, developer should not define the eslint configure directly. We should choose the from one of the major template.

The top 3 common used eslint config are airbnb, google and standard

![](<../../.gitbook/assets/image (1) (1) (1).png>)

From the download, we can see `airbnb` has the largest number of download. So Bolt team is based on this rule.



### Abstract the configure

Normally, for one develop team, it would have several different projects. If we configure the rule one by one, it is just wast time for it.

What we should do is much more like define the type of the project and each type of the project use it's configure.



Let's take protool api and protool FE as example:

```
// from protool api
module.exports = {
    extends: ['@ecg-bolt/typescript'],
};

```

```
// from protool FE
module.exports = {
    extends: ['@ecg-bolt/react'],
};

```



All the configure is point to another project `bolt-package`  and in bolt package:

![](<../../.gitbook/assets/image (2) (1) (1).png>)

There are 2 sub project in packages folder. It means if the project is only related to `typescript` it should use the `eslint-config-typescript` configuration; if the project is related to `React` this project should use `eslint-config-react` configuration.

In configuration project, it reuse the `airbnb` configure and disable or redefine the rule we need.

For example:

```
{
...
extends: [
        'airbnb',
        'plugin:@typescript-eslint/recommended',
        'plugin:prettier/recommended',
        'prettier',
    ],
    ...
        rules: {
        'import/extensions': [
            'error',
            'ignorePackages',
            {
                js: 'never',
                jsx: 'never',
                ts: 'never',
                tsx: 'never',
            },
        ],
        'react/jsx-filename-extension': [
            'error',
            {
                extensions: ['.js', '.jsx', '.ts', '.tsx'],
            },
        ],
        'import/no-extraneous-dependencies': [
            'error',
            {
                devDependencies: true,
            },
        ],
        'react/jsx-indent': 'off',
        'react/jsx-indent-props': 'off',
        'no-use-before-define': 'off',
        '@typescript-eslint/no-use-before-define': ['error'],
        'no-shadow': 'off',
        '@typescript-eslint/no-shadow': ['error'],
        'react/require-default-props': ['warn'],
        'react/no-unused-prop-types': ['warn'],
    },
}
```

By this way, all the configuration of eslint is reusable in any other project. For the other project, the eslint configure is just one line.

### How to use the configure

First of all, make sure the registry has been configured

```
    "publishConfig": {
        "registry": "https://nexus.es.ecg.tools/repository/ecg-global-npm-hosted/"
    },
```

The config above is from `package.json`, and it could also be configured in `.npmrc` :

```
@ecg-bolt:registry=https://nexus.es.ecg.tools/content/groups/ecg-global-npm-all/
package-lock=true
```

Second, add the configure to `eslintrc.js` or `eslintrc.json` :

```
module.exports = {
    extends: ['@team-name/project-type'],
};
```

### eslint ignore

After eslint being configured, the `.eslintignore` is also required to be added into root of the project so as to ignore necessary file.

```
build/*
.prettierrc.js
.eslintrc.js
```

### How to run eslint

Running eslint on bash could be

```bash
npx eslint .
```

the command could also be added in package.json:

```
{
...
    "scripts": {
        "lint": "eslint --ext .ts . --fix"
    },
...
}
```

Adding `fix` parameter could auto fix some problem and `ext` is to choose the extension type of the file.

```
npm run lint
```

In bash just need to type the line above the most of the style issue would resolved automatically.
