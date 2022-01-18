Cortex XDR is the world's first detection and response app that natively integrates network, endpoint, and cloud data to stop sophisticated attacks.
This integration was integrated and tested with version xx of Cortex Core - IR

## Configure Investigation & Response on Cortex XSOAR

1. Navigate to **Settings** > **Integrations** > **Servers & Services**.
2. Search for Investigation & Response.
3. Click **Add instance** to create and configure a new integration instance.

    | **Parameter** | **Description** | **Required** |
    | --- | --- | --- |
    | Incident type |  | False |
    | Server URL (copy URL from Core - click ? to see more info.) |  | True |
    | API Key ID |  | True |
    | API Key |  | True |
    | HTTP Timeout | The timeout of the HTTP requests sent to Cortex XDR API \(in seconds\). | False |
    | Sync Incident Owners | For Cortex XSOAR version 6.0.0 and above. If selected, for every incident fetched from Cortex XDR to Cortex XSOAR, the incident owners will be synced. Note that once this value is changed and synchronized between the systems, additional changes will not be reflected. For example, if you change the owner in Cortex XSOAR, the new owner will also be changed in Cortex XDR. However, if you now change the owner back in Cortex XDR, this additional change will not be reflected in Cortex XSOAR. In addition, for this change to be reflected, the owners must exist in both Cortex XSOAR and Cortex XDR. | False |
    | Trust any certificate (not secure) |  | False |
    | Use system proxy settings |  | False |

4. Click **Test** to validate the URLs, token, and connection.
## Commands
You can execute these commands from the Cortex XSOAR CLI, as part of an automation, or in a playbook.
After you successfully execute a command, a DBot message appears in the War Room with the command details.
### core-isolate-endpoint
***
Isolates the specified endpoint.


#### Base Command

`core-isolate-endpoint`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_id | The endpoint ID (string) to isolate. You can retrieve the string from the core-get-endpoints command. | Required | 
| suppress_disconnected_endpoint_error | Whether to suppress an error when trying to isolate a disconnected endpoint. When sets to false, an error will be returned. Possible values are: true, false. Default is false. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.Isolation.endpoint_id | String | The endpoint ID. | 

### core-unisolate-endpoint
***
Reverses the isolation of an endpoint.


#### Base Command

`core-unisolate-endpoint`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_id | The endpoint ID (string) for which to reverse the isolation. You can retrieve it from the core-get-endpoints command. | Required | 
| suppress_disconnected_endpoint_error | Whether to suppress an error when trying to unisolate a disconnected endpoint. When sets to false, an error will be returned. Possible values are: true, false. Default is false. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.UnIsolation.endpoint_id | String | Isolates the specified endpoint. | 

### core-get-endpoints
***
Gets a list of endpoints, according to the passed filters. If there are no filters, all endpoints are returned. Filtering by multiple fields will be concatenated using AND condition (OR is not supported). Maximum result set size is 100. Offset is the zero-based number of endpoint from the start of the result set (start by counting from 0).


#### Base Command

