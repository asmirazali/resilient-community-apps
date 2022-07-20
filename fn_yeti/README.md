<!--
  This README.md is generated by running:
  "resilient-sdk docgen -p fn_yeti"

  It is best edited using a Text Editor with a Markdown Previewer. VS Code
  is a good example. Checkout https://guides.github.com/features/mastering-markdown/
  for tips on writing with Markdown

  All fields followed by "::CHANGE_ME::"" should be manually edited

  If you make manual edits and run docgen again, a .bak file will be created

  Store any screenshots in the "doc/screenshots" directory and reference them like:
  ![screenshot: screenshot_1](./screenshots/screenshot_1.png)

  NOTE: If your app is available in the container-format only, there is no need to mention the integration server in this readme.
-->

# Yeti

## Table of Contents
- [Release Notes](#release-notes)
- [Overview](#overview)
  - [Key Features](#key-features)
- [Requirements](#requirements)
  - [SOAR platform](#soar-platform)
  - [Cloud Pak for Security](#cloud-pak-for-security)
  - [Proxy Server](#proxy-server)
  - [Python Environment](#python-environment)
  - [Endpoint Developed With](#endpoint-developed-with)
- [Installation](#installation)
  - [Install](#install)
  - [App Configuration](#app-configuration)
- [Function - Yeti](#function---yeti)
- [Rules](#rules)
- [Troubleshooting & Support](#troubleshooting--support)
---

## Release Notes
<!--
  Specify all changes in this release. Do not remove the release 
  notes of a previous release
-->
| Version | Date | Notes |
| ------- | ---- | ----- |
| 1.0.0 | 04/2022 | Initial Release | 

---

## Overview
<!--
  Provide a high-level description of the function itself and its remote software or application.
  The text below is parsed from the "description" and "long_description" attributes in the setup.py file
-->
**IBM Security SOAR app for Yeti**

 ![screenshot: main](./doc/screenshots/main.png)

Queries Yeti and updates SOAR with any information gained on the artifact. All Yeti observables are supported by this integration. For more info about YETI platform, please visit https://yeti-platform.github.io.	

### Key Features
<!--
  List the Key Features of the Integration
-->
* Queries Yeti and creates a hit in the artifact if any information is found

---

## Requirements
<!--
  List any Requirements 
--> 
* A Yeti instance

This app supports the IBM Security QRadar SOAR Platform and the IBM Security QRadar SOAR for IBM Cloud Pak for Security.

### SOAR platform
The SOAR platform supports two app deployment mechanisms, App Host and integration server.

If deploying to a SOAR platform with an App Host, the requirements are:
* SOAR platform >= `43.1.49`.
* The app is in a container-based format (available from the AppExchange as a `zip` file).

If deploying to a SOAR platform with an integration server, the requirements are:
* SOAR platform >= `43.1.49`.
* The app is in the older integration format (available from the AppExchange as a `zip` file which contains a `tar.gz` file).
* Integration server is running `resilient-circuits>=44.0.0`.
* If using an API key account, make sure the account provides the following minimum permissions: 
  | Name | Permissions |
  | ---- | ----------- |
  | Org Data | Read |
  | Function | Read |

The following SOAR platform guides provide additional information: 
* _App Host Deployment Guide_: provides installation, configuration, and troubleshooting information, including proxy server settings. 
* _Integration Server Guide_: provides installation, configuration, and troubleshooting information, including proxy server settings.
* _System Administrator Guide_: provides the procedure to install, configure and deploy apps. 

The above guides are available on the IBM Documentation website at [ibm.biz/soar-docs](https://ibm.biz/soar-docs). On this web page, select your SOAR platform version. On the follow-on page, you can find the _App Host Deployment Guide_ or _Integration Server Guide_ by expanding **Apps** in the Table of Contents pane. The System Administrator Guide is available by expanding **System Administrator**.

### Cloud Pak for Security
If you are deploying to IBM Cloud Pak for Security, the requirements are:
* IBM Cloud Pak for Security >= 1.9
* Cloud Pak is configured with an App Host.
* The app is in a container-based format (available from the AppExchange as a `zip` file).

The following Cloud Pak guides provide additional information: 
* _App Host Deployment Guide_: provides installation, configuration, and troubleshooting information, including proxy server settings. From the Table of Contents, select Case Management and Orchestration & Automation > **Orchestration and Automation Apps**.
* _System Administrator Guide_: provides information to install, configure, and deploy apps. From the IBM Cloud Pak for Security IBM Documentation table of contents, select Case Management and Orchestration & Automation > **System administrator**.

These guides are available on the IBM Documentation website at [ibm.biz/cp4s-docs](https://ibm.biz/cp4s-docs). From this web page, select your IBM Cloud Pak for Security version. From the version-specific IBM Documentation page, select Case Management and Orchestration & Automation.

### Proxy Server
The app does support a proxy server.

### Python Environment
Python 3.6 is supported.
Additional package dependencies may exist for each of these packages:
* pyeti-python3~=1.1
* resilient-circuits>=44.0.0

---

## Installation

### Install
* To install or uninstall an App or Integration on the _SOAR platform_, see the documentation at [ibm.biz/soar-docs](https://ibm.biz/soar-docs).
* To install or uninstall an App on _IBM Cloud Pak for Security_, see the documentation at [ibm.biz/cp4s-docs](https://ibm.biz/cp4s-docs) and follow the instructions above to navigate to Orchestration and Automation.

### App Configuration
The following table provides the settings you need to configure the app. These settings are made in the app.config file. See the documentation discussed in the Requirements section for the procedure.

| Config | Required | Example | Description |
| ------ | :------: | ------- | ----------- |
| **apikey** | Yes | `<apikey_value>` | Found on the Yeti platform|
| **password** | Yes | `` | Can be created in the Yeti Platform|
| **url** | Yes | `http://localhost:8080/api` | URL for your Yeti Instance |
| **username** | Yes | `<yeti_instance_username` | Found on Yeti Platform|


---

## Function - Yeti
Queries Yeti and updates SOAR with any information gained on the artifact. All Yeti observables are supported by this integration. For more info about YETI platform, please visit https://yeti-platform.github.io.

 ![screenshot: fn-yeti ](./doc/screenshots/fn-yeti.png)

<details><summary>Inputs:</summary>
<p>

| Name | Type | Required | Example | Tooltip |
| ---- | :--: | :------: | ------- | ------- |
| `yeti_artifact_type` | `text` | Yes | `-` | - |
| `yeti_artifact_value` | `text` | Yes | `-` | - |

</p>
</details>

<details><summary>Outputs:</summary>
<p>

> **NOTE:** This example might be in JSON format, but `results` is a Python Dictionary on the SOAR platform.

```python
results = {
  "content": [
    {
      "context": [],
      "created": "2022-04-04T18:52:23.699000",
      "description": null,
      "human_url": "http://localhost:8080/observable/624b3e67f533f89c2f700992",
      "id": "624b3e67f533f89c2f700992",
      "last_analyses": {},
      "sources": [],
      "tags": [
        {
          "first_seen": "2022-04-04T18:52:23.751000",
          "fresh": true,
          "last_seen": "2022-04-04T18:52:23.751000",
          "name": "dridex"
        }
      ],
      "type": "Path",
      "url": "http://localhost:8080/api/observable/624b3e67f533f89c2f700992",
      "value": "C:\\Users\\admin\\AppData\\Roaming\\Adada\\stolen.dat"
    }
  ],
  "inputs": {
    "yeti_artifact_type": "File Path",
    "yeti_artifact_value": "C:\\Users\\admin\\AppData\\Roaming\\Adada\\stolen.dat"
  },
  "metrics": {
    "execution_time_ms": 37,
    "host": "My Host",
    "package": "fn-yeti",
    "package_version": "1.0.0",
    "timestamp": "2022-04-04 16:50:55",
    "version": "1.0"
  },
  "raw": null,
  "reason": null,
  "success": true,
  "version": 2.0
}
```

</p>
</details>

<details><summary>Example Pre-Process Script:</summary>
<p>

```python
inputs.yeti_artifact_type = artifact.type
inputs.yeti_artifact_value = artifact.value
```

</p>
</details>

<details><summary>Example Post-Process Script:</summary>
<p>

```python
if results.success:
  if results.content:
    resp = results.content
    hit = []

    tags = ""
    for tag in resp[0]["tags"]:
        if tags != "":
            tags += ", "
        tags += tag["name"]
    
    descript = resp[0]["description"] if resp[0]["description"] else "None"
    hit = [
        {
          "name": "Type",
          "type": "string",
          "value": "{}".format(resp[0]["type"])
        }, 
        {
          "name": "Value",
          "type": "string",
          "value": "{}".format(resp[0]["value"])
        }, 
        {
          "name": "Tags",
          "type": "string",
          "value": "{}".format(tags)
        },
        {
          "name": "Created",
          "type": "string",
          "value": "{}".format(resp[0]["created"])
        },
        {
          "name": "URL",
          "type": "uri",
          "value": "{}".format(resp[0]["human_url"])
        },
        {
          "name": "Description",
          "type": "string",
          "value": "{}".format(descript)
        }
        ]
    artifact.addHit("Yeti Function hits added", hit)
else:
  incident.addNote("Yeti query failed: {}".format(results.reason))
  
```

</p>
</details>

---





## Rules
| Rule Name | Object | Workflow Triggered |
| --------- | ------ | ------------------ |
| Yeti Observable Query | artifact | `yeti_observables_query` |

---


## Troubleshooting & Support
Refer to the documentation listed in the Requirements section for troubleshooting information.

### For Support
This is a IBM Community provided App. Please search the Community [ibm.biz/soarcommunity](https://ibm.biz/soarcommunity) for assistance.