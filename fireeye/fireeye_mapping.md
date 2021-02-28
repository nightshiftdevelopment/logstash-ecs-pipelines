# FireEye Alert - Mapping to ECS

## Appliance Setup

- Within FireEye HX administration page, configure appliance to send HTTP alert data to the Logstash instance at a specific high-numbered port
- JSON data format is recommended

## Top-level Fields

| Data Field | ECS Field | Notes | 
| ---------- | --------- | ----- | 
| appliance | observer.hostname | |
| appliance-id | observer.serial_number | |
| version | observer.version | |
| host | observer.host | | 
| product | observer.product | |

## Alert sub-fields

| Data Field | ECS Field | Notes | 
| ---------- | --------- | ----- | 
| event_at | @timestamp | time at which event occurred |
| matched_at | event.created | time at which event was detected by observer |
| reported_at | event.ingested | time at which event arrived at central data store |
| host.domain | host.domain | |
| host.agent_version | agent.version | | 
| host.gmt_offset_seconds | host.gmt_offset_seconds | |
| host.hostname | host.hostname | |
| host.ip | host.ip | |
| host.os | host.os.full | |
| host.agent_id | agent.id | |
| host.containment_state | host.containment_state | |
| event_type | event.type | |
| event_id | event.id | |
| event_values | event.values | contains custom fields relevant to specific event type |
| source | event.reason | |
| condition | condition | | 
| indicator | indicator | |
| sysinfo.mac_address | host.mac | |
| indicator_category | indicator_category | |

Note: fields/objects present in data that are not found in ECS (e.g. `event_values`, `indicator`) are left as-is without mapping to an ECS field.


## Sample Record

```
{
    "version": "5.0.2.921836",
    "msg": "normal",
    "product": "HX",
    "appliance": "esccohxfe.network1.corp.edd.ca.gov",
    "appliance-id": "0CC47ADB5600",
    "alert": {
        "indicator": {
            "uri_name": "2b4753b0-9972-477e-ba16-1a7c29058cee",
            "_id": "2b4753b0-9972-477e-ba16-1a7c29058cee",
            "category_id": 7,
            "description": "IOC used for testing HX appliances and content packages to ensure that things work end to end",
            "display_name": "FIREEYE END2END TEST",
            "signature": null
        },
        "resolution": "ALERT",
        "_id": 281164,
        "host": {
            "hostname": "ETMSVCASB02",
            "containment_state": "normal",
            "gmt_offset_seconds": -28800,
            "agent_version": "32.30.13",
            "ip": "67.157.228.24",
            "domain": "EDD_DOMAIN",
            "os": "Windows Server 2016 Standard",
            "agent_id": "DuKOMhdD4xkbswZqzgxfH9"
        },
        "event_at": "2020-12-21T16:01:19.36+00:00",
        "condition": {
            "_id": "UQnn6VDlzmoacFpSAuK4cA==",
            "enabled": true,
            "tests": [
                {
                    "type": "text",
                    "token": "urlMonitorEvent/requestUrl",
                    "operator": "contains",
                    "value": "test-infection.exe"
                }
            ]
        },
        "indicator_category": {
            "uri_name": "mandiant_unrestricted",
            "_id": 7
        },
        "sysinfo": {
            "_id": "DuKOMhdD4xkbswZqzgxfH9",
            "mac_address": "00-50-56-a0-9b-f6"
        },
        "uuid": "23e5137e-2f39-47e5-af77-688199e81aaa",
        "event_type": "urlMonitorEvent",
        "matched_source_alerts": null,
        "matched_at": "2020-12-21T16:01:34+00:00",
        "reported_at": "2020-12-21T16:01:44.23+00:00",
        "source": "IOC",
        "event_id": 540924,
        "event_values": {
            "urlMonitorEvent/httpHeader": "GET /appliance-test/test-infection.exe HTTP/1.1\r\nHost: fedeploycheck.fireeye.com\r\nConnection: keep-alive\r\nUpgrade-Insecure-Requests: 1\r\nUser-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36\r\nAccept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9\r\nAccept-Encoding: gzip, deflate\r\nAccept-Language: en-US,en;q=0.9\r\n\r",
            "urlMonitorEvent/timestamp": "2020-12-21T16:01:19.360Z",
            "urlMonitorEvent/hostname": "fedeploycheck.fireeye.com",
            "urlMonitorEvent/requestUrl": "/appliance-test/test-infection.exe",
            "urlMonitorEvent/remoteIpAddress": "172.65.203.203",
            "urlMonitorEvent/remotePort": 80,
            "urlMonitorEvent/urlMethod": "GET",
            "urlMonitorEvent/userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36",
            "urlMonitorEvent/localPort": 51600,
            "urlMonitorEvent/pid": 15076,
            "urlMonitorEvent/process": "chrome.exe",
            "urlMonitorEvent/processPath": "C:\\Program Files (x86)\\Google\\Chrome\\Application",
            "urlMonitorEvent/username": "EDD_DOMAIN\\KKeehner-22"
        },
        "name": "indicator-executed"
    }
}
```