`core-get-endpoints`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| endpoint_id_list | A comma-separated list of endpoint IDs. | Optional | 
| dist_name | A comma-separated list of distribution package names or installation package names. <br/>Example: dist_name1,dist_name2. | Optional | 
| ip_list | A comma-separated list of IP addresses.<br/>Example: 8.8.8.8,1.1.1.1. | Optional | 
| group_name | The group name to which the agent belongs.<br/>Example: group_name1,group_name2. | Optional | 
| platform | The endpoint platform. Valid values are\: "windows", "linux", "macos", or "android". . Possible values are: windows, linux, macos, android. | Optional | 
| alias_name | A comma-separated list of alias names.<br/>Examples: alias_name1,alias_name2. | Optional | 
| isolate | Specifies whether the endpoint was isolated or unisolated. Possible values are: isolated, unisolated. | Optional | 
| hostname | Hostname<br/>Example: hostname1,hostname2. | Optional | 
| first_seen_gte | All the agents that were first seen after {first_seen_gte}.<br/>Supported values:<br/>1579039377301 (time in milliseconds)<br/>"3 days" (relative date)<br/>"2019-10-21T23:45:00" (date). | Optional | 
| first_seen_lte | All the agents that were first seen before {first_seen_lte}.<br/>Supported values:<br/>1579039377301 (time in milliseconds)<br/>"3 days" (relative date)<br/>"2019-10-21T23:45:00" (date). | Optional | 
| last_seen_gte | All the agents that were last seen before {last_seen_gte}.<br/>Supported values:<br/>1579039377301 (time in milliseconds)<br/>"3 days" (relative date)<br/>"2019-10-21T23:45:00" (date). | Optional | 
| last_seen_lte | All the agents that were last seen before {last_seen_lte}.<br/>Supported values:<br/>1579039377301 (time in milliseconds)<br/>"3 days" (relative date)<br/>"2019-10-21T23:45:00" (date). | Optional | 
| page | Page number (for pagination). The default is 0 (the first page). Default is 0. | Optional | 
| limit | Maximum number of endpoints to return per page. The default and maximum is 30. Default is 30. | Optional | 
| sort_by | Specifies whether to sort endpoints by the first time or last time they were seen. Can be "first_seen" or "last_seen". Possible values are: first_seen, last_seen. | Optional | 
| sort_order | The order by which to sort results. Can be "asc" (ascending) or "desc" ( descending). Default set to asc. Possible values are: asc, desc. Default is asc. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.Endpoint.endpoint_id | String | The endpoint ID. | 
| PaloAltoNetworksCore.Endpoint.endpoint_name | String | The endpoint name. | 
| PaloAltoNetworksCore.Endpoint.endpoint_type | String | The endpoint type. | 
| PaloAltoNetworksCore.Endpoint.endpoint_status | String | The status of the endpoint. | 
| PaloAltoNetworksCore.Endpoint.os_type | String | The endpoint OS type. | 
| PaloAltoNetworksCore.Endpoint.ip | Unknown | A list of IP addresses. | 
| PaloAltoNetworksCore.Endpoint.users | Unknown | A list of users. | 
| PaloAltoNetworksCore.Endpoint.domain | String | The endpoint domain. | 
| PaloAltoNetworksCore.Endpoint.alias | String | The endpoint's aliases. | 
| PaloAltoNetworksCore.Endpoint.first_seen | Unknown | First seen date/time in Epoch \(milliseconds\). | 
| PaloAltoNetworksCore.Endpoint.last_seen | Date | Last seen date/time in Epoch \(milliseconds\). | 
| PaloAltoNetworksCore.Endpoint.content_version | String | Content version. | 
| PaloAltoNetworksCore.Endpoint.installation_package | String | Installation package. | 
| PaloAltoNetworksCore.Endpoint.active_directory | String | Active directory. | 
| PaloAltoNetworksCore.Endpoint.install_date | Date | Install date in Epoch \(milliseconds\). | 
| PaloAltoNetworksCore.Endpoint.endpoint_version | String | Endpoint version. | 
| PaloAltoNetworksCore.Endpoint.is_isolated | String | Whether the endpoint is isolated. | 
| PaloAltoNetworksCore.Endpoint.group_name | String | The name of the group to which the endpoint belongs. | 
| Endpoint.Hostname | String | The hostname that is mapped to this endpoint. | 
| Endpoint.ID | String | The unique ID within the tool retrieving the endpoint. | 
| Endpoint.IPAddress | String | The IP address of the endpoint. | 
| Endpoint.Domain | String | The domain of the endpoint. | 
| Endpoint.OS | String | The endpoint's operation system. | 
| Account.Username | String | The username in the relevant system. | 
| Account.Domain | String | The domain of the account. | 
| Endpoint.Status | String | The endpoint's status. | 
| Endpoint.IsIsolated | String | The endpoint's isolation status. | 
| Endpoint.MACAddress | String | The endpoint's MAC address. | 
| Endpoint.Vendor | String | The integration name of the endpoint vendor. | 

### core-get-distribution-versions
***
Gets a list of all the agent versions to use for creating a distribution list.


#### Base Command

`core-get-distribution-versions`
#### Input

There are no input arguments for this command.

#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.DistributionVersions.windows | Unknown | A list of Windows agent versions. | 
| PaloAltoNetworksCore.DistributionVersions.linux | Unknown | A list of Linux agent versions. | 
| PaloAltoNetworksCore.DistributionVersions.macos | Unknown | A list of Mac agent versions. | 

### core-create-distribution
***
Creates an installation package. This is an asynchronous call that returns the distribution ID. This does not mean that the creation succeeded. To confirm that the package has been created, check the status of the distribution by running the Get Distribution Status API.


#### Base Command

`core-create-distribution`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| name | A string representing the name of the installation package. | Required | 
| platform | String, valid values are:<br/>• windows <br/>• linux<br/>• macos <br/>• android. Possible values are: windows, linux, macos, android. | Required | 
| package_type | A string representing the type of package to create.<br/>standalone - An installation for a new agent<br/>upgrade - An upgrade of an agent from ESM. Possible values are: standalone, upgrade. | Required | 
| agent_version | agent_version returned from core-get-distribution-versions. Not required for Android platfom. | Required | 
| description | Information about the package. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.Distribution.id | String | The installation package ID. | 
| PaloAltoNetworksCore.Distribution.name | String | The name of the installation package. | 
| PaloAltoNetworksCore.Distribution.platform | String | The installation OS. | 
| PaloAltoNetworksCore.Distribution.agent_version | String | Agent version. | 
| PaloAltoNetworksCore.Distribution.description | String | Information about the package. | 

### core-get-distribution-url
***
Gets the distribution URL for downloading the installation package.


#### Base Command

`core-get-distribution-url`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| distribution_id | The ID of the installation package.<br/>Copy the distribution_id from the "id" field on Endpoints &gt; Agent Installation page. | Required | 
| package_type | The installation package type. Valid<br/>values are:<br/>• upgrade<br/>• sh - For Linux<br/>• rpm - For Linux<br/>• deb - For Linux<br/>• pkg - For Mac<br/>• x86 - For Windows<br/>• x64 - For Windows. Possible values are: upgrade, sh, rpm, deb, pkg, x86, x64. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.Distribution.id | String | Distribution ID. | 
| PaloAltoNetworksCore.Distribution.url | String | URL for downloading the installation package. | 

### core-get-create-distribution-status
***
Gets the status of the installation package.


#### Base Command

`core-get-create-distribution-status`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| distribution_ids | A comma-separated list of distribution IDs to get the status of. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.Distribution.id | String | Distribution ID. | 
| PaloAltoNetworksCore.Distribution.status | String | The status of installation package. | 

