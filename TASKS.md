# TASKS — place-name-pronunciation

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

Itemized backlog for the open, consent-first corpus of place-name pronunciations (audio + IPA +
respelling + sourced origin notes). See [`PLAN.md`](./PLAN.md) for positioning, the licensing and
consent gates, and the roadmap (M0–M3).

## How these tasks map to Elyos

Each task below becomes an Elyos **Task JSON** validated against
`packages/schema/src/schemas.ts`. Field mapping:

- **id** — stable `place-name-pronunciation-<area>-NNN` (the table ID).
- **title** — the table Title.
- **project** — `place-name-pronunciation`.
- **type** — one of `code | research | writing | data | design-spec | maintenance` (table "Type").
- **lane** — `donated` for all tasks here. Any future metered run would be `funded` and must add
  `fundedBudgetUsd`.
- **priority** — `high | medium | low`.
- **domain** — e.g. `["language","accessibility","open-culture","geography","public-data"]`.
- **riskTier** — `low | medium | high`. Consent/privacy, etymology accuracy, and
  Indigenous/minority-language tasks are **medium**; scaffolding/docs/code are **low**. No `high`.
- **urgent** — boolean (default `false`).
- **deliverable** — `pr | dataset | document | translation` (table "Deliverable").
- **tokenEstimate** — `small | medium | large` (table "Size").
- **status** — `open | in-progress | review | delivered | done` (start `open`).
- **context / objective / acceptanceCriteria[] / resources[] / output** — per task.
- **requestor** — `jdev1977` / beneficiary class until a named partner is secured.
- **verifiedNeed** — **`false`** while no committed partner/steward is secured (honest; the gap is
  real but the last-mile beneficiary is **TO BE SECURED**).
- **outputLicense** — `MIT` (code), `CC0-1.0` (metadata / PD-derived), `CC-BY-4.0` (audio,
  transcriptions, docs by default), or `CC-BY-SA-4.0` (where CC BY-SA source is incorporated).

> **Standing guardrails on every data/recording task (binding):**
> 1. **No recording is ingested without a complete, valid `ConsentRecord`** (license grant + voice
>    release + withdrawal terms). CI fails otherwise.
> 2. **No source is touched until its `sources/allowlist.yml` entry is `approved`** by the license
>    reviewer. Forvo and any proprietary pronunciation DB are **categorically rejected**.
> 3. **Indigenous/minority-language names** require a community-steward sign-off (CARE); absent a
>    steward, they are **not published**.
> 4. **No synthetic/TTS/voice-cloned audio. No biometric/voiceprint/surveillance use.** Refuse and
>    flag.

---

## Milestone M0 — Foundation, consent spine & cold-start

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| place-name-pronunciation-schema-001 | Define core data model (Place/Recording/Speaker/ConsentRecord/OriginNote/Provenance) | design-spec | medium | low | document | — | Maintainer |
| place-name-pronunciation-consent-001 | Ratify consent record schema + speaker release + withdrawal terms | design-spec | small | medium | document | place-name-pronunciation-schema-001 | Privacy/consent reviewer |
| place-name-pronunciation-license-001 | Source allow-list schema + license policy (Forvo/proprietary rejected) | design-spec | small | medium | document | — | License reviewer |
| place-name-pronunciation-license-002 | Analyze & record first 3 candidate sources (≥1 approved) | research | medium | medium | document | place-name-pronunciation-license-001 | License reviewer |
| place-name-pronunciation-id-001 | Commit host-independent persistent ID namespace (w3id.org/PURL) | design-spec | small | low | document | place-name-pronunciation-schema-001 | Maintainer |
| place-name-pronunciation-ci-001 | CI: schema + license-allowlist + consent-completeness + provenance gates | code | medium | low | pr | place-name-pronunciation-schema-001, place-name-pronunciation-consent-001, place-name-pronunciation-license-001 | Maintainer |
| place-name-pronunciation-partner-001 | Steward + community-partner outreach (Wikimedia/library/revival org/broadcaster) | research | small | low | document | — | Maintainer |

**Acceptance criteria (key M0 tasks)**

