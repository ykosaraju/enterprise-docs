---
title: "Anchore Enterprise Notifications"
linkTitle: "Notifications"
weight: 4
---

### Glossary

**_Event_** An information packet generated by an Anchore Engine or Anchore Enterprise service to indicate some activity    
**_Endpoint_** External tool capable of receiving messages such as Slack, GitHub, Jira, Teams, email or webhooks  
**_Endpoint Configuration_** Connection information of the endpoint used for sending messages  
**_Selector_** Criteria for selecting events to be notified

### Overview

Added in Anchore Enterprise v2.2

Anchore Enterprise includes support for sending messages about activity within Anchore Engine to an external endpoint. The Notifications service provides a mechanism to select the events to notify and direct them to one or more endpoints

### Installation

Anchore Enterprise Notifications is included with Anchore Enterprise, and is installed by default when deploying a trial quickstart with [Docker Compose]({{< ref "/docs/installation/docker_compose" >}}) or a production deployment [Kubernetes]({{< ref "/docs/installation/helm" >}}).

#### Configuration

The service loads it's configuration from the `notifications` section of the config.yaml. Here is a snippet of the configuration

```yaml
...
services:
  notifications:
    enabled: true
    require_auth: true
    endpoint_hostname: "<hostname>"
    listen: '0.0.0.0'
    port: 8228
    cycle_timers:
      notifications: 30
    # Set Anchore Enterprise UI base URL to receive UI links in notifications
    ui_url: "<enterprise-ui-url>"
    authorization_handler: external
    authorization_handler_config:
      endpoint: "<rbac-authorizer-endpoint>"
```

`cycle_timers -> notifications` controls how often the service checks for events in the system and processes notifications. Default is every 30 seconds  

`ui_url` is used for constructing links to Enterprise UI pages in the messages. Configure this property to the Enterprise UI's base URL. This URL should be accessible from the endpoint receiving the notification for the links to work correctly. If the value is unset, the notification message is still sent to the endpoint but it won't contain a clickable link to the Enterprise UI page  

> NOTE: Any changes to the configuration requires a restart of the service for the updates to take effect

#### Permissions



### Concepts


### See it in action

To learn more about configuring Notifications service in the Enterprise UI go to [Notifications]({{< ref "/docs/using/ui_usage/reports" >}})             

For using the API directly refer to <API Access link here> 

