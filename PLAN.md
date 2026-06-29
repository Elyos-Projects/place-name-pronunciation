# place-name-pronunciation — PLAN

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) ·
> Lane: donated · Risk tier: low (project) — with **medium** gates on consent, etymology, and
> Indigenous/minority-language content.

An open, consent-first, provenance-tracked corpus of **how place names are actually pronounced**
by the people who live where they are — delivered as openly-licensed audio plus IPA, respelling,
and short sourced origin notes. CC-licensed, reusable by anyone, built to honour the speaker and
the community, not to crown a single "correct" pronunciation.

---

## Executive summary

Place names are mispronounced constantly — by newcomers, broadcasters, emergency dispatchers,
navigation and screen-reader software, language learners, and diaspora reconnecting with heritage.
A name said wrong is, in small ways, an identity erased: Indigenous and minority-language
toponyms in particular are routinely Anglicised out of recognition. The resources that exist are
either proprietary and restrictively licensed (Forvo), inconsistent and unsourced, or text-only
gazetteers with no audio at all. There is no **openly-licensed, provenance-tracked, consent-first**
body of place-name pronunciations that a developer, teacher, broadcaster, or community can freely
reuse.

This project builds that corpus and the pipeline that produces it. Each entry pairs a place
(linked to Wikidata/GeoNames) with one or more **recordings by consenting speakers**, each tagged
with language/locale (BCP-47), accent/dialect, pronunciation **variant type** (local, official,
Anglicised, historical), narrow and broad **IPA**, an English respelling, and a full **provenance +
consent record**. A short, sourced **origin note** may accompany the place, written non-partisan
and reviewed for cultural accuracy.

The thesis is captured by what the project *refuses* to do: it does not synthesise voices, does
not declare one pronunciation the only right one, does not scrape proprietary databases, does not
collect personal data it does not need, and does not publish Indigenous or community-controlled
names without that community's stewardship and consent. Those constraints are the identity of the
project, not friction against it.

**Status of need:** the gap is real and well-evidenced, but **no partner organisation or last-mile
steward is yet secured**. Throughout this plan the beneficiary commitment is marked
**TO BE SECURED**; `verifiedNeed` is `false` on every task until a named partner commits.

---

## Problem & beneficiaries

### The problem

- **Mispronunciation has real costs.** Emergency dispatchers and responders who cannot say a
  location risk delay; broadcasters and public-address systems normalise errors at scale;
  navigation and accessibility software (TTS, screen readers) mangle local names because they have
  no openly-licensed audio or phonetic data to learn from.
- **Cultural erasure.** Endonyms — names in the local or Indigenous language — are flattened into
  the colonising language's phonology. The act of pronouncing a name as its community does is a
  small act of respect that current tools cannot support because the data is not free to use.
- **No open, trustworthy source.** Forvo is proprietary with reuse-hostile terms; commercial TTS
  guesses; Wikidata/GeoNames carry names but little audio; Wikimedia's Lingua Libre has open
  pronunciations but thin place-name coverage and no structured origin/variant model. Nobody can
  freely answer "how do *locals* say this, and why is it called that?" with citable provenance.

### Who is helped (beneficiary classes)

- **Newcomers, immigrants, and travellers** learning to say where they now live.
- **Language learners and educators**, especially in geography and heritage-language classrooms.
- **Broadcasters, journalists, and public-address announcers** needing a citable, neutral source.
- **Accessibility, TTS, navigation, and map developers** who need *openly-licensed* audio + IPA to
  improve screen readers and voice guidance (a concrete public-good downstream).
- **Emergency-management and dispatch trainers** building location-pronunciation references.
- **Diaspora communities** reconnecting with ancestral places.
- **Indigenous and minority-language communities** reclaiming and teaching endonyms — but only as
  **partners and data stewards**, on their terms, never as extracted subjects.
- **GLAM institutions** (libraries, archives, museums) and Wikimedia projects that can host and
  reuse the corpus.

### Verified need & partner

**TO BE SECURED.** No partner has committed. Candidate partners to approach (none contacted at time
of writing): a **Wikimedia chapter / Lingua Libre** community; a **public or national library** or
geographic names authority with an open-data mandate; a **language-revitalisation organisation**;
and a broadcaster **pronunciation unit** (historically e.g. the BBC Pronunciation Unit) for a
neutral reviewer relationship. Until a named steward commits to host, reuse, or cite the corpus and
a beneficiary community confirms the need, `verifiedNeed = false` on all tasks.