### core-get-audit-management-logs
***
Gets management logs. You can filter by multiple fields, which will be concatenated using the AND condition (OR is not supported). Maximum result set size is 100. Offset is the zero-based number of management logs from the start of the result set (start by counting from 0).


#### Base Command

`core-get-audit-management-logs`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| email | User’s email address. | Optional | 
| type | The audit log type. Possible values are: REMOTE_TERMINAL, RULES, AUTH, RESPONSE, INCIDENT_MANAGEMENT, ENDPOINT_MANAGEMENT, ALERT_WHITELIST, PUBLIC_API, DISTRIBUTIONS, STARRED_INCIDENTS, POLICY_PROFILES, DEVICE_CONTROL_PROFILE, HOST_FIREWALL_PROFILE, POLICY_RULES, PROTECTION_POLICY, DEVICE_CONTROL_TEMP_EXCEPTIONS, DEVICE_CONTROL_GLOBAL_EXCEPTIONS, GLOBAL_EXCEPTIONS, MSSP, REPORTING, DASHBOARD, BROKER_VM. | Optional | 
| sub_type | The audit log subtype. | Optional | 
| result | Result type. Possible values are: SUCCESS, FAIL, PARTIAL. | Optional | 
| timestamp_gte | Return logs for which the timestamp is after 'log_time_after'.<br/>Supported values:<br/>1579039377301 (time in milliseconds)<br/>"3 days" (relative date)<br/>"2019-10-21T23:45:00" (date). | Optional | 
| timestamp_lte | Return logs for which the timestamp is before the 'log_time_after'.<br/>Supported values:<br/>1579039377301 (time in milliseconds)<br/>"3 days" (relative date)<br/>"2019-10-21T23:45:00" (date). | Optional | 
| page | Page number (for pagination). The default is 0 (the first page). Default is 0. | Optional | 
| limit | Maximum number of audit logs to return per page. The default and maximum is 30. Default is 30. | Optional | 
| sort_by | Specifies the field by which to sort the results. By default the sort is defined as creation-time and DESC. Can be "type", "sub_type", "result", or "timestamp". Possible values are: type, sub_type, result, timestamp. | Optional | 
| sort_order | The sort order. Can be "asc" (ascending) or "desc" (descending). Default set to "desc". Possible values are: asc, desc. Default is desc. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_ID | Number | Audit log ID. | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_OWNER_NAME | String | Audit owner name. | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_OWNER_EMAIL | String | Audit owner email address. | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_ASSET_JSON | String | Asset JSON. | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_ASSET_NAMES | String | Audit asset names. | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_HOSTNAME | String | Host name. | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_RESULT | String | Audit result. | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_REASON | String | Audit reason. | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_DESCRIPTION | String | Description of the audit. | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_ENTITY | String | Audit entity \(e.g., AUTH, DISTRIBUTIONS\). | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_ENTITY_SUBTYPE | String | Entity subtype \(e.g., Login, Create\). | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_CASE_ID | Number | Audit case ID. | 
| PaloAltoNetworksCore.AuditManagementLogs.AUDIT_INSERT_TIME | Date | Log's insert time. | 

### core-get-audit-agent-reports
***
Gets agent event reports. You can filter by multiple fields, which will be concatenated using the AND condition (OR is not supported). Maximum result set size is 100. Offset is the zero-based number of reports from the start of the result set (start by counting from 0).


#### Base Command

`core-get-audit-agent-reports`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| endpoint_ids | A comma-separated list of endpoint IDs. | Optional | 
| endpoint_names | A comma-separated list of endpoint names. | Optional | 
| type | The report type. Can be "Installation", "Policy", "Action", "Agent Service", "Agent Modules", or "Agent Status". Possible values are: Installation, Policy, Action, Agent Service, Agent Modules, Agent Status. | Optional | 
| sub_type | The report subtype. Possible values are: Install, Uninstall, Upgrade, Local Configuration, Content Update, Policy Update, Process Exception, Hash Exception, Scan, File Retrieval, File Scan, Terminate Process, Isolate, Cancel Isolation, Payload Execution, Quarantine, Restore, Stop, Start, Module Initialization, Local Analysis Model, Local Analysis Feature Extraction, Fully Protected, OS Incompatible, Software Incompatible, Kernel Driver Initialization, Kernel Extension Initialization, Proxy Communication, Quota Exceeded, Minimal Content, Reboot Eequired, Missing Disc Access. | Optional | 
| result | The result type. Can be "Success" or "Fail". If not passed, returns all event reports. Possible values are: Success, Fail. | Optional | 
| timestamp_gte | Return logs that their timestamp is greater than 'log_time_after'.<br/>Supported values:<br/>1579039377301 (time in milliseconds)<br/>"3 days" (relative date)<br/>"2019-10-21T23:45:00" (date). | Optional | 
| timestamp_lte | Return logs for which the timestamp is before the 'timestamp_lte'.<br/><br/>Supported values:<br/>1579039377301 (time in milliseconds)<br/>"3 days" (relative date)<br/>"2019-10-21T23:45:00" (date). | Optional | 
| page | Page number (for pagination). The default is 0 (the first page). Default is 0. | Optional | 
| limit | The maximum number of reports to return. Default and maximum is 30. Default is 30. | Optional | 
| sort_by | The field by which to sort results. Can be "type", "category", "trapsversion", "timestamp", or "domain"). Possible values are: type, category, trapsversion, timestamp, domain. | Optional | 
| sort_order | The sort order. Can be "asc" (ascending) or "desc" (descending). Default is "asc". Possible values are: asc, desc. Default is asc. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.AuditAgentReports.ENDPOINTID | String | Endpoint ID. | 
| PaloAltoNetworksCore.AuditAgentReports.ENDPOINTNAME | String | Endpoint name. | 
| PaloAltoNetworksCore.AuditAgentReports.DOMAIN | String | Agent domain. | 
| PaloAltoNetworksCore.AuditAgentReports.TRAPSVERSION | String | Traps version. | 
| PaloAltoNetworksCore.AuditAgentReports.RECEIVEDTIME | Date | Received time in Epoch time. | 
| PaloAltoNetworksCore.AuditAgentReports.TIMESTAMP | Date | Timestamp in Epoch time. | 
| PaloAltoNetworksCore.AuditAgentReports.CATEGORY | String | Report category \(e.g., Audit\). | 
| PaloAltoNetworksCore.AuditAgentReports.TYPE | String | Report type \(e.g., Action, Policy\). | 
| PaloAltoNetworksCore.AuditAgentReports.SUBTYPE | String | Report subtype \(e.g., Fully Protected,Policy Update,Cancel Isolation\). | 
| PaloAltoNetworksCore.AuditAgentReports.RESULT | String | Report result. | 
| PaloAltoNetworksCore.AuditAgentReports.REASON | String | Report reason. | 
| PaloAltoNetworksCore.AuditAgentReports.DESCRIPTION | String | Agent report description. | 
| Endpoint.ID | String | The unique ID within the tool retrieving the endpoint. | 
| Endpoint.Hostname | String | The hostname that is mapped to this endpoint. | 
| Endpoint.Domain | String | The domain of the endpoint. | 

