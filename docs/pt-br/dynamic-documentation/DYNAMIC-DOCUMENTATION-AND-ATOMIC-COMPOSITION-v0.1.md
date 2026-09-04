# ISO29110-Lite — Dynamic Documentation and Atomic Composition v0.1

- ID: `ISO29110L-DYNAMIC-DOCUMENTATION`
- Version: `0.1-draft`
- Status: `DOGFOODING`
- Owner domain: `ISO29110-Lite`

## 1. Purpose

Define a generic document model in which documentation is composed dynamically from authoritative atomic sources rather than maintained primarily as disconnected static prose.

This proposal is product-domain material for ISO29110-Lite and is intentionally independent from any single consumer such as FlowED.

## 2. Core law

```text
AUTHORITATIVE ATOMS
  ↓
COMPOSITION
  ↓
AUDIENCE-SPECIFIC PROJECTION
```

Documentation is a projection of controlled knowledge.

## 3. Language-neutral source documentation concept

The generic concept adopted by this model is **Source Documentation System**: a language-level convention for machine-readable or machine-extractable documentation attached to source elements, plus a **Source Documentation Generator** that projects those annotations into structured API/reference documentation.

Common language-specific realizations include documentation comments/doc comments, docstrings and Javadoc-style annotations. `Javadoc` is therefore one adapter/realization of the generic concept, not the generic concept itself.

Every programming language used by a conforming product SHOULD have an adapter capable of producing the canonical source-documentation model.

```text
LANGUAGE SOURCE
   ↓
LANGUAGE DOCUMENTATION ADAPTER
   ↓
CANONICAL SOURCE DOCUMENTATION MODEL
   ↓
ATOMIC DOCUMENTATION
   ↓
DYNAMIC PROJECTIONS
```

If a language already has a mature native or ecosystem mechanism, adopt or adapt it. If no adequate mechanism exists — including scripting/batch languages or constrained DSLs — the ecosystem MAY create a generic or language-specific adapter/tool. External market demand is not a prerequisite: internal architectural necessity is sufficient justification after the normal discovery/residual process.

## 4. Source hierarchy

A software documentation pipeline MAY use:

```text
SOURCE CODE
  ↓
SOURCE DOCUMENTATION SYSTEM
  + STRUCTURED AI-FIRST SEMANTIC ANNOTATIONS
  ↓
ATOMIC DOCUMENTATION NODES
  ↓
DEVELOPER DOCUMENTATION
  ↓
USER DOCUMENTATION
  ↓
PRODUCT / PROJECT DOCUMENTATION
```

## 5. AI-first semantic annotations

The model SHOULD support structured metadata that lets an AI or deterministic documentation tool resolve intent without first re-analyzing the full implementation.

Candidate fields:

- `purpose`
- `inputs`
- `outputs`
- `side_effects`
- `preconditions`
- `postconditions`
- `invariants`
- `errors`
- `dependencies`
- `domain_terms`
- `decision_refs`
- `evidence_refs`
- `doc_atom_refs`

The annotation is not permitted to become an unverified parallel truth source.

Where possible, validators MUST compare it with signatures, contracts, tests or generated metadata.

## 6. Documentation atom

A documentation atom is the smallest independently addressable unit of controlled documentation.

Each atom SHOULD include:

- stable ID;
- revision;
- owner;
- subject;
- intended audiences;
- authoritative source refs;
- dependencies;
- composition parents;
- evidence refs;
- status;
- integrity/provenance metadata.

## 7. Composition

Larger documents are graphs/compositions of atoms.

An atom may participate in multiple projections without being copied semantically.

Example:

```text
FUNCTION ATOM
   ├── DEVELOPER GUIDE
   ├── API REFERENCE
   └── USER WORKFLOW
```

Audience-specific prose may be generated while preserving lineage to the same source atom.

## 8. Dynamic materialization

When a documentation view is requested, the preferred behavior is:

```text
RESOLVE requested view
→ load authoritative atoms
→ validate revisions/dependencies
→ compose required graph
→ apply audience/profile projection
→ generate output
→ record provenance
```

Static generated artifacts are caches/projections, not the primary authority, unless explicitly promoted as controlled snapshots.

## 9. Controlled snapshots

Dynamic generation does not eliminate historical reproducibility.

A released or contractual document MAY be materialized as an immutable snapshot containing:

- source atom revisions;
- composition graph revision;
- generator/profile version;
- timestamp;
- integrity hash;
- provenance.

This allows the current documentation to evolve while prior released states remain reconstructable.

## 10. Relations with controlled-document actors

A controlled document or atom MAY define:

- `OWNER`
- `EDITOR`
- `EXECUTOR` when procedural;
- `FOLLOWER`
- `DEPENDENT`
- `CRITIC/CHALLENGER`

Changes SHOULD notify or invalidate dependent projections according to policy.

## 11. Dependency propagation

When an atom changes:

```text
ATOM CHANGE
   ↓
IDENTIFY DEPENDENTS
   ↓
MARK AFFECTED PROJECTIONS
   ↓
REVALIDATE / REGENERATE
   ↓
NOTIFY FOLLOWERS / OWNERS AS REQUIRED
```

The system SHOULD support transitive traversal.

## 12. POP composition

Procedures follow the same atomic-composition principle.

```text
ATOMIC POP
   ↓
reused by
COMPOSITE POP / WORKFLOW
   ↓
reused by
HIGHER-LEVEL PROCESS
```

A POP is atomic when decomposing it further would no longer produce independently meaningful executable procedures under the chosen abstraction level.

Composite POPs SHOULD reference child POPs instead of duplicating their instructions.

## 13. Queryability

The documentation model SHOULD enable questions such as:

- what source generated this paragraph/section?
- which functions contribute to this developer guide?
- which user documentation depends on this API atom?
- which documents must be regenerated after this change?
- which projects consume this controlled procedure?
- who owns, edits, executes, follows or challenges this document?
- which source-documentation adapter generated this atom?
- which language has no adequate documentation adapter yet?

## 14. External lineage and compliance projection

A documentation projection MAY display inspirations, dependencies, compliance and external-origin chains supplied by consuming governance systems.

ISO29110-Lite defines how such data can be represented/composed; the consuming product/domain remains owner of the actual adoption and compliance decisions.

## 15. Standards caution

ISO/IEC 29110 itself defines lifecycle profiles and guidance for very small entities, including process, task, role and work-product concepts. This proposal does not claim that the dynamic atom model above is prescribed by the external ISO/IEC 29110 standard.

It is an ISO29110-Lite product evolution inspired by the objective of practical, lightweight, controlled lifecycle information.

## 16. Final law

```text
WRITE KNOWLEDGE ONCE.
ADDRESS IT ATOMICALLY.
COMPOSE IT MANY WAYS.
GENERATE VIEWS ON DEMAND.
PRESERVE PROVENANCE.
REBUILD WHEN SOURCES CHANGE.
NORMALIZE LANGUAGE-SPECIFIC DOCUMENTATION THROUGH ADAPTERS.
NEVER FORCE CONSUMERS TO MAINTAIN DUPLICATED KNOWLEDGE.
```
