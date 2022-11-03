10. **(optional)** **exampleFlag**:

If a service wants to route the message to global bus if this flag is set to false. 
For example, If exampleFlag="false", the events can be routed to 'target-event-bus'. The routing is done using event pattern matching. 

[Here is the AWS doc of pattern macthing](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-event-patterns-content-based-filtering.html)


```javascript
{
  "source": ["name-of-service"],
  "detail": {
    "schema": {
      "exampleFlag": [{
        "prefix": "false"
      }]
    }
  }
}

```
So if this rule hits, i.e. the event has the flag exampleFlag="false" the event would be routed to the target-event-bus.
