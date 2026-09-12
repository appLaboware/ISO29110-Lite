# ISO29110-Lite — Document Relationships and POP Composition Model v0.1

- ID: `ISO29110L-DOC-RELATIONSHIPS-POP-COMPOSITION`
- Version: `0.1-draft`
- Status: `CANDIDATE_FOR_PO_REVIEW`
- Owner domain: `ISO29110-Lite`

## 1. Purpose

Define a generic model for relationships between controlled documents and actors/entities, and define how POPs compose other POPs without duplicating procedure knowledge.

This document does not impose LaboWare-specific organizational policy. It defines reusable document semantics that adopters may instantiate.

## 2. Document is a governed knowledge object

A controlled document is not only content. It has identity, revision history, authority, relationships, dependencies and notification obligations.

The model MUST keep distinct:

- who owns the document's authoritative content;
- who may edit it;
- who may execute it when it is executable;
- who follows it and must be informed about material changes;
- which documents/procedures depend on it;
- which criticisms/challenges are attached to it.

## 3. Core relationship types

### `OWNER`

The authoritative domain/entity responsible for the meaning of the document.

Ownership is semantic authority, not merely repository write access.

A document SHOULD have exactly one resolved owning domain at a time, although that domain may delegate operational duties.

### `EDITOR`

An actor/entity authorized to propose or perform edits according to the owning domain's governance.

`EDITOR` does not imply `OWNER`.

### `EXECUTOR`

An actor/entity authorized to execute a procedure represented by the document when the execution context satisfies the procedure's policy.

`EXECUTOR` does not imply `EDITOR`, `OWNER` or `FOLLOWER`.

### `FOLLOWER`

An actor, human, project, product, service or other entity that subscribes to material changes in the document.

A follower may care about the document without being authorized to execute or edit it.

### `DEPENDENT`

A document, procedure, configuration, product or other governed object whose validity or behavior depends on the referenced document.

Dependencies support impact propagation when a revision changes.

### `CRITIC` / `CHALLENGER`

An actor/entity that submits a criticism or challenge against the current document or decision.

A challenge becomes governed knowledge linked to the document; it is not permission to create a divergent local version.

## 4. Notification semantics

When a material revision becomes authoritative, the system SHOULD be able to notify or queue notification for:

- followers;
- direct dependents;
- owners of affected dependent documents;
- active executors when the procedure changes materially;
- open critics/challengers when the revision resolves or changes their challenge.

Notification transport is outside this document model. The model only requires that relationships are materialized so a communication subsystem can act on them.

## 5. Execution authorization: role plus context, not only identity

The model SHOULD NOT limit execution authorization to a static list of individual identities.

A static actor list is useful for simple cases, but many procedures are valid only when both the executor and the scenario satisfy conditions.

The recommended generic form is a hybrid of role-based and attribute/context-based authorization:

```text
MAY_EXECUTE =
    authorized_role_or_actor
    AND action_is_permitted
    AND procedure_is_applicable
    AND context_conditions_are_satisfied
```

This follows established access-control engineering:

- RBAC associates permissions with roles rather than directly with every individual;
- ABAC evaluates attributes of subject, object/resource, requested operation and environment/context against policy.

Therefore a POP SHOULD be able to describe both:

- `executor_roles[]` / explicitly authorized actors when needed;
- `execution_conditions[]` describing scenario, environment, state, resource, time, project phase or other relevant constraints.

## 6. Suggested execution-policy structure

```yaml
execution_policy:
  executor_roles:
    - REPOSITORY_ADMIN
  executor_actors: []
  action: CREATE_REPOSITORY
  conditions:
    - organization_access == AUTHORIZED
    - repository_name != EMPTY
    - requested_visibility in ALLOWED_VISIBILITIES
  forbidden_conditions:
    - organization_owner_approval_required_and_missing
```

The exact schema is future work; the semantic separation is normative.

## 7. Why not only RBAC

RBAC is appropriate when authorization depends primarily on organizational role.

It becomes insufficient when the same role may execute a POP only in specific situations.

Example:

```text
Role: DEPLOY_OPERATOR

May execute deployment POP
ONLY IF:
- target environment is approved;
- release gate passed;
- maintenance window is active;
- required evidence exists.
```

That is naturally represented as role + contextual policy.

## 8. POP atomicity

A POP SHOULD be born at the smallest reusable procedure boundary that still has a coherent purpose and verifiable outcome.

An atomic POP:

