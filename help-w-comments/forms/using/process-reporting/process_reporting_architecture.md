---
title: How Process Reporting Works
seo-title: How Process Reporting Works
description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
seo-description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
uuid: 481c4168-41de-47d5-97f9-708dab92dc3f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: process-reporting
discoiquuid: 4a034304-1e59-47ef-939b-f73f07860220
index: y
internal: n
snippet: y
---

# How Process Reporting Works{#how-process-reporting-works}

Process Reporting is the reporting module of the AEM Forms on JEE.

Process Reporting allows you to run reports on AEM Forms processes and tasks.

Process Reporting uses the embedded Process Reporting repository to publish Forms data. It then uses that data to run reports.

Process Reporting consists of the following modules:

* [ProcessDataPublisher service](../../../forms/using/process-reporting/process_reporting_architecture.md#main-pars-header-1)
* [ProcessDataStorage service](../../../forms/using/process-reporting/process_reporting_architecture.md#main-pars-header-2)
* [OSGi service](../../../forms/using/process-reporting/process_reporting_architecture.md#main-pars-header-3)
* [Query Data servlet](../../../forms/using/process-reporting/process_reporting_architecture.md#main-pars-header-4)
* [Process Reporting user interface](../../../forms/using/process-reporting/process_reporting_architecture.md#main-pars-header-5)

## Process Reporting architecture <br> {#process-reporting-architecture-br}

![](assets/processreportingarchitecture.png)

## Process Reporting modules {#process-reporting-modules}

### ProcessDataPublisher service <br> {#processdatapublisher-service-br}

The ProcessDataPublisher server runs periodically on the AEM Forms database and extracts the data that has changed since the last run of the service. It then publishes the data to the Process Data Storage service.

For details on configuring the service, see [Configure ProcessDataPublisher service](../../../forms/using/process-reporting/install-start-process-reporting.md#main-pars-header-4).

### ProcessDataStorageProvider service <br> {#processdatastorageprovider-service-br}

The ProcessDataStorageProvider service receives process data from the ProcessDataPublisher service and saves the data to the Process Reporting repository.

For details on configuring the service, see [Configure ProcessDataStorageProvider service](../../../forms/using/process-reporting/install-start-process-reporting.md#main-pars-header-1).

### OSGi service <br> {#osgi-service-br}

The QueryDataServlet uses this service to obtain the reporting data from the Process Reporting repository.

### QueryDataServlet service <br> {#querydataservlet-service-br}

The QueryDataServlet service accepts queries from Process Reporting user interface.

The service then uses OSGi services to obtain the relevant reporting data, processes the data, and returns the data to the user interface.

### Process Reporting user interface <br> {#process-reporting-user-interface-br}

The Process Reporting user interface is a Web browser-based interface. You use this interface to view process and task information that is published from the AEM Forms database.

For an introduction to the Process Reporting user interface, see [Process Reporting user interface](/forms/using/process-reporting/process-reporting-user-interface).

### QueryDataServlet service <br> {#querydataservlet-service-br-1}

The QueryDataServlet service accepts queries from Process Reporting user interface.

The service then uses OSGi services to obtain the relevant reporting data, processes the data, and returns the data to the user interface.

### Custom Reports <br> {#custom-reports-br}

You can create your own custom reports and display these reports in the Custom Reports tab of the Process Reporting user interface.

For the steps to create a custom report, see To create a custom report in the article [Custom Reports in Process Reporting](../../../forms/using/process-reporting/process-reporting-custom-reports.md).

[**Contact Support**](https://www.adobe.com/account/sign-in.supportportal.html)