---

## Goals and non-goals

### Goals

1. Produce an **openly-licensed, reusable corpus** of place-name pronunciations: audio + IPA +
   respelling + variant labels + origin notes, each fully provenanced and consented.
2. Make **descriptive variation** first-class: capture local, official, Anglicised, and historical
   pronunciations side by side with labels — never collapse to one "correct" answer.
3. Set a **consent-first, privacy-minimising** standard for community voice data that others can
   adopt.
4. Honour **Indigenous and minority-language data sovereignty** (CARE principles) so communities
   control their own names.
5. Ship a **machine-readable schema + validating pipeline** so the data is trustworthy, checkable,
   and easy to consume (JSON-LD, linked to Wikidata/GeoNames).
6. Hand the corpus to a **real steward** who hosts/cites/reuses it (the "delivered, not merged"
   bar).

### Non-goals

- **Not a TTS or voice-cloning system.** No synthetic voices, ever — least of all clones of real
  speakers. We publish *human* recordings only.
- **Not an arbiter of correctness.** We do not declare the single right pronunciation; we document
  who says what, where, and how, with labels.
- **Not a personal-data store.** We collect the minimum needed; speakers may be pseudonymous; we do
  not build or enable voiceprint/biometric identification.
- **Not personal or commercial names.** Scope is *places* (administrative areas, settlements,
  natural features; streets/POIs only as a later, explicit extension).
- **Not a dispute adjudicator.** Contested or dual names are recorded descriptively and
  non-partisan; we do not rule on sovereignty or "rightful" names.
- **Not a scraper of proprietary data.** Forvo and any reuse-restricted pronunciation database are
  categorically out of scope.
- **Not a live crowdsourcing app at MVP.** The corpus, schema, and pipeline come first; an
  ingestion/contribution UX is backlog.

---

## Success metrics (outcomes)

Outcome-centric (beneficiary impact), not vanity counts. Baselines are zero (greenfield).

| Outcome | Metric | Baseline | Target (through M3) |
|---|---|---|---|
| Real names made sayable | Place entries with ≥1 consented, provenanced recording | 0 | ≥ 500 places, ≥ 5 languages/locales |
| Variation captured, not flattened | Share of entries with ≥2 labelled variants where variation is known to exist | 0 | ≥ 60% of multi-variant places |
| Trustworthy provenance | Recordings with complete consent + provenance record | n/a | **100%** (hard gate; non-negotiable) |
| Phonetic usefulness | Entries carrying validated IPA + respelling | 0 | ≥ 90% of published entries |
| Sourced origins | Origin notes with ≥1 citable open/PD source, cultural-review passed | 0 | ≥ 200 entries |
| Community sovereignty honoured | Indigenous/minority entries published under a community-agreed stewardship record | 0 | 100% of such entries (or not published) |
| Actually reused (the real bar) | Documented downstream reuse (a TTS/screen-reader/map/classroom/Wikimedia use) | 0 | ≥ 1 named reuse + steward adoption |
| Accessibility impact | A11y/TTS developer integrates the open audio/IPA in a public tool | 0 | ≥ 1 pilot integration |

A metric the project deliberately **does not** optimise: raw recording count. Volume without
consent, provenance, and community respect is a liability, not a win.

---

## Scope

### In scope

- Pronunciations of **place names**: administrative units, settlements, and named natural features.
- **Audio** (archival lossless + delivery formats) by consenting human speakers.
- **Phonetic data**: narrow + broad IPA, English respelling, BCP-47 language/locale tags,
  accent/dialect labels, variant-type labels.
- **Short origin/etymology notes**, sourced from open/PD references, reviewed for cultural accuracy
  and neutrality.
- A **JSON-Schema data model**, a **validating pipeline** (license/consent/schema/audio gates), and
  **JSON-LD exports** linked to Wikidata/GeoNames.
- A static, no-account **explorer** to browse and listen (M2+).

### Out of scope

