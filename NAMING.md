# Repository Naming Convention

This document defines repository naming rules used across the Muavr GitHub organization.

Naming is treated as part of system architecture.
The goal is long-term clarity, semantic separation, and visual consistency.

---

## 1. General Principles

1. Each repository name must belong to exactly one layer.
2. Different layers use different vocabularies.
3. Naming reflects responsibility and lifecycle, not popularity or activity.
4. Repository names must be stable and must not depend on external state.
5. Once a repository leaves responsibility, it does not return to an active naming scheme.

---

## 2. Infrastructure Layer (Norse Mythology)

Used **only** for infrastructure, clusters, and system topology.

### 2.1 Root / Bootstrap

- `yggdrassil`  
  Root infrastructure repository.  
  Contains bootstrap logic, GitOps foundations, and base infrastructure.

---

### 2.2 Realms (Desired System States)

Prefix: `realm-`

A realm defines **what should be running**, not where.
Environments are expressed as desired states, not physical clusters.

Examples:
- `realm-asgard` (staging)
- `realm-midgard` (production)
- `realm-utgard` (labs)

---

### 2.3 Packs (Physical Clusters)

Prefix: `pack-`

A pack represents a **physical Kubernetes cluster**.
Each pack subscribes to exactly one realm.

Examples:
- `pack-fenrir`
- `pack-hati`
- `pack-amarok`

---

## 3. Product Layer (Latin / Archaic Codenames)

Used for applications and products.

Rules:
- One Latin (or archaic) codename per product
- Codenames are internal and not brand names
- Meaning is associative rather than descriptive
- Codenames must not encode architecture or implementation

Examples:
- `sententia`
- `scriptorium`
- `manifestum`

Branding, domains, and marketing names are intentionally decoupled from repository naming.

---

## 4. Role Naming Rule (Product Decomposition)

When a product is split into multiple repositories, **roles** are used instead of
technical clichés such as `frontend` or `backend`.

Roles describe **system responsibility**, not implementation details.

### 4.1 Canonical Roles

The following roles are defined and preferred:

- `kernel`  
  The execution and decision core of the system.  
  Contains business logic, APIs, and processing.

- `view`  
  The presentation layer.  
  Responsible for rendering, interaction, and user-facing behavior.

- `surface`  
  The visual shell of the system.  
  Contains design system artifacts such as visual language, tokens, and assets.

### 4.2 Usage Rules

- Roles are appended to the product codename using a hyphen.
- A monolithic product uses only the codename.
- Roles are optional and used only when separation is required.

Examples:
- `sententia-kernel`
- `sententia-view`
- `sententia-surface`

This rule is product-agnostic and applies equally to all products.

---

## 5. Integration and Domain Modules

This section defines naming rules for microservices and domain modules within a product.

### 5.1 Goal

Module names must remain stylistically consistent with the organization naming system:

- product codenames remain stable and associative
- module names describe **domain responsibility**, not external systems or technologies
- names must remain readable and stable over time

### 5.2 General Pattern

`<product>-<module>`

Where:
- `<product>` is the product codename (for example, `sententia`)
- `<module>` is a single-word noun describing the module’s domain role

Examples:
- `sententia-identity`
- `sententia-records`
- `sententia-render`

### 5.3 Module Naming Rules

1. **Use nouns only**  
   Module suffixes must be single-word nouns.  
   Verb forms and action-based names are not allowed.

2. **Do not use external system names**  
   Names of third-party services, government systems, vendors, or acronyms must not be used.  
   Examples to avoid: `esia`, `gosuslugi`, `pdf`.

3. **Do not encode technology or formats**  
   Module names must not depend on protocols, formats, libraries, or storage choices.  
   Names must survive implementation changes.

4. **Prefer domain responsibility over process**  
   Name the stable domain concept, not a temporary action.  
   For example, prefer `records` over “convocation” or “meeting”, and `render` over “printer”.

5. **Keep names short and stable**  
   Use lowercase `kebab-case`.  
   Avoid multi-word suffixes.

6. **Separate product roles from domain modules**  
   - Product roles use predefined role suffixes (`-kernel`, `-view`, `-surface`).
   - Domain modules use domain nouns (for example, `identity`, `records`, `estate`).

### 5.4 Repository Boundary Guidance

A module should have its own repository only if at least one of the following is true:

- it is deployed independently
- it has its own lifecycle or versioning
- it is reused across multiple products

Otherwise, it should remain an internal module or package within the main product repository, typically the kernel.

---

## 6. Library Layer

Used for shared utility libraries.

Rules:
- Library names must end with `x`
- Names must be short, technical, and non-architectural
- Libraries must not imply platform or foundation status

Examples:
- `uuidx`
- `nanx`
- `larax`

---

## 7. Archived Repositories

Archived repositories use GitHub’s built-in **Archive** status.

Rules:
- No renaming is required when archiving
- Archived repositories are permanently out of responsibility
- Archived repositories must not be reactivated under the same name

Lifecycle state is expressed through GitHub metadata, not naming.

---

## 8. Explicit Non-Rules

- Repository names do not need to match brand names
- Repository names do not describe technology stacks
- Repository names do not imply support level or activity

Naming is structural, not marketing-driven.

---

## 9. Summary

- Norse mythology — infrastructure topology
- Latin or archaic codenames — products
- Roles (`kernel`, `view`, `surface`) — product decomposition
- Domain nouns — integrations and domain modules
- `x` suffix — libraries
- GitHub archive state — lifecycle end

If a repository name does not clearly fit one category,
it is incorrectly named.
