# R1 report: Agent Village and Edge City infrastructure, and where a 54-hour build can plug in

**Method.** I read a clone of https://github.com/Edge-City/agentvillage (head `261b9f9`, 26 Oct; scratch copy at `<research-scratch>/r1_av/repo`). I also read the V1 write-up, agents.edgecity.live, the buildathon page, the Index protocol README and the GitHub org pages. The GitHub API and the MCP were blocked for Edge-City repos, so I took the PR and issue lists from the github.com pages through WebFetch. X/Twitter returned 402. **I found no public Agent Village V2 progress report from October 2026.** The newest Edge City India Substack post is dated Oct 9 (https://edgecityindia2026.substack.com/archive).

---

## (a) Architecture and APIs a builder can actually use

**Stack.** Each resident gets one persistent Hermes agent (Nous Research). The fleet is hosted on Railway, models come through OpenRouter, and Telegram is the interface. The core skills are Index Network (intents, matching, agent-to-agent negotiation) and EdgeOS (identity, calendar, directory, RSVPs) (https://blog.cosmos-institute.org/p/we-gave-a-village-personal-ai-agents).

The fleet model is `openai/gpt-6-luna` (README). The repo is an "overlay" of skills, a workspace, installers and Hermes plugins. It reaches residents only through a tag followed by a **Roll** of every VM. Merging to `main` does not make anything live (`docs/deployment.md`).

**Repos** (README "Repos" table):

| Repo | Visibility |
|---|---|
| `agentvillage` | public, MIT |
| `agentvillage-skills` | public mirror |
| `agentvillage-controlplane`, `-landing`, `-data`, `-onboarding`, the app (`agentvillage-app`) | **private** |
| `p2p-lanes/edgeos-monorepo` | public, MIT, FastAPI + Next.js portal (https://github.com/p2p-lanes/edgeos-monorepo) |
| `p2p-lanes/edge-agent-skill` | public, the India wiki/website indexer |

**APIs and who grants access:**

| Surface | What it gives | Access |
|---|---|---|
| **EdgeOS API** `https://api.edgeos.world/api/v1` (`skills/edgeos/SKILL.md`) | events, event participants, RSVP write/cancel, venues, tracks, popup. Partner keys are limited to `events:read`, `rsvp:write`, `venues:read`. Keys cannot create events or read the directory or `/humans/me`. | Any attendee: "Create an API key in the portal, hand it to Claude Code, Codex…" (https://edgecityindia2026.substack.com/p/the-community-calendar). Key form is `eos_live_…`. The popup id is `$AV_POPUP_ID`. |
| EdgeOS directory and profile | goes through the AV control plane, which uses the resident's own sign-in (`portal:directory:read`, `portal:profile:read`) | hosted agents only; a lapsed sign-in returns exit 4 |
| **Index Network MCP** `https://protocol.index.network/mcp` (header `x-api-key`) | profile (`get/update/enrich_my_profile`), signals (`create/list/update/pause/archive_intent`), opportunities (`list/get/accept/reject_opportunity`) (`skills/index-network/tools.md`) | Per-user key. In the village network it comes from `POST /api/networks/:id/signup` with the network **master key**, which is server-side and held by Edge City. Outside the village: "Generate one on your agents page at index.network" (README). |
| **Index self-host** | full protocol: Bun, Postgres+pgvector, Redis, OpenRouter (https://github.com/indexnetwork/index, MIT). Also `indexnetwork/hermes-plugin` (MIT) and `indexnetwork/agent` ("negotiates over A2A") | public; this is the realistic sandbox for a simulated village |
| **Custom negotiator hook** `$HERMES_HOME/index/negotiator.ts` | `negotiate(input, next)` returns `{turn:{action: propose\|counter\|accept\|decline, message}}` or `{stall:{reason, suggestedAsk}}`. The input carries `user`, `intent`, `brief` and `opportunity.turns`. (https://github.com/Edge-City/agentvillage/blob/main/docs/negotiator.md) | Resident edits their own box and restarts the gateway. About twenty residents wrote negotiation policies in V1 (blog). |
| Village tools (av-events) | `ask_village`, `search_village`, `query_village` (read-only SQL over the scrubbed main Telegram group: `messages(id,topic,sent_at,sender,text)`), `ask_odin`, `pray`, `record_intention`, `village_vote`, `share_digest`, `consent_status` | all go through the control plane with a per-tenant key and are dark behind flags. Resident agents only. |
| ODIN | the "village god agent": its own Hermes box, a SOUL with fixed floors, and a constitution chosen by resident vote. "No data access of any kind… no posting… no allocation" (`docs/odin-profile.md`, `workspace/odin/SOUL.md`) | organizers |

**Provenance and consent machinery already in place:**
- `record_intention` sources every want as `message`, `onboarding`, `note` or `ambient`. Inferred ("ambient") intents wait for the resident's tap. Agents never call `create_intent` directly (`workspace/AGENTS.md`).
- The approval gate (approval.md) logs every routed tool call. Three things need a Telegram tap, open for up to 72 hours: publishing an inferred intention, sharing a digest, and casting a vote (README "Approval").

---

## (b) Mini-app builder contract, and why it cannot go live in 54 hours

- **Catalog.** There are six reviewed apps: gold-stars, dizko, zzzbot, slopfolio, forkicks, mosaic (`mini-apps/catalog.json`). It is "not an arbitrary-code upload marketplace". `MINI_APPS_MANIFESTS` is **off in production** (`docs/MINI-APPS-DEVELOPER.md`).
- **Generic app** (the only shape a partner can ship without app-server code). It must have:
  - `service.kind: mcp`, `auth.mode: none`, an https `baseUrl`
  - only `class: "read"` operations named `<id>.<verb>`
  - an optional `data.context` namespace (`apps.<id>`, one-line entries of at most 200 characters, Private by default)
  - one SKILL.md of at most 32 KiB, whose sha256 is pinned in the manifest
  - no cards, writes, OAuth or payments

  The steps (https://github.com/Edge-City/agentvillage/blob/main/docs/MINI-APPS-QUICKSTART.md):
  1. One PR to the **private control-plane repo** (skill + manifest + catalog append).
  2. Edge City review.
  3. A staffer adds you to `MINI_APPS_TENANT_ALLOWLIST`.
  4. Hard rule: no generic app enters the catalog until the whole fleet runs v2.1.12 **and** cp#337 is merged **and** `MINI_APPS_MANIFESTS=1` and `MINI_APPS_SKILL_DELIVERY=1` are set.
- **Write, OAuth, token and card apps are "mini-apps v3".** They are not built for partners, and the generic approval card ships dark (ov#458, cp#352 draft) (developer guide §5, §8).
- **Consequence (INFERRED):** no outside build will reach residents' agents by Oct 30. A winning submission should be **standalone and demonstrable**, packaged as a conformant generic MCP read relay or a `negotiator.ts`. The pitch would be "ready to drop into the catalog or fleet". A builder must not claim it is live.

**Community mini-app PRs (open):**
- #506 Edge Library, a village knowledge graph with passage-level provenance (Nhajela)
- #450 eci-volunteers
- #512 Mochi, gatherings with per-gathering consent (jmilldotdev)
- #405/#394 kismet (deonmenezes)
- #393 dreamstarter
- #392 symbient-uncommons
- #389 Slopfolio
- #416 Contextsling (dark)

All have no reviews (https://github.com/Edge-City/agentvillage/pulls).

---

## (c) V1 findings and failure modes

Source: https://blog.cosmos-institute.org/p/we-gave-a-village-personal-ai-agents (Kosters, Law, Vendrov, Jul 31 2026).

**Numbers:**
- 239 agents, 17.5B tokens, 4,866 resident-to-agent messages
- Index funnel: **505 intents → 9,688 possible connections → 572 opportunities → 147 accepted**
- 11,593 negotiation sessions, 82% of which ended within two exchanges
- median **4.9 s** per accepted negotiation, and **20 h** from discovery to both humans saying yes
- 67% of sought connections crossed backgrounds; about 4% touched sensitive territory (grief, identity, spiritual seeking)
- Simocracy: 82 Sims, 35 proposals, ten $1,000 rounds (on a $10k fund plus $10k matching) allocated by the S-Process
- Agent Commons: 469 posts

**Failure modes:**
- Hallucinated self-summaries. A tester: "It hallucinated an interesting summary about me though. I don't know where it got that info from."
- Agents "attributed invented ideas to their principals."
- "Agents acting on behalf of their principals exhausted the shared credit supply"; "individual alignment does not automatically produce collective alignment."
- In Simocracy, "their principals did not confirm the final allocation before it was recorded."
- Railway provisioning "buckled".
- Social saturation: "four or five people messaged" Ivan after one talk.
- "Telegram was not a good user interface for this purpose."
- Hermes "not yet built for multiplayer mode".

**What worked.** Utility questions ("just ask the bot, don't read the docs"), serendipitous matches, and resident-built extensions (Simocracy, Agent Commons, Enzyme, Turing Falls, Edge Book, World ID…).

**Open questions.**
- Representation fidelity across contexts.
- Whether users can "understand, correct, withdraw, or ratify" consequential actions, and how to red-team that.
- Collective alignment.
- Whether introductions lead to useful relationships.

**Future work.**
- Compare "human-led, agent-led with human ratification, and mixed" conditions.
- A layer of "mezzanine agents" between personal agents and the collective.
- A persistent interface showing what agents do on a person's behalf.
- Call for collaboration: https://edgecity.notion.site/b2859e0230fe448a9b38a4333d5a2002

**V2 framing** (https://agents.edgecity.live/):
- Measures "verified useful outcomes for each intention".
- Research questions: "How can agents most faithfully represent their human principals?", "What can agents do alone, and what needs a human yes?", "Where does the funnel break?", "Do agents beat people at this?"
- Collaborators: Timour Kosters, Carter Crouch, Jonathan Miller, Amita Shukla, Seref Yarar, Seren Sandikci, Sydney Levine, Logan Walls (linked to the NYU Ethical Intelligence Lab), Jainit Purohit, Soumya Jain.
- I could not find any public page for an "Ethical Intelligence Lab" at NYU beyond that link.

---

## (d) What V2 is doing now, and the gaps

**Active work** (git log since Oct 11: 208 commits, about 170 by Carter Crouch):

- **ODIN plus the village constitution (GODCONST).**
  - Thirty statements, 15 written by residents' agents and 15 by ODIN, rated blind 1–5. The window closed Sun 25 Oct, 10:30 IST.
  - GC-ELICIT then has each agent interview its human, recording "only the human's own typed words".
  - `ask_odin` answers in Larkin-style verse (v2.1.17, 26 Oct).
  - Sources: `docs/GODCONST-TELEGRAM-BALLOT.md`, `plugins/av-elicit/README.md`.
- **Suggestion rating cards** (av-rate, 24 Oct). Match fit is rated 1–5, followed by "Could you imagine collaborating with this person 🤝?"
- **Village treasury experiment** (PR #193, docs only; the page says "nothing is built"):
  - $150/day plus $800 on Fridays, rollover, pot capped at $3,400, Oct 18–31, approval voting.
  - "No autonomous treasury acts"; "Odin records the result; Timour can veto"; "Operations pays by hand within 48 h with a receipt reference". Multisig or a prepaid card are listed as week-3 options.
  - A preregistration is included (H2: agent-channel proposals are funded no more than 10 points below human ones).
- **Referendum adapters** (PR #335, Timour, draft): a "silent personal-preference prediction" that returns probabilities or an abstention with source hashes, run with no tools.
- **MoralMod.** An NYU-supplied "Decision Studio" negotiator arm, run as a controlled experiment (`docs/moralmod_lifecycle.md`).
- **Judge** (`docs/design/judge.md`, "Nothing here is built"): a model reviewer, then adviser ("Your judge suggests: approve (high confidence)…"), then delegated approver. Each stage opens only after an evidence gate.
- **Other.** Village Digest (PR #276, Timour), the ODS data feed (PR #191, draft; "no partner read API").
- **Open issues.** Only #100 ("Heartbeat cron drains OpenRouter key budget (HTTP 402)") and #73 ("Fleet /update is fire-and-forget").

**Gaps that are unsolved and buildable without fleet access (INFERRED from the above):**

1. **Fidelity is enforced at write time but not measured.** Source tags cover intents. Nothing scores whether briefs, negotiation turns, opportunity headlines or the agent-written constitution statements say things the principal never said.
2. **Preference prediction is designed (#335) but unscored.** Nothing yet holds agents to sealed predictions checked against real votes and ratings.
3. **The judge has no evidence harness.** Its stages each need a signed evidence gate first.
4. **Release quality is checked by hand.** The 20-question eval (`docs/evals/edge-india-village-20.yaml`, proposed by Timour, with a pass/partial/fail rubric) automates only the retrieval half. The fleet went from v2.1.12 to v2.1.17 in five days with hotfixes.
5. **Treasury payout is manual,** with no proof-of-ratification or proof-of-delivery.
6. **Disclosure negotiation** ("negotiate what to disclose", V2 layer 2) has no privacy-preserving mechanism. Index negotiation exchanges plaintext turns.
7. **Shared-resource and attention depletion** (V1 credits, #100) has no village-level mechanism.

---

## (e) Plug-in opportunities, ranked by likely organizer value

Each line notes what the user can reuse and what they would need.

1. **Fidelity Auditor ("who said that?")**
   - **What it does:** traces every claim an agent makes about its principal back to the principal's own words. Inputs are an agent's brief, intents, negotiation turns or GODCONST-style statements, matched against chat, onboarding and Context with source tags. Each claim is classified as supported, inferred or fabricated/misattributed.
   - **How it plugs in:** ship it as a `negotiator.ts` guard that returns `{stall:{reason, suggestedAsk}}` when a turn carries an unsupported claim, plus an offline scorer.
   - **Why it matters:** it hits V1 failures 1–2 and V2 research question #1 head-on.
   - **Reuse:** Savlar's claim-to-moment linking, arcminute's "prove itself wrong", harness-lab's verifiers.
   - **Needs:** own agent data or a synthetic village. Can be done solo and remote.
2. **Sealed-prediction representation benchmark**
   - **What it does:** before the human votes or rates (village vote, constitution ratings, suggestion cards, treasury approvals), each agent commits a SHA-256-sealed probability. The seal is revealed afterwards, and the tool reports per-agent Brier/calibration and "agent vs. human proxy" accuracy.
   - **Why it matters:** this is research question #6, and it turns V1's "did vote pretty much how I would have" into a number. It is the measurement half of PR #335.
   - **Reuse:** arcminute.
   - **Needs:** volunteers in Goa for a live run (INFERRED); a synthetic version can be done remotely.
3. **Judge-in-shadow (stage 1 of `judge.md`)**
   - **What it does:** a pinned `model:<name>@<version>` reviewer grades sampled approval cards and logs agreement with human decisions. The output is the evidence-gate report the design requires before the adviser stage opens.
   - **Why it matters:** research question #3 ("what needs a human yes").
   - **Reuse:** harness-lab, dress-rehearsal.
   - **Needs:** synthetic card corpora built from the policy classes in `skills/approval/templates/APPROVAL.md`.
4. **Dress-rehearsal village / release gate**
   - **What it does:** spins up N agents running the public overlay against self-hosted Index (MIT) and recorded EdgeOS fixtures. It auto-grades the 20-question eval plus red-team suites for the four V1 failure modes, and diffs results per overlay tag.
   - **Who values it:** very high value to Carter's release process; less flashy on a demo stage (INFERRED).
   - **Reuse:** dress-rehearsal, harness-lab. Solo, remote.
5. **Savlar for the village: "where Edge converges and disagrees"**
   - **What it does:** maps talks and public village discourse: who agrees with whom, predictions, mind changes, each linked to the transcript moment.
   - **How it plugs in:** shipped as a **conformant generic mini-app** (public MCP, `auth: none`, read ops). That is the one partner shape the platform accepts.
   - **Why it matters:** it continues V1's Geo layer ("public talks, transcripts, and selected village knowledge in a shared graph"), complements Edge Library (#506), and gives ODIN village-level material.
   - **Reuse:** `Edge-City/edge-talk-transcriber` (MIT, built for the Esmeralda talk archive).
   - **Needs:** India talk recordings or transcripts (availability UNKNOWN) and public-only content.
6. **Ratification-gated treasury payouts**
   - **What it does:** escrow releases only on (a) a recorded ratification (ODIN record, veto window passed) and (b) proof of delivery or receipt (TLSNotary).
   - **Why it matters:** targets "fund decisions without a final yes" and replaces "pays by hand within 48 h".
   - **Reuse:** fermata.
   - **Risk:** organizers chose "a budget line… with no wallet" (#193), so this may read as crypto-first (INFERRED). Demo on testnet.
7. **Privacy-preserving disclosure negotiation**
   - **What it does:** a `negotiator.ts` that negotiates sensitive constraints (availability, paid work, sensitive topics, which were about 4% of V1 intents) without revealing them.
   - **Reuse:** batna-protocol FHE.
   - **Risk:** latency against the 4.9 s median and a weaker live demo. Medium value.
8. **Commons and attention budget**
   - **What it does:** a village-level quota or mechanism for agent intros, messages and LLM spend. It addresses V1's "exhausted shared resources" and social saturation, plus issue #100.
   - **Status:** mechanism design and simulation only. Medium value.

**Pitch fit (INFERRED).** Options 1–3 line up with the research partners' questions. The NYU lab that framed the buildathon rubric is also an Agent Village partner. Timour reads every V1 failure mode as a research question, and options 1–3 answer them with measurement rather than claims, which matches the user's "honest verification" style. Contact: timour@edgecity.live.

**Not found:** the published rubric; the India Community Demo Day builds (sign-in only); any public V2 metrics; and the open PRs of `agentvillage-skills` (8 exist, titles not visible).