### core-blocklist-files
***
Block lists requested files which have not already been block listed or added to allow list.


#### Base Command

`core-blocklist-files`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| hash_list | String that represents a list of hashed files you want to block list. Must be a valid SHA256 hash. | Required | 
| comment | String that represents additional information regarding the action. | Optional | 


#### Context Output

There is no context output for this command.
### core-whitelist-files
***
Adds requested files to allow list if they are not already on block list or allow list.


#### Base Command

`core-whitelist-files`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| hash_list | String that represents a list of hashed files you want to add to allow list. Must be a valid SHA256 hash. | Required | 
| comment | String that represents additional information regarding the action. | Optional | 


#### Context Output

There is no context output for this command.
### core-quarantine-files
***
Quarantines a file on selected endpoints. You can select up to 1000 endpoints.


#### Base Command

`core-quarantine-files`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_id_list | List of endpoint IDs. | Required | 
| file_path | String that represents the path of the file you want to quarantine. | Required | 
| file_hash | String that represents the file’s hash. Must be a valid SHA256 hash. | Required | 


#### Context Output

There is no context output for this command.
### core-get-quarantine-status
***
Retrieves the quarantine status for a selected file.


#### Base Command

`core-get-quarantine-status`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| endpoint_id | String the represents the endpoint ID. | Required | 
| file_hash | String that represents the file hash. Must be a valid SHA256 hash. | Required | 
| file_path | String that represents the file path. | Required | 


#### Context Output

There is no context output for this command.
### core-restore-file
***
Restores a quarantined file on requested endpoints.


#### Base Command

`core-restore-file`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| file_hash | String that represents the file in hash. Must be a valid SHA256 hash. | Required | 
| endpoint_id | String that represents the endpoint ID. If you do not enter a specific endpoint ID, the request will run restore on all endpoints which relate to the quarantined file you defined. | Optional | 


#### Context Output

There is no context output for this command.
### core-endpoint-scan
***
Runs a scan on a selected endpoint. To scan all endpoints, run this command with argument all=true. Do note that scanning all the endpoints may cause performance issues and latency.


#### Base Command

`core-endpoint-scan`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_id_list | List of endpoint IDs. | Optional | 
| dist_name | Name of the distribution list. | Optional | 
| gte_first_seen | Epoch timestamp in milliseconds. | Optional | 
| gte_last_seen | Epoch timestamp in milliseconds. | Optional | 
| lte_first_seen | Epoch timestamp in milliseconds. | Optional | 
| lte_last_seen | Epoch timestamp in milliseconds. | Optional | 
| ip_list | List of IP addresses. | Optional | 
| group_name | Name of the endpoint group. | Optional | 
| platform | Type of operating system. Possible values are: windows, linux, macos, android. | Optional | 
| alias | Endpoint alias name. | Optional | 
| isolate | Whether an endpoint has been isolated. Can be "isolated" or "unisolated". Possible values are: isolated, unisolated. | Optional | 
| hostname | Name of the host. | Optional | 
| all | Whether to scan all of the endpoints or not. Default is false. Scanning all of the endpoints may cause performance issues and latency. Possible values are: true, false. Default is false. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.endpointScan.actionId | Number | The action ID of the scan request. | 
| PaloAltoNetworksCore.endpointScan.aborted | Boolean | Was the scan aborted. | 

### core-endpoint-scan-abort
***
Cancel the scan of selected endpoints. A scan can only be aborted if the selected endpoints are Pending or In Progress. To scan all endpoints, run the command with the argument all=true. Note that scanning all of the endpoints may cause performance issues and latency.


#### Base Command