- Synthetic/TTS audio or voice cloning.
- Personal names, business/brand names; street- and POI-level names (deferred to backlog).
- Any proprietary source (Forvo, commercial gazetteers with reuse restrictions).
- Precise speaker geolocation, identity verification, or any biometric processing.
- Adjudicating naming/sovereignty disputes.
- A real-time contribution app/mobile client (backlog).
- Pronunciation *teaching* curricula (that is `open-pronunciation-audio` / education tracks).

---

## Solution approach & architecture

This is a **content + data pipeline** project built with Elyos engineering conventions
(TypeScript, ESM, pnpm workspaces). The deliverables are data, schema, and tooling.

### Components

1. **Schema package** — JSON Schema (draft-07, consistent with the Elyos task schema) for the core
   records (below), plus TypeScript types generated from it.
2. **Ingestion & validation pipeline** — CLI tooling that takes a submission (audio + metadata +
   consent), validates it against the schema and the **gates**, normalises audio, computes
   checksums, and writes a canonical entry.
3. **Audio processing** — `ffmpeg`-based transcode and loudness normalisation (EBU R128 / ~ -23
   LUFS), archival FLAC/WAV preserved, derived OGG Opus + MP3 generated; integrity checksums stored.
4. **Provenance & consent store** — every recording references a machine-readable consent record
   and a provenance chain (speaker pseudonym, capture context, license grant, source if reused).
5. **Reconciliation** — links each place to a **Wikidata QID** and **GeoNames ID** where one exists
   (Wikidata labels are CC0; GeoNames is CC-BY).
6. **Exports** — JSON-LD + Turtle for the corpus; per-entry audio bundles; a CSV/JSON data package.
7. **Explorer (M2+)** — a static site (no accounts, no visitor PII) to search, listen, and see
   every assertion's source and consent status.
8. **CI gates** — schema validation, license-allowlist enforcement, **consent-completeness gate**,
   audio-integrity/loudness check, IPA syntax check, and a stewardship-flag check for
   Indigenous/minority entries.

### Tech stack (locked)

- **Language/runtime:** TypeScript + ESM, pnpm workspaces (per CLAUDE.md).
- **Validation:** Ajv (already an Elyos dependency) against JSON Schema.
- **Audio:** `ffmpeg` (transcode/normalise), `ffprobe` (inspect), SHA-256 checksums.
- **Identifiers:** Wikidata QID + GeoNames ID + a stable host-independent entry ID
  (w3id.org/PURL namespace, decoupled from the unsecured host).
- **Data formats:** JSON (canonical), JSON-LD + Turtle (linked-data export), FLAC/WAV (archival),
  OGG Opus + MP3 (delivery), IPA (Unicode), BCP-47 (language tags).
- **Fonts for IPA rendering** in any UI: an **open-licensed** font (OFL) such as the existing open
  IPA-capable families — no proprietary fonts shipped.

### Data model (core records — finalised in M0)

- **Place** — `id`, `name` (as written), `script`, `wikidataQid?`, `geonamesId?`,
  `featureType` (admin/settlement/natural), `country/region` (generalised), `dualNames?`.
- **Recording** — `id`, `placeId`, `audio` (archival + derived refs + checksums + duration +
  loudness), `language` (BCP-47), `accent/dialect`, `variantType`
  (`local|official|anglicised|historical|other`), `ipaNarrow?`, `ipaBroad?`, `respelling?`,
  `speakerRef`, `consentRef`, `provenance`, `license`, `recordedDate`, `captureContext`.
- **Speaker** — pseudonymous `ref`, optional self-described `relationshipToPlace`
  (e.g. resident/native speaker/heritage), broad region (no precise PII), `consentRefs[]`. **No
  legal name, address, or contact stored in the public corpus.**
- **ConsentRecord** — `id`, scope, the **license granted** (CC-BY-4.0 / CC0-1.0), explicit
  voice-recording release, withdrawal terms, Indigenous/community-stewardship flag + terms,
  date, verification method. Stored so consent is mechanically checkable and auditable.
- **OriginNote** — `placeId`, prose, `sources[]` (open/PD citations), `reviewStatus`,
  `culturalReviewBy`, `neutralityNote`.
- **Provenance** — for reused upstream material: source IRI, license, attribution string, method.

### Key decisions

