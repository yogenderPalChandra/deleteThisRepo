10. **(optional)** **Service internal bus:**


Service can choose to have and publish to the internal bus.


- `eventBusName` in the schemas should be used to distinguish between internal and public events.

- Producers and consumers of internal events have to publish/listen to the internal bus since internal events should not appear on public bus.

- If the event becomes public:

  - if the event in question is command or request type:

    - all consumers and producers have to be modified to listen/publish to global eventbus.

  - if the event in question is broadcast type:

    - only consumers have to be modified to listen on global eventbus.

    - publishers should also be modified to publish to global event bus but it they are not, the events should be forwarded from internal bus to the global bus.

From there the events can be routed to global bus based on the `eventBusName`.

In order to forward the event from internal to public bus following rule event pattern can be used:

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
