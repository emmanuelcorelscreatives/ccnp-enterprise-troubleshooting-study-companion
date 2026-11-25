# CCNP Enterprise: an evidence-first troubleshooting review

## Define the packet before choosing the protocol

Write the source/destination addresses, protocol and ports, ingress device, routing instance/VRF, direction and expected path. Add the symptom's start time and the last known working state. Separate an intermittent loss report from a sustained routing failure.

Collect version/platform information and relevant observations before changing timers, restarting processes or clearing sessions. Preserve timestamps: a current interface state and a routing table from yesterday do not describe one coherent event.

Use four evidence layers:

1. **Physical and link state:** can the local interface and segment carry the intended traffic?
2. **Control-plane state:** are the relevant neighbors and advertisements present?
3. **Forwarding state:** which route and next hop are actually used in this VRF?
4. **Service/policy state:** do ACLs, NAT, security associations, QoS and the application permit the complete transaction?

Success at one layer is not automatic proof of the next. An established neighbor does not establish a specific prefix, and an installed prefix does not prove the return path or application policy.

## 1. Routing decisions happen in a specific context

For a destination, first identify the matching routing instance and the most specific applicable prefix. Then investigate which candidate route was selected and why. Administrative distance compares route sources for the same prefix; protocol metrics and BGP path selection have their own scope. Do not use an administrative-distance comparison to override longest-prefix matching between different prefix lengths.

Check the selected route's next-hop resolution and its forwarding representation. A route can be learned without becoming usable forwarding state. Verify the return route separately, especially across VRFs, firewalls or asymmetric designs.

| Observation | Useful inference | Still unproven |
|---|---|---|
| Neighbor is established | The relevant session has formed | Intended prefix reception, acceptance, selection and forwarding |
| Prefix is in a protocol table | The protocol knows a candidate | Installation in the IP routing/forwarding table |
| Route appears in the expected VRF | A route exists in that context | Correct next-hop resolution, filters and reverse path |
| Ping from the router succeeds | That sourced probe worked | The user's different source/VRF/application path |

Choose probes that represent the affected traffic, within authorization. A convenient management-source ping may test a different policy and return path than the user's packet.

## 2. OSPF: inspect the stage of adjacency

Different neighbor states suggest different investigation points. Check the actual interface, area, addressing/network type, timers and authentication as applicable. Determine whether a full adjacency is expected for that relationship; not every visible neighbor must be FULL in every multiaccess role.

For an adjacency stalled during database exchange, investigate MTU compatibility and related exchange conditions instead of treating every symptom as a hello failure. An MTU-ignore setting is not proof that the data path can carry application packets; it can bypass one check while leaving a real packet-size problem.

If adjacency is healthy but a route is missing, move to LSDB content, area behavior, filtering/summarization, route selection and next-hop resolution. Repeatedly clearing a healthy neighbor is disruptive and does not explain a policy decision elsewhere.

Record whether the failure affects one neighbor, one segment, one area or the entire process. That scope helps distinguish a local interface mismatch from a wider design or redistribution problem.

## 3. EIGRP and BGP: distinguish eligibility from preference

For EIGRP, separate neighbor formation, topology knowledge and installed successor routes. A loop-prevention condition is not merely a performance preference; bypassing safeguards to make a candidate appear usable can introduce a different failure. Check the relevant metrics, feasibility and query behavior in the actual topology.

For BGP, inspect the stages deliberately: session, received/accepted route, policy, best-path eligibility/selection, IP-route installation and forwarding. Establish which policy direction and address family apply. A valid prefix denied by import policy will not be repaired by changing an export policy on an unrelated neighbor.

Use the documented path-selection behavior for the platform and configuration. A high local preference or an attractive AS path does not cure an unresolved next hop. A BGP best-path decision also does not remove the need to check competing routing sources and forwarding context.

With redistribution, write down the route's source, direction, seed metric where required, tags and re-entry policy. A route map can prevent feedback, but only if its matching and policy application actually cover the route being redistributed. Validate both legitimate reachability and the absence of loops after any authorized change.