- **Variants are records, not overrides.** Multiple pronunciations coexist with labels; no entry
  declares a single canonical "right" pronunciation.
- **Consent is a hard gate, not metadata.** No recording enters the corpus without a complete,
  valid `ConsentRecord`; CI fails otherwise.
- **Sovereignty over completeness.** For Indigenous/minority-language names, community stewardship
  and the right to restrict/withdraw (even post-publication) override coverage goals. Some names
  will deliberately not be published.
- **Provenance over volume.** 100% provenance + consent is the metric that gates everything.

---

## Data, licensing & compliance

**This is the most important section. The posture is conservative.**

### Output licensing (what we publish)

- **Audio + transcriptions:** default **CC-BY-4.0** (attribution credits the speaker/community);
  contributors may instead choose **CC0-1.0** (public domain dedication). The chosen license is
  recorded in the `ConsentRecord` and is binding.
- **Structured metadata** (place links, IDs, schema-level fields): **CC0-1.0**.
- **Origin notes / documentation:** **CC-BY-4.0** (or **CC-BY-SA-4.0** where CC BY-SA source text
  is incorporated, to honour share-alike).
- **Code/tooling:** **MIT**.

### Input sources & their licenses (allow-list governed)

No source is touched until its `sources/allowlist.yml` entry is `approved` by the license reviewer.

| Source | Use | License | Posture |
|---|---|---|---|
| **Wikidata** | place identity, QIDs, multilingual labels | **CC0-1.0** | Approved class — public domain. |
| **GeoNames** | place IDs, coordinates (generalised), feature types | **CC-BY-4.0** | Allowed *with attribution*; record it. |
| **OpenStreetMap** | place geometry/extent (if used) | **ODbL** (share-alike, attribution) | Use cautiously; ODbL share-alike on *derived databases* — keep OSM-derived data separable; attribute. |
| **Wikimedia Commons / Lingua Libre** | existing open pronunciation audio | **CC-BY-SA / CC-BY / CC0** (per file) | Allowed **per-file**; verify each file's license + attribution; share-alike propagates to derivatives. |
| **Newly recorded audio** | primary contributions | granted by speaker (CC-BY-4.0 / CC0) | Primary path; consent record mandatory. |
| **Etymology references** | origin notes | **open-access / PD / CC** only | Cite; verify each; no paywalled or unlicensed copying. |
| **Forvo / proprietary pronunciation DBs** | — | restrictive | **Refused. Out of scope. Categorically rejected** in policy. |

Per-source rules: a PD original is not the same as a PD scan/recording; verify the specific
file/edition. CC BY-SA inputs make the derived audio/transcription share-alike — labelled per entry.

### Provenance model

Every recording and every origin-note assertion carries a resolvable provenance chain: for
recorded audio, the speaker pseudonym + capture context + consent record + license grant; for
reused material, the source IRI + license + attribution + method. Provenance completeness is a
**100% CI gate**.

### Privacy / PII stance (voice is sensitive)

- A **voice recording is personal data** (and, depending on jurisdiction, potentially
  biometric-adjacent). We minimise: speakers are **pseudonymous** in the public corpus; no legal
  name, contact, or precise location is published.
- **Explicit, informed, revocable consent** is mandatory and recorded. Consent text states the
  license, that the audio will be public and reusable, and the **withdrawal** process.
- **Right to withdraw** is honoured even post-publication (removal from the published corpus and
  future exports; we cannot recall third-party copies and say so plainly in the consent text).
- We never build, enable, or invite voiceprint/biometric identification, surveillance, or
  re-identification. Misuse for those ends is a refusal trigger.
- **Minors / vulnerable speakers:** require guardian consent and extra review; default is to avoid
  unless a partner has an appropriate protocol.

### Indigenous & minority-language data (binding)

- Follow the **CARE Principles for Indigenous Data Governance** (Collective benefit, Authority to
  control, Responsibility, Ethics) alongside FAIR.
- Such names are recorded and published **only** under a community-agreed stewardship record;
  communities retain authority to restrict, label, or withdraw. Coverage never overrides consent.
- Non-partisan handling of contested/dual names: describe, attribute, do not adjudicate.

### Attribution requirements

