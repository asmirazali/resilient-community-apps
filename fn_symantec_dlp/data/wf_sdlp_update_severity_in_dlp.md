<!--
    DO NOT MANUALLY EDIT THIS FILE
    THIS FILE IS AUTOMATICALLY GENERATED WITH resilient-sdk codegen
-->

# Symantec DLP: Update Severity in DLP

## Function - Symantec DLP: Update Incident in DLP

### API Name
`symantec_dlp_update_incident`

### Output Name
`None`

### Message Destination
`fn_symantec_dlp`

### Pre-Processing Script
```python
inputs.incident_id = incident.id
inputs.sdlp_incident_severity_id = incident.severity_code
inputs.sdlp_incident_status = None
```

### Post-Processing Script
```python
None
```

---
