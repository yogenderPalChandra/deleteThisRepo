
10. **(optional)** **Service internal bus:**:

Internal bus: Service can choose to have and publish to the internal bus. From there the events can be routed to global bus based on the `eventBusName`. 
- `eventBusName` in the schemas should be used to distinguish between internal and public events.
- Producers and consumers of internal events have to publish/listen to the internal bus (since internal events should not appear on public bus.
    - If the event becomes public, consumers and producers should be modified to listen/publish to global eventbus.
    - Switch of consumers is only necessary if it is expected that event in question could be published by other services.
    - Producers can still publish to internal event as long as there is the rule to forward the events to public event bus, but it might be better to switch all internal producers and consumers to public bus.

For example, If a service wants to route the event also to the general ISC bus `s2a-isc-eventbridge-eventbus`, this can be done. The routing is done using event pattern matching rule. 

[Here is the AWS doc of pattern matching](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-event-patterns-content-based-filtering.html)

One example of rule is:

```javascript
{
  "detail": {
    "schema": {
      "eventBusName": [{
        "anything-but": "oc-internal-bus"
      }]
    }
  }
}

```
So if this rule hits, i.e. `eventBusName!=oc-internal-bus` the event would be routed to the `s2a-isc-eventbridge-eventbus` which is the target in this case.
