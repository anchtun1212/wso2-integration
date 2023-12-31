# GENERAL TIPS
`You can use the version 4.0.0 instead of wso2am-4.2.0 if you have some import/export API issues`

See this video, Change API Context:

https://www.youtube.com/watch?v=-q2BacTL7jM

         Ignore the version number to be called in the context path:
         https://localhost:8243/context/methodName
         INSTEAD OF
         https://localhost:8243/context/versionNumber/methodName
         Just go to: API > Overview > Develop > Portal Configurations > Basic Info > Make this the default version > Yes

Run:         ps -ef | grep wso2         

# Previous releases/List Ports
https://wso2.com/api-manager/previous-releases/

https://apim.docs.wso2.com/en/latest/install-and-setup/setup/reference/default-product-ports/#api-m-ports

# TIPS: Full Deployment/Test Process
1) Go to: `/home/mohammedayman/projects/sme/fundingGate/integration/integration studio/WSO2-Integration-Studio-8.0.0/runtime/microesb/bin`
2) Run: `sudo JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 ./micro-integrator.sh -DenableManagementApi`
3) Put the `car` file into: `<MI_HOME>/repository/deployment/server/carbonapps` : `Car= Carbon Apps`. e.g. put: `HealthcareProjectCompositeExporter_1.0.0-SNAPSHOT.car`
4) Go to https://localhost:9443/publisher and try to create a new API > Import Open API > and import the file (json or yaml) from `http://<MI_HOST>:8290/<API_NAME>?swagger.yaml`
   and follow the steps: see the video attached in the `private project: support`.

# TIPS: Swagger documents of API artifacts
1) To access the swagger.json file, use the following URL: `http://<MI_HOST>:8290/<API_NAME>?swagger.json` e.g. `http://localhost:8290/HealthcareAPI?swagger.json`
2) To access the swagger.yaml file, use the following URL: `http://<MI_HOST>:8290/<API_NAME>?swagger.yaml` e.g. `http://localhost:8290/HealthcareAPI?swagger.yaml`

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
1) Go to: `/home/mohammedayman/projects/sme/fundingGate/integration/integration studio/WSO2-Integration-Studio-8.0.0/runtime/microesb/bin`

2) Run: `sudo JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 ./micro-integrator.sh -DenableManagementApi`
3) Put the `car` file into: `<MI_HOME>/repository/deployment/server/carbonapps` : `Car= Carbon Apps`. e.g. put: `HealthcareProjectCompositeExporter_1.0.0-SNAPSHOT.car`
4) Run: `mi remote login  [username] [password]` e.g. `mi remote login admin admin`.
5) NOTE: The default remote will be the micro integrator instance running on localhost with the port 9164.
6) To list all the endpoints deployed in the WSO2 Micro Integrator: `mi endpoint show`.
7) To get information about a specific endpoint: `mi endpoint show QueryDoctorEP`, you will see:

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
5) Alternative to 4) To `start` and `stop` you can use:
   
         Start the server: sudo JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 sh api-manager.sh
         Start the server in background mode: sudo JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 sh api-manager.sh start
         Stop the server: sudo JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 sh api-manager.sh stop
         You can change the default ports:
         sudo JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 sh api-manager.sh -DportOffset=1
         or change the `offset` in the `deployment.toml` file:
         [server]
         hostname = "localhost"
         #offset=1
         so the URLs will be:
         CarbonUIServiceComponent Mgt Console URL  : https://localhost:9444/carbon/
         CarbonUIServiceComponent API Developer Portal Default Context : https://localhost:9444/devportal
         CarbonUIServiceComponent API Publisher Default Context : https://localhost:9444/publisher
         This is useful when you want to make many environments.

6) Database location: `/home/mohammedayman/projects/sme/fundingGate/integration/wso2am-4.2.0/repository/database/WSO2SHARED_DB.mv.db`, WSO2AM_DB ... 
7) Open this URL to check: https://localhost:9443/devportal
8) The default credentials `username/password` are: `admin/admin`
9) Go to: https://localhost:9443/publisher to see APIs
10) For `Authorization` you can use: `header: 'Authorization : Bearer ACCESS_TOKEN' or 'Authorization : Basic ACCESS_TOKEN' or 'apikey: API_KEY'"`
11) CURL to Generate Access Token:

