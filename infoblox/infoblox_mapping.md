# Infoblox DNS - Mapping to ECS

Note: Ensure that `infoblox_syslogpri.yml` is at the path specified in the logstash conf file. This yml file contains the mapping between the integer syslog priority codes contained in the data message and their meaning.

## Sample Data

The original message is placed in `event.original`

```
<30>Dec 22 01:38:34  escvns02.network1.corp.edd.ca.gov 151.143.1.55 named[25679]: 22-Dec-2020 01:38:34.595 client 151.143.101.3#65520: UDP: query: ihealth-api.f5.com IN A response: REFUSED -ED
```

We match the message above to the following pattern:
```
<event.severity>event.created  host.hostname host.ip agent.type[integer]: syslog_message
```

Note: the `integer` mapped above is the pid of the agent and is ignored.

The `syslog_message` is further parsed into the appropriate ECS schema fields as best possible. 

[Infoblox DNS Record Documentation](https://docs.infoblox.com/display/NAG8/Capturing+DNS+Queries+and+Responses)