# CCNP Enterprise: deliberate troubleshooting workflow

## Keep ENCOR and ENARSI review distinct

Use the current official topics to choose the scope of each session. ENCOR review should not collapse into routing alone: include architecture, virtualization, infrastructure, assurance, security and automation. ENARSI deepens the routing, VPN, infrastructure security and services troubleshooting covered by that concentration.

Do not infer exact objective coverage or certification readiness from the number of practice items completed.

## A 40-minute session

1. **Five minutes — define the traffic.** Draw a small fictional topology and label addresses, VRF, direction and expected service.
2. **Ten minutes — predict evidence.** Select one failure boundary and predict interface, adjacency, route, forwarding and policy observations. Distinguish what would remain healthy.
3. **Ten minutes — investigate.** Use authorized lab observations or a paper analysis. Compare two plausible causes and choose the least disruptive distinguishing observation.
4. **Ten minutes — verify the mechanism.** Read the official platform/protocol reference. Note version and feature assumptions, then revise the explanation.
5. **Five minutes — record and revisit.** Write the failed boundary, the justified repair and the necessary regression checks. Schedule a delayed review with a different packet or direction.

Paper analysis is useful preparation, but label it honestly. It is not an executed lab or proof of operational skill.

## An observation-first lab sequence

In an isolated authorized lab, identify the software version, interface state, applicable VRF, neighbor state and route to a chosen destination. Record the corresponding reverse-path observations. Depending on platform support, commands may include `show version`, `show interfaces`, `show ip route`, `show ip ospf neighbor` or address-family/VRF-specific equivalents. Check the platform's help and documentation rather than assuming an exact universal syntax.

Do not clear adjacencies, debug indiscriminately, change routing policy or reset interfaces in an observation-only activity. Some collection operations can be resource-intensive or expose sensitive configuration. Keep output sanitized and access-controlled.

If you choose to introduce a fault later, use only a disposable lab and define rollback first. Never create a production outage to reproduce a study example.

## Private troubleshooting notebook

```text
Exam/topic / date / platform and software:
Topology and authorized scope:
Packet: source, destination, protocol/ports, VRF, direction:
Expected forward and return paths:
Observed state and timestamps:
Two plausible causes:
Observation that distinguishes them:
Expected evidence for each cause:
Actual evidence, or "paper analysis only":
Why the tempting alternative does not explain the evidence:
Minimal repair and rollback:
End-to-end and regression verification:
Reference / applicability limitation:
Next review date:
```

Use invented addresses, names and credentials in shared material. Do not share full running configurations, packet payloads or device access secrets.

## Classify the reasoning gap

Useful labels are **wrong VRF**, **adjacency versus route**, **policy direction**, **next-hop resolution**, **return path**, **MTU**, **counter timing**, **scheduled versus configured**, **model validation**, and **accepted versus completed**. Each suggests a specific next session.

When reviewing a practice result, explain the best competing action rather than memorizing the selected letter. A familiar command may act at the wrong layer. An uncertain correct selection is still a learning gap. Repeat the principle with one changed constraint so that recognizing wording is not enough.

Practice percentages are study signals, not Cisco score conversions or pass predictions. Readiness also requires breadth against the current objectives and appropriate permitted hands-on work beyond these notes.