The following cURL command shows how to generate an access token using the Password Grant type.

     curl -k -X POST https://localhost:9443/oauth2/token -d "grant_type=password&username=Username&password=Password" -H "Authorization: Basic Base64(consumer-key:consumer-secret)"

     e.g. ``curl -k -X POST https://localhost:9443/oauth2/token -d "grant_type=password&username=Username&password=Password" -H "Authorization: Basic UTdhZmhRZGdmV1ZobjhrRlBYeXdtUzRFX09NYTpEM01RbFU1WW1iQWZJMmU2Mkd3OHZINWZ0XzBh"``

In a similar manner, you can generate an access token using the Client Credentials grant type with the following cURL command.

     curl -k -X POST https://localhost:9443/oauth2/token -d "grant_type=client_credentials" -H "Authorization: Basic Base64(consumer-key:consumer-secret)"

     e.g. `curl -k -X POST https://localhost:9443/oauth2/token -d "grant_type=client_credentials" -H "Authorization: Basic UTdhZmhRZGdmV1ZobjhrRlBYeXdtUzRFX09NYTpEM01RbFU1WW1iQWZJMmU2Mkd3OHZINWZ0XzBh"`

# WSO2 Carbon Product
When you using a WSO2 Carbon Product (API Manager, Identity Server, Enterprise Integrator or Stream Processor) rather than a testing session in your local machine you should change the default passwords. In default, for ‘Super Tent’ admin account has the following credentials.

     Username: admin
     Password: admin

There are 3 methods:

     - At the first startup (Define a new password)
     - Change password using the previous password (Change the password)
     - Change password without the previous password (Reset the Password)

1) At the first startup:
   In this method, you only can define the admin login password before the first startup of the WSO2 product server. Therefore, you should modify admin password at the very begging 
   of the server start.

   In all WSO2 carbon products, user data stored database has been defined on user-mgt.xml file which is located at

        <PRODUCT_HOME>/repository/conf/user-mgt.xml
        e.g. /home/mohammedayman/projects/sme/fundingGate/integration/wso2am-4.2.0/repository/conf

   You can change the admin login password parameter in the user-mgt.xml file. Then start the product and login to the carbon console with new credentials.
   After the first startup, all the credentials will store in the user database and you would not able to change it from the above file. So you can only change it (where the change 
   is actually effective) before you start the WSO2 carbon product for the first time.
   
2) Change password using the previous password:
   - After the first startup the WSO2 product, you would not be able to change the admin password by the above method. However, we can easily change the admin login password by 
     login to carbon console that is available through the browser. You should have the previous admin credentials to login carbon console first.
   - Go to carbon management console using your favorite browser. ( default path is: https://localhost:9943/carbon).
   - Login with the admin credentials (default is admin/admin).
   - On the Main tab, click List under Users and Roles.
   - To change the admin password, click Change My Password, enter your current admin password and new admin password, and click Change. 

3) Change password without the previous password:
   - What would happen, if you have forgotten the admin password (and therefore cannot access the Management Console) or you do not have the credentials with you. Do not worry, not 
     everything is lost yet and still, you can change the admin password with this method.
   - If you have not installed “ant” in your server, install it by running following command. ( Apache Ant is a prerequisite for this method)
     
          sudo apt-get install ant

   - Copy related JDBC driver (which match with the database management system you have used) to the following location.

          <PRODUCT_HOME>/lib/
     
   - If you are using MySQL database, you can download MySQL database drivers.
   - Go to the following location.

          cd <PRODUCT_HOME>/bin/
     
   - Run the following command to reset the password for your admin account.

