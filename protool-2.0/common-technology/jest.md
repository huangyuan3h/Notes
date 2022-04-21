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

1. `setupFiles` could set basic testing environment
2. `setupFilesAfterEnv` could define the running script before run each test
3. `transform` filed use the `ts-jest` package transform ts file before runing the test.
4. &#x20;`collectCoverageFrom` is the path to collect the coverage data, if set '!path' some path could be ignored.

### Mock

#### mock field

When writing unit test, it is highly recommend that use mock data to do the test. The benefit includes:

1. mock data is random so as to make the test more robust
2. mock data save the memory as the random words has been reused



The `fake.js` is one of the choice to mock data. You can install it by:

```bash
npm install @faker-js/faker --save-dev
```

In code you can generate random mock data like:

```typescript
import { faker } from '@faker-js/faker';

const randomName = faker.name.findName();
const randomEmail = faker.internet.email();
```

more details:

[https://fakerjs.dev/guide/](https://fakerjs.dev/guide/)

#### mock packages

Sometimes, we only want to test the target file, but the the packages the target file required. In this case , we can mock the packages that is not in the testing plan:

```javascript
jest.mock('../moduleName', () => {
  return jest.fn(() => 42);
});

// This runs the function specified as second argument to `jest.mock`.
const moduleName = require('../moduleName');
moduleName(); // Will return '42';
```

And this is the recommend way for writing UT in our daily work. These setting could also added into jest setup file.



#### mock functions

Another reason I like jest is the way to mock functions. Let me show you little bit about this part:&#x20;

```javascript
const mockFn = jest.fn((x:string):string => {
    // factory function
    return x;
});
const anyData = 'any';
const result = mockFn(anyData);
expect(mockFn).tobecalledWith(anyData);
expect(result).toEqual(anyData);
```

With this example, 90% of the function could be mocked and tested with expected mock result.



These is another way to mock function and not change the original result:

```javascript
const video = require('./video');

test('plays video', () => {
  const spy = jest.spyOn(video, 'play');
  const isPlaying = video.play();

  expect(spy).toHaveBeenCalled();
  expect(isPlaying).toBe(true);

  spy.mockRestore();
});
```



These 2 examples above is current major way in our project.



### &#x20;Run test in IDE

Run the test in idea is pretty simple:

![](<../../.gitbook/assets/image (4) (1) (1) (1).png>)

the environment will be setup automatically, you can run the test just by click the run icon at left.



run test in vs code:

There are variety ways to run jest in vs code, the plugin I choose is `jest-running`

``![](<../../.gitbook/assets/image (2).png>)``

After install this plugin,  it would be same as IDEA click the `run` or `debugger` ,  the test would run automatically.

![](<../../.gitbook/assets/image (3) (1).png>)



### Coverage

The coverage support for jest is also very nice. I would like to introduce it together with [sonar](sonar.md).

















