# DATA DICTIONARY

# Data Dictionary — Glass Onion STIX JSON

This document describes the structure and fields of the STIX 2.1 JSON bundles in this folder. The data is exported from **OpenCTI** and follows the [STIX 2.1 specification](https://docs.oasis-open.org/cti/stix/v2.1/stix-v2.1.html), with OpenCTI-specific extensions.

---

## Top-level structure (bundle)

| Field | Type | Description |
| --- | --- | --- |
| `type` | string | Always `"bundle"`. |
| `id` | string | UUID in form `bundle--<uuid>`. Unique identifier for the bundle. |
| `objects` | array | List of STIX objects (identities, reports, domain-names, relationships, etc.). |

---

## Common fields (across most objects)

These appear on many STIX domain objects:

| Field | Type | Description |
| --- | --- | --- |
| `id` | string | STIX identifier, e.g. `domain-name--02c9f73f-3d73-5a66-b3ac-088ac7ffbedf`. |
| `type` | string | Object type (see Object types below). |
| `spec_version` | string | STIX version, e.g. `"2.1"`. |
| `created` | string | ISO 8601 timestamp when the object was created. |
| `modified` | string | ISO 8601 timestamp when the object was last modified. |
| `revoked` | boolean | If `true`, the object is revoked. |
| `confidence` | integer | 0–100 confidence score (OpenCTI/Graphika usage). |
| `x_opencti_id` | string | OpenCTI internal UUID for the entity. |
| `x_opencti_type` | string | OpenCTI entity type (e.g. `"Domain-Name"`, `"Report"`). |

---

## Object types and type-specific fields

### `identity`

Represents an organization, group, or individual (e.g. author, company, person).

| Field | Type | Description |
| --- | --- | --- |
| `identity_class` | string | e.g. `"organization"`, `"individual"`. |
| `name` | string | Display name. |
| `description` | string | Optional description (e.g. “Author or Creator of this Incident/Report…”). |

---

### `report`

High-level report (e.g. “Glass Onion: Peeling Back the Layers…”).

| Field | Type | Description |
| --- | --- | --- |
| `name` | string | Report title. |
| `description` | string | Full narrative / key findings. |
| `published` | string | ISO 8601 publication date. |
| `created_by_ref` | string | `id` of the identity that created the report. |
| `object_refs` | array | List of STIX object `id`s (attack-patterns, domain-names, channels, etc.) referenced by the report. |
| `external_references` | array | e.g. `source_name`, `url` (Graphika platform link). |
| `x_opencti_workflow_id` | string | OpenCTI workflow UUID. |

---

### `attack-pattern`

Tactic or technique. 

| Field | Type | Description |
| --- | --- | --- |
| `name` | string | e.g. “Develop Inauthentic News Articles”, “Bots Amplify via Automated Forwarding and Reposting”. |
| `x_mitre_id` | string | Technique ID (e.g. [T0098.002](https://github.com/DISARMFoundation/DISARMframeworks/blob/main/generated_pages/techniques/T0098.002.md), [T0049.003](https://github.com/DISARMFoundation/DISARMframeworks/blob/main/generated_pages/techniques/T0049.003.md)).  |
| `external_references` | array | `source_name` (e.g. `"disarm"`), `external_id`. |

---

### `domain-name`

Domain or hostname indicator.

| Field | Type | Description |
| --- | --- | --- |
| `value` | string | The domain name (e.g. `"ifengcdn.com"`, `"yzpxxw.gotoip2.com"`). |

---

### `ipv4-addr`

IPv4 address indicator.

| Field | Type | Description |
| --- | --- | --- |
| `value` | string | IPv4 address (e.g. `"101.133.135.41"`). |

In **Glass Onion _ STIX_bundle.json**, `ipv4-addr` objects may appear inside an `extensions` block with extra properties (e.g. `domain_name` array linking the IP to domains).

---

### `channel`

Communication channel (social account, URL).

| Field | Type | Description |
| --- | --- | --- |
| `name` | string | Channel identifier (e.g. `"x.com/PeggyGranata"`, `"facebook.com/profile.php?id=..."`). |
| `channel_types` | array | Optional, e.g. `["Facebook"]`. |

---

### `location`

Geographic or administrative location.

| Field | Type | Description |
| --- | --- | --- |
| `name` | string | e.g. `"CN-HA"`, `"Shenzhen"`. |
| `description` | string | Optional (e.g. “Henan”, “Sichuan”). |
| `city` | string | Optional; used when type is City. |
| `x_opencti_location_type` | string | OpenCTI type: e.g. `"Administrative-Area"`, `"City"`. |

---

### `incident`

A security or influence incident.

| Field | Type | Description |
| --- | --- | --- |
| `name` | string | e.g. “Spamouflage Amplify Articles Targeting Shen Yun and Falun Gong”. |
| `created` | string | ISO 8601 date. |
| `created_by_ref` | string | `id` of the creating identity. |

Some incidents may have an `extensions` object (e.g. OpenCTI toplevel-property-extension).

---

### `intrusion-set`

Named grouped set of adversarial behaviors and resources with common properties. 

| Field | Type | Description |
| --- | --- | --- |
| `name` | string | e.g. `"Spamouflage"`. |

---

### `relationship`

Links two STIX objects.

| Field | Type | Description |
| --- | --- | --- |
| `relationship_type` | string | e.g. `"related-to"`, `"located-at"`. |
| `source_ref` | string | `id` of the source object. |
| `target_ref` | string | `id` of the target object. |
| `lang` | string | Optional language (e.g. `"en"`). |
| `start_time` | string | ISO 8601 date of observed start of relationship |

---

### `media-content`

STIX 2.1 object for a piece of media (e.g. article, post) referenced in the report.

| Field | Type | Description |
| --- | --- | --- |
| (varies) | — | Structure follows STIX 2.1 media-content; may include URLs, content references. |
| `url` | string | URL hosting content |
| `content` | string | Content in article or at other URL |
| `publication_date` | string | ISO 8601 date |
| `x_opencti_created_by_ref` | string | `id` of the creating identity. |

---

### `narrative`

Structured narrative or storyline object (STIX 2.1)

| Field | Type | Description |
| --- | --- | --- |
| `name` | string | Descriptive name for narrative |

---

### `threat-actor`

Knowned threat actor or actor group (STIX 2.1)

| Field | Type | Description |
| --- | --- | --- |
| `name` | string | Name for threat actor |
| `threat_actor_group` | string | Name for group of actors |

---

## File-specific notes

- **Glass_Onion_STIX_bundle_OpenCTI_Export.json**: Pretty-printed; contains the main report plus identities, attack-patterns, domain-names, channels, locations, incidents, intrusion-sets, ipv4-addrs, relationships, media-content, and narratives. No custom extensions on observables in this file.
- **Glass_Onion_STIX_bundle.json**: Single-line bundle; includes incidents and ipv4-addr with **extensions** that add a `domain_name` array to IP objects. Same STIX 2.1 + OpenCTI conventions otherwise.

For the authoritative STIX 2.1 schema, see [OASIS CTI TC](https://docs.oasis-open.org/cti/stix/v2.1/stix-v2.1.html).
