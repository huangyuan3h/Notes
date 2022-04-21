# Lerna

Lerna is the tool to manage the js packages. It could split the big project into several small projects. When a project require some components or tools, it can only require the sub-package into the project. It would also create some soft link for the sub-project, so as to require the relations more easily.&#x20;

To use Lerna or not is decided by developer, The idea of the chapter is to divide large package into small. So that it could be more easily reused.

### Setup

First, install the `lerna` globally:

```bash
npm install --global lerna
```

Let's say we have a project called `kt-packages`

```bash
cd kt-pakcages
lerna init --independent
```

Independent mode Lerna projects allows maintainers to increment package versions independently of each other. For me, I would prefer to manage the packages into the version belong to themself, so I will use this mode.

After the command finished, you will see basic lerna structure:

```
lerna-repo/
  |--packages/
  |--package.json
  |--lerna.json
```



The packages folder include all the sub-package projects.

The lerna config file should also configured like:

```
{
    "npmClient": "npm",
    "packages": [
        "packages/*"
    ],
    "version": "independent",
    "command": {
        "ignoreChanges": [
            "*.test.*",
            "*.spec.*",
            "*.md"
        ],
        "publish": {
            "ignoreChanges": [
                "*.md"
            ],
            "registry": "example.registry.url"            
        }
    }
}
```





Let's create 4 packages inside the project structure:

```
lerna create shared-components -y
lerna create storybook -y
lerna create eslint-config-typescript -y
lerna create eslint-config-react -y
```

the project structure should looks like:

![](<../../.gitbook/assets/image (5) (1).png>)

This is also part of the project structure designed in protool 2.0, let me explain little bit about 4 packages.

1. shared-components contains all the common components for other project use
2. storybook is the project use [`storybook`](https://storybook.js.org) to display `shared-component` for Fe devs and designer
3. eslint-config-\[typescript|react] project is to defined eslint rules and reused in other project.
4. we also have api layer using [`got`](https://github.com/sindresorhus/got) as the client for micro-service.

### Publish

As lerna is the tool to manage the version of packages, so publish these packages to registry is the key step.



First of all the registry url is set in `lerna.json`

```
"registry": "example.registry.url" 
```

Second, in package json file add related scripts, such as:

```
    "scripts": {
        "init": "lerna init", // init project
        "test": "lerna run test --parallel", // run all the test in packages
        "test-coverage": "lerna run test-coverage --parallel", // run all the coverages
        "lint": "lerna run lint --parallel", 
        "bootstrap": "lerna bootstrap", // install packages
        "version-prepatch": "lerna version prepatch --yes", //update the version
        "version-patch": "lerna version patch --conventional-commits --yes",
        "version-preminor": "lerna version preminor --yes",
        "publish": "lerna publish",
        "build": "lerna run build --parallel" // buld all
    },
```

After this step, it should be possible to publish the packages by command line. But we need to make this project more smart.

when commit or merge it into master branch, it should publish automatically.&#x20;

So we add the config in jenkins file:

```
steps {
        script {
          def PRE_ID = job.getSCMCommitShortId()
          if (job.isPullRequest()) {
            PRE_ID = CHANGE_BRANCH + '-' + PRE_ID
          } else {
            PRE_ID = BRANCH_NAME + '-' + PRE_ID
          }
          job.avoidBuildAfterAutomaticCommit('BumpVersionCI')
          docker.image(BASE_GIT_IMAGE).inside(MOUNT_NPM_CACHE_VOLUME) {
            withCredentials([
              usernamePassword(credentialsId: 'ecg-global-npm-publisher', passwordVariable: 'password', usernameVariable: 'username'),
              string(credentialsId: 'GITHUBBOT-BOLTCI-TOKEN', variable: 'TOKEN')
            ]) {
              sh '''#!/bin/sh -xel
                git config user.email \"BumpVersionCI@ebay.com\";
                git config user.name \"BumpVersionCI\";
                git remote set-url origin https://${TOKEN}:x-oauth-basic@github.es.ecg.tools/ecg-global/bolt-packages.git
                git status
              '''
              if (BRANCH_NAME == "master") {
                sh """#!/bin/sh -xel
                  # add publishing creds to .npmrc
                  auth=\$(echo -n "$username:$password" | base64)
                  echo \"//nexus.es.ecg.tools/repository/ecg-global-npm-hosted/:_auth=\${auth}\" >> .npmrc
                  # debug
                  git tag | tail -n 10
                  npx lerna changed --all --include-merged-tags --long --loglevel debug
                  npm run publish patch -- --yes --include-merged-tags
                """
              } else {
                sh """#!/bin/sh -xel
                  # add publishing creds to .npmrc
                  auth=\$(echo -n "$username:$password" | base64)
                  echo \"//nexus.es.ecg.tools/repository/ecg-global-npm-hosted/:_auth=\${auth}\" >> .npmrc
                  # debug
                  git tag | tail -n 10
                  npx lerna changed --all --include-merged-tags --long --loglevel debug
                  # do publish
                  npm run publish prepatch -- --preid ${PRE_ID} --no-git-tag-version --no-push --include-merged-tags --yes
                """
              }
            }
          }
```



###

###

### &#x20;



&#x20;
