# README

# Glass Onion — STIX Threat Intelligence Data

This folder contains **STIX 2.1** (Structured Threat Information eXpression) bundles related to the **Glass Onion** research: *Peeling Back the Layers of a Pro-China Online Ecosystem*.

view at:

[https://graphika.com/reports/glass-onion](https://graphika.com/reports/glass-onion)

## Source

The intelligence was produced by **Graphika Technologies Inc.** and describes a network of domains and subdomains that pushed pro-China messaging while impersonating major outlets (e.g., New York Times, Guardian, Wall Street Journal). The activity has been linked to campaigns such as **HaiEnergy**, **Paperwall**, **DuringBridge**, and **BayBridge**, and overlaps with **Spamouflage**-linked amplification.

## Data dictionary

A **data dictionary(DATA_DICTIONARY.md)** documents the JSON structure: bundle layout, common fields, object types (`identity`, `report`, `attack-pattern`, `domain-name`, `ipv4-addr`, `channel`, `location`, `incident`, `intrusion-set`, `relationship`, etc.), OpenCTI extensions, and ID formats. Use it when parsing, querying, or mapping the STIX bundles.

[DATA_DICTIONARY](https://www.notion.so/DATA_DICTIONARY-306128f3172a804288acd59d55e39956?pvs=21)

## References

- Graphika platform: [Glass Onion report](https://graphika.com/reports/glass-onion)
- [STIX 2.1 specification](https://docs.oasis-open.org/cti/stix/v2.1/stix-v2.1.html)

## Notes

- Data may include **TLP (Traffic Light Protocol)** and handling instructions; follow your organization’s policies when sharing or processing.
- Export timestamp in the report filename: **2026-02-04** (OpenCTI export).
