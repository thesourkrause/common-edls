# Description
This project will include a Python Script that generates an EDL for a given service. An EDL, or External Data List is used in Palo Alto Networks PanOS to dynamically pull updates to address groups - which is extremely useful given the proliferation of cloud hosting providers and everything as a service.
# EDL vs Address Groups
Simplified, EDLs are an alternative that should be used when dealing with a large number of URLs, IPv4 Addresses (singular, range, or CIDR), domain names, and IPv6 addresses. They allow you to dynamically update an address group as well - which is perfect for a scenario where you're responsible for the assigned IP ranges.

An EDL is just a text file with little formatting. You have the option to add comments if you want, but you're not required. EDLs can be hosted anywhere, so long as the URL is accesible by the firewalls management plane.

[Palo Alto TechDocs - External Dynamic List](https://docs.paloaltonetworks.com/pan-os/9-1/pan-os-admin/policy/use-an-external-dynamic-list-in-policy/external-dynamic-list)
# Supported Services
__This is a list of planned services. it is subject to change.__
- [ ] Amazon Prime Video
- [ ] Amazon Web Services
- [ ] BlueJeans
- [ ] Cisco Webex
- [ ] Dialpad
- [ ] Disney Plus
- [ ] Google Video
- [ ] Google Voice
- [ ] Hulu
- ~~[ ] Line2~~ Unable to find public database (no ARIN Assignment or help page)
- [ ] Microsoft 365 
- [ ] Microsoft Azure
- ~~[ ] Microsoft Teams~~ (Covered in Microsoft 365)
- [ ] Netflix
- [ ] Pandora Radio
- [ ] Ring Central
- [ ] Skype
- ~~[ ] Slack~~ (Too single instance specific - perhaps \*.slack.us/ or \*.enterise.slack.us)
- [ ] Spotify
- [ ] Tidal
- [ ] YouTube
- [ ] Zoom
## Methods of Import
The script will support parsing and grabbing relevant ranges based on the following:
1. JSON Parsing
2. Web Scraping
3. Query ARIN Assignment Database (or equal regional entity)
4. Direct Import (for .txt files in already usable format)
## Outputs
The script will place a file in the `lists/` directory for each service and output type. The format of each file is `[service-name]-[output-type].txt` Examples:
* `lists/amazon-web-services-ipv4.txt` - IPv4 Assignments for AWS
* `lists/amazon-web-services-ipv6.txt` - IPv6 Assignments for AWS
* `lists/amazon-web-services-url.txt` - URL List for AWS
## Configuring a Service for Import:
Add an entry to the `configs/services.yml` file with the service you desire to add: 
```yaml
services:
    - service-name: my-service
        method: "arin-query"
        sources:
            - "ASXXXXX"
        status: "validated"
        types:
            - ipv4
        enabled: true
```
## Mapping a schema for the JSON Parser
Simple place the scheme in the `configs/schemas/` directory and add the schema to the `configs/services.yml` file.
```yaml
    services:
        - service-name: my-service
            method: "json-query"
            schema: "my-service-schema.json"
            # Ommitted for brevity...
```