# Test ProxyService Project

1) Run the jar file with Java 8: `/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java -jar stockquote_service.jar`

2) Install SOAPUI

3) Create a new SOAP Project (in SOAPUI) based on: sample_proxy_1.wsdl

4) Execute: `getQuote` ==> `<xsd:symbol>IBM</xsd:symbol>`


# Deployed Proxy Services

1) Run the project

2) Go to: `Deployed Proxy Services` and copy the WSDL and run it on browser:

Example: http://support-ThinkPad-T490:8290/services/CustomProxyServiceStockQuoteService?wsdl

you can change manually by:

Exmaple: http://localhost:8290/services/CustomProxyServiceStockQuoteService?wsdl

You can use this WSDL to create a new SOAP project in SOAPUI


