# Competitive & Improvement Analysis — `place-name-pronunciation`

Analysis of the Elyos good-deed project: an open, consent-first corpus of how toponyms are
actually pronounced (audio + IPA + respelling + sourced origin notes), grounded against
real-world competitors with cited sources. Plan reviewed: PLAN.md v0.1.0 (draft), with TASKS.md
M0–M3 skimmed.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually strong on governance and is already disciplined where most pronunciation
projects are weakest (consent, licensing, sovereignty). Findings, roughly in order of importance:

**Strong / correct as written**

- **Indigenous data sovereignty is correctly framed.** Binding CARE adherence, a community-steward
  sign-off gate, and an explicit *default-exclude* ("some names will deliberately not be
  published") are the right posture. This matches how the leading Indigenous projects actually
  operate — Native Land Digital explicitly respects "the rights of Indigenous data sovereignty"
  and treats its map as a living document fed by knowledge-holders, and FirstVoices is governed by
  First Nations-led bodies with private/community-controlled sites. The plan's stance is
  consistent with GIDA's "Authority to Control" pillar. This is genuinely best-in-class and should
  be protected.
- **Variants-as-records, not a single "correct" answer.** The decision to model
  `variantType` (`local|official|anglicised|historical|other`) and `dualNames` as first-class
  fields, and to refuse to crown one pronunciation, is both linguistically honest and the core
  differentiator. It directly avoids the colonial-prescription trap.
- **Consent as a hard CI gate** (not metadata), pseudonymous speakers, no biometric/voiceprint
  use, withdrawal honored post-publication with honest language about un-recallable third-party
  copies — all correct and aligned with CLAUDE.md refusal guardrails.
- **Endonym/exonym handled implicitly** via `variantType` (local vs official/anglicised) and
  `dualNames`. Good, but see gap below.
- **Honest `verifiedNeed=false` / "TO BE SECURED"** throughout. Refreshingly non-promotional.

**Gaps / corrections needed**

1. **Endonym vs exonym is under-modelled as a concept.** `variantType` captures *pronunciation*
   variants of one written name, but a true endonym/exonym distinction is about *different names*
   (e.g. Aotearoa/New Zealand, Uluru/Ayers Rock, Kolkata/Calcutta, Wien/Vienna). `dualNames`
   exists but is thin. Recommend an explicit `nameStatus` (`endonym|exonym|official|historical`)
   on the *name*, distinct from the pronunciation `variantType`, with a relationship link between
   paired names. Without this, the corpus can't cleanly answer "what do locals *call* it" vs "how
   do locals *say* the official name."
2. **Sourcing-not-colonial-gazetteers-as-truth needs an explicit data-model rule.** The plan
   leans on Wikidata/GeoNames/GNIS for *identity and linking* (good — those are openly licensed),
   but the plan should state in policy that gazetteer spelling/pronunciation is **not** an
   authority for the *local/Indigenous* pronunciation; it is a reconciliation key only. GNIS in
   particular historically encoded offensive/colonial names. Add: gazetteer = identifier source;
   community/native speaker = pronunciation authority. The hierarchy is implied but should be
   written as a locked decision.
3. **"Native-speaker / community member" is asserted but not verifiable in-schema.** `Speaker`
   has self-described `relationshipToPlace` (resident/native/heritage) but it is unverified and
   pseudonymous. That tension (privacy vs authenticity) is real and unresolved. Recommend a
   `speakerVerificationMethod` field and a partner-attested tier, so a consumer can distinguish
   "self-asserted local" from "community-steward-attested native speaker." This matters for the
   accessibility/TTS downstream that the plan courts.
4. **IPA accuracy has a syntax gate but no *correctness* gate.** CI does an "IPA syntax check,"
   but valid IPA can still be wrong. The cultural/linguistic reviewer covers etymology; the plan
   should explicitly assign **IPA-vs-audio agreement review** to a phonetically trained reviewer
   (the BBC Pronunciation Unit relationship is the right model — trained phoneticians transcribing
   from local usage). Right now IPA correctness is partly an honor system.
5. **Consent provenance for *reused* Lingua Libre/Commons audio.** The plan verifies per-file CC
   license (correct), but a CC-BY file on Commons does **not** carry the project's own
   `ConsentRecord` (voice release, withdrawal terms, CARE flag). The schema should distinguish
   "natively captured under our consent spine" from "reused open audio under upstream license
   only" — otherwise the 100%-consent metric is ambiguous for imported audio.
6. **Scope boundary vs `open-pronunciation-audio` is asserted but porous.** Both produce
   openly-licensed human audio + IPA. The line ("places" vs "words/teaching") is reasonable but
   the shared pipeline (ffmpeg/EBU R128/consent schema) should be *factored out* to avoid two
   divergent consent spines. See spin-offs.
7. **Minor:** "Anglicised" as a `variantType` value bakes an Anglocentric frame into the schema
   for a global corpus. Prefer a neutral `colonial|dominant-language|adapted` taxonomy, or
   `assimilatedTo: <BCP-47>`, so a Spanish-ised Nahuatl name or Russified Sakha name fits the same
   model. This is small but matters for the anti-colonial-prescription thesis.

Overall: the plan is approvable and notably mature. The biggest *correctness* risks are (a) the
endonym/exonym name-vs-pronunciation modelling and (b) the consent/authority status of reused vs
natively-captured audio — both fixable in M0 schema work before any data exists.

---

## 2. Competitive landscape

| Competitor | What it is | Strengths | Weaknesses (vs this project) |
|---|---|---|---|
| **Forvo** | Largest crowd pronunciation DB, incl. place names, native speakers | Huge coverage; native speakers; place-name section | **Reuse-hostile license** — dropped CC BY-NC-SA in 2019 for an ad-hoc restrictive license; API gated; no structured variant/origin model. Categorically out of scope as a *source*, but the incumbent to beat on coverage. |
| **Wikipedia / Wikimedia (IPA + respelling, MoS)** | IPA + respelling in article ledes; Help:IPA/* keys | Open (CC BY-SA); IPA discipline; massive place coverage; explicit rule that place names get IPA from *local* usage | Text-only IPA, **little/no audio**; respelling is Anglocentric; no consent/sovereignty model; no machine-readable per-place variant dataset. |
| **Wikimedia Lingua Libre / Commons** | Open mass-recording tool → CC audio on Commons | **Open licenses**, native-speaker audio, minority-language focus (30+ Indonesian langs, Malayalam 50k), some village-name efforts | **Thin, unstructured place-name coverage**; no origin/variant/endonym model; no consent spine beyond Commons license; discovery is poor. The closest open ally — partner, don't compete. |
| **GeoNames** | Global gazetteer | **CC BY**, free download/API, IDs + coordinates + feature types, multilingual alternate names | Names/spellings only, **no audio, no pronunciation, no IPA**; identity source, not pronunciation authority. |
| **GNIS / US BGN** | US federal geographic names | **Public domain**, authoritative US names | US-only; **no pronunciation**; historically encoded colonial/offensive names — a cautionary "gazetteer ≠ truth" example. |
| **Google Maps (TTS pronunciation)** | Speaker button reads place name via Google Translate TTS (since 2019, ~50 langs) | Ubiquitous; convenient for travellers | **Synthetic TTS, not native speakers**; no IPA; no provenance; closed; exactly the "commercial TTS guesses" the plan critiques. |
| **PronounceItRight** | Expert-checked pronunciation site (people + some places) | Expert-vetted (not pure UGC); apps | Proprietary; people-name focus; thin place coverage; no open license, no IPA dataset, no sovereignty model. |
| **BBC Pronunciation Unit** | In-house phonetician team advising broadcasters | Gold-standard method: trained phoneticians, *local educated usage* for place names, consults locals; published guides (Oxford BBC Guide) | **Not open** (internal/commercial OUP books); no public dataset/audio corpus; advisory, not reusable data. Ideal *reviewer/partner*, not a dataset competitor. |
| **Native Land Digital** | Indigenous-led map of territories/languages/place names | **Indigenous-led**, free GeoJSON + API, sovereignty-respecting, ≥2-source method | Maps/names, **not pronunciation audio + IPA**; complementary, a model partner for the Indigenous lane. |
| **FirstVoices** | First Nations-led language archive (audio incl. place names) | **Community-governed**, audio for place names, 65+ public + 17 private BC sites, US/NZ/AU reach | Community-controlled (often *not* openly relicensable — by design); platform, not a reusable open corpus. A sovereignty *exemplar*, not a source to harvest. |

**Bottom line:** No competitor combines *open license + native-speaker audio + structured IPA/variant model + provenance + consent + Indigenous sovereignty*. Forvo has coverage but is closed; Lingua Libre/Commons has openness but no structure; gazetteers have identity but no sound; Google has reach but synthetic voices; the BBC has method but no open data; Indigenous projects have sovereignty and names but not an open pronunciation corpus.

Sources:
- Forvo license: https://forvo.com/license/ , https://en.wikipedia.org/wiki/Forvo
- Wikipedia pronunciation: https://en.wikipedia.org/wiki/Wikipedia:Manual_of_Style/Pronunciation , https://en.wikipedia.org/wiki/Help:Pronunciation_respelling_key
- Lingua Libre: https://meta.wikimedia.org/wiki/Lingua_Libre , https://commons.wikimedia.org/wiki/Category:Lingua_Libre_pronunciation
- GeoNames license: https://www.geonames.org/about.html
- GNIS: https://geonames.usgs.gov/ , https://geonames.nga.mil/
- Google Maps TTS: https://techcrunch.com/2019/11/13/google-maps-adds-a-new-translation-feature-that-speaks-place-names-out-loud/ , https://voicebot.ai/2019/11/15/google-maps-will-pronounce-foreign-place-names-out-loud-for-travelers/
- PronounceItRight: https://www.pronounceitright.com/
- BBC Pronunciation Unit: https://en.wikipedia.org/wiki/BBC_Pronunciation_Unit , https://www.encyclopedia.com/humanities/encyclopedias-almanacs-transcripts-and-maps/bbc-pronunciation-unit
- Native Land Digital: https://native-land.ca/ , https://www.npr.org/2022/10/10/1127837659/native-land-map-ancestral-tribal-lands-worldwide
- FirstVoices: https://www.firstvoices.com/ , https://en.wikipedia.org/wiki/FirstVoices
- CARE / GIDA: https://www.gida-global.org/care , https://nni.arizona.edu/publications/care-directs-us-home-reclaiming-indigenous-authority-over-data-0

---

## 3. Gaps we can fill

1. **The open + structured + audio intersection is empty.** Forvo is closed; Lingua Libre is open
   but unstructured; gazetteers are open but silent. We fill the combination.
2. **No machine-readable place→variants model exists** that records *local vs official vs
   historical* pronunciations side-by-side with IPA, respelling, audio, and provenance. This is
   the single clearest gap.
3. **No open consent/sovereignty spine for voice data of place names.** Lingua Libre relies on
   Commons license alone; FirstVoices keeps data closed. A reusable, auditable consent + CARE
   stewardship record attached to each recording is novel as *open* infrastructure.
4. **No open endonym/exonym pronunciation dataset** linking the local name and its colonised
   counterpart with how each is actually said.
5. **No openly-licensed pronunciation training data for accessibility/TTS** (screen readers,
   navigation) — the concrete downstream public good; current open audio (Commons) is too
   unstructured to be a drop-in resource.
6. **No provenance-tracked origin notes** ("why is it called that") that are cited, neutral, and
   cultural-review-passed at place granularity.

---

## 4. Differentiators to win

1. **Constraints as identity** — consent-first, sovereignty-respecting, descriptive-not-prescriptive.
   This is a moat precisely because incumbents *can't* retrofit it (Forvo's license, Google's TTS).
2. **Variants-as-records** — multiple valid pronunciations with labels; nobody else models this.
3. **Open + reusable** (CC BY / CC0 + JSON-LD linked to Wikidata/GeoNames) vs Forvo's lock-in.
4. **Native-speaker human audio, never synthetic** — directly counters Google/commercial TTS.
5. **CARE/community stewardship as a hard gate** — partnerable with Native Land Digital /
   FirstVoices / language-revitalisation orgs rather than extracting from them.
6. **Provenance + 100% consent** — citable trust the crowd DBs lack.
7. **Accessibility/TTS public-good framing** gives a concrete, fundable downstream that pure
   linguistic archives don't foreground.

---

## 5. Claude API leverage (and hard limits)

**Where Claude adds leverage (assistive, human-governed):**

- **Toponym list curation & prioritisation** — generate candidate place lists by region/language,
  dedupe, cluster by feature type, flag likely-mispronounced or high-variance names for human
  recording. (Curation, not authority.)
- **IPA candidate generation + respelling drafts** — propose narrow/broad IPA and English (and
  other-language) respellings *as drafts* for a phonetician + native speaker to verify against
  audio. Speeds the bottleneck; never the final word.
- **Metadata enrichment** — BCP-47 tag suggestion, accent/dialect labelling hints, Wikidata/
  GeoNames reconciliation candidate matching, dual-name/endonym-pair detection.
- **Origin-note drafting from open sources** — summarise PD/open etymology references into neutral
  draft notes *with citations*, surfaced for cultural review (flagging contested framings).
- **Pipeline/QA tooling** — consent-record completeness linting, license-allowlist checks,
  provenance-chain validation, audit-sample selection, schema-error explanation.
- **An MCP server** exposing the corpus for assistants to *query* (read-only), with provenance.

**Where Claude must NOT decide (human/community-governed, hard gates):**

- **Authority over a community's own place names** — only the community/steward decides inclusion,
  labelling, restriction, withdrawal. CARE "Authority to Control" is non-delegable to a model.
- **What counts as the/a correct pronunciation** — native speakers do; Claude cannot adjudicate
  endonym vs anglicised "rightness."
- **Native-speaker audio + consent** — recording, identity/relationship attestation, and consent
  capture are human, consent-spine-governed; no synthetic/cloned voice, ever.
- **Final IPA correctness** — must be verified against real audio by a trained reviewer; Claude IPA
  is a draft only.
- **No colonial prescription** — Claude must not "normalise" a local name to a dominant-language
  phonology or pick the official gazetteer form as truth.
- **License/CARE/provenance sign-off** — the license reviewer and community steward decide; Claude
  assists the check but does not approve a source or flip `verifiedNeed`.

---

## 6. Ten concrete optimizations

1. **Split name-identity from pronunciation-variant in the schema:** add `nameStatus`
   (`endonym|exonym|official|historical`) on the name and a name-pair relationship, separate from
   `variantType` on the recording. (Fixes the §1 gap.)
2. **Distinguish natively-captured vs reused audio** with a provenance `captureMode`
   (`native-consent-spine | reused-open-license`), so the 100%-consent metric is unambiguous and
   imported Commons/Lingua Libre files aren't miscounted as consented-by-us.
3. **Add an explicit IPA-vs-audio agreement review step** assigned to a phonetician reviewer; make
   "IPA verified against audio" a gate field, not just IPA syntax validity.
4. **Add `speakerVerificationMethod` / attestation tier** (self-asserted vs steward-attested) so
   consumers can weight authenticity without breaching pseudonymity.
5. **Re-neutralise the variant taxonomy:** replace bare `anglicised` with
   `assimilatedTo: <BCP-47>` or `dominant-language-adaptation`, removing the Anglocentric default
   from a global corpus.
6. **Factor a shared "open audio consent + pipeline" core** with `open-pronunciation-audio` (one
   consent schema, one ffmpeg/EBU R128 normaliser) to avoid two divergent spines.
7. **Codify "gazetteer = identifier, not pronunciation authority"** as a locked decision and a CI
   lint that refuses to derive a *local* pronunciation solely from a gazetteer field.
8. **Partner-first cold start:** prioritise a Lingua Libre import pilot (open audio already exists)
   and a Native Land Digital / FirstVoices conversation *before* M1 recording — fastest path to
   real, sovereignty-respecting coverage and a steward (flips `verifiedNeed`).
9. **Ship an accessibility/TTS-ready export profile** (per-place: best native IPA + audio +
   license) to make the "documented downstream reuse" outcome easy for a screen-reader/nav
   integrator — the strongest fundable public-good signal.
10. **Add an MCP server + read-only query API early** (even thin) so the corpus is *consumed*
    during M2, generating reuse evidence (the real "shipped" bar) instead of after M3.

---

## 7. Parallel & perpendicular spin-offs

- **Parallel — `open-pronunciation-audio`:** shared consent spine + audio pipeline + IPA review.
  Place names are one vertical of a broader open human-audio pronunciation corpus; factor the core
  so both reuse it. Highest-leverage tie.
- **Parallel — toponym-pronunciation *dataset* product:** a clean, versioned, JSON-LD/CSV data
  package (place→variants→IPA→audio→provenance) as a first-class citable artifact for researchers,
  Wikidata, and TTS/ML teams — distinct from the explorer.
- **Perpendicular — `open-map-gaps`:** prioritise recording for under-mapped/under-served regions;
  pronunciation gaps and map gaps correlate, and the same community partners serve both.
- **Perpendicular — `local-history-stubs` / `historical-markers-index`:** origin notes are
  mini-histories; share the cited-open-source + cultural-review workflow and cross-link a place's
  pronunciation to its marker/history stub.
- **Perpendicular — MCP server ("how do locals say X, and why?")** that any assistant can call,
  returning provenance + consent status + variants — turns the corpus into live infrastructure and
  manufactures reuse evidence.
- **Perpendicular — Indigenous endonym reclamation pack:** a steward-governed, opt-in bundle for a
  partner community (their endonyms, their audio, their license terms) — deepens the
  FirstVoices/Native Land Digital relationship and exercises the CARE workflow concretely.

---

## 8. Open questions

1. **Endonym/exonym modelling:** adopt the proposed `nameStatus` + name-pair link, or keep variant
   labels only? (Affects whether the corpus can answer "what do locals *call* it.")
2. **Reused-audio consent status:** how is imported Commons/Lingua Libre audio counted against the
   100%-consent gate when it carries only an upstream license, not our consent spine?
3. **Speaker authenticity vs pseudonymity:** can "native speaker / community member" be attested
   (e.g. via steward) without breaching the no-PII rule?
4. **Steward identity:** Wikimedia chapter vs library/names authority vs broadcaster unit — which
   flips `verifiedNeed`, and does Lingua Libre become the *de facto* host?
5. **Lingua Libre relationship:** import-only, contribute-upstream, or full two-way sync (and whose
   license/consent governs)?
6. **Default output license:** CC BY-4.0 vs CC0 — and how does share-alike propagation from
   CC BY-SA Commons inputs interact with a CC0 default?
7. **Contested/dual names presentation:** exact non-partisan UI/data treatment that satisfies all
   communities (e.g. Uluru/Ayers Rock, Derry/Londonderry).
8. **IPA correctness authority:** who is the standing phonetician reviewer, given the BBC-style
   "trained phonetician + local usage" bar the plan implicitly sets?
