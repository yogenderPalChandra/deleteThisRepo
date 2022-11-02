[Back to README](./README.md)


# busInternal flag

OC Schemas are extended for busInternal flag.

All the current OC services should send events to the 'oc-internal-bus'. For this, a flag called 'busInternal' has been introduced in the schemas.

When the busInternal = "true" the events are persisted in the 'oc-internal-bus'. While, when busInternal = "false" the events should be routed to ISC global bus. This is done by the eventbus pattern matching rule.

The Schema looks after extension looks like this:

```javascript
{
"title": "Equipment Unit Deleted", 
"type": "object", 
"service": "Equipment",
"action": "unit:deleted", 
"version": "v3.0.0", 
"eventBusName": "oc-internal-bus", 
"properties": {
"equipmentId": {
"type": "string",
"example": "example-equipment-id"
},
"account": {
"type": "string",
"example": "syskron"
}
}, 
"required": ["equipmentId", "account"], 
"additionalProperties": true, 
"busInternal": "true" // added property
}
```

Event rule:

```javascript
{
  "detail": {
    "busInternal": [{
      "prefix": "false"
    }]
  }
}

```

So if this rule hits, i.e. the event has the flag busInternal = "false" the event is routed to the ISC global bus.