CC-BY/CC-BY-SA reuse and GeoNames use require attribution strings carried in metadata and exports;
the explorer and data package surface attribution and license per entry.

---

## Quality, review & risk gates

### Risk tier

- **Project tier: low** (open, non-controversial content for most names).
- **Elevated (medium) gates** apply to three areas and require a qualified reviewer before "done":
  1. **Consent & privacy** — every recording (privacy/consent reviewer).
  2. **Etymology / origin notes** — historical/linguistic accuracy + neutrality (cultural/linguistic
     reviewer).
  3. **Indigenous / minority-language entries** — community steward sign-off (sovereignty gate).

No `high`-tier (medical/legal/safety) content is in scope. Origin notes carry no advice; they are
descriptive and sourced.

### Required review before a deed is "done"

- Schema + license + **consent** + audio-integrity CI all green.
- For etymology: cultural/linguistic reviewer sign-off.
- For Indigenous/minority entries: community-steward sign-off (or the entry is not published).
- Human approval by the maintainer/reviewer.
- For the "delivered" bar: the artifact is in a form a steward can actually host/reuse.

### Definition of Shipped (project)

A consented, provenanced corpus of place-name pronunciations (target ≥500 places across ≥5
locales) with 100% consent+provenance, validated IPA/respelling on ≥90%, sourced origin notes on
≥200 entries, **all Indigenous/minority entries under a stewardship record**, exported as
open-licensed JSON-LD + audio bundles, **adopted or cited by ≥1 named steward**, and with ≥1
documented downstream reuse (e.g. an accessibility/TTS or classroom integration).

---

## Roadmap & milestones

### M0 — Foundation, consent spine & cold-start (thin)

**Goal:** make it impossible to add data wrongly before any data exists.
**Exit criteria:**
- Core schema (Place/Recording/Speaker/ConsentRecord/OriginNote/Provenance) published + Ajv-valid.
- `sources/allowlist.yml` schema + license policy merged; ≥3 sources analysed, ≥1 approved
  (Wikidata CC0 expected); Forvo/proprietary categorically rejected in policy text.
- **Consent record template + machine-readable schema** ratified (license grant + voice release +
  withdrawal + CARE/stewardship flag).
- Host-independent persistent **ID namespace** committed (w3id.org/PURL).
- CI live: schema + license-allowlist + **consent-completeness** + provenance gates.
- A **privacy/consent reviewer** and a **cultural/linguistic reviewer** named (hard exit; if a seat
  is empty M0 cannot exit — escalate per fallback).
- Partner/steward outreach initiated and logged.

### M1 — First consented slice (proof end-to-end)

**Goal:** prove the whole pipeline on a small, real, fully-consented batch.
**Exit criteria:**
- Audio pipeline (transcode + EBU R128 normalise + checksums + derived formats) working.
- ≥ 50 places with ≥1 consented, provenanced recording across ≥2 locales; 100% consent+provenance.
- IPA + respelling on ≥90% of the batch; variant labels applied.
- Independent QA audit (sample) ≥95% verified for license/consent/citation correctness.
- Wikidata/GeoNames reconciliation applied; JSON-LD export validates and round-trips.
- ≥1 candidate steward in active conversation.

### M2 — Variation, origins & explorer

**Goal:** scale coverage, add sourced origins, make it browsable.
**Exit criteria:**
- ≥ 250 places; multi-variant capture on ≥60% of known-variant places.
- Origin notes on ≥100 entries, each cultural-review passed and sourced (open/PD/CC).
- Static explorer live (no accounts/PII) showing audio, IPA, variants, source + consent status.
- Indigenous/minority workflow exercised on ≥1 community partnership (or documented decision not to
  include any pending a partner).
- Reuse metrics tracking in place.

### M3 — Scale, sovereignty & steward adoption (shipped)

**Goal:** reach the shipped bar and hand off.
**Exit criteria:**
- ≥ 500 places across ≥5 locales; origin notes ≥200; IPA/respelling ≥90%.
- 100% consent+provenance maintained; fresh independent audit ≥95%.
- All Indigenous/minority entries under a stewardship record (or excluded).
- ≥1 named steward adopts/hosts/cites the corpus; ≥1 documented downstream reuse.
- Sustainability + reviewer-rotation + hosting plan in effect.

---