`core-endpoint-scan-abort`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_id_list | List of endpoint IDs. | Optional | 
| dist_name | Name of the distribution list. | Optional | 
| gte_first_seen | Epoch timestamp in milliseconds. | Optional | 
| gte_last_seen | Epoch timestamp in milliseconds. | Optional | 
| lte_first_seen | Epoch timestamp in milliseconds. | Optional | 
| lte_last_seen | Epoch timestamp in milliseconds. | Optional | 
| ip_list | List of IP addresses. | Optional | 
| group_name | Name of the endpoint group. | Optional | 
| platform | Type of operating system. Possible values are: windows, linux, macos, android. | Optional | 
| alias | Endpoint alias name. | Optional | 
| isolate | Whether an endpoint has been isolated. Can be "isolated" or "unisolated". Possible values are: isolated, unisolated. | Optional | 
| hostname | Name of the host. | Optional | 
| all | Whether to scan all of the endpoints or not. Default is false. Note that scanning all of the endpoints may cause performance issues and latency. Possible values are: true, false. Default is false. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.endpointScan.actionId | Unknown | The action id of the abort scan request. | 
| PaloAltoNetworksCore.endpointScan.aborted | Boolean | Was the scan aborted. | 

### core-get-policy
***
Gets the policy name for a specific endpoint.


#### Base Command

`core-get-policy`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| endpoint_id | The endpoint ID. Can be retrieved by running the core-get-endpoints command. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.Policy | string | The policy allocated with the endpoint. | 
| PaloAltoNetworksCore.Policy.policy_name | string | Name of the policy allocated with the endpoint. | 
| PaloAltoNetworksCore.Policy.endpoint_id | string | Endpoint ID. | 

### core-get-scripts
***
Gets a list of scripts available in the scripts library.


#### Base Command

`core-get-scripts`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| script_name | A comma-separated list of the script names. | Optional | 
| description | A comma-separated list of the script descriptions. | Optional | 
| created_by | A comma-separated list of the users who created the script. | Optional | 
| limit | The maximum number of scripts returned to the War Room. Default is 50. | Optional | 
| offset | (Int) Offset in the data set. Default is 0. | Optional | 
| windows_supported | Whether the script can be executed on a Windows operating system. Possible values are: true, false. | Optional | 
| linux_supported | Whether the script can be executed on a Linux operating system. Possible values are: true, false. | Optional | 
| macos_supported | Whether the script can be executed on a Mac operating system. Possible values are: true, false. | Optional | 
| is_high_risk | Whether the script has a high-risk outcome. Possible values are: true, false. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.Scripts | Unknown | The scripts command results. | 
| PaloAltoNetworksCore.Scripts.script_id | Unknown | Script ID. | 
| PaloAltoNetworksCore.Scripts.name | string | Name of the script. | 
| PaloAltoNetworksCore.Scripts.description | string | Description of the script. | 
| PaloAltoNetworksCore.Scripts.modification_date | Unknown | Timestamp of when the script was last modified. | 
| PaloAltoNetworksCore.Scripts.created_by | string | Name of the user who created the script. | 
| PaloAltoNetworksCore.Scripts.windows_supported | boolean | Whether the script can be executed on a Windows operating system. | 
| PaloAltoNetworksCore.Scripts.linux_supported | boolean | Whether the script can be executed on a Linux operating system. | 
| PaloAltoNetworksCore.Scripts.macos_supported | boolean | Whether the script can be executed on Mac operating system. | 
| PaloAltoNetworksCore.Scripts.is_high_risk | boolean | Whether the script has a high-risk outcome. | 
| PaloAltoNetworksCore.Scripts.script_uid | string | Globally Unique Identifier of the script, used to identify the script when executing. | 

### core-delete-endpoints
***
Deletes selected endpoints in the Cortex XDR app. You can delete up to 1000 endpoints.


#### Base Command

`core-delete-endpoints`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| endpoint_ids | Comma-separated list of endpoint IDs. You can retrieve the endpoint IDs from the core-get-endpoints command. | Required | 


#### Context Output

There is no context output for this command.
### core-get-endpoint-device-control-violations
***
Gets a list of device control violations filtered by selected fields. You can retrieve up to 100 violations.


#### Base Command

