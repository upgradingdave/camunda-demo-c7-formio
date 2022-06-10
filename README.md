# Camunda 7 form.io Demo

![Compatible with: Camunda Platform 7](https://img.shields.io/badge/Compatible%20with-Camunda%20Platform%207-26d07c)

[![](https://img.shields.io/badge/Lifecycle-Proof%20of%20Concept-blueviolet)](https://github.com/Camunda-Community-Hub/community/blob/main/extension-lifecycle.md#proof-of-concept-)

Many concepts and some code used in this project was inspired and copied from here: https://github.com/StephenOTT/camunda-formio-plugin. 

This is an example of integrating http://form.io into a Camunda Spring Boot Starter project.

## Quick Start

This project follows the same conventions and is compatible with the
[Camunda Demo Starter](https://github.com/camunda-consulting/camunda-demo-starter#camunda-demo-starter).

1. Clone this project (`camunda-demo-c7-formio` project) into your local `camunda-demo` directory

  ```
  cd camunda-demo
  git clone https://github.com/camunda-consulting/camunda-demo-c7-formio.git
  ```

2. Use the following command to start an environment:

```
docker-compose  \
  -f ./camunda-starter-demo/docker-compose.postgres.yml \
  -f ./camunda-starter-demo/docker-compose.data-api.yml \
  -f ./camunda-starter-demo/docker-compose.smtp.yml \
  -f ./docker-compose.c7-client.yml \
  -f ./camunda-demo-c7-formio/docker-compose.c7-formio.yml \
  up -d --build
```

## Development

1. Start the Spring Boot Application

Open this project in Intellij and open `src/main/java/io/camunda/starter/MyApplication.java`. 

Click the green triangle to start the project

2. Browse to the Form Builder

Once the Spring boot application starts, open your browser and navigate to: 

http://localhost:8090/forms/builder.html

Create a form. Then copy the json 

--- 








