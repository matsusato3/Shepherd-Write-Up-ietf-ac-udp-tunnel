# Document Shepherd Write-Up for Working Group Documents (DRAFT — not yet submitted)

Document: draft-ietf-dmm-udp-tunnel-acaas-extn-03
Title: A YANG Data Model Extension for Attachment Circuit as a Service with UDP Tunnel Support
Shepherd: Satoru Matsushima
Responsible Area Director: Charles Eckel
Date of this draft write-up: 3 November 2026
Format: version dated 9 October 2026

Note: this draft uses the shepherd write-up format dated 9 October 2026.
The explanatory text of that template has been removed, as the template
instructs. Items marked [TODO] need the shepherd's own confirmation
before this write-up is entered into the Datatracker.

For context: this document specifies a YANG data model extension that
adds a Layer 3 UDP tunnel as a bearer type to the Attachment Circuit
as-a-Service (ACaaS) model defined in RFC 9834. It defines the
"ietf-ac-udp-tunnel" module, which augments the AC service model of
RFC 9834 using the common types of RFC 9833, defines a new 'udp'
identity derived from the 'l3-tunnel-type' base identity of RFC 9833,
and allows a UDP source port number, or a range of source port numbers,
to be specified (reusing the port-range-or-operator grouping of
RFC 8519). A typical use is a UDP (e.g., GTP-U) bearer in 5G transport
networks, where the UDP source port identifies the bearer at the
transport network Provider Edge; an example is given in Appendix A of
the document.

## Document History & Implementations

1. Have the Chairs confirmed Working Group (WG) consensus for this
   document? Did they indicate any issues to be called out with regard
   to that rough consensus? If so, what were they? Please supply any
   additional information about the quality of the WG consensus from
   the Shepherd's view.

   Yes. The chairs have confirmed WG consensus for this document,
   and they did not indicate any issues to be called out with regard
   to that rough consensus.

   From the shepherd's view, there is WG consensus to publish (the
   Datatracker consensus flag is set to "Yes"). The document was
   adopted following a WG call for adoption of
   draft-jlu-dmm-udp-tunnel-acaas-02 (2 March 2026, ended 16 March
   2026), which received support on the mailing list together with
   editorial comments (terminology consistency, definitions in
   Section 2) that were taken into account; the WG -00 was approved on
   28 March 2026. The work was presented and discussed at WG sessions,
   including IETF 124. A Working Group Last Call on -01 ran from
   10 September 2026 to 24 September 2026 and drew explicit support
   and substantive review comments from multiple participants beyond
   the authors (including Lionel Morand, Sridhar Bhaskaran, and
   Carlos J. Bernardos Cano), to which the authors responded on the
   list. On 28 September 2026 the document was tagged "Revised I-D
   Needed" to address the WGLC comments; the -02 (4 October 2026) and
   -03 (15 October 2026) revisions address them. No opposition has
   been recorded. The document is a narrow extension of a model
   family the WG (and the OPS area) has already standardised, so the
   consensus is the concurrence of the interested participants, with
   others silent, rather than a broad re-litigation of the approach.
   All WGLC comments are considered resolved in -03, and there is no
   remaining dissent.

2. Indicate any significant disagreement in the WG about whether or
   not this document falls within the current charter.

   None known. The extension is done in DMM because the use case
   (UDP/GTP-U bearers in mobile transport networks) sits in DMM's
   scope, even though the base models were produced by OPSAWG/TEAS
   (RFC 9833, RFC 9834). No significant disagreement about charter
   fit was raised during the adoption call or the WGLC.

3. If anyone threatened an appeal or otherwise indicated extreme
   discontent, please summarize the areas of conflict in separate
   email messages to the responsible Area Director.

   No. No contributor has threatened an appeal or otherwise indicated
   extreme discontent, so no separate email is needed.

4. For protocol documents, indicate whether the document adheres to
   the WG implementation policy (if any). Also, indicate whether
   there are existing (or planned) implementations and, if so, where
   they are listed (RFC 7942 recommends they be reported in the
   document itself).

   The DMM WG has no specific implementation policy applicable to
   this document known to the shepherd. The document does not include
   an Implementation Status section, and no implementations are
   listed in it. At this time, no implementations of the
   "ietf-ac-udp-tunnel" module have been observed, and no
   implementation report has been received from the authors. The
   model augments the ACaaS models of RFC 9834, for which
   implementation experience exists, and the absence of an
   implementation section is not considered a blocker for a YANG
   service model extension of this kind.

## Additional Reviews