`bash chpasswd.sh --db-driver "<DB_DRIVER_CLASS>" --db-url "<DB_URL>" --db-username "<DB_USERNAME>" --db-password "<DB_PASSWORD>" --username "admin" --new-password "<NEW_PASSWORD>"`
     
   - The following message is displayed if the password is updated successfully.

          Password of user [username] updated successfully
          
   - Login to the carbon management console with new admin credentials.

# Associating User Accounts
WSO2 Identity Server (WSO2 IS) allows you to associate multiple accounts you may have, and switch between accounts once you associate accounts. WSO2 IS also allows you to connect your federated user credentials with your WSO2 Identity Server account. This topic provides instructions on how to associate all your user accounts to the account with which you have logged on.
If you want to associate user accounts of federated users via the dashboard, add the following configuration to the /repository/conf/deployment.toml file.

     `[user.association]
     enable_for_federated_users = true`
     
The recommended approach is to have the enable_for_federated_users parameter set to false so that manual federated user association is not allowed by default via the dashboard.

Follow one of the two approaches below to associate all your user accounts:

1) Using the AdminService:

   The first approach is to use the AdminService. You can access this admin service using the following URL: `https://<HOST_NAME>:9443/services/UserAccountAssociationService?wsdl`.

   If you are new to admin services, see Calling Admin Services: https://is.docs.wso2.com/en/5.9.0/develop/calling-admin-services/.

   The following actions can be performed using above admin service.

    - Create a new user account association
    - Delete an existing user account association
    - Get all associated user accounts of the logged in user
    - Switch between associated user accounts without re-authenticate with the system

2) Using the dashboard:
    The WSO2 Identity Server end user dashboard can be used to associate the accounts. You can associate a local user account or a federated user account:

    Managing local user IDs:
   
    - Go to the dashboard URL: https://localhost:9443/dashboard/
    - Log in using your username and password.
    - Click the View details button that corresponds to the Associated User Accounts gadget.
    - You can see all associated accounts of the user that you logged in as. This table includes the user ID and identity provider of all the associated user accounts of the user.
    - You can initiate a new user account association by clicking the Add Association button under Associated Accounts.
    - Select Local as the Account Type, and enter the username and password of the user account that you want to connect to.
      Click Associate to associate this user account.  If it is authentic, WSO2 Identity Server authenticates the user account and saves that user account as an association to the         user account of the logged in user.
    - You can delete this user account association by clicking Remove in the Associated Accounts list.
    - You can also switch between associated user accounts without having to re-authenticate the user account with the Identity Server. In the user dashboard UI, the associated user       accounts appear under the dropdown list at the top 
      right corner of your screen. You can switch between accounts by selecting the required user account from the dropdown. Note that the session key does not change during this          operation.

    Managing federated user IDs

    - You can connect your federated user IDs with your WSO2 Identity Server account from the end user dashboard. To set this up, do the following.

      Note: You need to setup an Identity Provider before continuing this process. For more information on how to do this, see Adding and Configuring an Identity Provider.

    - Go to the dashboard URL: https://localhost:9443/dashboard/
    - Log in using your username and password.
    - Click the View details button that corresponds to the Associated User Accounts gadget.
    - You can see all associated accounts of the user that you logged in as. This table includes user ID and the identity provider of all associated user accounts of the user.
    - You can initiate a new user account association by clicking the Add Association button under Associated Accounts.
    - Select the Federated as the Account Type from the dropdown provided, and enter the username and password.
      Click Associate to connect this user account to the WSO2 Identity Server account of the logged in user.
   - You can delete this user account association by clicking Remove on the Associated Accounts list.

# Getting Started with WSO2 API Controller (apictl)
WSO2 API Controller (apictl) is a command-line tool providing the capability to move APIs, API Products, and Applications across environments and to perform CI/CD operations. It can also be used to perform these same tasks on a Kubernetes deployment. Furthermore, it can perform WSO2 Micro Integrator (WSO2 MI) server specific operations such as monitoring Synapse artifacts and performing MI management/administrative tasks from the command line.

1) Download and initialize the `apictl`:
   
https://apim.docs.wso2.com/en/4.0.0/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#getting-started-with-wso2-api-controller-apictl

