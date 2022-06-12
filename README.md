# Camunda 7 form.io Demo

![Compatible with: Camunda Platform 7](https://img.shields.io/badge/Compatible%20with-Camunda%20Platform%207-26d07c)

[![](https://img.shields.io/badge/Lifecycle-Proof%20of%20Concept-blueviolet)](https://github.com/Camunda-Community-Hub/community/blob/main/extension-lifecycle.md#proof-of-concept-)

Concepts and code used in this project were copied from here: https://github.com/StephenOTT/camunda-formio-plugin. 

This is an example of integrating http://form.io into a Camunda Spring Boot Starter project.

## Quick Start

This project is compatible with the [Camunda Demo Starter](https://github.com/camunda-consulting/camunda-demo-starter#camunda-demo-starter). If you are unfamiliar, first try following the steps described in the [Camunda Demo Starter](https://github.com/camunda-consulting/camunda-demo-starter#camunda-demo-starter) to bring up a Camunda 7 environment. 

Then, instead of using the default Docker Compose command described in the [Camunda Demo Starter](https://github.com/camunda-consulting/camunda-demo-starter#camunda-demo-starter), use the following steps instead: 

1. Clone this project (`camunda-demo-c7-formio` project) into your local `camunda-demo` directory

  ```
  cd camunda-demo
  git clone https://github.com/camunda-consulting/camunda-demo-c7-formio.git
  ```

2. Use the following command to start an environment:

```
docker-compose  \
  -f camunda-demo-starter/docker-compose.postgres.yml \
  -f camunda-demo-starter/docker-compose.data-api.yml \
  -f camunda-demo-starter/docker-compose.smtp.yml \
  -f camunda-demo-c7-formio/docker-compose.c7-formio.yml \
  -f camunda-demo-c7-formio/docker-compose.c7-client.yml \
  up -d --build
```

3. Test out the Example Process

![Form io Example Process](./screenshots/FormioExample.png?raw=true "Form io Example Process")

Once the Spring Boot application starts, you should be able to access the Camunda 7 Cockpit, Tasklist, and Admin here:

http://localhost:8080

The Camunda Rest API should be available here:

http://localhost:8080/engine-rest

Try starting a `Form io Example` instance from Tasklist. You should see the `StartForm.json` rendered like this:

![Start Form](./screenshots/startForm.png?raw=true "Start Form")

When you submit, the form data is saved as instance variables.

You should then be able to see the next User Task `Review Email Message` that renders the `ApproveForm.json` form.

![Approve Form](./screenshots/approveForm.png?raw=true "Approve Form")

If you choose `Approve` the token will go to `Notify Approved`. If you're running in the docker compose environment, a fake email will be sent. You can check the emails here: 

http://localhost:9999

![Mail Screen](./screenshots/mailScreen.png?raw=true "Mail Screen")

To create a new http://form.io form or update an existing form, browse here:

http://localhost:8080/forms/builder.html

## Development Mode

Here's how to start the project from intellij.

Open this project in Intellij and then open this java file: `src/main/java/io/camunda/starter/MyApplication.java`.

Click the green triangle to start the project

By default, the webapp should start on port `8081` when run in "development mode".

> **Note** -- Some versions of Java don't include Javascript Engines. If you get an error related to Scripting Engines, try using Java 8.

## How it works

When the Spring Boot application starts, a Camunda Deployment is automatically created and deployed based on the `src/main/resources/META-INF/processes.xml` file. 

The default deployment contains the following 3 resources: 

* `src/main/resources/processes/FormioExample.bpmn`
* `src/main/resources/forms/StartForm.json`
* `src/main/resources/forms/ApproveForm.json`

The start form task inside the `FormioExample.bpmn` is configured to use an embedded form. The url to the embedded form looks like this: 

```
embedded:/forms/formio.html?deployment=forms/StartForm.json&var=startFormData&transient=false
```

Open Tasklist and try to start a new instance of the `Form io Example` Process.

Tasklist loads `formio.html` which contains custom code in a `<script cam-script>` tag. This code loads the `forms/StartForm.json` file and then uses the `form.io` js library to display the form.

After the start form, there is a script task that copies data submitted from the form to process variables. These variables are used to send an email if 
the email is approved.

## Build and Deploy a new release

1. Make your changes and build new jar

       mvn clean install

2. Test and Verify your changes
3. Build new docker image

       docker build . -t camunda-demo-c7-formio

4. Publish to a Docker Repo and update the docker-compose yml files accordingly. 



