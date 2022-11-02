[Back to README](./README.md)

# busInternal flag

OC Schemas are extended for busInternal flag.

All the current OC services should send events to the 'oc-internal-bus'. For this a flag called 'busInternal' has been introduced in the schemas.

When the busInternal = "true" the events are persisted in the 'oc-internal-bus'. While when busInternal = "false" the events should be routed to ISC global bus. This is done by the eventbus pattern matching rule 
