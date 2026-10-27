# R4 report: what the Edge City India village is talking about (as of Tue 27 Oct 2026)

**Coverage limits, stated first.** I could not read X/Twitter. WebFetch on x.com returned HTTP 402, and the permission policy denied access through a mirror. Web search only finds X posts from before the event. The official Substack has published nothing since Oct 9 (22 posts in total; I pulled them all through its public API), so there are no public weekly recaps. Live village talk happens in the private Telegram group and the logged-in portal. The best public view of in-village activity is the Agent Village GitHub repo, the wiki (read through Notion's public API), and local Goan press. Anything below that is not directly sourced is marked INFERRED.

---

## (a) What has happened, week by week

**Before opening (Oct 1–10)**
- The Road to Edge caravan crossed about 1,000 km from Bangalore through 6+ farms (https://www.edgecity.live/india26).
- Oct 10 press conference at Paryatan Bhavan, Panaji, with Tourism/IT Minister Rohan Khaunte, Telamon Ardavanis (Edge City), DITE&C, the Startup & IT Promotion Cell and NomadGao. They announced about 800 participants from 60+ countries. Khaunte said: "Our ambition is not simply to attract more visitors." (https://sugermint.com/goa-to-host-indias-first-edge-city/)
  - The Anima House site reportedly says the village has more than 1,000 people. I saw that only in a search summary; it is not verified.
- The Light DAO page says about 65% of participants are from outside India (https://luma.com/LightDAOEdgeCity).

**Week 1, Environments of Tomorrow (Oct 11–17)**
- Oct 11: Opening Ceremony at The Forresta Kinaro.
- Oct 12: Residency Fair, "Building in Public: … Jungli the Nomad Village", Intro to Experiments, Orientation, and a community dinner at Oo! Olivia.
- Oct 13 talks:
  - "From Digital Nomad to Building Communities: Lessons from Goa"
  - "Chai, Code, and Circuit Boards: The Robotic Takeover of India"
  - "From AI to AGI"
  - "Hyper growth for beginners: from 2K to 100K"
  - Community Care Share with Jess
  - Women's Nourishment Potluck at Anima House
  - Source: https://edgecityindia2026.substack.com/p/the-first-three-days-at-edge-city
- Ground Floor field labs with the Goa Chamber of Commerce (GCCI) started on the Oct 13 Tuesday/Thursday schedule. Sessions run in English, Konkani, Hindi and Marathi. Businesses keep ownership of whatever is built for them (https://nenews.in/goa/goa-chamber-of-commerce-and-industry-partners-with-tech-firms-to-promote-ai-adoption-among-small-businesses/67264/).
- Community Builders concentrated its programming in week 1: a Hero's Journey workshop, a Physical Communities panel (Jungli, NomadGao, Build3, Oddtable) and an "AI for Experience" workshop (https://edgecityindia2026.substack.com/p/announcing-the-community-builders).
- Hub Culture, inside the Light DAO residency, began testing "Mandala", an AI-to-AI autonomous protocol (https://hubculture.com/hubs/809/news/1969/).
- Agent Village V2 went live. The research proposal (updated Oct 15) says "The India experiment is underway". MoralMod, run with Sydney Levine's group at NYU, assigns participants at random to ON and OFF conditions. Administrators used it in week 1 and participants got it in week 2 (https://edgecity.notion.site/Research-Partner-Proposal-Agent-Village-V2-at-Edge-City-India-Shared-3c1d45cdfc5981d7b7bac1e216f3678b).

**Week 2, Rasayana (Oct 18–24)**
- Ambhasi (with CIMC) started Oct 18 and includes a Vedic-philosophy track on AI sentience (https://www.edgecity.live/india26).
- A shuttle loop (Nanu, Riva, Circle.Work, Namaka) and a "new… few quirks" live tracker appeared on the wiki (https://edgecity.notion.site/Edge-City-India-2026-Wiki-038d45cdfc5983c7a1fe013fdc77135b).
- Oct 22: the Goa AI Policy 2026 was unveiled at the Goa AI Tech Conclave in Panaji. It sets a target of 50,000 people trained in AI by 2030, and a state Goa AI Hackathon launched alongside it (https://nenews.in/goa/goa-launches-ai-policy-to-promote-innovation-skills-and-startups/68538/). The draft policy proposes a Konkani-first LLM (https://www.thegoan.net/goa-news/goa’s-draft-ai-policy-aims-for-a-techdriven-future/147690.html).
- The Agent Village team shipped at high speed (https://github.com/Edge-City/agentvillage/pulls):
  - "For Kicks": café menus and approval-gated coffee orders paid by UPI.
  - "Dizko": event discovery.
  - An Edge Volunteers mini-app (#450, open).
  - A village constitution ballot on Telegram, where residents rate pairs of "one agent + one ODIN statement" from 1 to 5 (#483, #489).

**Week 3, Frontier Intelligence (Oct 25 to now)**
- Oct 25: Community Demo Day with 13 builds (from the task context) and the Sunday dinner at Morjim Culture.
- ODIN became "the village's god agent" (#510). It answers in rhyming verse modelled on Philip Larkin and is reached through `ask_odin`.
- An "Edge Library" knowledge graph mini-app was proposed (#506, open).
- Oct 26–28: The Awareness Lab with Tso.
- Coming up:
  - Oct 28–31: Hacker House Goa.
  - Oct 30: Project Odin workshop and build3 pitch day. build3's own post puts its closing week at Startup Ecoāshrām in Sindhudurg, not in the village (https://edgecityindia2026.substack.com/p/build3-and-edge-city-are-bringing).
  - Oct 31: Demo Day.
  - Nov 3–6: Devcon Mumbai.

## (b) Recurring themes and tensions

1. **Agents acting for people, and the approval gate.** This shows up in Agent Village, Hub Culture's Mandala, For Kicks (agents placing UPI orders), and the AI×crypto Hacker House. Every Agent Village PR is about failing closed and getting explicit human approval. Example: Mochi's PR says "confirm shows every outbound field and requires a direct approval… Autonomous decisions fail closed" (https://github.com/Edge-City/agentvillage/pull/512).
2. **Whether agents represent their people faithfully.** The failures from the first Agent Village (V1) were agents that "hallucinated personal details, attributed invented ideas to their principals, and exhausted shared resources". A resident said: "It hallucinated an interesting summary about me though" (https://blog.cosmos-institute.org/p/we-gave-a-village-personal-ai-agents). V2 answers this with MoralMod, "inspectable and correctable" decision assumptions. Edge Library sends any claim attributed to a named person to admin review.
3. **Community versus commerce.** The guiding norm asks: "Am I contributing to a conversation or trying to start a transaction?" (https://www.edgecity.live/india26). At the same time the village hosts Forge ("raised $3.3M by Demo Day"), Vyne House ("first $1,000 earned"), build3 pitch day and $50K in Hacker House bounties.
4. **A safe, off-the-record space versus capturing and documenting.** The media policy says "All discussions and events are off the record unless…" (see d). Against that, the Creator Residency must publish, Agent Village copies Telegram messages for group summaries, and Edge Library wants to build a village knowledge graph.
5. **Global visitors versus the host community.**
   - The norm is "Honor Our Host Community".
   - Fridays are a locals night.
   - Ground Floor asks: "Who should own the data? Who benefits when the infrastructure is built?" and "Much of today's AI tooling struggles to serve the languages many Goans use every day" (https://edgecityindia2026.substack.com/p/the-future-arrives-locally).
   - The state frames Edge City as part of "Work from Goa" and longer-stay tourism (sugermint, above).
6. **Ancient practice meeting frontier tech.** Examples: Rasayana (Ayurveda) next to biohacking, a Vedic track inside a machine-consciousness residency, and the Awareness Lab measuring inner experience with wearables plus AI.
7. **Collective governance.** V1's Simocracy recorded allocations "without final principal ratification". V2 is running a constitution ballot and plans "bounded representation".
8. **Competition for attention in the final week (INFERRED).** The Buildathon, Hacker House Goa, Project Odin, build3, the Awareness Lab and Demo Day all fall on Oct 28–31. That may explain why only 2 teams had registered for the Buildathon.

## (c) Felt needs and pain points

**Residents**
- **Overload.** "Contains more people, events, and ideas than anyone can absorb." After one talk, a V1 resident got 4 or 5 meeting requests and scheduling them "became its own burden", and he missed a lunch because its title was unclear (Cosmos post above). The calendar guide says to "check it each morning", and the culture norm is "Embrace JOMO".
- **Hard to know who people are and to remember them.** The tools are Rolodex "We met", Gold Stars (3 per day) and directory lookups. The Telegram agent "cannot currently… mark someone as met" (wiki).
- **Logistics.**
  - Riva is sold out, so housing is spread across Mandrem.
  - The shuttle tracker "is new, so there may be a few quirks", and taxi prices are negotiated.
  - Foreigners need CheqUPI to pay with UPI.
  - Lunch delivery to The Circle has to be arranged "via Telegram".
  - Lost wristbands cost $50.
  - Source: the wiki.
- **Families.** Parents need coverage and coordination, and the blog suggests a "babysitting club" between families (https://edgecityindia2026.substack.com/p/bring-your-family-to-edge-city-india).
- **Wellbeing follow-through.** The Sankalpa accountability bot (https://edgecityindia2026.substack.com/p/health-and-wellbeing-at-edge-city).

**Organizers and researchers**
- **Proving that anything useful happened.** V1 "could measure agent and platform activity more reliably than completed meetings, collaborations, or lasting value." V2's primary metric is "Verified useful outcomes per eligible intention" (research proposal). This is the central open problem.
- **Representation accuracy, correction and revocation.** The safety dashboard tracks "attention concentration, shared-resource use, manipulation, collusion" (same proposal). There is also a $150K funding target, with funding, research and technical partners being sought.
- **Consent plumbing.** Rejoining research is "currently paused". Group message copies are "deleted by December 1, 2026". "Complete anonymity cannot be guaranteed." Source: https://agents.edgecity.live/research-register
- **Public memory of the village (INFERRED).** The Substack has been silent since Oct 9. The Esmeralda precedent was a "Month in Review" post plus a Drive folder of recordings.

**Host community**
- Owners need "discernment" more than adopting more tools. At Healdsburg, the owners who benefited most "were the ones who became clear about what deserved their attention."
- Konkani support is weak.
- Local ownership of data and tools.
- Sources: Ground Floor post and nenews, both above.

**Specific residencies**
- Project Odin: sustaining open-source funding "until the grant runs out" (https://blog.ethereum.org/2026/02/27/project-odin).
- Awareness Lab: finding patterns across self-reports, practitioner observations, wearables and context "on a single timeline".
- Community Builders: "what makes people stick around?"
- Anima House: women's health "went understudied for decades".

## (d) Media and recording policy, and what it means for projects

Edge City's media policy (https://edgecity.notion.site/Edge-City-Media-Policy-Shared-263d45cdfc59803cbf30f181bb164955), quoted:
- "All discussions and events are off the record, unless the speaker and all participants consent ahead of time."
- Press wear badges and "announce their role whenever they enter a conversation".
- "If you wish to use any photos shared in the attendee group chat, please get permission from everyone who is in the photo and also one of the core team members of Edge City (Timour, Telamon, Sophie)."

Agent Village research register: Telegram text from the main group and the AV Hub is "planned for group summaries after notice", and research use "separately requires the sender's active research consent". There is a separate opt-in for model training. The agent `ask_village` tool reads "what they said in the main group" (https://raw.githubusercontent.com/Edge-City/agentvillage/main/skills/edge-india/SKILL.md).

What this means for a build:
- A project that records, transcribes or maps conversations must collect consent **before** recording, from the speaker **and all participants**.
- It must default to dropping or redacting anyone who has not consented.
- It must not reuse group-chat photos without per-person permission plus a sign-off from the core team.
- A consent-first capture tool does not just comply with the policy. It solves a problem the organizers already have (INFERRED).
- Mochi's "exact per-gathering resident consent" PR (#512) shows the Agent Village team already thinks at per-gathering granularity.

## (e) Data a project could use

| Source | Access | Notes |
|---|---|---|
| Substack (22 posts) | Public JSON: `https://edgecityindia2026.substack.com/api/v1/archive` and `/api/v1/posts/{slug}` | Nothing after Oct 9 |
| Wiki | Public through Notion `loadCachedPageChunkV2` / `syncRecordValuesMain` | Covers venues, shuttles, dinners, Agent Village how-to, feedback form |
| Community calendar (EdgeOS) | Requires a ticket. Residents "create an API key in the portal" and hand it to an agent (https://edgecityindia2026.substack.com/p/the-community-calendar). API at `https://api.edgeos.world/api/v1`; partner keys get `events:read`, `rsvp:write`, `venues:read`, plus event participants | The directory and profile go only through the Agent Village control plane (edgeos SKILL.md) |
| Agent Village repo (MIT) | https://github.com/Edge-City/agentvillage | Mini-app builder contract; existing apps: Gold Stars, Dizko, For Kicks, Mosaic, ODIN, constitution ballot; open PRs: Edge Library (#506), Volunteers (#450), Mochi (#512) |
| Talk recordings | No public India recordings found. I could not list the Edge City YouTube channel (WebFetch got no content) | Precedent: at Esmeralda, "All photos and talks from EE26 can be accessed in the drive" (https://edgeesmeralda2026.substack.com/p/edge-esmeralda-2026-month-in-review). Patagonia has a YouTube archive. Creator Residency output goes to creators' channels and Edge City's. LocalhostHQ is the media lab partner. Whether India talks are being recorded is UNKNOWN; ask Timour or Telamon |
| Shuttle tracker | https://eci-shuttle.positivesumcompany.com/ and @eci_shuttles_bot | |
| Goa context | Goa AI Policy draft (https://www.dit.goa.gov.in/assets/books/goa_ai_policy_draft.pdf) | GCCI/Ground Floor program details in nenews (above) |
| Savlar MCP | Covers only Dwarkesh, Latent Space, MLST and No Priors | No Edge City content |

## (f) Idea seeds rooted in these needs

1. **"Said-By": a provenance guard for agent claims about people.** *Need:* the V1 failures (fabrication, misattributed ideas), MoralMod's goal of inspecting and correcting, and Edge Library's admin review of attributions. *Build:* an Agent Village mini-app or skill. Every statement an agent makes about a resident (intro blurbs, Mosaic summaries, Rolodex cards, constitution statements) must cite that resident's own consented words. Unsupported claims get flagged or blocked. A small evaluation shows the misattribution rate before and after. *Reuses:* Savlar's claim-to-source linking, arcminute's "prove itself wrong" stance, dress-rehearsal and harness-lab evaluation. *Fit (INFERRED):* the NYU Ethical Intelligence Lab co-designed both the rubric and MoralMod. *Logistics:* solo, remote OK; integrating with the live fleet needs the Agent Village team (Carter, Amita, soycarts).

2. **"On the Record": consent-first capture for salons and talks.** *Need:* the media policy (all off the record unless everyone consents) against the organizers' wish for public memory and Creator Residency output. *Build:* participants join a session by QR or Telegram and tap "record me" or "not me". The transcript keeps only consenting speakers. The output is a Savlar-style map of the session (claims, open questions, disagreements) that the speaker approves before it is published, optionally into Edge Library. *Logistics:* best in person in Goa to demo on a real consented session; a remote demo would use a staged session. Solo is possible; one in-village teammate helps.

3. **Outcome Ledger: measuring "verified useful outcomes per intention" honestly.** *Need:* V2's primary metric and V1's gap between counted activity and real value. *Build:* opportunities are tracked from intent through negotiation, approval, "We met" and a 48-hour follow-up asking "was it useful?". Both sides confirm. The dashboard shows where the funnel leaks. Agents cannot self-report outcomes. *Reuses:* fermata's "release on proof" pattern. *Logistics:* solo, remote OK with synthetic data; much stronger with Agent Village data access, which requires partner scoping.

4. **"What Goa Learned": the village's consented collective memory (Demo Day piece).** *Need:* no public recaps, the community-builders question "what makes people stick around?", and continuity into Devcon and Bhutan. *Build:* from consented talks, Demo Day pitches and the public Substack and wiki, map where the village converged, disagreed and changed its mind, with each point linked to its source moment. *Risk:* depends on idea 2 or on recordings existing. *Logistics:* a team helps; it could be partly non-technical (a written or film companion with the Creator Residency).

5. **Ground Floor in Konkani: a business-owner copilot in the local language.** *Need:* Ground Floor's Konkani gap and data-ownership questions, the Healdsburg "discernment" lesson, and the Konkani-first LLM in the Goa AI Policy unveiled Oct 22. *Build:* a voice or WhatsApp helper in Konkani, Marathi and Hindi for one real business. Use Sarvam and ElevenLabs if available; both are listed partners, but I have not verified their availability. The owner keeps an export of their data, and a "what to ignore" scorecard is included. *Logistics:* must be in Goa with a Konkani-speaking teammate and a Ground Floor introduction. Highest appeal on the host-community norm, but also the highest language and data risk in 54 hours.

6. **Sealed negotiation for shared village resources.** *Need:* V1 agents exhausted shared resources, Simocracy recorded allocations without ratification, and V2 plans budget negotiation. *Build:* agents submit encrypted reservation values for a shared fund, venue slots or rides. A deal is found without revealing those numbers, and a human ratification gate is required. *Reuses:* batna-protocol (FHE). *Logistics:* solo, remote OK. *Risk:* may read as abstract; tie it to a concrete pool such as a Gold Stars–funded sauna (precedent: the Esmeralda sauna win).

7. **Awareness Lab "inner weather" timeline with pre-registered hypotheses.** *Need:* Tso's goal of putting all streams on a single timeline and asking whether AI can find patterns across them. *Build:* merge self-report, wearable and context data. Predictions are SHA-256-sealed before the AI looks for patterns, to guard against p-hacking (reuses arcminute). *Logistics:* needs Tso's consent and data; best in person. The lab runs Oct 26–28, so the window is closing.

8. **Odin Paywall-for-Commons.** *Need:* the Project Odin workshop (Oct 30) on open-source funding "until the grant runs out", with Devcon next week. *Build:* agents pay open-source maintainers per verified use through x402 escrow (reuses fermata/preflight). *Logistics:* solo, remote OK. Weaker tie to the village's lived needs.

**Strongest picks (INFERRED):** 1 and 3 hit the published research agenda and the rubric co-designers (NYU) directly. 2 and 4 hit a policy constraint the organizers really have and could be packaged for Demo Day. 5 makes the strongest moral case, but only with on-site local partners.