# Custom Annotations Framework for Splunk Enterprise Security

## Overview
This Splunk application implements a **customizable annotation framework** that allows administrators to manage and track correlation searches through various stages. Users can tag correlation searches with custom **annotations** such as DEV, PREPROD, PROD, or DEPRECATED, reflecting their current phase in development, testing, production, or decommissioning. 

This framework is fully **customizable**, enabling you to add new annotation values, modify existing ones, or even rename the framework itself to fit the needs of your organization.

Administrators, developers, and security analysts can use this framework to better organize, filter, and monitor correlation searches, ensuring clear visibility and separation of workflows within Splunk Enterprise Security (ES).

## Features
* **Custom Annotations**: Easily tag correlation searches with **customizable** annotations to denote their lifecycle stage:
  * DEV (Development)
  * PREPROD (Pre-Production)
  * PROD (Production)
  * DEPRECATED (Deprecated)
  
  You can modify or extend these values based on your organization's requirements by updating the framework’s lookup file.

* **Customizability**:
  * **Add New Annotations**: You can add new stages (e.g., QA, STAGING) by adding entries to the framework's lookup table.
  * **Rename the Framework**: The framework name is configurable. You can change it to align with internal terminology (e.g., “Deployment Phases”).
  
* **Filtered Incident Review Links**: By utilizing the custom annotations, you can create direct links to filtered Incident Review pages that only display correlation searches for a specific lifecycle stage. For example:
  * A **DEV Incident Review** page showing only correlation searches tagged as DEV (in development).
  * A **PROD Incident Review** page displaying only correlation searches marked as PROD (in production).
  * You can generate these filtered views by appending the appropriate filter to the Incident Review URL based on the annotation you want to target. More information on [this page](https://docs.splunk.com/Documentation/ES/7.3.2/Admin/Customizemenubar#Add_a_link_to_a_filtered_view_of_Incident_Review).


* **Streamlined Workflow**: The Incident Review page in ES can be filtered by annotation, ensuring that only searches in the desired phase are visible or triggered. This prevents development-related notables from affecting production workflows.

* **Enhanced Visibility**: Quickly identify the lifecycle status of any correlation search via annotation tags directly within the Content Management or Incident Review dashboards.

## Installation Instructions

### 1. Download and Install the App:
* Download the app package (`SA-custom_annotations_framework_for_ES.spl`).
* Log in to your Splunk instance and navigate to **Apps > Manage Apps**.
* Click **Install app from file**, then select the `.spl` file and upload it.
* Click **Install** to complete the process.

### 2. Edit the `custom_annotations_framework_lookup`:
* To integrate the framework into the **New / Edit Correlation Search** menu,edit the _Security Frameworks_ lookup (`security_framework_lookup` lookup, app:`SA-ThreatIntelligence`) an add the following line in order for ES to integrate our framework in the New:
  ```plaintext
  | custom_annotations_framework_lookup | Custom Annotations Framework | #AB006B | custom_annotations_framework_lookup | annotation_value | description |
  ```

### 3. Customize the Framework (Optional):
* To **add new annotation values**, edit the `custom_annotations_framework_lookup` to include additional stages (e.g., QA, STAGING, etc.).
* If you want to **rename the framework**, modify the `security_framework_lookup` lookup table to reflect the new name (e.g., "Deployment Phases Framework").

### 4. Verify Installation:
* Open any Correlation Search and verify that a new dropdown menu under the _Annotations_ section includes your custom annotations.

## Customization Notes
This framework is designed to be flexible:
* **Add or Remove Annotations**: You can easily modify the available stages by updating the `custom_annotations_framework_lookup` lookup file.
* **Change the Framework Label**: If your organization prefers different terminology, feel free to rename the framework label in `security_framework_lookup`.

---

