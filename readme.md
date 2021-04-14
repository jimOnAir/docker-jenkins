# Docker Jenkins image

Docker Jenkins image with several additional tools and plugins preinstalled:

- ansible
- awscli
- dive
- docker-ce
- docker-compose
- goss
- jq
- make
- yq

The plugin list is saved in the /usr/share/jenkins/plugins.txt file.
You can save the plugin list from your current Jenkins instance with the following script:
Run in `<jenkins_url>/script`

```groovy
Jenkins.instance.pluginManager.plugins.stream().sorted().each{
  plugin ->
    println ("${plugin.getShortName()}:${plugin.getVersion()}")
}
```

List of installed plugins:

- ace-editor:latest
- ansible:latest
- ansicolor:latest
- antisamy-markup-formatter:latest
- apache-httpcomponents-client-4-api:latest
- authentication-tokens:latest
- authorize-project:latest
- bootstrap4-api:latest
- bouncycastle-api:latest
- branch-api:latest
- build-timeout:latest
- checks-api:latest
- cloudbees-disk-usage-simple:latest
- cloudbees-folder:latest
- cobertura:latest
- code-coverage-api:latest
- command-launcher:latest
- conditional-buildstep:latest
- configuration-as-code:latest
- credentials:latest
- credentials-binding:latest
- dashboard-view:latest
- display-console-output:latest
- display-url-api:latest
- docker-build-publish:latest
- docker-commons:latest
- docker-java-api:latest
- docker-plugin:latest
- docker-workflow:latest
- durable-task:latest
- echarts-api:latest
- email-ext:latest
- extended-read-permission:latest
- font-awesome-api:latest
- git:latest
- git-client:latest
- git-server:latest
- github:latest
- github-api:latest
- github-autostatus:latest
- github-branch-source:latest
- handlebars:latest
- jackson2-api:latest
- jacoco:latest
- javadoc:latest
- jdk-tool:latest
- jjwt-api:latestc8b45b8bb173
- jquery3-api:latest
- jsch:latest
- junit:latest
- lockable-resources:latest
- mailer:latest
- matrix-auth:latest
- matrix-project:latest
- maven-plugin:latest
- metrics:latest
- momentjs:latest
- okhttp-api:latest
- parallel-test-executor:latest
- parameterized-trigger:latest
- pipeline-build-step:latest
- pipeline-github-lib:latest
- pipeline-graph-analysis:latest
- pipeline-input-step:latest
- pipeline-milestone-step:latest
- pipeline-model-api:latest
- pipeline-model-definition:latest
- pipeline-model-extensions:latest
- pipeline-rest-api:latest
- pipeline-stage-step:latest
- pipeline-stage-tags-metadata:latest
- pipeline-stage-view:latest
- pipeline-utility-steps:latest
- plain-credentials:latest
- plugin-util-api:latest
- popper-api:latest
- postbuild-task:latest
- prometheus:latest
- resource-disposer:latest
- run-condition:latest
- scm-api:latest
- script-security:latest
- snakeyaml-api:latest
- ssh-credentials:latest
- ssh-slaves:latest
- sshd:latest
- structs:latest
- timestamper:latest
- token-macro:latest
- trilead-api:latest
- variant:latest
- workflow-aggregator:latest
- workflow-api:latest
- workflow-basic-steps:latest
- workflow-cps:latest
- workflow-cps-global-lib:latest
- workflow-durable-task-step:latest
- workflow-job:latest
- workflow-multibranch:latest
- workflow-scm-step:latest
- workflow-step-api:latest
- workflow-support:latest
- ws-cleanup:latest
