# Sonar

In the Project, `jenkins`  is used to continue integration. And the code quality is analysed by `sonar` .



![](<../../.gitbook/assets/image (5) (1).png>)



The screenshot above is the master branch of protool 2.0 project. To use Sonar has several advantage:

1. we can defined the code coverage, normally most of the pr it is greater than 90%.
2. There are some coding style defined in the rule of Sonar such as the password check and regex check, it always useful in code smell.
3. Sonar will analyze the vulnerability of current system, and display the report for developer.



Normally, these part is configured by DevOps, but still, we need to know the basic rules. The basic configure is inside the `Jenkins` file.&#x20;



```
 stage('Lint & Test') {
      steps {
        withCredentials([string(credentialsId: 'PROTOOL-SONAR-TOKEN', variable: 'SONAR_LOGIN')]) {
          script {
            def sonarOpts = '''-Dsonar.projectKey=${PROJECT_NAME} \
              -Dsonar.sources=./src \
              -Dsonar.host.url=sonar.url \
              -Dsonar.login=${SONAR_LOGIN} \
              -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info \
              -Dsonar.exclusions=tests/**/*.*,src/**/*.test.*,coverage/**/*.*,src/**/__test__/**/*.* \
            '''
            if (job.isPullRequest()) {
              sonarOpts += '''-Dsonar.pullrequest.provider=github \
                -Dsonar.pullrequest.github.repository=ecg-global/${PROJECT_NAME} \
                -Dsonar.pullrequest.branch=${CHANGE_BRANCH} \
                -Dsonar.pullrequest.key=${CHANGE_ID} \
                -Dsonar.projectVersion=${CHANGE_BRANCH}-${BUILD_ID}
              '''
            } else {
              sonarOpts += '''-Dsonar.branch.name=${BRANCH_NAME} \
              -Dsonar.projectVersion=${BRANCH_NAME}-${BUILD_ID}
              '''
            }
            docker.image(BASE_IMAGE).inside(MOUNT_NPM_CACHE_VOLUME) {
              sh '''#!/bin/sh -xel
              npm install
              npm run lint
              npm run coverage
              sonar-scanner ''' + sonarOpts
            }
          }
        }
      }
    }
```

This is the example for the configure for test and lint. The jest coverage would be run inside a docker and the result would be sent to sonar cube.