## Work breakdown

The itemised, schema-mapped backlog lives in [`TASKS.md`](./TASKS.md): ~16 tasks across M0–M3 plus
a sized backlog, each as an Elyos Task JSON with acceptance criteria, a Definition of Done per
milestone, and a schema-valid example. M0 establishes the schema, license allow-list, consent
spine, ID namespace, and CI gates; M1 proves the pipeline on a consented batch; M2 adds variation,
origins, and the explorer; M3 scales and secures steward adoption.

---

## Governance, roles & stakeholders

- **Maintainer (Owner):** TBD — accountable for the corpus, CI gates, and the quality bar.
- **License/ToS reviewer:** approves every `allowlist.yml` source; **hard-required** seat.
- **Privacy/consent reviewer:** audits every recording's consent record; **hard-required** for any
  data ingestion.
- **Cultural/linguistic reviewer(s):** sign off etymology/origin notes and IPA quality; rotation as
  volume grows. A neutral broadcaster pronunciation unit is a candidate relationship.
- **Community stewards (Indigenous/minority languages):** authority over their own names; sign-off
  gate; **TO BE SECURED** per community.
- **Steward (last-mile owner):** the org that hosts/cites/reuses the corpus — **TO BE SECURED**.
- **Requestor / beneficiary:** `jdev1977` standing in for beneficiary classes until a partner
  commits.
- **Contributors:** donated-lane human speakers and agent operators who run pipeline tasks.

---

## Dependencies & integrations

- **Wikidata** (CC0) — place identity, QIDs, multilingual labels.
- **GeoNames** (CC-BY) — IDs, generalised coordinates, feature types.
- **Wikimedia Commons / Lingua Libre** — existing open pronunciation audio (per-file license).
- **OpenStreetMap** (ODbL) — optional place extent; share-alike handled.
- **`ffmpeg`/`ffprobe`** — audio transcode, normalisation, inspection.
- **Ajv** — schema validation (shared Elyos dependency).
- **Open IPA fonts (OFL)** — phonetic rendering in any UI.
- **Elyos pieces:** task schema (`packages/schema`), CLI workspace conventions, CI/governance
  workflows, registry.
- **Hosting** for audio + explorer — **TO BE SECURED** (steward or Wikimedia Commons).

---

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| Recording ingested without valid consent | Medium | High | Consent is a hard CI gate; no ingest without machine-readable `ConsentRecord`; independent privacy review | Privacy/consent reviewer |
| Speaker re-identification / voice misuse | Low–Med | High | Pseudonymous speakers; minimal PII; no biometric tooling; refusal trigger for surveillance reuse; clear consent terms | Maintainer |
| Indigenous/minority names extracted without community consent | Medium | High | CARE principles; sovereignty sign-off gate; default-exclude without a steward | Community stewards |
| Treating one pronunciation as "the correct one" | Medium | Medium | Variants-as-records design; mandatory variant labels; descriptive, non-prescriptive framing | Maintainer |
| License contamination (Forvo/proprietary/CC-BY-SA confusion) | Medium | High | Allow-list gate; per-file license capture; share-alike labelled per entry; Forvo categorically rejected | License reviewer |
| Etymology error or partisan framing on contested names | Medium | Medium | Sourced + cultural-review gate; non-partisan handling of dual/contested names; cite, don't adjudicate | Cultural/linguistic reviewer |
| No partner/steward secured (need unverified) | High | High | `verifiedNeed=false` until secured; M0 outreach task; do not over-build before adoption signal | Maintainer |
| Withdrawal requests hard to honour post-publication | Medium | Medium | Withdrawal workflow; consent text sets honest expectations on third-party copies; removal from future exports | Maintainer |
| Audio quality/integrity drift | Low | Medium | EBU R128 normalisation + checksums + CI audio-integrity check | Maintainer |
| Minors/vulnerable speakers recorded improperly | Low | High | Guardian consent + extra review; default avoid without a partner protocol | Privacy/consent reviewer |

---

## Security & privacy

- **Threat surface:** audio files + (minimal) speaker metadata + consent records. Primary risks are
  re-identification, consent bypass, and license contamination — addressed by minimisation and CI
  gates above.
