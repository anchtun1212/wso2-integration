# Getting started with WSO2 Micro Integrator CLI Tool
1) Go to: https://wso2.com/integration/micro-integrator/tooling/ and download Linux version.
2) Navigate to: `<MI_HOME>/bin` e.g.: `/home/mohammedayman/projects/sme/fundingGate/integration/integration studio/WSO2-Integration-Studio-8.0.0/runtime/microesb/bin`
3) MI is supported only on JDK 1.8, 9, 10 and 11
4) Run: `sudo JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 ./micro-integrator.sh -DenableManagementApi` to enable the `enableManagementApi` system property
5) (Optional you can use step 4) only)`export PATH=/path/to/mi/cli/directory/bin:$PATH` e.g. `export PATH=/home/mohammedayman/projects/sme/fundingGate/integration/wso2mi-cli-1.2.0/bin:$PATH`
6) Run: `mi`

# Using the Management API
1) See this: https://ei.docs.wso2.com/en/7.0.0/micro-integrator/administer-and-observe/working-with-management-api/

# Log in to the CLI
1) `mi remote login`.
2) The default username is `admin` and the default password is `admin`.
3) To login: `mi remote login [username] [password]`
4) To logout: `mi remote logout`
5) Usage: `mi [command]`
6) Version: `mi version`
7) Global Flags: `--verbose    Enable verbose logs (Provides more information on execution), --help, -h Display information and example usage of a command`
8) For more see: https://ei.docs.wso2.com/en/7.0.0/micro-integrator/administer-and-observe/using-the-command-line-interface/

# Test the application using CLI
1) Run: `sudo JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 ./micro-integrator.sh -DenableManagementApi`
2) Put the `car` file into: `<MI_HOME>/repository/deployment/server/carbonapps` : `Car= Carbon Apps`. e.g. put: `HealthcareProjectCompositeExporter_1.0.0-SNAPSHOT.car`
3) Run: `mi remote login  [username] [password]` e.g. `mi remote login admin admin`.
4) NOTE: The default remote will be the micro integrator instance running on localhost with the port 9164.
5) To list all the endpoints deployed in the WSO2 Micro Integrator: `mi endpoint show`.
6) To get information about a specific endpoint: `mi endpoint show QueryDoctorEP`, you will see:

     Name - `QueryDoctorEP`

     Type - HTTP Endpoint

     Active - true

     Method - GET

     URI Template - http://localhost:9090/healthcare/
   
8) To get information about a specific composite app: `mi compositeapp show HealthcareCompositeExporter`
9) We will call the endpoint: First, encode your username:password in Basic Auth format (encoded in base64). For example, use the default admin:admin credentials.
10) Get the token: `curl -X GET "https://localhost:9164/management/login" -H "accept: application/json" -H "Authorization: Basic YWRtaW46YWRtaW4=" -k -i`
11) GET ENDPOINTS: `curl -X GET "https://localhost:9164/management/endpoints" -H "accept: application/json" -H "Authorization: Bearer eyJraWQiOiI4ZTAzYjU4MC03M2UzLTRkYTAtOGYzYi1kZGQzMjg0ODMyOTIiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJhZG1pbiIsInNjb3BlIjoiZGVmYXVsdCIsImlzcyI6Imh0dHBzOlwvXC8xMjcuMC4wLjE6OTE2NFwvIiwiZXhwIjoxNjk0OTU2MTY3fQ.q9WqHaVxz21fKBLa5Sd4T0TXFGqgfayLoVeCY6bUqCTnYtpfPYvC6lVF7ukk4wzHd3LdOLJSt7N9I5lpra2cX4FuWjOqp6wBs2dSQWebK4jRHmJFbJfTgnFNKLV-zrhBwtRdyd4rTyUX3HfRx25C8vY53ETQ765DgK9W_ZTiGmudgj2mwv4HuZdTBXoBqigYzmrV6RULf51wmb8MrnV4jO97jYCKMdsCWcwo4XzJ-AUwvA0majo62XFEBnwXQracESpI8HqntYwkSKNlakcS4BiUKc48CC92E63kbaHUBSkWJLGDFjh02RMhrTmUjiWfrcZqtDvKbWaaQI600WnldQ" -k -i`
12) Resource: `/endpoints?endpointName={endpointname}`: `curl -X GET "https://localhost:9164/management/endpoints?endpointName=QueryDoctorEP" -H "accept: application/json" -H "Authorization: Bearer eyJraWQiOiIyOTkxZDZjNC1lZWExLTRkMDgtODQ3Yi1kMWI5YWM0OTEyNjYiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJhZG1pbiIsInNjb3BlIjoiZGVmYXVsdCIsImlzcyI6Imh0dHBzOlwvXC8xMjcuMC4wLjE6OTE2NFwvIiwiZXhwIjoxNjk0OTU4ODM4fQ.FEsGOGMD1kZl5ZCO_C-LAQEESEo7fdixe4gl-EAB6mby8wmDVHutsF8cBIxv00DK29-6unUcoyqYbRyUSoZi9O2Xka6_wD6UeTCIWandPs-NJopw2940vU_0i8Vz8aytAdzf7p_0C10Fp_k8OGEX5OMlPIyxaUcMPnfkBH8gaOWTgzYqtw7yL3mWj3SDiZfM0Zs3JoCOz69aNeZVUQ6JsP2QITovd02aUbk_SGhBhPj8G-ae8xnFDNgLulWurjPYjZ_wqMr68_PHadG_GXSGMmW-PAATS-lh0OChI7UJn8HYJ3D9vNev8FCVDUBjNUXbzIWfHSe2wPNOFkOy27CjUg" -k -i`
13) Select MI server: Run: `mi remote show` the `mi remote select <server-name>`.

# Deploy and run the integration
1) Go to: https://wso2.com/api-manager
2) Subscribe and then download: `wso2am-4.2.0` folder
3) Go to: `/home/mohammedayman/projects/sme/fundingGate/integration/wso2am-4.2.0/bin`
4) Run: `sudo JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 ./api-manager.sh`
5) Open this URL to check: https://localhost:9443/devportal
6) The default credentials `username/password` are: `admin/admin`
7) Go to: https://localhost:9443/publisher to see APIs
8) For `Authorization` you can use: `header: 'Authorization : Bearer ACCESS_TOKEN' or 'Authorization : Basic ACCESS_TOKEN' or 'apikey: API_KEY'"`
