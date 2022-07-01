# Description
this project is intended to generate EDLs for use with a Palo Alto firewall. It scrapes APIs for Maxmind and the likes for the ASNs assigned to common service providers like Netflix, Zoom, etc. 

# Why
This is not intended to be used for blocking traffic - in reality I'm using this to create policy based forwarding rules for applications like Netflix for my home firewall. I route most of my traffic through an encrypted VPN hosted on a VPS and Netflix (and some other streaming providers) like to block data center IP ranges.

_Its not perfect unfortunately, but its better than an Error 403 whenever I try to load Netflix._