- **Secrets handling:** no secrets/tokens/keys in logs, receipts, or committed files (per CLAUDE.md).
  Pipeline runs need no production secrets in the donated lane.
- **PII:** pseudonymous speakers; no legal name/contact/precise geolocation in the public corpus.
  Any contributor-identifying intake (if a partner collects it) stays with the partner, never in the
  public repo.
- **Abuse/misuse prevention:** refuse surveillance/identification uses; refuse proprietary scraping;
  refuse non-consensual recordings; refuse partisan/derogatory origin framing. Withdrawal honoured.
- **Integrity:** checksums on every audio artifact; provenance chain on every assertion.

---

## Sustainability & maintenance

- **After delivery:** the named steward (TO BE SECURED) hosts and maintains the published corpus;
  the maintainer + reviewer rotation handle ongoing contributions and withdrawals.
- **Persistence:** host-independent ID namespace committed in M0 so identifiers survive a host
  change; archival audio preserved alongside delivery formats; mirrors to Wikimedia Commons
  considered.
- **Outcome tracking:** reuse metrics (downloads, documented integrations, citations) tracked from
  M2; quarterly review of the outcomes table.
- **Reviewer throughput:** consent + cultural review is the bottleneck; rotation and clear
  checklists keep it sustainable; volume goals are intentionally modest to protect review quality.

---

## Open questions

1. **Who is the steward?** Which org commits to host/cite/reuse — Wikimedia chapter, library, or
   broadcaster pronunciation unit? (Blocks `verifiedNeed=true`.)
2. **Default output license** — CC-BY-4.0 vs CC0-1.0 as the project default (contributor choice
   either way)?
3. **Consent collection mechanics** — who runs intake and stores any identifying release? A partner
   with an existing consent protocol is strongly preferred over the project collecting PII.
4. **Minors / vulnerable speakers** — include at all in v1, and under whose protocol?
5. **Lingua Libre integration** — import existing open audio, contribute upstream, or both?
6. **Contested/dual names** — exact descriptive presentation that stays non-partisan and respectful
   to all communities.
7. **Hosting of large audio** — Wikimedia Commons vs steward infrastructure vs object storage?

---

## References

- `C:\code\elyos\CLAUDE.md` — Elyos work rules, lanes, quality bar, refusal guardrails.
- `C:\code\elyos\docs\good-deed-definition.md` — the 5 criteria + risk tiers.
- `C:\code\elyos\packages\schema\src\schemas.ts` — the Task JSON schema TASKS.md maps to.
- `C:\code\elyos\planning\ROADMAP.md` — portfolio context (Track 4; `place-name-pronunciation`).
- CARE Principles for Indigenous Data Governance (Global Indigenous Data Alliance).
- FAIR data principles.
- Wikidata (CC0), GeoNames (CC-BY), Wikimedia Commons / Lingua Libre (per-file CC), OpenStreetMap
  (ODbL) — source license references.
- IPA (International Phonetic Association); BCP-47 language tags; EBU R128 loudness.
- Sibling Elyos projects: `open-pronunciation-audio`, `open-accessible-fonts`,
  `historical-markers-index`.

---

## Appendix A — Improvements applied

Twenty-five specific improvements made to the draft above, each already applied in the text:

1. **Reframed the headline from "audio" to "consent-first corpus,"** so the privacy posture leads
   rather than trails the description.
2. **Made `verifiedNeed=false` and "TO BE SECURED" explicit** in the executive summary, not just in
   TASKS — honest about the missing partner up front.
3. **Added an outcome the project deliberately won't optimise** (raw recording count) to the metrics
   section, making the constraints-as-identity stance measurable.
4. **Split risk tier into project-low + three medium gates** (consent, etymology, Indigenous), so
   reviewers know exactly where elevated review applies.
5. **Promoted consent from metadata to a hard CI gate** with a dedicated `ConsentRecord` schema and
   a consent-completeness check.
6. **Added CARE Principles** as a binding governance rule for Indigenous/minority data, with a
   sovereignty sign-off gate and default-exclude.
7. **Made "variants are records, not overrides" a locked decision**, preventing the corpus from ever
   crowning a single "correct" pronunciation.
8. **Specified concrete audio formats and the EBU R128 normalisation target**, removing ambiguity in
   the pipeline.
