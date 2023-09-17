# Getting started with WSO2 Micro Integrator CLI Tool

1) Go to: https://wso2.com/integration/micro-integrator/tooling/ and download Linux version.
2) Navigate to: `<MI_HOME>/bin` e.g.: `/home/mohammedayman/projects/sme/fundingGate/integration/integration studio/WSO2-Integration-Studio-8.0.0/runtime/microesb/bin`
3) MI is supported only on JDK 1.8, 9, 10 and 11
4) Run: `sudo JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 ./micro-integrator.sh -DenableManagementApi` to enable the `enableManagementApi` system property
5) `export PATH=/path/to/mi/cli/directory/bin:$PATH` e.g. `export PATH=/home/mohammedayman/projects/sme/fundingGate/integration/wso2mi-cli-1.2.0/bin:$PATH`
6) Run: `mi`

# Log in to the CLI

1) `mi remote login`.
2) The default username is `admin` and the default password is `admin`.
3) To login: `mi remote login [username] [password]`
4) To logout: `mi remote logout`
5) Usage: `mi [command]`
6) Version: `mi version`
7) Global Flags: `--verbose    Enable verbose logs (Provides more information on execution)--help, -h Display information and example usage of a command`


