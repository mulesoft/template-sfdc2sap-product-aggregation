
# Template: Salesforce and SAP Product Aggregation

This template aggregates products from Salesforce and materials from SAP into a CSV file. You can modify this basic pattern to collect from more or different sources, and to produce formats other than CSV. 

You can trigger the application with an HTTP call either manually or programmatically. Products are sorted such that the products only in Salesforce appear first, followed by materials only in SAP, and lastly by products found in both systems. The custom sort or merge logic can be easily modified to present the data as needed. This template also serves as a great base for building APIs using the Anypoint Platform.

Aggregation templates can be easily extended to return a multitude of data in mobile friendly form to power your mobile initiatives by providing easily consumable data structures from otherwise complex backend systems.

![e603dee4-9951-47bb-9acf-607b1ca1aa67-image.png](https://exchange2-file-upload-service-kprod.s3.us-east-1.amazonaws.com:443/e603dee4-9951-47bb-9acf-607b1ca1aa67-image.png)

**Note:** Any references in the video to DataMapper have been updated in the template with DataWeave transformations.

[//]: # (![]\(https://www.youtube.com/embed/uOmaCVex_aA?wmode=transparent\))
[![YouTube Video](http://img.youtube.com/vi/uOmaCVex_aA/0.jpg)](https://www.youtube.com/watch?v=uOmaCVex_aA)

### License Agreement

This template is subject to the conditions of the [MuleSoft License Agreement](https://s3.amazonaws.com/templates-examples/AnypointTemplateLicense.pdf).

Review the terms of the license before downloading and using this template. You can use this template for free with the Mule Enterprise Edition, CloudHub, or as a trial in Anypoint Studio.

# Use Case

I want to aggregate products from Salesforce and SAP and compare them to see which products can only be found in one of the two and which products are in both.

This template generates the result a CSV report that is sent by email to addresses you configure.

This template extracts data from two systems, aggregates data, compares values of fields for the objects, and generates a CSV report of the differences.

This template gets products from Salesforce and materials from SAP, compares by the name of the products, and generates a CSV file which shows product in Salesforce, product in SAP, and products in Salesforce and SAP. The report is then emailed to a configured group of email addresses.

# Considerations

To make this template run, there are certain preconditions that must be considered. All of them deal with the preparations in both, that must be made for all to run smoothly.

Failing to do so could lead to unexpected behavior of the template.

## Disclaimer

This template uses a few private Maven dependencies from MuleSoft to work. If you intend to run this template with Maven support, you need to add three dependencies in the pom.xml file that begin with the following group IDs:

    com.sap.conn.jco or com.sap.conn.idoc

## SAP Considerations

Here's what you need to know to get this template to work with SAP.

### As a Data Destination

There are no considerations with using SAP as a data destination.

## Salesforce Considerations

Here's what you need to know about Salesforce to get this template to work.

### FAQ

- Where can I check that the field configuration for my Salesforce instance is the right one? See: [Salesforce: Checking Field Accessibility for a Particular Field](https://help.salesforce.com/HTViewHelpDoc?id=checking_field_accessibility_for_a_particular_field.htm&language=en_US "Salesforce: Checking Field Accessibility for a Particular Field")
- Can I modify the Field Access Settings? How? See: [Salesforce: Modifying Field Access Settings](https://help.salesforce.com/HTViewHelpDoc?id=modifying_field_access_settings.htm&language=en_US "Salesforce: Modifying Field Access Settings")

### As a Data Source

If the user who configured the template for the source system does not have at least _read only_ permissions for the fields that are fetched, then an _InvalidFieldFault_ API fault displays.

```
java.lang.RuntimeException: [InvalidFieldFault [ApiQueryFault [ApiFault  
exceptionCode='INVALID_FIELD'
exceptionMessage='
Account.Phone, Account.Rating, Account.RecordTypeId, Account.ShippingCity
^
ERROR at Row:1:Column:486
No such column 'RecordTypeId' on entity 'Account'. If you are attempting 
to use a custom field, be sure to append the '__c' after the custom field 
name. Reference your WSDL or the describe call for the appropriate names.'
]
row='1'
column='486'
]
]
```

# Run it!

Simple steps to get Salesforce and SAP Product Aggregation running.

## Running On Premises

In this section we help you run your template on your computer.

### Where to Download Anypoint Studio and the Mule Runtime

If you are a newcomer to Mule, here is where to get the tools.

- [Download Anypoint Studio](https://www.mulesoft.com/platform/studio)
- [Download Mule runtime](https://www.mulesoft.com/lp/dl/mule-esb-enterprise)

### Importing a Template into Studio

In Studio, click the Exchange X icon in the upper left of the taskbar, log in with your

Anypoint Platform credentials, search for the template, and click **Open**.

### Running on Studio

After you import your template into Anypoint Studio, follow these steps to run it:

- Locate the properties file `mule.dev.properties`, in src/main/resources.
- Complete all the properties required as per the examples in the "Properties to Configure" section.
- Right click the template project folder.
- Hover your mouse over `Run as`
- Click `Mule Application (configure)`
- Inside the dialog, select Environment and set the variable `mule.env` to the value `dev`
- Click `Run`To make this template run in Studio, there are a few extra steps that needs to be made.Search for "Enabling Your Studio Project for SAP" at `https://docs.mulesoft.com` for more information.

### Running on Mule Standalone

Complete all properties in one of the property files, for example in mule.prod.properties and run your app with the corresponding environment variable. To follow the example, this is `mule.env=prod`.

After this, to trigger the use case, browse to the local HTTP endpoint with the port you configured in your file. For example if you use `9090` for the port, browse to `http://localhost:9090/generatereport` and the application creates a CSV report and sends it to the configured emails.

## Running on CloudHub

While creating your application on CloudHub (or you can do it later as a next step), go to Runtime Manager > Manage Application > Properties to set the environment variables listed in "Properties to Configure" as well as the **mule.env**.

After you have your app running, if you chose `template-sfdc2sap-product-aggregation` as the domain name to trigger the use case, browse to `http://template-sfdc2sap-product-aggregation.cloudhub.io/generatereport`, and report gets sent to the configured emails.

### Deploying your Anypoint Template on CloudHub

Studio provides an easy way to deploy your template directly to CloudHub, for the specific steps to do so check this

## Properties to Configure

To use this template, configure properties (credentials, configurations, etc.) in the properties file or in CloudHub from Runtime Manager > Manage Application > Properties. The sections that follow list example values.

### Application Configuration

### HTTP Connector Configuration

- http.port `9090` 

### Salesforce Connector Configuration

- sfdc.username `bob.dylan@sfdc`
- sfdc.password `DylanPassword123`
- sfdc.securityToken `avsfwCUl7apQs56Xq2AKi3X`

### SAP Connector Configuration

- sap.jco.ashost `your.sap.address.com`
- sap.jco.user `SAP_USER`
- sap.jco.passwd `SAP_PASS`
- sap.jco.sysnr `14`
- sap.jco.client `800`
- sap.jco.lang `EN`
- sap.maxrows `100`

### SMTP Services Configuration

- smtp.host `smtp.example.com`
- smtp.port `587`
- smtp.user `exampleuser@example.com`
- smtp.password `ExamplePassword456`

### Email Details

- mail.from `exampleuser@example.com`
- mail.to `woody.guthrie@example.com`
- mail.subject `SFDC Products report`
- mail.body `Report comparing products from Salesforce and SAP Materials`
- attachment.name `Productsreport.csv`

# API Calls

Salesforce imposes limits on the number of API calls that can be made. However, this template

only makes one API call to Salesforce during aggregation.

# Customize It!

This brief guide intends to give a high level idea of how this template is built and how you can change it according to your needs.

As Mule applications are based on XML files, this page describes the XML files used with this template.

More files are available such as test classes and Mule application files, but to keep it simple, we focus on these XML files:

- config.xml
- businessLogic.xml
- endpoints.xml
- errorHandling.xml

## config.xml

Configuration for connectors and configuration properties are set in this file. Even change the configuration here, all parameters that can be modified are in properties file, which is the recommended place to make your changes. However if you want to do core changes to the logic, you need to modify this file.

In the Studio visual editor, the properties are on the _Global Element_ tab.

## businessLogic.xml

The functional aspect of the template is implemented in this XML, directed by one flow responsible for conducting the aggregation of data, comparing records, and finally formatting the output as a CSV report.

Using the Scatter-Gather component, this template queries the data in different systems. After that the aggregation is implemented in a DataWeave 2 script using the Transform component.

Aggregated results are sorted by:

1. Products only in Salesforce.
2. Products (Materials) only in SAP.
3. Products (Materials) in both Salesforce and SAP.

The result is transformed to CSV format. The final report in CSV format is sent to the email addresses  you configured in the `mule.*.properties` file.

## endpoints.xml

This is the file where you find the endpoint to start the aggregation. This template uses an HTTP Listener to trigger the use case.

### Trigger Flow

**HTTP Listener** - Start Report Generation

- `${http.port}` is set as a property to be defined either on a property file or in CloudHub environment variables.
- The path configured by default is `generatereport` and you are free to change as you prefer.
- The host name for all endpoints in your CloudHub configuration is `localhost`. CloudHub then routes requests from your application domain URL to the endpoint.

## errorHandling.xml

This is the right place to handle how your integration reacts depending on the different exceptions.

This file provides error handling that is referenced by the main flow in the business logic.
