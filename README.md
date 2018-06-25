# Office365 API audit log collector

Subscribe to and collect logs from Office365 auditing APIs (https://msdn.microsoft.com/en-us/office-365/office-365-management-activity-api-reference).
Currently has the option to output to a network socket (when using e.g. Graylog) or a file. 
Feel free to contribute other outputs if you happen to build any. Default behavior is to retrieve logs of the last 24 hours.

## Use cases:

- Ad-lib log retrieval;
- Scheduling regular execution to retrieve the full audit trail.

## Features:

- Subscribe to the audit logs of your choice through the subscription script;
- Collect General, Exchange, Sharepoint, Azure active directory and/or DLP audit logs through the collector script;
- Output to file or to a Graylog input (i.e. send the logs over a network socket)

## Requirements:
- Office365 tenant;
- Azure application created for this script (see instructions)
- AzureAD tenant ID;
- Client key of the new Azure application;
- Secret key (created in the new Azure application, see instructions);
- App permissions to access the API's for the new Azure application (see instructions);
- Subscription to the API's of your choice (General/Sharepoint/Exchange/AzureAD/DLP, 
run AuditLogSubscription script and follow the instructions).

## Instructions:

### Creating an application in Azure:
- Create the 'Web app / API' type app by following these instructions: 
https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application
- Grant your new app permissions to read the Office API's: 
https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications#configure-a-client-application-to-access-web-apis 
- Use the 'AuditLogSubscriber' script to subscribe to the audit API's of your choice
- You can now run the script and retrieve logs. 

### Running the script:
- Retrieve all logs and send to a network socket / Graylog server:
`python3 AuditLogCollector.py 'tenant_id' 'client_key' 'secret_key' --exchange --dlp --azure_ad --general --sharepoint -p 'random_publisher_id' -g -gA logging.mooiland.nl -gP 6000`

## Todo:
- Add parameter for start- and end date for log retrieval.