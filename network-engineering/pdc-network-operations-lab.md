# Perishable Distribution Center Network Operations Lab

## Project Status

**In development — flagship portfolio project**

## Objective

Design, document, and troubleshoot a simulated high-volume perishable distribution center network where network availability directly supports receiving, inventory, picking, voice-directed work, printing, scanning, staging, and shipping operations.

The project is intentionally focused on the operational relationship between:

**Network infrastructure → warehouse technology → business continuity**

---

## Environment

The simulated environment includes:

- Aruba wireless infrastructure
- LAN switching
- VLAN segmentation
- DHCP and DNS
- Fortinet firewall / SD-WAN concepts
- RF handheld devices
- Honeywell voice devices
- Zebra printers and mobile devices
- Network monitoring
- Incident and change documentation

> Vendor-specific components in this project are clearly identified as laboratory/simulation work unless separately supported by production experience.

---

## Proposed Network Segmentation

| VLAN | Purpose |
|---|---|
| 10 | Corporate Users |
| 20 | Warehouse / RF Devices |
| 30 | Voice |
| 40 | Printers |
| 50 | Wireless Infrastructure |
| 60 | Network Management |
| 70 | Servers / Applications |
| 80 | Guest |
| 90 | IoT / Automation |

---

## Core Troubleshooting Flow

```text
User / Device Symptom
        |
        v
Determine Business Impact
        |
        v
Check Physical / L1
        |
        v
Validate VLAN / L2
        |
        v
Validate IP / DHCP
        |
        v
Validate DNS / Gateway
        |
        v
Validate Routing / WAN
        |
        v
Validate Application
        |
        v
Restore Service
        |
        v
Document Root Cause
```

---

# Incident Scenarios

## INC-001 — Zebra Printer Unreachable

### Symptom

A shipping workstation cannot communicate with a Zebra label printer.

### Investigation

- Validate physical connectivity
- Check switch port state
- Verify VLAN assignment
- Verify printer IP address
- Test gateway reachability
- Check DHCP/reservation status
- Test printer connectivity

### Example validation commands

```bash
ping <printer-ip>
ipconfig
arp -a
nslookup <printer-hostname>
tracert <printer-ip>
```

### Engineering objective

Determine whether the failure is physical, Layer 2, IP addressing, DHCP, DNS, or endpoint-related.

---

## INC-002 — RF Scanner Intermittent Connectivity

### Symptom

Multiple warehouse handheld devices disconnect in one operating zone.

### Investigation

- Determine affected geographic area
- Identify associated AP
- Validate AP and switch connectivity
- Check VLAN assignment
- Review DHCP status
- Examine signal quality / RF conditions
- Check roaming behavior
- Compare affected clients with healthy clients

### Engineering objective

Distinguish between an RF problem, AP/uplink problem, VLAN/DHCP issue, or application/backend issue.

---

## INC-003 — Honeywell Voice Device Connectivity

### Symptom

A selector reports intermittent voice communication while moving between warehouse zones.

### Investigation

```text
Client
  ↓
Wireless Association
  ↓
AP
  ↓
RF / Signal Quality
  ↓
Roaming
  ↓
VLAN
  ↓
DHCP
  ↓
Gateway
  ↓
Voice Application
```

### Engineering objective

Determine whether the problem originates with the device, wireless infrastructure, network services, or application layer.

---

## INC-004 — Warehouse AP Failure

### Symptom

A group of handheld devices loses connectivity in one warehouse zone.

### Investigation

- Confirm scope
- Check AP reachability
- Check switch port
- Check PoE
- Validate uplink
- Verify VLAN
- Compare neighboring AP coverage
- Validate client association after remediation

---

## INC-005 — Primary WAN Failure

### Symptom

The primary WAN path becomes unavailable.

### Investigation

- Check circuit state
- Check FortiGate/SD-WAN health
- Validate tunnel status
- Confirm alternate path
- Test Internet/application reachability
- Measure latency and packet loss

### Engineering objective

Validate service continuity and collect evidence for escalation to the Network Engineering or carrier team.

---

## INC-006 — DHCP Scope Exhaustion

### Symptom

New warehouse devices fail to obtain an IP address.

### Investigation

- Check client configuration
- Verify DHCP scope utilization
- Validate VLAN
- Check DHCP relay/helper configuration
- Compare static and dynamic clients

---

## INC-007 — Incorrect VLAN Assignment

### Symptom

A newly installed warehouse device receives an unexpected IP address and cannot access the required application.

### Investigation

- Check switch port
- Verify access VLAN
- Check MAC address table
- Validate DHCP scope
- Test gateway and application reachability

---

## INC-008 — DNS Resolution Failure

### Symptom

A device can reach its gateway and external IP addresses but cannot resolve application hostnames.

### Investigation

```bash
ping <gateway>
ping 8.8.8.8
nslookup <hostname>
tracert <hostname>
```

Determine whether the issue is client configuration, DNS server reachability, record resolution, or application-specific.

---

# Engineering Documentation

Each completed incident will contain:

1. Incident summary
2. Business impact
3. Scope
4. Initial hypothesis
5. Troubleshooting evidence
6. Root cause
7. Remediation
8. Validation
9. Escalation information, if applicable
10. Preventative action

---

# Success Criteria

The project is complete when the portfolio demonstrates the ability to:

- Design a segmented warehouse network
- Explain the role of WLAN, VLAN, DHCP, DNS and WAN services
- Troubleshoot network-connected warehouse devices
- Separate device, network and application failures
- Document incidents professionally
- Communicate technical findings to operations teams
- Escalate complex issues with useful evidence
- Connect technical availability to business operations
