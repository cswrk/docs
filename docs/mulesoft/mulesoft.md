---
layout: default
title: Mulesoft
nav_order: 1
permalink: docs/mulesoft
---
# Mulesoft

## ESB (Enterprise Service Bus)
An ESB is a mediating layer connecting independent pieces of software. These apps often use different protocols. Consequently, the ESB will take care of transforming and routing the data. This allows for the creation of decoupled services. Therefore, each service does not need to worry about how another service will consume its output.

## Anypoint Platform

### Desing Center

### Anypoint Studio

#### Flows
A flow is a connected collection of Mule components.
It usually consists of an inbound endpoint component (from where a message originates), and an outbound endpoint component. Therefore, the flow is responsible for the various processing stages in which the message may undergo.

There are three different types of flows in Mule:
    Subflows – a synchronous flow inheriting the processing and exception handling strategy of the parent flow
    Synchronous Flows – a synchronous flow with its processing and exception handling strategy
    Asynchronous Flows – an asynchronous flow with its processing and exception handling strategy

#### MEL Expressions
Show payload as string:: `#[message.payloadAs(java.lang.String)]`

## Components
### Logger
```xml
<logger 
  doc:name="Log Payload"
  message="Rest Request: #[payload]" 
  level="INFO"
/>
```

message:: Mel expression.
level:: INFO, DEBUG, WARN, etc.
doc:name:: Nombre que se va a mostrar en el flow.

