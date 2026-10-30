# Document Shepherd Write-Up (DRAFT — not yet submitted)

Document: draft-ietf-dmm-udp-tunnel-acaas-extn-03
Title: A YANG Data Model Extension for Attachment Circuit as a Service with UDP Tunnel Support
Shepherd: Satoru Matsushima
Date of this draft write-up: 25 October 2026

Note: items marked [TODO] need the shepherd's own confirmation before this
write-up is entered into the Datatracker.

## Document Announcement Write-Up

### Technical Summary

This document specifies a YANG data model extension that adds a Layer 3
UDP tunnel as a bearer type to the Attachment Circuit as-a-Service
(ACaaS) model defined in RFC 9834. It defines the "ietf-ac-udp-tunnel"
module, which augments the AC service model of RFC 9834 using the common
types of RFC 9833: it defines a new 'udp' identity derived from the
'l3-tunnel-type' base identity of RFC 9833, and augments the Layer 3
tunnel service of an attachment circuit so that a UDP source port number,
or a range of source port numbers, can be specified (reusing the
port-range-or-operator grouping of RFC 8519). A typical use is a UDP
(e.g., GTP-U) bearer in 5G transport networks, where the UDP source port
identifies the bearer at the transport network Provider Edge; an example
is given in Appendix A.

### Working Group Summary

The document is a product of the DMM working group. It was adopted
following a WG call for adoption of draft-jlu-dmm-udp-tunnel-acaas-02
(2 March 2026, ended 16 March 2026), which received support on the
mailing list together with editorial comments (terminology consistency,
definitions in Section 2) that were taken into account; the WG -00 was
approved on 28 March 2026. The work was presented and discussed at WG
sessions, including IETF 124.

A Working Group Last Call on -01 ran from 10 September 2026 to
24 September 2026. Substantive review comments were received on the list
(including from Lionel Morand, Sridhar Bhaskaran, and Carlos J.
Bernardos Cano) and the authors responded on the list. On 28 September
2026 the document was tagged "Revised I-D Needed" to address the WGLC
comments; the -02 (4 October 2026) and -03 (15 October 2026) revisions
address them. [TODO: shepherd to confirm that all WGLC comments are
resolved in -03 and that there is no remaining dissent.] No contributor
has threatened an appeal or otherwise indicated extreme discontent.

### Document Quality

The document is a small, focused extension of the published ACaaS
models (RFC 9833 and RFC 9834) and reuses their types and groupings
rather than defining a parallel model. It received review during the
adoption call and WGLC, including review of the YANG structure:
Mohamed Boucadair reviewed the document, and Lionel Morand helped with
the review and the YANG structures (see the Acknowledgements section of
the document). The Security Considerations follow the template of
RFC 9907 (BCP 216). [TODO: state whether a YANG Doctors early review
was requested/completed, or note that a YANG Doctors review will be
requested at publication request.] [TODO: implementation status — the
document does not include an implementation section; state here whether
any implementations of the model are known.]

### Personnel

Document Shepherd: Satoru Matsushima (also a DMM WG co-chair; not an
author of this document, and no conflict of interest).
Document authors: John Kaippallimalil (Futurewei), Luis M. Contreras
(Telefonica), Uma Chunduri (Intel Corporation).
Responsible Area Director: Charles Eckel

## Shepherd Questionnaire

(1) What type of RFC is being requested?

Proposed Standard (title page: Standards Track; the Datatracker
intended status is Proposed Standard). This is appropriate: the
document specifies a normative YANG module that augments the Proposed
Standard ACaaS service model of RFC 9834, and interoperable
configuration of attachment circuits by different implementations
requires a standards-track data model, consistent with the status of
the base models it extends (RFC 9833, RFC 9834, RFC 8519 are all
Proposed Standard).

(2) Document Announcement Write-Up: provided above.

(3) Briefly describe the review of this document performed by the
Document Shepherd.