- Download apictl based on your preferred platform (i.e. Linux).
- Extract the downloaded archive of the apictl to the desired location.
- Navigate to the working directory where the executable apictl resides.
- Add the current working directory to your system's $PATH variable to be able to access the executable from anywhere.
  
       export PATH=/home/mohammedayman/projects/sme/fundingGate/integration/apictl-4.0.4-linux-x64/apictl:$PATH
- Execute the following command to start the apictl: `apictl`
- For `environment` and for more details:

  https://apim.docs.wso2.com/en/4.0.0/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#add-an-environment

# Importing APIs Via Dev First Approach

  You can see this:

  https://apim.docs.wso2.com/en/4.0.0/install-and-setup/setup/api-controller/managing-apis-api-products/importing-apis-via-dev-first-approach/
  
  WSO2 API Controller (`apictl`) allows you to create and deploy APIs without using the Publisher Portal of the WSO2 API Manager (WSO2 API-M). 
  You can use this feature to create an API `from scratch` or `using an existing Swagger or Open API specification` and then deploy it to the desired WSO2 API-M environment.
   1)  `export PATH=/home/mohammedayman/projects/sme/fundingGate/integration/apictl-4.0.4-linux-x64/apictl:$PATH`.
   2)  The directory structure for the configuration files (`<USER_HOME>/.wso2apictl`) will be created upon the execution of the apictl command.
   3)  If you want to change the default location for the .wso2apictl directory, set an environment variable (APICTL_CONFIG_DIR) as follows with the path for the desired location:

             export APICTL_CONFIG_DIR="/home/wso2user/CLI"
       
   4) Global flags for apictl:
      
            --verbose
                Enable verbose logs (Provides more information on execution)
            --insecure, -k
                Allow connections to SSL sites without certs
            --help, -h
                Display information and example usage of a command
   
   5) Set mode of apictl:
      From the apictl 4.0.0 onwards the flag (--mode) which was used to set the mode of apictl has been deprecated. Now, you do not need to set the mode of apictl, because if you 
      want to execute Kubernetes based commads, you just need to add the k8s keyword after apictl keyword. (Example: `apictl k8s add api`). By default apictl will execute the 
      commands in the default mode (which means if you did not use k8s keyword).
      You can still use the mode flag as explained below if you need it, but it will be removed in the future.

            apictl set --mode <mode>

            apictl set --mode default

            apictl set --mode kubernetes
      
   6) Add an environment: You can add environments by either manually editing the `<USER_HOME>/.wso2apictl/main_config.yaml`  e.g. `/home/mohammedayman/.wso2apictl/main_config.yaml` 
      file or by running the following apictl command:
      
            apictl add env <environment-name>

      - Make sure that the WSO2 API Manager (WSO2 API-M) 4.0.0 version is started and that the 4.0.4 version of apictl is set up.
      - Run the following apictl command to add an environment:
        
              apictl add env <environment-name> \
                     --registration <client-registration-endpoint> \
                     --apim <API-Manager-endpoint> \
                     --token <token-endpoint> \
                     --admin <admin-REST-API-endpoint> \
                     --publisher <publisher-portal-endpoint> \
                     --devportal <developer-portal-endpoint> \
                     --mi <mi-management-endpoint>
     
        Flags: To add a WSO2 API-M

               Required:
               (either)
               --apim : API Manager endpoint for the environments
               OR (the following 4)
               --registration : Registration endpoint for the environment
               --admin : Admin endpoint for the environment
               --publisher : Publisher Portal endpoint for the environment
               --devportal : Developer Portal endpoint for the environment
               
               Optional :
               --token : Token endpoint for the environment
               
               To add a WSO2 MI
               
               Required :
               --mi : Management endpoint of the Micro Integrator

              When adding an environment, when the optional flags are not given, apictl will automatically derive those from `--apim` flag value.
        
              You can either provide only the flag `--apim` , or all the other 4 flags (`--registration`, `--publisher`, `--devportal`, `--admin`)
              without providing --apim flag.
              If you are omitting any of `--registration`, `--publisher`, `--devportal`, `--admin` flags,
              you need to specify `--apim` flag with the WSO2 API-M endpoint. In both of the above cases
              `--token` flag is optional and can be used to provide a user-preferred token endpoint.
              You can use the `--mi` flag to add a Micro Integrator instance to an environment.

        - Adding a WSO2 API-M to an environment using `--apim` flag:

                apictl add env dev \
                  --apim https://localhost:9443
     
        - Adding a WSO2 API-M to an environment using --registration, --publisher, --devportal, --admin flags

                apictl add env production \
                  --registration https://idp.com:9444 \
                  --admin https://apim.com:9444 \
                  --publisher https://apim.com:9444 \
                  --devportal https://apps.com:9444 \
                  --token https://gw.com:8244/token   

        - Adding a WSO2 MI to an environment using `--mi` flag:

                 apictl add env dev \
                     --mi https://localhost:9164
        - Adding both WSO2 API-M and WSO2 MI to an environment:

                apictl add env local \
                  --apim https://localhost:9443 \
                  --mi https://localhost:9164

        - Remove an environment:

                  apictl remove env <environment-name> e.g.apictl remove env production

        - Get environments:

                apictl get envs

                Flags:
                  Optional :
                  --format : pretty-print environments using templates

        - Login to an environment:
          - After adding an environment, you can log in to the WSO2 API-M instance in that environment using credentials.
            
                  apictl login <environment-name> 
                  apictl login <environment-name> -u <username> 
                  apictl login <environment-name> -u <username> -p <password>
                  if you got certification error Run: apictl -k login test
                  If you run apictl login <environment-name> you are prompted to provide both the username and the password.
                  If you run apictl login <environment-name> --username <username>, you are prompted to provide the password.                
                  Flags:
                  Optional :
                  --username or -u : Username for login
                  --password or -p : Password for login
                  --password-stdin : Get password from stdin
                  Example:
                  apictl login dev 
                  apictl login dev -u admin -p admin 
                  apictl login dev --username admin --password admin
                  apictl -k login dev -u admin -p admin 
                  Using --password in apictl is not secure. You can use --password-stdin instead.
                  For example: cat ~/.mypassword | ./apictl login dev --username admin --password-stdin 
          
        - Logout from an environment:

                  apictl logout <environment-name> e.g. apictl logout dev

        - For other options (Set HTTP request timeout, Set TLS renegotiation mode, Set export directory, SSL) see the link:
       
          https://apim.docs.wso2.com/en/4.0.0/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#add-an-environment
          
   7) From Scratch:

      - Open a terminal window and navigate to the path you need to create the project.

                 apictl init <Project Path>   
                 apictl init <Project Path> --definition <API definition template file>  --force=<force create project>
                 Example
                 cd /home/mohammedayman/projects/sme/fundingGate/integration/myProjects
                 apictl init SampleAPI
                 apictl init SampleAPI --definition definition.yaml --force=true
        
   8) From OpenAPI/Swagger Specification:

      - Open a terminal window and navigate to the path you need to create the project.
      - You can use a Swagger2 and OpenAPI3 specification to generate an API. The file format should be YAML or JSON.

                  apictl init <Project Path> --oas <Path to API specification>
                  apictl init <Project Path> --oas <Path to API specification> --definition <API definition template file> --force=<force create project>
                  Example
                  apictl init Petstore --oas petstore.yaml
                  apictl init Petstore --oas https://petstore.swagger.io/v2/swagger.json
                  apictl init Petstore --oas petstore.yaml --definition definition.yaml --force=true
                  In my case: apictl init FundingGate --oas fundinggate.yaml --definition fundinggate.yaml --force=true
                  Info:
                  When you initialize an API project using an OpenAPI specification, apictl will automatically read the OpenAPI definition
                  and populate a certain set of configs in the API definition file, api.yaml.
                  Flags:
                  Optional :
                  --definition or -d : Provide a YAML definition of API
                  --oas : Provide an OpenAPI specification file/URL for the API
                  --force or -f : To overwrite the directory and create the project

        A project folder with the following default structure will be created in the given directory.

                  
                  ├── api.yaml
                  ├── api_meta.yaml
                  ├── deployment_environments.yaml
                  ├── Client-certificates
                  ├── Definitions
                  │   └── swagger.yaml
                  ├── Docs
                  ├── Endpoint-certificates
                  ├── Image
                  └── Sequences
                      ├── fault-sequence
                      ├── in-sequence
                      └── out-sequence
        
        
   9) Import an API project:
       
      Before you begin...
         - Make sure you have already created an environment to which you are planning to import the API.
         - Make sure you have logged-in to the importing environment.
         - After editing the mandatory fields in the API Project, you can import the API to an environment using any of the following commands.
           
                 apictl import api -f <path to API Project> -e <environment> 
                 apictl import api --file <path to API Project> --environment <environment> --rotate-revision
                 apictl import api --file <path to API Project> --environment <environment> --params=<environment params file>
                 Flags:
                     Required :
                     --file or -f : The file path of the API project to import.
                     --environment or -e : Environment to which the API should be imported.
                     Optional :
                     --rotate-revision : If the maximum revision limit reached, delete the oldest revision and create a new revision.
                     --skip-deployments : Skip the deployment environments specified in the project and only update the current API of the API.
                     --preserve-provider : Preserve the existing provider of API after importing. The default value is true.
                     --update : Update an existing API or create a new API in the importing environment.
                     --params : Provide a API Manager environment params file. For more information, see Configuring Environment Specific Parameters.
                     --skip-cleanup : Leave all temporary files created in apictl during import process. The default value is false.
                     Example                    
                     apictl import api -f ~/myapi -e production 
                     apictl import api --file ~/myapi --environment production --rotate-revision
                     apictl import api --file ~/myapi --environment production --params prod/params.yaml

                     When using the --update flag with the import api command, apictl will check if the given API exists in the targeted environment.
                     If the API exists, it will update the existing API. If not, it will create a new API in the imported environment.
                     Changes to the import command with the revision support for APIs
                     From WSO2 API-M 4.0.0 onwards, you have to create a new revision in order to deploy an API in a Gateway environment and only a revision can be deployed in a 
                     Gateway environment.
                     With the import command of the apictl, if the API project has specified the deployment environments, the import will first update the current API of the API.
                     If the number of revisions created for that API do not exceed the max revision limit of 5, a new revision of that API will be created and that revision will be 
                     deployed in the specified Gateway environments.
                     If the max revision numbers are reached, the imported API will only update the current API and not be deployed in the specified Gateway environments.
                     You can use the --rotate-revision flag with the import command and if the max revision limit is reached, the import operation will delete the earliest revision 
                     for that API and create a new revision. This new revision will be deployed in the specified Gateway environments.

