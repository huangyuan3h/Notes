# Prettier

Prettier is a code formatter tool. The difference between prettier and other formatter tool is prettier would totally read the file and rewrite it to the correct format. I personally highly recommend using prettier as the default code formatter. &#x20;



### Configure

To configure prettier is very similar with eslint.

install prettier packages:

```bash
npm i prettier --save-dev
```





then, adding `.prettierrc.js` to the root of project:

```javascript
module.exports = {
    semi: true,
    singleQuote: true,
    printWidth: 80,
    trailingComma: 'all',
    bracketSameLine: false,
};
```

also adding the `.prettierignore` file:

```
.idea/
.history/
build/

# Logs
logs
*.log
```

#### For Idea user:

![](<../../.gitbook/assets/image (1).png>)

install prettier plugin

![](<../../.gitbook/assets/image (4).png>)

make sure the prettier point to the `node_module/prettier` .

The default short cut is:

![](<../../.gitbook/assets/image (2).png>)

`command+shift+ctrl p`

#### For vs code user:

![](<../../.gitbook/assets/image (3).png>)







