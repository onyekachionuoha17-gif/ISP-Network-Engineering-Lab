# MPLS & VRF — What I Learned

**Onyekachi Onuoha | Conceptual technical study, not a completed MPLS configuration**

After my Network Engineer interview, I wanted to understand how a service provider connects multiple businesses without mixing their networks together. Two key ideas I studied are MPLS and VRF.

## MPLS: Think of packages in a shipping center
Packages have destination addresses, but sorting stations can use labels to move them along a delivery path. MPLS means **Multiprotocol Label Switching**. A provider-edge router can **push** a label onto traffic, core routers **swap** labels as packets move through the provider, and a router near the exit can **pop** a label.

MPLS doesn't automatically encrypt traffic, and it isn't guaranteed to be faster than IP forwarding. Its value includes providing a flexible label-forwarding method that supports provider services such as Layer 3 VPNs.

## VRF: Separate address books in the same building
Think of several businesses sharing an office building but each having its own address book. **Virtual Routing and Forwarding (VRF)** gives different customers separate routing/forwarding tables on shared network equipment. Two customers can even use an overlapping prefix such as `192.168.10.0/24` without those routes being treated as the same customer's route. VRF is logical separation, not encryption.

## How the provider technologies fit together
- **OSPF:** helps internal provider routers learn how to reach backbone destinations.
- **MPLS:** forwards traffic across the provider core using labels.
- **VRF:** separates customer routing tables.
- **MP-BGP:** exchanges VPN routes between provider-edge routers.
- **Route distinguisher (RD):** gives otherwise identical VPN prefixes distinct identities.
- **Route target (RT):** controls which VRFs import and export VPN routes.

For an MPLS Layer 3 VPN, a customer-edge router connects to a provider edge. The PE places customer routes in the appropriate VRF, MP-BGP distributes VPN routing information to other PEs, and MPLS transports traffic across the core toward the destination PE.

## How I would troubleshoot
I'd first confirm the reported failure and its scope, check customer-facing interfaces and the relevant VRF route table, and test PE-to-PE reachability. Then I'd investigate MP-BGP VPN route exchange, route-target policy, MPLS transport labels, and forwarding entries. In production I would check change records before making a fix and verify recovery from the affected customer's perspective.

## What I have and have not done
I **have** built an OSPF provider-backbone simulation in Packet Tracer and demonstrated routing outage and recovery. I **have not yet** configured a working MPLS L3VPN or VRF/MP-BGP service in that simulator. My next goal is to use an emulator with those capabilities and verify label forwarding, VRF isolation and VPN route exchange.

This study helped me think beyond connecting routers: a provider must keep the backbone reachable while managing many separate customer networks reliably.
