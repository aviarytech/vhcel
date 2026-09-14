# Initial import notes

The source is the specification in the
[shared conversation](https://chatgpt.com/share/6aa6418d-191c-83e8-99c0-48a4112da4b4),
including the completed security section. The presentation preceding it and the
conversational closing text were omitted. The content of all 30 original
specification sections was retained; an alignment appendix and generated issue
summary were added.

The following editorial changes are proposals for review, not decisions already
agreed in the source conversation:

- Qualified integrity claims: a valid chain does not prove freshness, uniqueness,
  the absence of hidden forks, or the intended identity without an expected commitment.
- Expanded verification to calculate every event ID, compare supplied IDs, check
  genesis proofs and policy, validate required external data, enforce deactivation,
  and commit state only after required checks pass.
- Made prior-state authorization mandatory for successors while preserving the
  possibility that a prior commitment authorizes a newly revealed rotation key.
- Required witness profiles to specify policy activation and handover, count
  distinct witnesses, and keep witnessing separate from controller authorization.
- Required authenticated checkpoints to bind the state and policy needed to
  resume verification; clarified the limits of checkpoint-based verification.
- Distinguished missing required external data from successful state verification.
- Required rejection of duplicate JSON member names used in cryptographic processing.
- Clarified that colluding witnesses cannot make an event pass otherwise failing
  integrity, authorization, or state-transition checks.
- Marked DID integration as a proposed application of the model. Field conversion
  does not preserve the original cryptographic identifiers or signatures by itself.
- Marked examples as conceptual and unresolved protocol choices as ReSpec issues.

The CEL and did:webvh specifications are informative alignment references.
A normative binding, mandatory algorithms, proof suite, concrete application
profile, and cryptographic test vectors remain to be written.

## CEL presentation alignment

At the editor's request, the document now follows CEL's chapter structure:
Introduction (including goals, terminology, and conformance), Data Model,
Serializations, Algorithms, and Application Specifications, followed by security,
privacy, and appendices. Existing anchors are preserved as sections or definition
list entries. The longer abstract explanation moved into the introduction.

Property tables, compact definition lists, labeled examples, a versioned short
title, code styling, and hierarchical algorithm numbering follow CEL's presentation
conventions. These are presentation changes; the CEL binding remains an open issue.

## Log comparisons

Added separate informative comparisons against did:webvh v1.0 and CEL v0.1,
reviewed on 13 September 2026. Each includes a field-and-behavior table and paired
schematic examples. The comparisons distinguish current-entry identity from
predecessor linkage, controller proofs from witness receipts, and storage chunking
from checkpoint trust. Proposed VHCEL mappings are explicitly not wire bindings
or cryptographically valid conversion examples.

## Required SCID and current-event identifiers (superseded)

The editor selected mandatory SCIDs for all VHCEL histories and the did:webvh
current-event identifier model. This supersedes the imported draft's optional
SCID and explicit `previousEvent` model. Genesis carries the SCID; each event
carries its own identifier. The hash-input seed is the SCID for genesis and the
preceding verified event ID for successors. Examples use the provisional names
`scid` and `eventId`; field names and cryptographic encoding are not finalized.

Verification now requires recomputing the genesis SCID, checking every event's
own identifier, retaining the same SCID throughout the history, and returning
the SCID in results. Checkpoints bind the SCID. A caller-supplied expected SCID
is still distinguished from a self-consistent SCID obtained with the history.
Both comparisons reflect the selected direction. Exact placeholder processing,
protected fields, proof coverage, and the common derivation algorithm remain open.

## Mandatory SCID with CEL predecessor linkage

The editor retained mandatory SCIDs and restored CEL-style `previousEvent`
linkage. This supersedes the current-event identifier and seed-substitution
choice above: mandatory SCIDs do not require that construction.

Genesis carries the SCID and has no `previousEvent`. Each successor references
the calculated digest of the completed preceding event. A stored `eventId` is
not required. Verification computes event digests, checks predecessor references,
and validates required proofs and trusted commitments, including for the final
supplied event. Computing a digest alone does not authenticate it.

Updated terminology, conformance, the data model, genesis and verification
algorithms, examples, and both log comparisons. The mandatory SCID, expected-SCID
checks, and checkpoint binding remain. Exact genesis self-reference processing,
SCID placement, event hashing, and proof coverage remain binding decisions.

## Pros and cons of related log formats

Replaced the field-by-field comparison tables and paired sketches with pros
and cons for did:webvh and CEL as foundations for VHCEL. Each assessment states
what the approach contributes and what adaptation or profile work remains.
The existing comparison section anchors are preserved. The assessments are
informative and do not change the event model or claim wire compatibility.

## Design choices carried forward

Reframed the related-format sections around what VHCEL takes from did:webvh
and CEL, what it leaves outside the core or changes, and what remains undecided.
This replaces the pros-and-cons assessment with an account of the current
design. Deferred choices such as the CEL envelope, proof suite, and digest
encoding are explicitly distinguished from rejected choices. No normative
processing requirements changed.
