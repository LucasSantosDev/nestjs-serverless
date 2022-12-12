### NestJS & Serverless

To implement serverless into NestJS project.

> Add necessary packages

```console
yarn add aws-lambda aws-serverless-express @nestjs/mapped-types @nestjs/config
```

> Add types

```console
yarn add -D @types/aws-lambda @types/aws-serverless-express serverless-offline serverless-plugin-typescript serverless-plugin-optimize
```

> Add config into imports: [] on src/app.module.ts

```console
imports: [ConfigModule.forRoot()]
```

> Add serverless.yml

```console
service: nestjs-serverless

useDotenv: true

plugins:
 - 'serverless-plugin-typescript'
 - serverless-plugin-optimize
 - serverless-offline

provider:
  name: aws
  stage: dev
  region: us-east-1
  runtime: nodejs12.x
  environment:
    PORT: ${env:PORT}
  
functions:
  main:
    handler: src/serverless.handler
    events:
      - http:
          method: ANY
          path: /{any+}
      
custom:
  serverless-offline:
    httpPort: ${self:provider.environment.PORT}
```

> Add on tsconfig.json

```console
"esModuleInterop": true
```

> Change incremental to true in tsconfig.json

```console
"incremental": false
```

##### Link documentation: https://nishabe.medium.com/nestjs-serverless-lambda-aws-in-shortest-steps-e914300faed5