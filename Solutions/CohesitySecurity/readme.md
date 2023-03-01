# Cohesity Data Cloud Integration with Microsoft Sentinel
You can integrate Cohesity Data Cloud with Microsoft Sentinel to provide security operators and IT operation teams with the automation and operational simplicity to respond to threats and recover from ransomware incidents through Microsoft Sentinel. This integration allows you to:
 
* Send ransomware alerts into Microsoft Sentinel.
* View incidents with the alert details.
* Escalate to ITSM tool.
* Initiate recovery of clean snapshot.
* Closed loop integration resolves alerts in Cohesity Data Cloud.

## Package Building and Validation Instructions
__Disclaimer:__ You can skip these steps and use one of the pre-built packages from [this directory](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/CohesitySecurity/Package). These steps are required only if you want to rebuild the package.
1. Follow this [readme.md](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/README.md) to set up the build prerequisites.
2. Edit [cohesity.json](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/CohesitySecurity/cohesity.json) to add the required values. __Note:__ The dummy values are provided to protect Personal Identifiable Information (PII) information.
3. Run [build.ps1](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/CohesitySecurity/build.ps1) to build the package.
4. Follow [readme.md](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/README.md) for post-build manual validation.

## Deployment
This package contains the following Azure functions to communicate with Microsoft Sentinel and Cohesity Data Cloud, and playbooks to automate workflows.

The package consists of the following Azure functions:
* _IncidentProducer_ to retrieve Cohesity Data Cloud alerts through REST API. For more information, see [IncidentProducer](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/CohesitySecurity/Data%20Connectors/Helios2Sentinel/IncidentProducer/readme.md).
* _IncidentConsumer_ to create incidents in Microsoft Sentinel. For more information, see [IncidentConsumer](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/CohesitySecurity/Data%20Connectors/Helios2Sentinel/IncidentConsumer/readme.md).

You can refer to the [Azure Functions](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/CohesitySecurity/Data%20Connectors/Helios2Sentinel#readme) file to learn more about the pre-requisites and the deployment of Azure functions.

The package contains the following playbooks:

* *Cohesity Send Incident Email* allows you to send an email to the recipient with the incident details. For more information, see [Cohesity Send Incident Email](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/CohesitySecurity/Playbooks/Cohesity_Send_Incident_Email#readme.md).
* *Cohesity Create or Update ServiceNow Incident* allows you to create and update the incident in the ServiceNow platform. For more information, see [Cohesity Create or Update ServiceNow Incident](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/CohesitySecurity/Playbooks/Cohesity_CreateOrUpdate_ServiceNow_Incident#readme.md).
* *Cohesity Restore From Last Snapshot* allows you to restore data from the latest clean snapshot in Cohesity Data Cloud. For more information, see [Cohesity Restore From Last Snapshot](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/CohesitySecurity/Playbooks/Cohesity_Restore_From_Last_Snapshot#readme.md).
* *Cohesity Close Helios Incident* allows you to resolve the corresponding Cohesity Data Cloud alerts. For more information, see [Cohesity Close Helios Incident](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/CohesitySecurity/Playbooks/Cohesity_Close_Helios_Incident).
* *Cohesity Delete Incident Blobs* allows you to deletes the blobs on Azure storage created by an incident that is generated by Cohesity function apps. For more information, see [Cohesity Delete Incident Blobs](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/CohesitySecurity/Playbooks/Cohesity_Delete_Incident_Blobs).

## Misc
This GitHub file directory also includes [build_one_solution.ps1](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/CohesitySecurity/build_one_solution.ps1) that is required to build a solution if the default build-script, provided by Microsoft, takes more time than expected.