<!--
    DO NOT MANUALLY EDIT THIS FILE
    THIS FILE IS AUTOMATICALLY GENERATED WITH resilient-sdk codegen
-->

# Defender Machine Isolation

## Function - Defender Machine Isolation

### API Name
`defender_machine_isolation`

### Output Name
`None`

### Message Destination
`fn_microsoft_defender`

### Pre-Processing Script
```python
inputs.defender_machine_id = row['machine_id']
inputs.defender_isolation_type = str(rule.properties.defender_isolation_type)
inputs.defender_description = rule.properties.defender_action_comment
inputs.defender_isolation_action = str(rule.properties.defender_isolation_action)
```

### Post-Processing Script
```python
import java.util.Date as Date

if results.success:
  row['report_date'] = Date().getTime()
  
  action_msg = "Action: {}\nComment: {}\nStatus: {}\nStart Date: {}".format(
    results.content['type'],
    results.content['requestorComment'],
    results.content['status'],
    results.content['creationDateTimeUtc']
    )
  row['machine_last_action'] = helper.createPlainText(action_msg)
else:
  msg = u"Defender Isolate Action {}.\nMachine: {} ({})\nAction: {}\nType: {}\nComment: {}\nReason: {}"\
   .format("successful" if results.success else "unsuccessful",
           row['machine_name'], row['machine_id'],
           str(rule.properties.defender_isolation_action),
           str(rule.properties.defender_isolation_type),
           rule.properties.defender_action_comment,
           results.reason)

  incident.addNote(helper.createPlainText(msg))

```

---