- **place-name-pronunciation-schema-001**
  - All six record types defined with fields, datatypes, and cardinality; Ajv-valid JSON Schema +
    generated TS types.
  - `variantType` (`local|official|anglicised|historical|other`) and `dualNames` modelled as
    first-class fields — variation and contested names are data, not free text.
  - Every Recording reserves mandatory `consentRef` + `provenance` slots.
  - Speaker record carries **no** legal name/contact/precise location (pseudonymous by design).
- **place-name-pronunciation-consent-001**
  - Consent schema captures: license granted (CC-BY-4.0 / CC0-1.0), explicit public-reuse + voice
    release, withdrawal process, CARE/community-stewardship flag, date, verification method.
  - Withdrawal terms state honestly that third-party copies cannot be recalled; corpus + future
    exports will drop withdrawn recordings.
  - Minors/vulnerable-speaker clause (guardian consent + extra review; default avoid).
- **place-name-pronunciation-license-001**
  - `allowlist.yml` schema: title, custodian, URL, format, license/PD basis, attribution string,
    `status: approved|rejected|pending`.
  - Policy text categorically rejects Forvo and any reuse-restricted pronunciation DB; documents
    per-file CC verification for Wikimedia/Lingua Libre and ODbL share-alike handling for OSM.
- **place-name-pronunciation-ci-001**
  - CI fails on any record without a resolvable provenance link.
  - CI fails on any recording lacking a complete, valid `ConsentRecord`.
  - CI rejects data referencing a source not marked `approved` in the allow-list.

**M0 Definition of Done:** core schema published + Ajv-valid; consent record schema ratified;
allow-list schema + policy merged with ≥3 sources analysed and ≥1 approved; host-independent ID
namespace committed; CI consent + license + provenance gates live; steward/community outreach
initiated and logged; **a privacy/consent reviewer AND a cultural/linguistic reviewer named (hard
exit — if a seat is empty, M0 cannot exit; escalate per PLAN.md fallback)**.
`pnpm build && pnpm test && pnpm lint` green.

---

## Milestone M1 — First consented slice (end-to-end)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| place-name-pronunciation-pipeline-001 | Audio pipeline: transcode + EBU R128 normalise + checksums + derived formats | code | medium | low | pr | place-name-pronunciation-ci-001 | Maintainer |
| place-name-pronunciation-data-001 | First consented batch: ≥50 places, ≥2 locales, 100% consent+provenance | data | large | medium | dataset | place-name-pronunciation-pipeline-001, place-name-pronunciation-license-002 | Privacy/consent + cultural reviewer |
| place-name-pronunciation-recon-001 | Reconcile batch to Wikidata QID + GeoNames ID | data | medium | low | dataset | place-name-pronunciation-data-001 | Maintainer |
| place-name-pronunciation-qa-001 | Independent audit: license/consent/citation correctness (≥95%) | research | small | medium | document | place-name-pronunciation-data-001 | Privacy/consent reviewer |
| place-name-pronunciation-export-001 | JSON-LD + Turtle + audio-bundle export tooling | code | medium | low | pr | place-name-pronunciation-recon-001 | Maintainer |
| place-name-pronunciation-partner-002 | Engage ≥1 candidate steward for adoption | research | small | low | document | place-name-pronunciation-partner-001 | Maintainer |

**Acceptance criteria (key M1 tasks)**

- **place-name-pronunciation-pipeline-001**
  - Archival FLAC/WAV preserved; derived OGG Opus + MP3 generated; SHA-256 checksums stored.
  - Loudness normalised to EBU R128 target (~ -23 LUFS); duration + loudness recorded per recording.
  - Pipeline refuses any input lacking a valid `ConsentRecord` or referencing an unapproved source.
- **place-name-pronunciation-data-001**
  - ≥50 places, ≥2 locales; each recording carries language (BCP-47), accent/dialect, variant label.
  - **100%** of recordings have a complete consent record + resolvable provenance.
  - IPA (narrow and/or broad) + respelling on ≥90% of the batch.
  - No Indigenous/minority-language name included unless under a community-steward record.
  - Passes CI (schema + consent + license + provenance) before review.
