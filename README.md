# circleci-sonar-scanner

CircleCi Sonar Scanner

Usage:
Add secret environment variables in CircleCi:

- `SONAR_TOKEN`: authentication token.
- `SONAR_HOST`: sonar server url.


Add job to `.circleci/config.yml`:

```
analyze:
    docker:
      - image: wunderio/circleci-sonar-scanner
    steps:
      - checkout
      # Run sonar scanner on project.
      - run: cd /home/circleci/project/ && run-sonar-scanner
```

For more advanced cases create `sonar-scanner.properties` file or
 run `sonar-scanner` with 
 [parameters](https://docs.sonarqube.org/latest/analysis/analysis-parameters/):
```
- run: >-
      cd /home/circleci/project/ &&
      sonar-scanner -Dsonar.host.url=$SONAR_HOST
      -Dsonar.login=$SONAR_TOKEN
      -Dsonar.php.coverage.reportPaths=/home/circleci/project/coverage.xml
      -Dsonar.projectKey=project-name-in-sonar
      -Dsonar.sources=/home/circleci/project/src
      -Dsonar.exclusions=/home/circleci/project/tests/**
```