5. Have reviews for the document happened in other IETF WGs or
   external organizations that you are aware of? If so, please
   provide references to those reviews (if any).

   No formal review in another IETF WG or in an external organization
   is known. The document was reviewed within DMM during the adoption
   call and the WGLC, including by ACaaS/YANG experts: Mohamed
   Boucadair (editor of RFC 9833/RFC 9834) reviewed the document, and
   Lionel Morand helped with the review and the YANG structures (see
   the Acknowledgements section of the document). No formal cross-WG
   last call was run.

6. Describe the results of formal expert reviews (e.g., media type,
   URI) that the document has undergone. Also, indicate whether any
   of the required reviews are missing.

   The applicable formal expert review is the YANG Doctors review,
   because the document consists mainly of a YANG module. [TODO:
   record the status of the YANG Doctors review. No completed YANG
   Doctors review of a recent version is recorded in this draft; if
   none has been done, it is the one required review still missing,
   to be requested at publication request.] The document defines no
   MIB, media type, or new URI scheme; the XML namespace URI and YANG
   module name registrations are standard IANA registrations for a
   YANG module document (see item 22), so no separate media type or
   URI expert review applies.

7. If the document contains a YANG module, does the document's
   Datatracker page indicate that it has no errors and warnings? Has
   a YANGDOCTOR review been done on a recent version, indicating that
   it is ready for publication? Does the document use the various
   templates in RFC 9907 (mainly, YANG module, Security, and IANA
   templates)?

   Yes to the validation point: when -03 was posted on 15 October
   2026, the author reported to the DMM list that the YANG model had
   been verified as up to date, with YANG validation showing 0 errors
   and 0 warnings (message archived at
   https://mailarchive.ietf.org/arch/msg/dmm/ubzIOea3A89UEIYiDlMst5p-LRc/).
   YANG Doctors review: see item 6 — [TODO: status to be recorded;
   not recorded as completed in this draft.] On templates: yes, in
   substance. The Security Considerations state that the section is
   modelled after the template described in Section 3.7 of RFC 9907;
   the YANG module carries the Revised BSD License text in its
   description statement and is delimited by <CODE BEGINS> /
   <CODE ENDS> markers, with a "Note to RFC Editor" asking for
   RFC XXXX to be replaced by the assigned RFC number; and the IANA
   Considerations follow the standard registration format for YANG
   modules (see item 22).

8. Describe all reviews and automated checks performed to validate
   sections of the document written in a formal language, such as
   XML, JSON code, ABNF/RBNF/BNF rules, ASN.1, CBOR CDDL, etc.

   The only formal language in the document is YANG (the
   "ietf-ac-udp-tunnel" module in Section 4), together with the YANG
   tree diagram (per RFC 8340) in Section 3 and JSON examples in
   Appendix A. Checks performed: YANG validation of the module with
   0 errors and 0 warnings (see item 7); WG review of the YANG
   structure, including by the reviewers named in item 5; and idnits
   2.17.1 run on -03 on 25 October 2026 (see item 17).
   [TODO: shepherd to describe own review — suggested text: "The
   shepherd reviewed the -01 text during WGLC and the -02/-03 deltas,
   checked the YANG module against RFC 9833/RFC 9834, and verified
   that the WGLC comments raised on the list were addressed."] There
   are no ABNF, ASN.1, or CDDL sections.

9. Does the document describe any protocol elements that are intended
   for human interpretation and understanding? If so, does the
   document contain an Internationalization Considerations section
   that describes how those protocol elements are suitable for
   international use?

   N/A. The document defines YANG configuration data nodes (a UDP
   source port number or range). It defines no protocol elements
   intended for human interpretation, and the -03 text contains no
   Internationalization Considerations section; none is needed.

## Document Shepherd Checks

10. Confirm that (in your opinion) this document is clearly written,
    complete, technically accurate, correctly designed, and ready to
    be handed off to the responsible Area Director.

    In the shepherd's opinion the document is clearly written,
    complete, technically accurate, and correctly designed as a
    small augment of the RFC 9834 ACaaS model, and is ready to be
    handed off to the Responsible Area Director, subject to
    resolving the BCP 14 boilerplate point in item 14.

11. Several IETF Areas have assembled lists of common issues that
    their reviewers encounter. Have such issues been identified and
    addressed? For which areas are subsequent reviews believed
    particularly important to happen?

    No area common-issue items have been identified for this document
    beyond the YANG-specific points covered in items 6, 7, and 14.
    Subsequent review believed particularly important: the YANG
    Doctors review (OPS area), because the document is primarily a
    YANG module. The usual IESG-stage security review of a YANG
    module also applies; the Security Considerations already follow
    the RFC 9907 template (see item 7).

12. What type of RFC publication is being requested? Why is this the
    appropriate type of RFC?

    Proposed Standard (title page: Standards Track; the Datatracker
    intended status is Proposed Standard). This is appropriate: the
    document specifies a normative YANG module that augments the
    Proposed Standard ACaaS service model of RFC 9834, and
    interoperable configuration of attachment circuits by different
    implementations requires a standards-track data model, consistent
    with the status of the base models it extends (RFC 9833,
    RFC 9834, RFC 8519 are all Proposed Standard).

13. Will publication of this document change the status of any
    existing RFC(s)? If so, does the Datatracker status page for this
    document correctly list those RFCs on the Title page, in the
    Abstract, and in the Introduction of the document?

    No. Publication will not change the status of any existing RFC.
    The document extends the RFC 9834 model by YANG augmentation,
    which is not an "Updates" relationship; consistently, the -03
    title page carries no Updates or Obsoletes header (checked
    against the -03 text on 3 November 2026), and the Abstract and
    Introduction describe the work as an extension of RFC 9834.

14. If the document uses BCP 14 key words, does the document follow
    the guidance in the IESG Statement on Clarifying the Use of
    BCP 14 Key Words? Is there any use of the BCP 14 key words that
    could be considered unclear or inappropriate? Please flag those.

    Flagged: the only uppercase BCP 14 keyword in -03 is "MUST" in
    "Servers MUST verify ..." in the Security Considerations, a
    sentence inherited from the RFC 9907 (Section 3.7) security
    template (checked against the -03 text on 3 November 2026). The
    document contains neither a BCP 14 / RFC 2119 reference nor the
    RFC 2119 boilerplate, which is also the single error reported by
    idnits (see item 17). The keyword use itself is clear and
    appropriate in context — it states an access-control obligation
    for management servers — but the missing boilerplate and
    reference should be fixed, or explicitly confirmed as acceptable.
    [TODO: authors to add the RFC 2119 boilerplate and reference in a
    next revision, or confirm the keyword use is acceptable as-is;
    this is one of the three questions in the drafted, not yet sent,
    confirmation mail to the authors.] No other unclear or
    inappropriate BCP 14 use was identified.

15. Confirm that reasonable efforts have been made to remind the WG
    (including the document authors, editors, and contributors) about
    the intellectual property rights (IPR) disclosure obligations
    described in BCP 79. Please summarize any relevant discussion.

    The adoption call and WGLC announcements reminded participants of
    the BCP 79 obligations, and the document itself is submitted in
    full conformance with BCP 78 and BCP 79. In their replies to the
    WGLC announcement on the DMM mailing list (22 September 2026),
    two of the three authors confirmed that they are not aware of any
    IPR applicable to this document: Uma Chunduri stated "Not aware
    of any IPRs on this document", and Luis M. Contreras stated that
    he was "not being aware of any IPR applicable to it". [TODO:
    obtain the same confirmation from the remaining author, John
    Kaippallimalil, whose WGLC reply expressed support but did not
    address IPR.] No IPR disclosures have been filed referencing
    this document: the shepherd verified this in the Datatracker
    IPR search on 3 November 2026, which returned no disclosures
    for the document. No other IPR discussion has taken place on
    the list.

16. Confirm that each author, editor, and contributor has shown their
    willingness to be listed as such. If the total number of authors
    and editors on the front page is greater than five, please
    provide a justification.

    The front page lists three authors — John Kaippallimalil
    (Futurewei), Luis M. Contreras (Telefonica), and Uma Chunduri
    (Intel Corporation) — so the total is not greater than five and
    no justification is needed. Their willingness to be listed is
    shown by their continued authorship through -03, including
    posting revisions and responding to WGLC comments on the list.
    Contributors (Mohamed Boucadair, Lionel Morand, and others) are
    thanked in the Acknowledgements and are not listed as authors.
    A separate explicit confirmation from each author was not sought:
    with three authors, this item requires no justification, and no
    further confirmation is needed (N/A).

17. Please list any remaining I-D nits in the version of the document
    you reviewed that you feel are actual errors.

    idnits 2.17.1 was run on -03 on 25 October 2026. Summary: 1 error,
    0 flaws, 4 warnings, 2 comments.

    The one item the shepherd considers an actual error is the error
    already described in item 14: the document uses an RFC 2119
    keyword but contains neither an RFC 2119 reference nor the
    RFC 2119 boilerplate.

    The remaining idnits output is not considered actual errors:
    - Warning, unused reference RFC 8792: it is in fact used by the
      "NOTE: '\' line wrapping per RFC 8792" marker in Appendix A,
      but is not cited by an explicit [RFC8792] citation in the text.
    - Warnings, 11 lines with non-ASCII characters and two lines with
      unusual spacing in the YANG tree diagram (Figure 1):
      presentational, not content errors.
    - Comment, the examples use IPv4 documentation addresses only and
      IPv6 examples might be considered: Appendix A already notes the
      example is adapted from Appendix A.7 of RFC 9834, uses IPv4
      addresses, and that the same reasoning applies to IPv6, so this
      is addressed by explanation.

## Document References

18. List any informative references that should be normative or
    vice-versa.

    None identified. Normative and informative references are split
    into separate sections and the classification was checked: the
    normative references are the RFCs the module imports from or
    depends on (see item 20), while, e.g., 3GPP TS 29.281 (GTPv1-U)
    and RFC 8085 (UDP Usage Guidelines) are correctly informative —
    they motivate and inform the design but are not required to
    implement the module.

19. List any normative references that are not freely available to
    anyone. Does the community have sufficient access to review these
    references?

    None. All normative references are RFCs, which are freely
    available to anyone.

20. List any normative downward references (see RFC 3967 and BCP 97)
    that are not already listed in the DOWNREF registry.

    None. The normative references are RFC 3688 (BCP 81), RFC 6020,
    RFC 8341 (STD 91), RFC 8519, RFC 9833, RFC 9834, and RFC 9907
    (BCP 216) — all standards-track or BCP. There are no normative
    references to Internet-Drafts and no downrefs.

21. List any normative references to documents that are not ready to
    be submitted to the IESG for publication or are otherwise in an
    unclear state. For each, indicate the plan for their completion,
    if known.

    None. All normative references are published RFCs (see item 20).

## IANA Considerations

22. Describe your review of the IANA considerations section,
    especially its consistency with the body of the document. Confirm
    that all IANA requested actions are associated with the
    appropriate reservations in IANA registries. Confirm that any
    referenced IANA registries have been clearly identified. Confirm
    that each newly created IANA registry specifies its initial
    contents, allocation procedures, and a reasonable name (see
    RFC 8126).

    Reviewed and found complete, clear, and consistent with the body
    of the document (the module name, namespace, and prefix in the
    IANA section match Section 4). IANA is asked to register (i) the
    URI urn:ietf:params:xml:ns:yang:ietf-ac-udp-tunnel in the "ns"
    registry of the IETF XML Registry [RFC 3688], and (ii) the module
    name "ietf-ac-udp-tunnel" (prefix ac-udpt) in the "YANG Module
    Names" registry within the YANG parameters registry group
    [RFC 6020]. Both registries are clearly identified, the
    registrations identify the IESG as registrant contact and this
    document (RFC XXXX) as the reference, and these are the standard
    registrations for a YANG module document. No new IANA registry is
    created, so the registry-creation requirements of RFC 8126 do not
    apply.

23. List any new IANA registries that require Designated Expert
    Review for future allocations (Expert Review, Specification
    Required). If any, please confirm that the document includes
    guidelines for Designated Experts.

    None. The document creates no new IANA registry (see item 22), so
    no Designated Expert Review applies and no expert guidelines are
    needed.

## Facts checked while preparing this draft
- Original (previous-format) draft write-up of 25 October 2026:
  Datatracker history (replaces draft-jlu-dmm-udp-tunnel-acaas;
  adoption call 2026-03-02 to 2026-03-16; WG -00 approved 2026-03-28;
  -01 2026-07-19; WGLC 2026-09-10 to 2026-09-24; "Revised I-D Needed"
  and state "Waiting for WG Chair Go-Ahead" set 2026-09-28; -02
  2026-10-04; -03 2026-10-15, current, expires 2027-04-18); WGLC list
  comments; idnits on -03 (see item 17); IPR search page could not be
  retrieved (403) at that time.
- Responsible Area Director Charles Eckel, confirmed against the DMM
  charter (checked 2026-10-27) and entered into this write-up on
  2026-10-28.
- Conversion to the 9 October 2026 format, 3 November 2026: the -03
  text was re-checked for the new items — YANG validation reported as
  0 errors / 0 warnings in the author's -03 announcement to the DMM
  list (item 7); Security Considerations modelled on the RFC 9907
  Section 3.7 template (item 7); the single uppercase "MUST" in the
  Security Considerations and the absence of BCP 14 boilerplate
  (item 14); no Updates/Obsoletes header (item 13); and no
  Internationalization Considerations section (item 9).