# CMDs

            Go to: https://localhost:9443/carbon
            create a new user:devops with this role: Internal/devops          
            cd ~
            mkdir vcs
            cd vcs;mkdir Source;mkdir Deployment
            apictl set --vcs-source-repo-path /home/mohammedayman/vcs/Source/
            apictl set --vcs-deployment-repo-path /home/mohammedayman/vcs/Deployment/
            apictl add env development --apim https://localhost:9443
            apictl add env production --apim https://localhost:9444
            apictl -k login development
            => username: devops / password: 123456
            You should deplo/pulish the application then:
            apictl -k export api -n PizzaShackAPI -v 1.0.0 -e development
            tree /home/mohammedayman/.wso2apictl/exported/apis
            unzip /home/mohammedayman/.wso2apictl/exported/apis/development/PizzaShackAPI_1.0.0.zip -d ~/vcs/Source/
            apictl gen deployment-dir -s Source/PizzaShackAPI-1.0.0 -d Deployment/
            cd Deployment/
            git init
            apictl vcs init ==> vcs.yaml file will be created
            git add .
            git commit -m "Add new specific configs"
            cd ../Source/
            git init
            apictl vcs init ==> vcs.yaml file will be created
            git add .
            git commit -m "Add Projects"
            apictl -k login production
            => username: devops / password: 123456
            apictl -k vcs deploy -e production

