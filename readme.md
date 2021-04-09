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

- ace-editor:1.1
- ansible:1.1
- ansicolor:0.7.5
- antisamy-markup-formatter:2.1
- apache-httpcomponents-client-4-api:4.5.13-1.0
- authentication-tokens:1.4
- authorize-project:1.4.0
- bootstrap4-api:4.6.0-3
- bouncycastle-api:2.20
- branch-api:2.6.3
- build-timeout:1.20
- checks-api:1.7.0
- cloudbees-disk-usage-simple:0.10
- cloudbees-folder:6.15
- cobertura:1.16
- code-coverage-api:1.3.2
- command-launcher:1.5
- conditional-buildstep:1.4.1
- configuration-as-code:1.47
- credentials:2.3.15
- credentials-binding:1.24
- dashboard-view:2.15
- display-console-output:1.0.5
- display-url-api:2.3.4
- docker-build-publish:1.3.3
- docker-commons:1.17
- docker-java-api:3.1.5.2
- docker-plugin:1.2.2
- docker-workflow:1.26
- durable-task:1.35
- echarts-api:5.0.2-1
- email-ext:2.82
- extended-read-permission:3.2
- font-awesome-api:5.15.2-2
- git:4.7.1
- git-client:3.7.1
- git-server:1.9
- github:1.33.1
- github-api:1.123
- github-autostatus:3.6.2
- github-branch-source:2.10.2
- handlebars:3.0.8
- jackson2-api:2.12.1
- jacoco:3.1.1
- javadoc:1.6
- jdk-tool:1.5
- jjwt-api:0.11.2-9.c8b45b8bb173
- jquery3-api:3.6.0-1
- jsch:0.1.55.2
- junit:1.49
- lockable-resources:2.10
- mailer:1.34
- matrix-auth:2.6.6
- matrix-project:1.18
- maven-plugin:3.10
- metrics:4.0.2.7
- momentjs:1.1.1
- okhttp-api:3.14.9
- parallel-test-executor:1.13
- parameterized-trigger:2.40
- pipeline-build-step:2.13
- pipeline-github-lib:1.0
- pipeline-graph-analysis:1.10
- pipeline-input-step:2.12
- pipeline-milestone-step:1.3.2
- pipeline-model-api:1.8.4
- pipeline-model-definition:1.8.4
- pipeline-model-extensions:1.8.4
- pipeline-rest-api:2.19
- pipeline-stage-step:2.5
- pipeline-stage-tags-metadata:1.8.4
- pipeline-stage-view:2.19
- pipeline-utility-steps:2.7.1
- plain-credentials:1.7
- plugin-util-api:2.1.0
- popper-api:1.16.1-2
- postbuild-task:1.9
- prometheus:2.0.9
- resource-disposer:0.15
- run-condition:1.5
- scm-api:2.6.4
- script-security:1.76
- snakeyaml-api:1.27.0
- ssh-credentials:1.18.2
- ssh-slaves:1.31.7
- sshd:3.0.3
- structs:1.22
- timestamper:1.12
- token-macro:2.15
- trilead-api:1.0.13
- variant:1.4
- workflow-aggregator:2.6
- workflow-api:2.42
- workflow-basic-steps:2.23
- workflow-cps:2.90
- workflow-cps-global-lib:2.18
- workflow-durable-task-step:2.38
- workflow-job:2.40
- workflow-multibranch:2.23
- workflow-scm-step:2.12
- workflow-step-api:2.23
- workflow-support:3.8
- ws-cleanup:0.39