## 4. VRFs, overlays and encryption are different boundaries

An address that exists in the global table does not automatically exist in a tenant VRF. Investigate route import/export or the deliberate leak mechanism, next-hop reachability and policy in both directions. Avoid leaking every route as a shortcut to restore one service.

An overlay adds a logical connectivity or segmentation mechanism; it is not automatically encryption. Verify the underlay, tunnel endpoints, mappings and overlay identifiers separately. With SD-Access or SD-WAN, distinguish controller/control reachability from the actual data-plane and policy outcome.

For IPsec, a security association is not proof that the affected traffic matches the intended selectors and completes a round trip. Correlate the packet definition with policy, routing, NAT interaction, encapsulation/decapsulation counters and peer observations. A tunnel interface being up can still coexist with a failed application path.

When counters increase only in one direction, examine return routing and the remote policy before assuming that encryption itself is broken. When only large traffic fails, investigate MTU/fragmentation and encapsulation overhead rather than interpreting a small ping as complete validation.

## 5. Security controls protect different targets

| Control | Review boundary | Misdiagnosis to avoid |
|---|---|---|
| Interface ACL | Direction, packet fields and actual attachment point | Editing a similar named ACL that is not on the packet path |
| AAA | Authentication, authorization and accounting | Assuming successful login grants every operational command |
| CoPP | Traffic directed to the device's control plane | Treating a control-plane policy as a universal transit-traffic filter |
| uRPF | Source validity relative to the configured mode and routing | Enabling strict assumptions on an intentionally asymmetric path without checking consequences |
| Layer 2/first-hop protections | Correct port roles and trust boundary | Marking untrusted access ports trusted to suppress legitimate protection events |

Inspect matched counters with timestamps and the real packet tuple. A counter that never increments can mean the wrong attachment, direction or test traffic; it does not prove the entire policy is harmless. A cumulative drop count without timing is not proof of the current incident's cause.

Do not disable an entire protection system merely to see whether connectivity returns. Use a bounded approved test with rollback and preserve access to the management plane.

## 6. Assurance: evaluate what the measurement sampled

For an IP SLA failure, inspect operation type, source, destination, VRF, scheduling, return path and target behavior. A configured but unscheduled operation has not supplied a current measurement. A device can answer ICMP while the application transaction fails, or filter ICMP while the application works.

For flow telemetry, verify exporter, collector reachability, observation point, template/record compatibility, sampling and timestamps. Missing collector records are not automatically zero traffic. For packet captures, establish the capture point and filters; traffic absent from that point may have been routed elsewhere.

Queue drops, interface errors, CPU utilization and application latency are different signals. Correlate them in the same time window before selecting a QoS or capacity change. Protect privacy when collecting packets; payloads and management exchanges can contain sensitive information.

## 7. Automation: accepted is not completed

Treat an API operation as a sequence: authenticate, authorize, validate the payload, submit, correlate the response, follow asynchronous status if applicable and read back resulting state. NETCONF/RESTCONF syntax and capabilities depend on the device and service configuration; inspect them rather than assuming identical behavior everywhere.

A successful connection does not prove authorization to modify the intended model. Well-formed JSON is not necessarily a valid YANG-modeled request. An HTTP acceptance response is not proof of final convergence, and a client timeout can leave the result unknown rather than definitely failed.

Before retrying a write, reconcile its operation identity and the actual target state. Make automation bounded, preserve per-device results and avoid treating partial success as fleet-wide completion. Never put credentials into a shared notebook or hard-code them into a study script.

## 8. Verify the repair without erasing the explanation

After an authorized change, verify the original source/VRF/application path and the reverse direction. Check route/policy stability, intended segmentation and relevant counters. Remove temporary tests and record the before/after evidence and rollback outcome.

The strongest troubleshooting explanation is not simply “the command fixed it.” It states the failed boundary, the observations that isolated it, the minimal justified change and the verification that excluded the most important regressions.