`core-get-endpoint-device-control-violations`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| endpoint_ids | Comma-separated list of endpoint IDs. You can retrieve the endpoint IDs from the core-get-endpoints command. | Optional | 
| type | Type of violation. Possible values are: "cd-rom", "disk drive", "floppy disk", and "portable device". Possible values are: cd-rom, disk drive, floppy disk, portable device. | Optional | 
| timestamp_gte | Timestamp of the violation. Violations that are greater than or equal to this timestamp will be returned. Values can be in either ISO date format, relative time, or epoch timestamp. For example:  "2019-10-21T23:45:00" (ISO date format), "3 days ago" (relative time) 1579039377301 (epoch time). | Optional | 
| timestamp_lte | Timestamp of the violation. Violations that are less than or equal to this timestamp will be returned. Values can be in either ISO date format, relative time, or epoch timestamp. For example:  "2019-10-21T23:45:00" (ISO date format), "3 days ago" (relative time) 1579039377301 (epoch time). | Optional | 
| ip_list | Comma-separated list of IP addresses. | Optional | 
| vendor | Name of the vendor. | Optional | 
| vendor_id | Vendor ID. | Optional | 
| product | Name of the product. | Optional | 
| product_id | Product ID. | Optional | 
| serial | Serial number. | Optional | 
| hostname | Hostname. | Optional | 
| violation_id_list | Comma-separated list of violation IDs. | Optional | 
| username | Username. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.EndpointViolations | Unknown | Endpoint violations command results. | 
| PaloAltoNetworksCore.EndpointViolations.violations | Unknown | A list of violations. | 
| PaloAltoNetworksCore.EndpointViolations.violations.os_type | string | Type of the operating system. | 
| PaloAltoNetworksCore.EndpointViolations.violations.hostname | string | Hostname of the violation. | 
| PaloAltoNetworksCore.EndpointViolations.violations.username | string | Username of the violation. | 
| PaloAltoNetworksCore.EndpointViolations.violations.ip | string | IP address of the violation. | 
| PaloAltoNetworksCore.EndpointViolations.violations.timestamp | number | Timestamp of the violation. | 
| PaloAltoNetworksCore.EndpointViolations.violations.violation_id | number | Violation ID. | 
| PaloAltoNetworksCore.EndpointViolations.violations.type | string | Type of violation. | 
| PaloAltoNetworksCore.EndpointViolations.violations.vendor_id | string | Vendor ID of the violation. | 
| PaloAltoNetworksCore.EndpointViolations.violations.vendor | string | Name of the vendor of the violation. | 
| PaloAltoNetworksCore.EndpointViolations.violations.product_id | string | Product ID of the violation. | 
| PaloAltoNetworksCore.EndpointViolations.violations.product | string | Name of the product of the violation. | 
| PaloAltoNetworksCore.EndpointViolations.violations.serial | string | Serial number of the violation. | 
| PaloAltoNetworksCore.EndpointViolations.violations.endpoint_id | string | Endpoint ID of the violation. | 

### core-retrieve-files
***
Retrieves files from selected endpoints. You can retrieve up to 20 files, from no more than 10 endpoints. At least one endpoint ID and one file path are necessary in order to run the command. After running this command, you can use the core-action-status-get command with returned action_id, to check the action status.


#### Base Command

`core-retrieve-files`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_ids | Comma-separated list of endpoint IDs. | Required | 
| windows_file_paths | A comma-separated list of file paths on the Windows platform. | Optional | 
| linux_file_paths | A comma-separated list of file paths on the Linux platform. | Optional | 
| mac_file_paths | A comma-separated list of file paths on the Mac platform. | Optional | 
| generic_file_path | A comma-separated list of file paths in any platform. Can be used instead of the mac/windows/linux file paths. The order of the files path list must be parellel to the endpoints list order, therefore, the first file path in the list is related to the first endpoint and so on. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.RetrievedFiles.action_id | string | ID of the action to retrieve files from selected endpoints. | 

### core-retrieve-file-details
***
View the file retrieved by the core-retrieve-files command according to the action ID. Before running this command, you can use the core-action-status-get command to check if this action completed successfully.


#### Base Command

`core-retrieve-file-details`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| action_id | Action ID retrieved from the core-retrieve-files command. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| File | Unknown | The file details command results. | 
| File.Name | String | The full file name \(including the file extension\). | 
| File.EntryID | String | The ID for locating the file in the War Room. | 
| File.Size | Number | The size of the file in bytes. | 
| File.MD5 | String | The MD5 hash of the file. | 
| File.SHA1 | String | The SHA1 hash of the file. | 
| File.SHA256 | String | The SHA256 hash of the file. | 
| File.SHA512 | String | The SHA512 hash of the file. | 
| File.Extension | String | The file extension. For example: "xls". | 
| File.Type | String | The file type, as determined by libmagic \(same as displayed in file entries\). | 

### core-get-script-metadata
***
Gets the full definition of a specific script in the scripts library.


#### Base Command

`core-get-script-metadata`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| script_uid | Unique identifier of the script, returned by the core-get-scripts command. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.ScriptMetadata | Unknown | The script metadata command results. | 
| PaloAltoNetworksCore.ScriptMetadata.script_id | number | Script ID. | 
| PaloAltoNetworksCore.ScriptMetadata.name | string | Script name. | 
| PaloAltoNetworksCore.ScriptMetadata.description | string | Script description. | 
| PaloAltoNetworksCore.ScriptMetadata.modification_date | unknown | Timestamp of when the script was last modified. | 
| PaloAltoNetworksCore.ScriptMetadata.created_by | string | Name of the user who created the script. | 
| PaloAltoNetworksCore.ScriptMetadata.is_high_risk | boolean | Whether the script has a high-risk outcome. | 
| PaloAltoNetworksCore.ScriptMetadata.windows_supported | boolean | Whether the script can be executed on a Windows operating system. | 
| PaloAltoNetworksCore.ScriptMetadata.linux_supported | boolean | Whether the script can be executed on a Linux operating system. | 
| PaloAltoNetworksCore.ScriptMetadata.macos_supported | boolean | Whether the script can be executed on a Mac operating system. | 
| PaloAltoNetworksCore.ScriptMetadata.entry_point | string | Name of the entry point selected for the script. An empty string indicates  the script defined as just run. | 
| PaloAltoNetworksCore.ScriptMetadata.script_input | string | Name and type for the specified entry point. | 
| PaloAltoNetworksCore.ScriptMetadata.script_output_type | string | Type of the output. | 
| PaloAltoNetworksCore.ScriptMetadata.script_output_dictionary_definitions | Unknown | If the script_output_type is a dictionary, an array with friendly name, name, and type for each output. | 

