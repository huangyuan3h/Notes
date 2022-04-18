# Git pre-commit

There are several things to do before commit code to current branch:

1. format the coding style by prettier
2. check the typescript and the eslint part
3. pass all the test (optional)
4. add the auto fixed file from above step to git

### Install

```bash
npm i husky lint-staged pretty-quick --save-dev
```

The packages above is would help to make pre-commit work and let me give you some introduction about them:

1. `husky` is the tool to setup git hooker
2. `lint-staged` could help to filter the file and do the configured cmd
3. `pretty-quick` could format the changed file



By enable husky, we need to run install script for it:

```bash
npx husky-init && npm install
npx husky add .husky/pre-commit "npx lint-staged"
```

You can delete the prepare in package json after install.

### Configure

Let's add some `test` and `lint` command in `package.json` first:



```json
{
...
    "scripts": {
        "test": "jest --passWithNoTests --silent",
        "lint": "tsc --noEmit --skipLibCheck && eslint --ext .tsx,.ts . --fix"
    },
...
}
```

`test` script will run jest unit test

`lint` would first do the type check, then it would check eslint rules&#x20;



Then, the pre-commit config file should be set in `package.json` :

```json
{
    ...
    "lint-staged": {
        "*.{js,jsx,ts,tsx}": [
            "pretty-quick --staged",
            "npm run lint",
            "npm run test",
            "git add"
        ]
    },
...
}
```

You can also configure lint-staged in it's configure file like `.lintstagedrc.json` in different folders.



The command above is to do prettier format, lint, ut test, and add the result to git. So that all the result could be commit to repository together with the changes.