# Change Default Databases

1- Define the hostname for configuring permissions for the new database in the /etc/hosts file. (Do this step only if your database is not on your local machine and on a separate server.)

2- Start the MySQL service.

3- Install a mysql-client in each of the API-M servers in which WSO2 API-M is deployed.

4- mysql -h <MYSQL_HOST_IP> -u <USER_NAME> -p (e.g. mysql -h localhost -u root -p) => The user should have database creation privileges.

5- CREATE DATABASE <DATABASE_NAME>; (When creating the database related to apim_db with MySQL 8.0, add character set latin1 to avoid the MySQL Linux ERROR 1071 (42000).CREATE DATABASE <APIM_DATABASE_NAME> character set latin1;)
e.g. CREATE DATABASE wso2_db character set latin1;

6- If you are using MySQL version - 8.0.x, use the following commands to create the users and the grant authorization:

                  CREATE USER 'apimadmin'@'localhost' IDENTIFIED BY '!Apimadmin123';
                  GRANT ALL ON apim_db.* TO 'apimadmin'@'localhost';
                  CREATE USER 'sharedadmin'@'localhost' IDENTIFIED BY '!Sharedadmin123';
                  GRANT ALL ON shared_db.* TO 'sharedadmin'@'localhost';


7- After you have finalized the permissions, reload all the privileges. => FLUSH PRIVILEGES;

