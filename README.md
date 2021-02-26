# Docker image to deploy on Vapor

## Usage

**How to use with Bitbucket Pipelines**

1. Learn [how to Deploying From CI](https://docs.vapor.build/1.0/projects/deployments.html#deploying-from-ci).
2. And can use the snippet below as starting point to create your `bitbucket-pipelines.yml`:

```
image: jrobinsonc/laravel-vapor:7.4

pipelines:
  branches:
    production:
      - step:
          name: Build Production
          caches:
            - composer
            - yarn
          script:
            - cd front-end
            - yarn build
            - cd ../back-end
            - composer install --no-interaction --no-progress --prefer-dist
          artifacts:
            - back-end/storage/**
            - back-end/vendor/**
            - back-end/public/**
      - step:
          name: Test Production
          script:
            - cd back-end
            - php artisan test --testsuite=Unit
      - step:
          name: Deploy Production
          deployment: production
          script:
            - cd back-end
            - vapor deploy production --commit="$BITBUCKET_COMMIT"

definitions:
  caches:
    yarn: /usr/local/share/.cache/yarn
```