- has one clear operational objective;
- produces one coherent outcome;
- has explicit preconditions and postconditions;
- can be executed/tested independently when its prerequisites are satisfied;
- does not merely duplicate another POP's instructions.

Atomic does not mean one command or one line. It means one reusable unit of procedure responsibility.

## 9. POP composition

A non-atomic POP SHOULD orchestrate existing POPs instead of copying their steps.

```text
POP-A
  ├── invokes POP-B
  ├── evaluates condition
  ├── invokes POP-C
  └── invokes POP-D
```

The composed POP owns orchestration logic; child POPs own their own procedure logic.

Example:

```text
POP: BOOTSTRAP-GITHUB-PROJECT

1. invoke POP-CREATE-GITHUB-REPOSITORY
2. invoke POP-CONFIGURE-BASELINE
3. invoke POP-INSTALL-REQUIRED-INTEGRATIONS
4. invoke POP-VERIFY-BOOTSTRAP
```

`POP-CREATE-GITHUB-REPOSITORY` is written once and referenced wherever needed.

## 10. POP as executable flow graph

A composed POP MAY be represented as a directed flow graph with nodes such as:

- POP invocation;
- decision/condition;
- parallel branch;
- join;
- wait/gate;
- manual gate;
- evidence collection;
- stop/escalation;
- terminal outcome.

The graph is not required for an atomic POP.

The same procedure must not have contradictory prose and graph authorities. One representation must be canonical or both must be generated/validated from the same source model.

## 11. Composition relations

Suggested relations:

- `invokes`
- `precedes`
- `requires`
- `conditional_on`
- `parallel_with`
- `joins_after`
- `produces`
- `consumes`
- `validates`
- `escalates_to`
- `supersedes`

## 12. Version propagation

A composed POP SHOULD reference child POPs by stable identity plus an adoption/version constraint appropriate to the adopter's governance.

When a child POP changes materially, parent POPs and their owners must be discoverable as dependents.

A revision system SHOULD support at least:

- stable document identity;
- immutable published revisions;
- supersession links;
- dependency links;
- material-change classification;
- impact discovery;
- follower notification.

## 13. Criticism accumulation

Criticisms SHOULD be linked to the authoritative document/revision or to a stable decision represented by it.

The owner receives unresolved criticism and maintains its disposition.

Equivalent prior criticism SHOULD be discoverable before new processing begins.

Possible dispositions include:

- accepted;
- rejected with rationale;
- superseded by later evidence;
- deferred;
- experiment required;
- duplicate/equivalent to existing challenge.

The objective is constructive accumulation of knowledge and reduction of repeated cognitive cost.

## 14. Minimal relationship model

A future machine-readable representation SHOULD be able to express at least:

```text
document_id
revision_id
owner_domain
editors[]
followers[]
execution_policy
parents[]
children[]
dependents[]
dependencies[]
criticisms[]
supersedes
superseded_by
material_change
```

## 15. Scientific / standards basis for execution policy

This model deliberately uses established authorization concepts rather than inventing a procedure-specific permission theory.

References:

- NIST Role-Based Access Control (RBAC): roles receive permissions; users obtain permissions through role assignment. https://csrc.nist.gov/Projects/Role-Based-Access-Control
- NIST SP 800-162, Attribute Based Access Control (ABAC): authorization may evaluate subject, object/resource, operation and environment attributes against policy. https://csrc.nist.gov/pubs/sp/800/162/upd2/final
- NIST SP 800-205, Attribute Considerations for Access Control Systems. https://csrc.nist.gov/pubs/sp/800/205/final

ISO29110-Lite adopts the conceptual separation, not those standards wholesale.

## 16. Final laws

```text
OWNERSHIP DEFINES CONTENT AUTHORITY.
EDIT PERMISSION DOES NOT DEFINE OWNERSHIP.
EXECUTION PERMISSION DOES NOT DEFINE EDIT PERMISSION.
FOLLOWING DOES NOT DEFINE EXECUTION PERMISSION.
```

```text
EXECUTION AUTHORIZATION = ACTOR/ROLE + ACTION + APPLICABLE CONTEXT.
```

```text
WRITE AN ATOMIC POP ONCE.
COMPOSE IT EVERYWHERE.
DO NOT COPY PROCEDURE KNOWLEDGE INTO PARENT POPS.
```

```text
WHEN A CONTROLLED DOCUMENT CHANGES,
ITS FOLLOWERS AND DEPENDENTS MUST BE DISCOVERABLE.
```