- **place-name-pronunciation-qa-001**
  - Stratified sample (min ≥30 or whole batch) checked; ≥95% verify for consent validity, license
    correctness, and source/citation accuracy.
  - **Auditor is independent of the contributor** of the sampled records (no self-grading).
  - Any consent/license/citation defect blocks sign-off until fixed.

**M1 Definition of Done:** audio pipeline proven; ≥50 places across ≥2 locales with 100%
consent+provenance and ≥90% IPA/respelling; reconciliation applied; independent audit ≥95%; exports
validate and round-trip under the persistent-ID namespace; ≥1 candidate steward in conversation.

---

## Milestone M2 — Variation, origins & explorer

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| place-name-pronunciation-data-002 | Scale to ≥250 places; multi-variant capture on ≥60% of known-variant places | data | large | medium | dataset | place-name-pronunciation-export-001 | Privacy/consent + cultural reviewer |
| place-name-pronunciation-origins-001 | Sourced origin notes on ≥100 entries (open/PD/CC sources, non-partisan) | writing | large | medium | document | place-name-pronunciation-data-002 | Cultural/linguistic reviewer |
| place-name-pronunciation-explorer-001 | Static explorer: search/listen, show IPA, variants, source + consent status (no accounts/PII) | code | medium | low | pr | place-name-pronunciation-export-001 | Maintainer |
| place-name-pronunciation-sovereignty-001 | Exercise Indigenous/minority CARE workflow with ≥1 community partner (or document non-inclusion) | research | medium | medium | document | place-name-pronunciation-partner-002 | Community steward + maintainer |
| place-name-pronunciation-metrics-001 | Reuse-metrics tracking (downloads, integrations, citations) | maintenance | small | low | document | place-name-pronunciation-explorer-001 | Maintainer |

**Acceptance criteria (key M2 tasks)**

- **place-name-pronunciation-origins-001**
  - Each origin note cites ≥1 open/PD/CC source; no paywalled or unlicensed text copied.
  - Contested/dual names handled descriptively and non-partisan (describe, attribute, do not
    adjudicate sovereignty).
  - Every note passes cultural/linguistic review before publication.
- **place-name-pronunciation-explorer-001**
  - Browse a place and hear each variant; see IPA, respelling, variant label, and **every
    assertion's source + consent status**.
  - Static / no account; collects no visitor PII; links to raw exports and attribution.
- **place-name-pronunciation-sovereignty-001**
  - CARE principles applied; community retains authority to restrict/label/withdraw.
  - Outcome documented even if it is "no Indigenous/minority names included pending a partner."

**M2 Definition of Done:** ≥250 places; multi-variant on ≥60% of known-variant places; ≥100 sourced,
review-passed origin notes; static explorer live (no PII); CARE workflow exercised or non-inclusion
documented; reuse metrics tracked.

---

## Milestone M3 — Scale, sovereignty & steward adoption (shipped)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| place-name-pronunciation-data-003 | Scale to ≥500 places across ≥5 locales; origin notes ≥200; maintain 100% consent+provenance | data | large | medium | dataset | place-name-pronunciation-data-002, place-name-pronunciation-origins-001 | Privacy/consent + cultural reviewers |
| place-name-pronunciation-partner-003 | Secure steward adoption + ≥1 documented downstream reuse | research | medium | low | document | place-name-pronunciation-partner-002 | Maintainer |
| place-name-pronunciation-sustain-001 | Sustainability, hosting + reviewer-rotation/withdrawal-handling plan | writing | small | low | document | place-name-pronunciation-partner-003 | Maintainer |

**Acceptance criteria (key M3 tasks)**

- **place-name-pronunciation-data-003**
  - ≥500 places across ≥5 locales; origin notes on ≥200 entries; IPA/respelling ≥90%.
  - 100% consent+provenance maintained; fresh independent audit sample still ≥95% verified.
  - All Indigenous/minority entries under a stewardship record (or excluded).
