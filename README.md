# Getting started with WSO2 Micro Integrator CLI Tool

1) Go to: https://wso2.com/integration/micro-integrator/tooling/ and download Linux version.
2) Navigate to: `<MI_HOME>/bin` e.g.: `/home/mohammedayman/projects/sme/fundingGate/integration/integration studio/WSO2-Integration-Studio-8.0.0/runtime/microesb/bin`
3) Run: `export JAVA_HOME=/usr/lib/jvm/java-1.17.0-openjdk-amd64/bin/java`
4) Run: `export PATH=$PATH:/usr/lib/jvm/java-1.17.0-openjdk-amd64/bin`
5) Run: `sh micro-integrator.sh -DenableManagementApi` to enable the `enableManagementApi` system property
6) `export PATH=/path/to/mi/cli/directory/bin:$PATH` e.g. `export PATH=/home/mohammedayman/projects/sme/fundingGate/integration/wso2mi-cli-1.2.0/bin:$PATH`
7) Run: `mi`

# Log in to the CLI

1) `mi remote login`.
2) The default username is `admin` and the default password is `admin`.