[TODO: shepherd to describe own review — suggested text: "The shepherd
reviewed the -01 text during WGLC and the -02/-03 deltas, checked the
YANG module against RFC 9833/RFC 9834, and verified that the WGLC
comments raised on the list were addressed."]

(4) Does the Shepherd have any concerns about the depth or breadth of
the reviews that have been performed?

No. The document was reviewed during the adoption call and during
WGLC, including by reviewers with YANG and ACaaS expertise (the
editor of RFC 9833/9834 among them).
[TODO: adjust if a YANG Doctors review is still outstanding — in that
case state it here and in (14).]

(5) Do portions of the document need review from a particular set of
expertise (e.g., MIB Doctor, YANG Doctor, etc.)?

Yes — the document consists mainly of a YANG module, so YANG Doctor
review is the relevant expert review. The module is a small augment of
existing, recently published models and has already been reviewed by
ACaaS/YANG experts in the WG. [TODO: record the status of any formal
YANG Doctors review request.]

(6) Describe the specific concerns or issues the Document Shepherd has
with this document that the Responsible Area Director and/or the IESG
should be aware of.

None. The WGLC resulted in a "Revised I-D Needed" state; the issues
raised were addressed in -02 and -03. [TODO: confirm.]

(7) Has each author confirmed that any and all appropriate IPR
disclosures required for full conformance with the provisions of BCP 78
and BCP 79 have already been filed? If not, explain why.

[TODO: collect/confirm the authors' IPR confirmations (normally done
in reply to the shepherd's mail before publication request). The
adoption call and WGLC announcements reminded participants of the BCP 79
obligations.]

(8) Has an IPR disclosure been filed that references this document? If
so, summarize any WG discussion and conclusion regarding the IPR
disclosures.

No IPR disclosures referencing this document are known to the shepherd.
[TODO: verify once more in the Datatracker IPR search at submission
time — the shepherd was unable to retrieve the IPR search page while
preparing this draft.]

(9) How solid is the WG consensus behind this document? Does it
represent the strong concurrence of a few individuals, with others
being silent, or does the WG as a whole understand and agree with it?

There is WG consensus to publish (the Datatracker consensus flag is set
to "Yes"). The adoption call and the WGLC both drew explicit support
and detailed comments from multiple participants beyond the authors,
and the comments received have been addressed. The document is a
narrow extension of a model family the WG (and the OPS area) has
already standardised, and no opposition has been recorded.

(10) Has anyone threatened an appeal or otherwise indicated extreme
discontent? If so, summarise the areas of conflict in separate email
messages to the Responsible Area Director.

No.

(11) Identify any ID nits the Document Shepherd has found (see
https://www.ietf.org/tools/idnits/ and the Internet-Drafts Checklist).

idnits 2.17.1 was run on -03 on 25 October 2026. Summary: 1 error,
0 flaws, 4 warnings, 2 comments. The items the authors should fix or
the shepherd should be ready to explain are:
- Error: the document uses an RFC 2119 keyword ("Servers MUST verify
  ..." in the Security Considerations, inherited from the RFC 9907
  template) but contains neither an RFC 2119 reference nor the RFC 2119
  boilerplate. [TODO: ask the authors to add the RFC 2119 boilerplate
  and reference, or confirm the keyword use is acceptable as-is.]
- Warning: unused reference RFC 8792 — it is in fact cited by the
  "NOTE: '\' line wrapping per RFC 8792" marker in Appendix A, but not
  by an explicit [RFC8792] citation in the text.
- Warnings: 11 lines with non-ASCII characters; two lines with unusual
  spacing in the YANG tree diagram (Figure 1).
- Comment: the examples use IPv4 documentation addresses only; idnits
  suggests considering IPv6 examples (Appendix A notes the same
  reasoning applies to IPv6).

(12) Describe how the document meets any required formal expert review
criteria, such as the MIB Doctor, YANG Doctor, media type, and URI
type reviews.

The document defines one YANG module; YANG Doctor review is the
applicable formal review (see (5)). It defines no MIB, media type, or
new URI scheme; the XML namespace URI registration is a standard IANA
registration for YANG modules (see (15)).

(13) Does the document have significant interaction with other IETF
working groups or external organisations?

The base models were produced by OPSAWG/TEAS (RFC 9833, RFC 9834);
this extension is done in DMM because the use case (UDP/GTP-U bearers
in mobile transport networks) sits in DMM's scope, and it has been
reviewed by the ACaaS authors. It references 3GPP TS 29.281 (GTPv1-U)
informatively as the motivating UDP bearer. No formal cross-WG last
call was run. [TODO: shepherd to confirm no additional cross-review
(e.g., OPSAWG/NETMOD) is wanted.]

(14) For Standards Track documents, are all normative references
standards-track or BCP? Check downrefs.

Yes. The normative references are RFC 3688 (BCP 81), RFC 6020,
RFC 8341 (STD 91), RFC 8519, RFC 9833, RFC 9834, and RFC 9907
(BCP 216) — all standards-track or BCP. There are no normative
references to Internet-Drafts and no downrefs. Normative and
informative references are split into separate sections.

(15) IANA Considerations

Complete and clear. IANA is asked to register (i) the URI
urn:ietf:params:xml:ns:yang:ietf-ac-udp-tunnel in the "ns" registry of
the IETF XML Registry, and (ii) the module name "ietf-ac-udp-tunnel"
(prefix ac-udpt) in the "YANG Module Names" registry. These are the
standard registrations for a YANG module document; the registrations
identify the IESG as registrant contact and this document (RFC XXXX)
as the reference.

(16) Describe the implementation status.

[TODO: no implementations are documented in the draft. If none are
known, state: "The shepherd is not aware of implementations of this
specific module; the model augments the ACaaS models of RFC 9834, for
which implementation experience exists. The absence of an
implementation section is not considered a blocker for a YANG service
model extension of this kind."]

(17) Code components and license notice

The YANG module in Section 4 is a code component. It carries the
Revised BSD License text in its description statement, as required by
the IETF Trust Legal Provisions, and is delimited by <CODE BEGINS> /
<CODE ENDS> markers. The module contains a "Note to RFC Editor" asking
for RFC XXXX to be replaced by the assigned RFC number.

## Facts checked while preparing this draft (2026-10-25)
- Datatracker history: replaces draft-jlu-dmm-udp-tunnel-acaas;
  adoption call 2026-03-02 → 2026-03-16; WG -00 approved 2026-03-28;
  -01 2026-07-19; WGLC 2026-09-10 → 2026-09-24; "Revised I-D Needed"
  and state "Waiting for WG Chair Go-Ahead" set 2026-09-28; -02
  2026-10-04; -03 2026-10-15 (current, expires 2027-04-18).
- WGLC list comments: Lionel Morand, Sridhar Bhaskaran,
  Carlos J. Bernardos Cano, plus author responses (mail archive).
- idnits on -03 via author-tools (see item (11)).
- IPR search page could not be retrieved (403); re-verify before
  submission.