8- Log out from the MySQL command prompt. => quit;

9- Executing DB scripts to create tables on MySQL database

         Execute the relevant script to create tables in the registry and user manager database (WSO2_SHARED_DB).
         mysql -u sharedadmin -p -Dshared_db < '<API-M_HOME>/dbscripts/mysql.sql';
         e.g. mysql -u sharedadmin -p -Dshared_db < '/home/mohammedayman/projects/sme/fundingGate/integration/wso2am-4.2.0/dbscripts/mysql.sql';
         Execute the relevant script to create tables in the apim database (WSO2AM_DB).
         mysql -u apimadmin -p -Dapim_db < '<API-M_HOME>/dbscripts/apimgt/mysql.sql';
         e.g. mysql -u apimadmin -p -Dapim_db < '/home/mohammedayman/projects/sme/fundingGate/integration/wso2am-4.2.0/dbscripts/apimgt/mysql.sql';

10- Setting up the drivers

         Be sure to use the connector version that is supported by the MySQL version you use. If you come across any issues due to version incompatibility, follow the instructions below:
         Shut down the server and remove all the existing connectors from the <API-M_HOME>/repository/components/lib and <API-M_HOME>/repository/components/dropins directories.
         Download the connector JAR that is compatible with your current MySQL version.
         Copy the JAR file only to the <API-M_HOME>/repository/components/lib location.
         Files will be copied automatically to the dropins folder during the server startup.
         /home/mohammedayman/projects/sme/fundingGate/integration/wso2am-4.2.0/repository/components/lib

11- Changing the database to MySQL

         Creating the datasource connection to MySQL
         A datasource is used to establish a connection to a database. By default, WSO2_SHARED_DB and WSO2AM_DB datasources are configured in the deployment.toml file to connect to the                 default H2 databases.

12- Open the <API-M_HOME>/repository/conf/deployment.toml configuration file and locate the [database.shared_db] and [database.apim_db] configuration elements.

         example:
         [database.apim_db]
         type = "mysql"
         url = "jdbc:mysql://localhost:3306/apim_db?useSSL=false"
         username = "apimadmin"
         password = "!Apimadmin123"
         driver="com.mysql.cj.jdbc.Driver"
         
         [database.shared_db]
         type = "mysql"
         url = "jdbc:mysql://localhost:3306/shared_db?useSSL=false"
         username = "sharedadmin"
         password = "!Sharedadmin123"
         driver="com.mysql.cj.jdbc.Driver"