### core-get-script-code
***
Gets the code of a specific script in the script library.


#### Base Command

`core-get-script-code`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| script_uid | Unique identifier of the script, returned by the core-get-scripts command. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.ScriptCode | Unknown | The script code command results. | 
| PaloAltoNetworksCore.ScriptCode.code | string | The code of a specific script in the script library. | 
| PaloAltoNetworksCore.ScriptCode.script_uid | string | Unique identifier of the script. | 

### core-action-status-get
***
Retrieves the status of the requested actions according to the action ID.


#### Base Command

`core-action-status-get`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| action_id | The action ID of the selected request. After performing an action, you will receive an action ID. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.GetActionStatus | Unknown | The action status command results. | 
| PaloAltoNetworksCore.GetActionStatus.endpoint_id | string | Endpoint ID. | 
| PaloAltoNetworksCore.GetActionStatus.status | string | The status of the specific endpoint ID. | 
| PaloAltoNetworksCore.GetActionStatus.action_id | number | The specified action ID. | 

### core-run-script
***
Initiates a new endpoint script execution action using a script from the script library.


#### Base Command

`core-run-script`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_ids | Comma-separated list of endpoint IDs. Can be retrieved by running the core-get-endpoints command. | Required | 
| script_uid | Unique identifier of the script. Can be retrieved by running the core-get-scripts command. | Required | 
| parameters | Dictionary contains the parameter name as key and its value for this execution as the value. For example, {"param1":"param1_value","param2":"param2_value"}. | Optional | 
| timeout | The timeout in seconds for this execution. Default is 600. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.ScriptRun.action_id | Number | ID of the action initiated. | 
| PaloAltoNetworksCore.ScriptRun.endpoints_count | Number | Number of endpoints the action was initiated on. | 

### core-run-snippet-code-script
***
Initiates a new endpoint script execution action using the provided snippet code.


#### Base Command

`core-run-snippet-code-script`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_ids | Comma-separated list of endpoint IDs. Can be retrieved by running the core-get-endpoints command. | Required | 
| snippet_code | Section of a script you want to initiate on an endpoint (e.g., print("7")). | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.ScriptRun.action_id | Number | ID of the action initiated. | 
| PaloAltoNetworksCore.ScriptRun.endpoints_count | Number | Number of endpoints the action was initiated on. | 

### core-get-script-execution-status
***
Retrieves the status of a script execution action.


#### Base Command

`core-get-script-execution-status`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| action_id | Action IDs retrieved from the core-run-script command. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.ScriptStatus.general_status | String | General status of the action, considering the status of all the endpoints. | 
| PaloAltoNetworksCore.ScriptStatus.error_message | String | Error message regarding permissions for running APIs or the action doesn’t exist. | 
| PaloAltoNetworksCore.ScriptStatus.endpoints_timeout | Number | Number of endpoints in "timeout" status. | 
| PaloAltoNetworksCore.ScriptStatus.action_id | Number | ID of the action initiated. | 
| PaloAltoNetworksCore.ScriptStatus.endpoints_pending_abort | Number | Number of endpoints in "pending abort" status. | 
| PaloAltoNetworksCore.ScriptStatus.endpoints_pending | Number | Number of endpoints in "pending" status. | 
| PaloAltoNetworksCore.ScriptStatus.endpoints_in_progress | Number | Number of endpoints in "in progress" status. | 
| PaloAltoNetworksCore.ScriptStatus.endpoints_failed | Number | Number of endpoints in "failed" status. | 
| PaloAltoNetworksCore.ScriptStatus.endpoints_expired | Number | Number of endpoints in "expired" status. | 
| PaloAltoNetworksCore.ScriptStatus.endpoints_completed_successfully | Number | Number of endpoints in "completed successfully" status. | 
| PaloAltoNetworksCore.ScriptStatus.endpoints_canceled | Number | Number of endpoints in "canceled" status. | 
| PaloAltoNetworksCore.ScriptStatus.endpoints_aborted | Number | Number of endpoints in "aborted" status. | 

### core-get-script-execution-results
***
Retrieve the results of a script execution action.


#### Base Command

`core-get-script-execution-results`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| action_id | Action IDs retrieved from the core-run-script command. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.ScriptResult.action_id | Number | ID of the action initiated. | 
| PaloAltoNetworksCore.ScriptResult.results.retrieved_files | Number | Number of successfully retrieved files. | 
| PaloAltoNetworksCore.ScriptResult.results.endpoint_ip_address | String | Endpoint IP address. | 
| PaloAltoNetworksCore.ScriptResult.results.endpoint_name | String | Number of successfully retrieved files. | 
| PaloAltoNetworksCore.ScriptResult.results.failed_files | Number | Number of files failed to retrieve. | 
| PaloAltoNetworksCore.ScriptResult.results.endpoint_status | String | Endpoint status. | 
| PaloAltoNetworksCore.ScriptResult.results.domain | String | Domain to which the endpoint belongs. | 
| PaloAltoNetworksCore.ScriptResult.results.endpoint_id | String | Endpoint ID. | 
| PaloAltoNetworksCore.ScriptResult.results.execution_status | String | Execution status of this endpoint. | 
| PaloAltoNetworksCore.ScriptResult.results.return_value | String | Value returned by the script in case the type is not a dictionary. | 
| PaloAltoNetworksCore.ScriptResult.results.standard_output | String | The STDOUT and the STDERR logged by the script during the execution. | 
| PaloAltoNetworksCore.ScriptResult.results.retention_date | Date | Timestamp in which the retrieved files will be deleted from the server. | 

