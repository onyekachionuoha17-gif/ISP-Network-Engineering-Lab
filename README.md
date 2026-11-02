# ISP Network Engineering — OSPF Troubleshooting & MPLS/VRF Study

**Onyekachi Onuoha | Cisco Packet Tracer simulation**

## Why I built this
After my Network Engineer interview, I wanted to take the technical feedback and apply it, not just memorize definitions. I built a five-router ISP-style network to understand how routing works, how outages affect it, and how to explain my troubleshooting decisions clearly.

## Network topology
`CE1 — PE1 — P1 — PE2 — CE2`

PE1, P1 and PE2 run **OSPF Area 0**. CE1 and CE2 represent customer sites. This is a learning environment, **not a production network or an MPLS VPN**.

## What I completed hands-on
- Configured IPv4 point-to-point links and tested each direct connection.
- Configured provider OSPF Area 0, loopbacks and router IDs.
- Verified two FULL neighbors on P1 and OSPF-learned routes on PE1.
- Simulated an outage by shutting down P1 GigabitEthernet0/1.
- Verified missing PE2 adjacency, unavailable remote route, and failed ping.
- Restored the interface with `no shutdown`, verified both OSPF neighbors, the learned route and a successful ping to 3.3.3.3.

## My troubleshooting process
**Confirm symptom → test next hop → inspect interfaces → check OSPF → verify configuration → restore → retest.**

The immediate cause in this controlled exercise was an administratively disabled P1 Gi0/1. In production I would check approved maintenance and change records before reversing a shutdown.

## Evidence
See [Screenshot evidence guide](documentation/Screenshot_Evidence_Guide.md) for the screenshots and what each proves. The actual screenshots and Packet Tracer project are supplied separately until uploaded.

## Further technical study
[MPLS and VRF — relatable technical study](documentation/MPLS_VRF_Technical_Study.md) explains label forwarding, customer separation, MP-BGP, route distinguishers, route targets, and a proposed expansion. **MPLS/VRF have not yet been configured in this Packet Tracer lab.**

## Video
The demonstration has been recorded. A view-only video link will be added once hosted.

## Next steps
Add the Packet Tracer project, screenshots, incident PDF and video link; then extend the lab with redundancy and BGP. My goal is to show not just the commands, but why the commands matter and how each result supports a troubleshooting decision.
