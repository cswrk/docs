---
title: Mulesoft
has_children: false
nav_order: 3
---

# Mulesoft

## ESB (Enterprise Service Bus)
The MuleSoft approach to integration, integration of data from different systems using a layer of APIs. An ESB is a mediating layer connecting independent pieces of software. These apps often use different protocols. Consequently, the ESB will take care of transforming and routing the data. This allows for the creation of decoupled services. Therefore, each service does not need to worry about how another service will consume its output.

### Message Inbound Properties
* http.context.path: _String_
* http.context.uri: _String_
* http.headers: _Map_
* http.method: _String_
* http.query.params: _Map_
  * email: _String_
* http.query.string: _String_
* http.relative.path: _String_
* http.request: _String_
* http.request.path: _String_
* http.status: _String_
* http.version: _String_
  
  
#### Source
https://docs.mulesoft.com/general/