### core-get-script-execution-result-files
***
Gets the files retrieved from a specific endpoint during a script execution.


#### Base Command

`core-get-script-execution-result-files`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| action_id | Action ID retrieved from the core-run-script command. | Required | 
| endpoint_id | Endpoint ID. Can be retrieved by running the core-get-endpoints command. | Required | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| File.Size | String | The size of the file. | 
| File.SHA1 | String | The SHA1 hash of the file. | 
| File.SHA256 | String | The SHA256 hash of the file. | 
| File.SHA512 | String | The SHA512 hash of the file. | 
| File.Name | String | The name of the file. | 
| File.SSDeep | String | The SSDeep hash of the file. | 
| File.EntryID | String | EntryID of the file | 
| File.Info | String | Information about the file. | 
| File.Type | String | The file type. | 
| File.MD5 | String | The MD5 hash of the file. | 
| File.Extension | String | The extension of the file. | 

### core-run-script-execute-commands
***
Initiate a new endpoint script execution of shell commands.


#### Base Command

`core-run-script-execute-commands`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_ids | Comma-separated list of endpoint IDs. Can be retrieved by running the core-get-endpoints command. | Required | 
| commands | Comma-separated list of shell commands to execute. | Required | 
| timeout | The timeout in seconds for this execution. Default is 600. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.ScriptRun.action_id | Number | ID of the action initiated. | 
| PaloAltoNetworksCore.ScriptRun.endpoints_count | Number | Number of endpoints the action was initiated on. | 

### core-run-script-delete-file
***
Initiates a new endpoint script execution to delete the specified file.


#### Base Command

`core-run-script-delete-file`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_ids | Comma-separated list of endpoint IDs. Can be retrieved by running the core-get-endpoints command. | Required | 
| file_path | Paths of the files to delete, in a comma-separated list. Paths of the files to check for existence. All of the given file paths will run on all of the endpoints. | Required | 
| timeout | The timeout in seconds for this execution. Default is 600. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.ScriptRun.action_id | Number | ID of the action initiated. | 
| PaloAltoNetworksCore.ScriptRun.endpoints_count | Number | Number of endpoints the action was initiated on. | 

### core-run-script-file-exists
***
Initiates a new endpoint script execution to check if file exists.


#### Base Command

`core-run-script-file-exists`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_ids | Comma-separated list of endpoint IDs. Can be retrieved by running the core-get-endpoints command. | Required | 
| file_path | Paths of the files to check for existence, in a comma-separated list. All of the given file paths will run on all of the endpoints. | Required | 
| timeout | The timeout in seconds for this execution. Default is 600. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.ScriptRun.action_id | Number | ID of the action initiated. | 
| PaloAltoNetworksCore.ScriptRun.endpoints_count | Number | Number of endpoints the action was initiated on. | 

### core-run-script-kill-process
***
Initiates a new endpoint script execution kill process.


#### Base Command

`core-run-script-kill-process`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| incident_id | Allows to link the response action to the incident that triggered it. | Optional | 
| endpoint_ids | Comma-separated list of endpoint IDs. Can be retrieved by running the core-get-endpoints command. | Required | 
| process_name | Names of processes to kill. Will kill all of the given processes on all of the endpoints. | Required | 
| timeout | The timeout in seconds for this execution. Default is 600. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.ScriptRun.action_id | Number | ID of the action initiated. | 
| PaloAltoNetworksCore.ScriptRun.endpoints_count | Number | Number of endpoints the action was initiated on. | 

### endpoint
***
Returns information about an endpoint.


#### Base Command

`endpoint`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| id | The endpoint ID. | Optional | 
| ip | The endpoint IP address. | Optional | 
| hostname | The endpoint hostname. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| Endpoint.Hostname | String | The endpoint's hostname. | 
| Endpoint.OS | String | The endpoint's operation system. | 
| Endpoint.IPAddress | String | The endpoint's IP address. | 
| Endpoint.ID | String | The endpoint's ID. | 
| Endpoint.Status | String | The endpoint's status. | 
| Endpoint.IsIsolated | String | The endpoint's isolation status. | 
| Endpoint.MACAddress | String | The endpoint's MAC address. | 
| Endpoint.Vendor | String | The integration name of the endpoint vendor. | 

### core-get-endpoints-by-status
***
Returns the number of the connected\disconnected endpoints.


#### Base Command

`core-get-endpoints-by-status`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| status | The status of the endpoint to filter. Possible values are: connected, disconnected, lost, uninstalled. | Required | 
| last_seen_gte | All the agents that were last seen before {last_seen_gte}. Supported<br/>        values: 1579039377301 (time in milliseconds) "3 days" (relative date) "2019-10-21T23:45:00"<br/>        (date). | Optional | 
| last_seen_lte | All the agents that were last seen before {last_seen_lte}. Supported<br/>        values: 1579039377301 (time in milliseconds) "3 days" (relative date) "2019-10-21T23:45:00"<br/>        (date). | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| PaloAltoNetworksCore.EndpointsStatus.status | String | The endpoint's status. | 
| PaloAltoNetworksCore.EndpointsStatus.count | Number | The number of endpoint's with this status. | 