13- Restart the server.         

# Writing logs into an external DB

see this:

https://stackoverflow.com/collectives/wso2/articles/72709174/how-to-write-wso2-product-logs-to-external-database

        	CREATE DATABASE Log_DB character set latin1;
        	CREATE USER 'adminlog'@'%' IDENTIFIED BY '!Adminlog123';
		GRANT ALL PRIVILEGES ON Log_DB.* TO 'adminlog'@'%';
	 	FLUSH PRIVILEGES;
   		USE Log_DB;
		CREATE TABLE LOGS(LOG_TIME VARCHAR(20) NOT NULL, LOG_LEVEL VARCHAR(20) NOT NULL, MESSAGE VARCHAR(1000) NOT NULL);
   		If you get error: Public Key Retrieval is not allowed
   		Right-click your connection, choose "Edit Connection"
		On the "Connection settings" screen (main screen), click on "Edit Driver Settings"
		Click on "Driver properties"
		Change two properties: "useSSL" and "allowPublicKeyRetrieval"
		Set their values to "false" and "true" by double-clicking on the "value" column

		in this file: /home/mohammedayman/projects/sme/fundingGate/integration/wso2am-4.0.0/repository/conf/log4j2.properties
		add those lines:
  		appenders=CARBON_CONSOLE, CARBON_LOGFILE, AUDIT_LOGFILE, ATOMIKOS_LOGFILE, CARBON_TRACE_LOGFILE, ERROR_LOGFILE, OPEN_TRACING,SERVICE_APPENDER, TRACE_APPENDER, osgi, 		
  		CORRELATION, BOTDATA_APPENDER, API_LOGFILE, jdbc
		#####################################################Logs to External Database##################################################################################
  		appender.jdbc.type = JDBC
		appender.jdbc.name=jdbc
		appender.jdbc.connectionSource.driverClassName=com.mysql.cj.jdbc.Driver
		appender.jdbc.connectionSource.type= DriverManager
		appender.jdbc.connectionSource.connectionString=jdbc:mysql://localhost:3306/Log_DB?allowPublicKeyRetrieval=true&useSSL=false
		appender.jdbc.connectionSource.userName=adminlog
		appender.jdbc.connectionSource.password=!Adminlog123
		appender.jdbc.tableName=LOGS
		appender.jdbc.ignoreExceptions=false
		appender.jdbc.columnConfigs[0].type = COLUMN
		appender.jdbc.columnConfigs[0].name = LOG_TIME
		appender.jdbc.columnConfigs[0].pattern =%d
		appender.jdbc.columnConfigs[0].isUnicode =false
		appender.jdbc.columnConfigs[1].type = COLUMN
		appender.jdbc.columnConfigs[1].name = LOG_LEVEL
		appender.jdbc.columnConfigs[1].pattern =%5p
		appender.jdbc.columnConfigs[1].isUnicode =false
		appender.jdbc.columnConfigs[2].type = COLUMN
		appender.jdbc.columnConfigs[2].name = MESSAGE
		appender.jdbc.columnConfigs[2].pattern =%mm%ex%n
		appender.jdbc.columnConfigs[2].isUnicode =false
		appender.jdbc.bufferSize=1000
		#appender.jdbc.filter.1.type=RegexFilter
		#appender.jdbc.filter.1.regex="<regex-pattern>"
		#appender.jdbc.filter.1.onMatch=ACCEPT
		#appender.jdbc.filter.1.onMismatch=DENY
		
		logger.AUDIT_LOG.appenderRef.jdbc.ref = jdbc
		logger.AUDIT_LOG.name = AUDIT_LOG
		logger.AUDIT_LOG.level = INFO
		logger.AUDIT_LOG.appenderRef.AUDIT_LOGFILE.ref = AUDIT_LOGFILE
		logger.AUDIT_LOG.appenderRef.jdbc.ref = jdbc
		logger.AUDIT_LOG.additivity = false
		
		Thats it. Restart the server.
