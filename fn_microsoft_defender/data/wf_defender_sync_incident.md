<!--
    DO NOT MANUALLY EDIT THIS FILE
    THIS FILE IS AUTOMATICALLY GENERATED WITH resilient-sdk codegen
-->

# Defender Sync Incident

## Function - Defender Update Incident

### API Name
`defender_update_incident`

### Output Name
`None`

### Message Destination
`fn_microsoft_defender`

### Pre-Processing Script
```python
inputs.defender_incident_id = incident.properties.defender_incident_id
inputs.defender_classification = incident.properties.defender_classification
inputs.defender_determination = incident.properties.defender_determination
inputs.defender_tags = incident.properties.defender_tags
```

### Post-Processing Script
```python
None
```

---
