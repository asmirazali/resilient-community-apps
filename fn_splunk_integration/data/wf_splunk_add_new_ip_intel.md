<!--
    DO NOT MANUALLY EDIT THIS FILE
    THIS FILE IS AUTOMATICALLY GENERATED WITH resilient-sdk codegen
-->

# Example of adding artifact to Splunk ES

## Function - Splunk Add Intel Item

### API Name
`splunk_add_intel_item`

### Output Name
`None`

### Message Destination
`splunk_es_rest`

### Pre-Processing Script
```python
lookup_map = {
  "DNS Name": ("ip_intel", "domain"),
  "Email Attachment": None,
  "Email Attachment Name": ("file_intel", "file_name"),
  "Email Body": None,
  "Email Recipient": None,
  "Email Sender": ("email_intel", "src_user"),
  "Email Sender Name": ("email_intel", "src_user"),
  "Email Subject": ("email_intel", "subject"),
  "File Name": ("file_intel", "file_name"),
  "File Path": None,
  "HTTP Request Header": None,
  "HTTP Response Header": None,
  "IP Address": ("ip_intel", "ip"),
  "Log File": None,
  "MAC Address": None,
  "Malware Family/Variant": None,
  "Malware MD5 Hash": ("file_intel", "file_hash"),
  "Malware Sample": None,
  "Malware Sample Fuzzy Hash": ("file_intel", "file_hash"),
  "Malware SHA-1 Hash": ("file_intel", "file_hash"),
  "Malware SHA-256 Hash": ("file_intel", "file_hash"),
  "Mutex": None,
  "Network CIDR Range": None,
  "Other File": None,
  "Password": None,
  "Port": None,
  "Process Name": ("process_intel", "process"),
  "Registry Key": ("registry_intel", "registry_value_name"),
  "RFC 822 Email Message File": None,
  "Service": ("service_intel", "service"),
  "String": None,
  "System Name": ("service_intel", "service"),
  "URI Path": None,
  "URL": ("http_intel", "url"),
  "URL Referer": ("http_intel", "http_referrer"),
  "User Account": None,
  "User Agent": ("http_intel", "http_user_agent")
}

if artifact.type in lookup_map and lookup_map[artifact.type]:
  threat_type, threat_field_name = lookup_map[artifact.type]
  inputs.splunk_threat_intel_type = threat_type
  inputs.splunk_query_param1 = threat_field_name
  inputs.splunk_query_param2 = artifact.value
  inputs.splunk_label = rule.properties.splunk_servers
else:
  helper.fail("Artifact type not supported: {}".format(artifact.type))

```

### Post-Processing Script
```python
# {'status_code': 201, 'content': {'message': 'Create operation successful.', 'status': True}}
import java.util.Date as Date 

now = Date().time

result_note = u"""<b>Artifact</b>: {}<br><br>
<b>Splunk Add Status</b>: {}<br>
<b>Message</b>: {}""".format(artifact.value, 
                             "Successful" if results.get("content", {}).get("status", False) else "Unsuccessful",
                             results.get("content", {}).get("message", "None"))

if results.get("content", {}).get("status", False):
  incident.addNote(helper.createRichText(result_note))
  result_row = incident.addRow("splunk_intel_results")
  result_row.create_date = now
  result_row.status = "Added"
  result_row.intel_collection = results.inputs['splunk_threat_intel_type']
  result_row.intel_field = results.inputs['splunk_query_param1']
  result_row.intel_value = results.inputs['splunk_query_param2']
  result_row.splunk_server = rule.properties.splunk_servers

```

---