9. **Committed a host-independent persistent ID namespace in M0** (w3id.org/PURL), decoupling IDs
   from the unsecured host — borrowed from the patriots-kg pattern.
10. **Added per-file license verification for Wikimedia/Lingua Libre audio**, since CC license varies
    per file and share-alike propagates.
11. **Handled ODbL share-alike for OpenStreetMap** explicitly (keep derived data separable;
    attribute), rather than lumping all sources together.
12. **Categorically rejected Forvo and proprietary databases in policy text**, mirroring the
    patriots-kg "categorically rejected" gate.
13. **Added a withdrawal/right-to-erasure workflow** with honest language about third-party copies we
    cannot recall.
14. **Added explicit minors/vulnerable-speaker handling** (guardian consent + extra review; default
    avoid).
15. **Named candidate partner types** (Wikimedia chapter, library/names authority, language-revival
    org, broadcaster pronunciation unit) so outreach is actionable.
16. **Added an accessibility/TTS downstream outcome and pilot-integration metric**, tying the corpus
    to a concrete public good (screen readers, navigation).
17. **Specified non-partisan handling of contested/dual names** ("describe, don't adjudicate") in
    scope, risks, and open questions.
18. **Added an independent-QA audit (≥95%, independent auditor)** to M1/M3, preventing self-grading.
19. **Listed OFL open IPA fonts** so phonetic rendering never depends on proprietary fonts.
20. **Distinguished this project from siblings** (`open-pronunciation-audio`, `open-accessible-fonts`)
    in scope/references to avoid overlap.
21. **Made the M0 reviewer seats a hard exit gate** (privacy + cultural reviewer named, or M0 cannot
    exit), matching the patriots-kg discipline.
22. **Added a privacy threat-surface paragraph** naming re-identification, consent bypass, and license
    contamination as the three primary risks.
23. **Set 100% consent+provenance as a non-negotiable gate** in metrics, quality, and the DoS, not a
    soft target.
24. **Added an explicit "no biometric/voiceprint/surveillance" refusal**, aligning with the CLAUDE.md
    refusal guardrails for surveillance tooling.
25. **Modelled `dualNames` and `variantType` in the schema** so contested names and pronunciation
    variation are first-class data, not free-text afterthoughts.

---

## Review sign-off

**Reviewed against:** PLAN_SPEC.md (17 required H2 sections present and in order), CLAUDE.md
(architecture rules, refusal guardrails, quality bar, engineering conventions), the good-deed
definition (5 criteria + risk tiers), and the task schema.

**Completeness:** All 17 spec sections present. Metadata header conforms (Status/Version/Date/
Owner/Lane). Success metrics are outcome-based with baselines + targets. Roadmap M0–M3 each carry
measurable exit criteria with M0 as a thin cold-start. Risks table uses the required columns.
TASKS.md cross-referenced and schema-mapped.

**Correctness checks & fixes applied during review:**
- Verified every named license is open/PD/CC/OFL or explicitly rejected (Forvo). ODbL share-alike
  and CC-BY-SA propagation called out rather than glossed.
- Confirmed `verifiedNeed=false` and "TO BE SECURED" appear consistently (summary, beneficiaries,
  governance, risks, open questions, and across TASKS).
- Confirmed no `high`-tier content is claimed; origin notes are descriptive/sourced, not advice;
  medium gates assigned where domain accuracy or sovereignty applies.
- Confirmed privacy posture treats voice as personal data with minimisation, consent, withdrawal,
  and an explicit no-biometric/no-surveillance refusal (aligns with CLAUDE.md guardrails).
- Confirmed the project does not primarily benefit a for-profit entity and outputs are openly
  licensed (criteria 1–4 of the good-deed definition satisfied; criterion 5 satisfied by the
  schema-mapped, reviewable task backlog).

**Outstanding (human decision required):** secure a named steward/partner (flips `verifiedNeed`);
choose the default output license (CC-BY-4.0 vs CC0); decide the consent-intake operator and the
minors policy. These are tracked in Open questions and as M0 outreach tasks.

**Verdict:** Approved as a Draft (v0.1.0) plan. Safe to begin M0 foundation work; data ingestion
(M1+) is blocked until the M0 consent spine, reviewer seats, and license gates are live.
