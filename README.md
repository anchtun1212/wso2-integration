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
5) Open this URL to check: https://localhost:9443/devportal
6) The default credentials `username/password` are: `admin/admin`
7) Go to: https://localhost:9443/publisher to see APIs
8) For `Authorization` you can use: `header: 'Authorization : Bearer ACCESS_TOKEN' or 'Authorization : Basic ACCESS_TOKEN' or 'apikey: API_KEY'"`
9) CURL to Generate Access Token:

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
  You can use this feature to create an API from scratch or using an existing Swagger or Open API specification and then deploy it to the desired WSO2 API-M environment.
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
