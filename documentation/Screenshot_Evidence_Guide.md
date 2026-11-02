# Evidence walkthrough — OSPF outage and recovery

All screenshots should be captures from the actual Packet Tracer project or recording, with no simulated output represented as real output.

| Order | Screenshot | What to look for | What it proves |
|---|---|---|---|
| 01 | Topology with failed link | P1-to-PE2 red | Location of the simulated outage |
| 02 | Restored topology | P1-to-PE2 green | Physical/link recovery |
| 03 | P1 running config during failure | Gi0/1 with `shutdown` | Immediate configuration cause |
| 04 | P1 neighbor during failure | Only 1.1.1.1 FULL | PE2 adjacency disappeared |
| 05 | PE1 OSPF routes during failure | PE2 routes absent | Remote route was withdrawn |
| 06 | PE1 failed ping | `ping 3.3.3.3` 0% | Actual reachability problem |
| 07–09 | Failure detail and configuration | Down/down on P1 Gi0/1 | Corroborates root cause |
| 10 | P1 after recovery | Gi0/1 up/up; two FULL neighbors | Link and adjacency restored |
| 11 | PE1 route after recovery | OSPF route to 3.3.3.3 via 10.0.12.2 | Route learned again |
| 12 | PE1 recovered ping | 5/5 replies | End-to-end recovery verified |

**Incident summary:** The controlled outage was caused by administratively shutting down P1's GigabitEthernet0/1 toward PE2. Testing narrowed the failure to that link; inspecting interface state, OSPF neighbors and running configuration confirmed the cause. The link was re-enabled, OSPF adjacencies returned, and PE1-to-PE2 loopback connectivity was verified.

**Important:** Screenshots and the .pkt file still need to be uploaded to this repository. This guide describes already captured evidence, not newly created screenshots.
