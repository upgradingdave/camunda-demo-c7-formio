# Camunda 7 form.io Demo

![Compatible with: Camunda Platform 7](https://img.shields.io/badge/Compatible%20with-Camunda%20Platform%207-26d07c)

[![](https://img.shields.io/badge/Lifecycle-Proof%20of%20Concept-blueviolet)](https://github.com/Camunda-Community-Hub/community/blob/main/extension-lifecycle.md#proof-of-concept-)

Concepts and code used in this project were copied from here: https://github.com/StephenOTT/camunda-formio-plugin. 

This is an example of integrating http://form.io into a Camunda Spring Boot Starter project.

Current Status: Forms are displaying, but an error is thrown when they are submitted: 

![Submit Error](./screenshots/submitError.png?raw=true "Submit Error")

## Quick Start

Open this project in Intellij and open `src/main/java/io/camunda/starter/MyApplication.java`.

Click the green triangle to start the project

Once the Spring Boot application starts, you should be able to access the Camunda 7 environment (Cockpit, Tasklist, and Admin Webapps) here: 

http://localhost:8081

## How it works

When the Spring Boot application starts, a deployment is automatically created and deployed based on the `src/main/resources/META-INF/processes.xml` file. 

The default deployment contains the following 3 resources: 

* `src/main/resources/processes/FormioExample.bpmn`
* `src/main/resources/forms/StartForm.json`
* `src/main/resources/forms/ApproveForm.json`

The start form task inside the `FormioExample.bpmn` is configured to use an embedded form. The url to the embedded form looks like this: 

```
embedded:/forms/formio.html?deployment=forms/StartForm.json&var=submission&transient=true
```

Open Tasklist and try to start a new instance of the `Form io Example` Process.

Tasklist loads `formio.html` which contains custom code in a `<script cam-script>` tag. This code loads the `forms/StartForm.json` file and then uses the `form.io` js library to display the form. 

![Start Form](./screenshots/startForm.png?raw=true "Start Form")

NOTE: the form should currently display, however there is an error submitting the form. This is a work in progress.

## Create and/or update Forms

This project also includes a page to generate json for new forms. Or, copy existing schema json to update existing forms: 

http://localhost:8081/forms/builder.html

## Use as Part of Demo (WIP)

Note: this is still a work in progress!

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