- **place-name-pronunciation-partner-003**
  - A named steward (library / Wikimedia chapter / broadcaster unit / revival org) commits to
    adopt/host/cite the corpus.
  - ≥1 concrete downstream reuse documented (e.g. a TTS/screen-reader/navigation/classroom or
    Wikimedia integration).

**M3 Definition of Done (project "shipped"):** ≥500 places, ≥5 locales, ≥200 origin notes, ≥90%
IPA/respelling; 100% consent+provenance with audit ≥95%; all Indigenous/minority entries under a
stewardship record; ≥1 named steward adopted/cited the corpus; ≥1 documented reuse; sustainability +
withdrawal-handling plan in effect.

---

## Backlog / future (sized, unscheduled)

| ID | Title | Type | Size | Risk | Deliverable | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| place-name-pronunciation-linguabridge-001 | Two-way Lingua Libre integration (import open audio + contribute upstream) | code | medium | medium | pr | Per-file CC verification; share-alike propagation |
| place-name-pronunciation-contribute-001 | Lightweight web contribution flow with built-in consent capture | code | large | medium | pr | Only with a partner consent-intake protocol |
| place-name-pronunciation-align-001 | Forced alignment / phoneme timing for learning tools | code | medium | low | pr | Assistive; human-confirmed |
| place-name-pronunciation-streets-001 | Extend scope to street/POI names | data | large | medium | dataset | Explicit scope expansion; OSM ODbL care |
| place-name-pronunciation-tts-001 | Reference a11y/TTS integration demo (open audio + IPA) | code | medium | low | pr | Demonstrates the accessibility outcome |
| place-name-pronunciation-i18n-001 | Multilingual labels/UI for the explorer (Wikidata CC0 labels) | data | small | low | dataset | CC0 labels |

---

## Example task JSON

Schema-valid Task JSON for the first M0 task (`place-name-pronunciation-schema-001`):

```json
{
  "id": "place-name-pronunciation-schema-001",
  "title": "Define core data model (Place/Recording/Speaker/ConsentRecord/OriginNote/Provenance)",
  "project": "place-name-pronunciation",
  "type": "design-spec",
  "lane": "donated",
  "priority": "high",
  "domain": ["language", "accessibility", "open-culture", "geography", "public-data"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "medium",
  "status": "open",
  "context": "An open, consent-first corpus of place-name pronunciations (audio + IPA + respelling + sourced origin notes) needs a shared data model before any audio is ingested. Recordings are personal data, so consent and provenance must be first-class and mechanically checkable. Variation (local/official/Anglicised/historical) and contested/dual names must be representable without crowning a single 'correct' pronunciation. Indigenous/minority-language names follow CARE principles. Forvo and proprietary databases are out of scope. No partner steward is secured yet. See PLAN.md.",
  "objective": "Define the six core record types (Place, Recording, Speaker, ConsentRecord, OriginNote, Provenance) as Ajv-valid JSON Schema with generated TypeScript types, making variantType, dualNames, mandatory consentRef, and provenance first-class, and keeping the Speaker record free of legal name/contact/precise location.",
  "acceptanceCriteria": [
    "All six record types defined with fields, datatypes, and cardinality; Ajv-valid JSON Schema + generated TS types.",
    "variantType (local|official|anglicised|historical|other) and dualNames modelled as first-class fields.",
    "Every Recording requires a resolvable provenance slot and a consentRef; CI can enforce both.",
    "Speaker record stores no legal name, contact, or precise location (pseudonymous by design).",
    "Place links to optional Wikidata QID and GeoNames ID; language tags use BCP-47.",
    "Audio fields capture archival + derived refs, checksums, duration, and loudness."
  ],
  "resources": [
    "planning/projects/place-name-pronunciation/PLAN.md",
    "packages/schema/src/schemas.ts",
    "https://www.wikidata.org/",
    "https://www.geonames.org/",
    "https://www.gida-global.org/care"
  ],
  "output": "A data-model specification (schema/README.md) plus Ajv-valid JSON Schema files for the six record types and generated TypeScript types, committed via PR.",
  "requestor": "jdev1977",
  "verifiedNeed": false,
  "outputLicense": "CC0-1.0"
}
```
