# ValueAnalytics
A Tableau CRM templated app that leverages Event Monitoring data to highlight adoption, technical debt, and ultimately the business value in your core Salesforce implementation.

## Installation Instructions

This package requires Event Monitoring and Tableau CRM (Einstein Analytics) Platform, Growth or Plus licences. It utilises existing datasets containing event log data that you may already have in Tableau CRM, created either from the Event Monitoring Analtyics templated app, or from a custom log-ingestion process that created datasets with event log data via the API.

### Prerequisite: Setting Up The Log Ingestion process:

Easy Option: Tableau CRM Templated App

* (If the "Event Monitoring Analytics" Tableau CRM app is already running with the below-listed log types, you can skip to Package Deployment)
* Select a sandbox or production org
* [Ensure Event Monitoring Analytics is enabled](https://help.salesforce.com/s/articleView?id=sf.bi_app_event_monitor_enable_select_PSL.htm&type=5)
* [Assign permissions to users](https://help.salesforce.com/s/articleView?id=bi_app_event_monitor_create_permsets.htm&type=5&language=en_US)
* [Create the analytics app](https://help.salesforce.com/s/articleView?language=en_US&type=5&id=sf.bi_app_admin_wave_create.htm)
    * *Hard Requirement*: **must** include following log types:  LightningInteraction, LightningPageview, ApexExecution, ApexUnexpectedException, VisualforceRequest)

Harder Option: [Set up a custom process to push Event Logs into Tableau CRM](https://www.salesforcehacker.com/2015/01/simple-script-for-loading-event.html)

### Deploying the new dashboards

* After a successful AppExchange installation, navigate to the Tableau CRM Analytics studio, create a new app from a template, and search for "Value Analytics" in the list of templates.
* Select the existing datasets when prompted by the wizard. If you see multiple datasets of the same name, it is recommended that you clean-up your Event Monitoring app setup by ensuring there are not multiple apps ingesting the same logs.
* In the last step of the wizard, it is recommended to name the app "Value Analytics".
* After completing the wizard, the app will take some time to build. When complete, you can navigate the dashboards within the app.


## Dashboards

### User Journeys:
It is imperative that every business understands what parts of a Salesforce implementation are valuable to its users.  This dashboard gives a top-to-bottom view of what UI-level interactions users perform in Lightning, from apps, standard and custom objects, to components of a page layout, what they view and what they click. As a result, Salesforce sponsors, stakeholdes, owners, product owners, project managers, admins and developers have a clearer sense of what is valuable to users by virtue of their level of interaction with many of the customisations they have developed and improved and put in the hands of users.
This dashboard leverages the [LightingInteration event log](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_eventlogfile_lightninginteraction.htm); reading the documentation is strongly encouraged.

### Apex Performance:
A narrative of the raw ApexExecution dataset in order to help pin-point slow-performing code. Ideally for a Developer, Admin, QA, Release Manager and / or Product Owner to identify what code is consistently slow, what's started being slow, and what skillset is required to begin reviewing the code. Try and use this early-on in your development process, or at the very latest in a UAT full-copy sandbox, so you can spot trends in newly-problematic code and decide if a current release is about to introduce risk to the business in production.
This dashboard leverages the [ApexExecution event log](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_eventlogfile_apexexecution.htm); reading the documentation is strongly encouraged.

### Apex Exceptions
When Apex starts to break, quick and decisive action is needed. This dashboard gives a clear view of what Apex classes and methods are generating unhandled exceptions, by volume, over time. Realistically, every datapoint on this dashboard is something for developers to review, consider, and fix or prevent. QAs, Release Managers and Product Owners should be reviewing this dashboard early in the development process, or at the very latest in a UAT full-copy sandbox. If things are beaking, this dashboard will help decide if a current release is about to introduce risk to the business in production by breaking business-critical processes.
This dashboard leverages the [ApexUnexpectedException event log](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_eventlogfile_apexunexpectedexception.htm); reading the documentation is strongly encouraged.

### Lightning Page Performance
Helps you to identify the pages that are performing poorly in Lightning, by GEO, App, Object. Uses TCRM compare tables to calculate lost productivity due to poor page load time (EPT).
This dashboard leverages the [LightningPageView](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_eventlogfile_lightningpageview.htm) and [LightingInteration event log](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_eventlogfile_lightninginteraction.htm); reading the documentation is strongly encouraged.

![image](https://user-images.githubusercontent.com/20658634/157493917-9955c525-0332-4c2a-8b67-0caea2508815.png) 

## Notes, Observations, Comments:
