# Jest

Since our project is based on React, and Jest is created by `Meta` as well. So `jest`  is chose to be the testing framework.

### &#x20;Install&#x20;

To install `jest` , first of all is to add the jest package

```bash
npm install --save-dev jest @types/jest
```

As all the project is also based on `typescript` , the `ts-jest` plugin is also necessary:

```bash
npm install --save-dev ts-jest
```

### Configure

After the required packages added, the next step is to add configure file:

```json
// jest.config.js
module.exports = {
    setupFiles: ['dotenv/config'],
    transform: {
        '^.+\\.ts?$': 'ts-jest',
    },
    testEnvironment: 'node',
    testPathIgnorePatterns: ['/node_modules', '/dist/'],
    testRegex: [
        '/test/.*\\.(test|spec)?\\.(ts|tsx)$',
        '/src/.*\\.(test|spec)?\\.(ts|tsx)$',
    ],
    moduleFileExtensions: ['ts', 'tsx', 'js', 'jsx', 'json', 'node'],
    setupFilesAfterEnv: ['<rootDir>/test/setup/setupTests.ts'],
    modulePaths: ['<rootDir>/src'],
    collectCoverageFrom: [
        '!**/node_modules/**',
        '<rootDir>/src/**/*.{ts,tsx}'
    ],
};
```

The configure above contains several field, need to be mention:

1. `setupFiles` could define the running script before run each test
2. `transform` filed use the `ts-jest` package transform ts file before runing the test.
3. &#x20;`collectCoverageFrom` is the path to collect the coverage data, if set '!path' some path could be ignored.



























