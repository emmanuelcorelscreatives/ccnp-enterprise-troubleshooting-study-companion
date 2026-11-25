# Official references: CCNP Enterprise decisions

Links point to original publishers; no full manuals or exam documents are included. This offline companion uses the preserved ENCOR v1.2 / ENARSI v1.1 course context, dated November 25, 2026. Check the current certification page, topic list and platform release documentation for changes. Links were not rechecked live for this task.

## Certification and topic boundaries

- [Cisco CCNP Enterprise](https://www.cisco.com/site/us/en/learn/training-certifications/certifications/enterprise/ccnp-enterprise/index.html) — verify the core/concentration path and follow current exam information.
- [Cisco ENCOR v1.2 topic PDF](https://learningcontent.cisco.com/documents/marketing/exam-topics/350-401-ENCORE-v1.2.pdf) — review the enterprise-core scope; obtain newer topics from Cisco if the version changes.
- [Cisco ENARSI v1.1 topic PDF](https://learningcontent.cisco.com/documents/300-410-ENARSI-v1.1.7-2025.pdf) — keep concentration preparation distinct from the core outline.

## Routing and forwarding

- [Cisco route selection](https://www.cisco.com/c/en/us/support/docs/ip/enhanced-interior-gateway-routing-protocol-eigrp/8651-21.html) — distinguish route selection principles and their scopes.
- [Cisco OSPF neighbor troubleshooting](https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/13685-13.html) — connect the observed neighbor state to the investigation stage.
- [Cisco OSPF MTU mismatch troubleshooting](https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/13684-12.html) — distinguish database-exchange issues from a complete packet-size solution.
- [Cisco BGP best-path selection](https://www.cisco.com/c/en/us/support/docs/ip/border-gateway-protocol-bgp/13753-25.html) — verify documented selection and next-hop requirements for the actual platform/configuration.
- [Cisco VRF-Lite configuration guide](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst9500/software/release/17-14/configuration_guide/rtng/b_1714_rtng_9500_cg/configuring_vrf_lite.html) — examine routing-instance boundaries; this page's platform/release is not a promise of identical syntax on all devices.

## Architecture, protection and assurance

- [Cisco SD-WAN design guide](https://www.cisco.com/c/en/us/td/docs/solutions/CVD/SDWAN/cisco-sdwan-design-guide.html) — distinguish control, transport, overlay and policy responsibilities.
- [Cisco SD-Access deployment profile](https://www.cisco.com/c/en/us/td/docs/cloud-systems-management/network-automation-and-management/catalyst-center/cisco-validated-solution-profiles/validated-profile-sda-deployment.html) — review the specific design assumptions before generalizing a fabric behavior.
- [Cisco unicast reverse path forwarding](https://www.cisco.com/c/en/us/td/docs/routers/ios-xe/ip-routing/b-ip-routing/m_cfg-unicast-rpf-0.html) — compare source validation modes with the network's routing symmetry.
- [Cisco control-plane policing](https://www.cisco.com/c/en/us/td/docs/routers/ios/config/17-x/qos/b-quality-of-service/m_qos-plcshp-ctrl-pln-plc-0.html) — identify the traffic being protected rather than treating CoPP as a universal transit filter.
- [Cisco IP SLA ICMP echo operations](https://www.cisco.com/c/en/us/td/docs/routers/ios/config/17-x/ip-addressing/b-ip-addressing/m_sla_icmp_echo.html) — verify probe source, operation and scheduling before interpreting a result.

## Modeled automation

- [Cisco NETCONF configuration](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/prog/configuration/26x/26x-programmability-cg/netconf_protocol.html) and [RESTCONF configuration](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/prog/configuration/26x/26x-programmability-cg/restconf_protocol.html) — check capabilities, authorization and release applicability.
- [IETF NETCONF, RFC 6241](https://www.rfc-editor.org/rfc/rfc6241.html) and [RESTCONF, RFC 8040](https://www.rfc-editor.org/rfc/rfc8040.html) — distinguish protocol semantics from any one device's supported models and features.

Examples and conceptual reasoning in this companion are original. A reference link is not authorization for a production change, proof of an executed lab or Cisco endorsement.
