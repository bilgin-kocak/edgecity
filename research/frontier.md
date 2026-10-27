# R6 report: frontier capability menu and buildathon craft (as of 27 Oct 2026)

## (a) Capability menu

**Sponsor credits: not found.** No public source confirms that OpenAI, Cartesia, ElevenLabs, PostHog, Cursor or Microsoft gave residents credits.
- The partner strip on https://www.edgecity.live/india26 shows ElevenLabs and Microsoft logos, among others.
- The Substack posts don't mention credits.
- The wiki at edgecity.notion.site is rendered by JavaScript, so I couldn't read it.
- Ask at the kickoff or check the portal.

1. **Frontier LLMs with 1M-token context**
   - Claude: Fable 5.1, Opus 5.5, Sonnet 5.5 and Haiku 5.5 all have 1M-token context and 128K output (https://platform.claude.com/docs/en/about-claude/models/overview).
   - OpenAI: GPT-6.1 Sol (Sep 29, multi-agent delegation in beta), GPT-6.1 Terra (Oct 26, "precise computer use"), Decisions API GA (Oct 22) (https://developers.openai.com/changelog/).
   - Google: Gemini 4 Argon GA (Oct 13) and Gemini 3.8 Flash (https://ai.google.dev/gemini/docs/changelog).
   - *Magic moment:* "the village in one prompt". All talk transcripts, the calendar and opted-in profiles sit in context, and each answer cites the exact moment it came from (the Savlar pattern).
   - *Feasibility:* high. The limit is consent and collecting the data, not context size.

2. **Hosted agent runtimes**
   - Claude Managed Agents: public beta since 8 Apr 2026, about $0.08 per session-hour according to secondary sources (https://alternativeto.net/news/2026/4/anthropic-launches-claude-managed-agents-to-accelerate-ai-agent-development-and-deployment).
   - OpenAI Agents API: public beta Sep 10, computer use added Sep 29.
   - *Magic moment:* an agent works overnight and leaves a trail of receipts by morning.
   - *Feasibility:* high. The Opus 4.7 hackathon had a "Best Use of Claude Managed Agents" prize (https://www.claude.com/blog/meet-the-winners-of-built-with-opus-4-7-claude-code-hackathon).

3. **MCP Apps**
   - Tools return `ui://` resources that the host renders in a sandboxed iframe. The spec (SEP-1865) has been stable since 2026-01-26.
   - Hosts include Claude, ChatGPT, VS Code and Goose (https://www.morphllm.com/mcp-apps).
   - *Magic moment:* a judge types one sentence into their own Claude or ChatGPT and an interactive card appears.
   - *Feasibility:* medium-high. The user already ships MCP servers.

4. **Realtime voice**
   - OpenAI GPT-Live 1: GA Sep 10 at $0.05/min. Hindi voices added Oct 16. Decisions integration added Oct 15, so apps can act while the user is still speaking.
   - Gemini 3.8 Live: GA Sep 15.
   - ElevenLabs: Eleven v4 Turbo at about 100 ms median latency (Sep 28). Eleven Realtime v1 Mini and Max for ElevenAgents (Oct 19). WhatsApp and Twilio support (https://elevenlabs.io/docs/changelog).
   - Cartesia: Sonic 3.6 (Aug 27) covers 44 languages and documents a Hinglish setup. Ink-2 speech-to-text added Hindi in September. Sonic-2 is sunset after Oct 20 (https://docs.cartesia.ai/changelog/2026).
   - *Magic moment:* the speaker interrupts and switches language mid-sentence, and the agent keeps up.
   - *Feasibility:* high, as long as the demo doesn't depend on venue wifi.

5. **Indic voice (Sarvam)**
   - Saaras v4 speech-to-text: 22 Indian languages plus English, with transcribe, translate and code-mix modes.
   - Bulbul v4 Flash text-to-speech: 10 languages, 200+ voices.
   - Also: voice-cloning beta, the Sarvam-105B-conversations model, Samvaad phone agents from ₹3/min, and Sarvam Vision OCR in 23 languages (https://docs.sarvam.ai/api-reference-docs/getting-started/models).
   - *Magic moment:* a Goan shop owner phones in, speaks Konkani or Hinglish, and gets an answer.
   - INFERRED: Konkani is one of India's 22 scheduled languages, so Saaras probably accepts it. It is not among Bulbul's 10 output languages. Verify before promising it.
   - *Feasibility:* high. This is the best fit with "respect the host community" and the Ground Floor residency.

6. **Vision and video**
   - SAM 3.1 (March 2026) adds Object Multiplex, about 7x faster at 128 objects on one H100. The checkpoint is gated (https://huggingface.co/facebook/sam3.1).
   - Gemini agentic video understanding launched Sep 1.
   - *Magic moment:* a phone video turns into a measured, segmented record (the user's arcminute pattern).
   - *Feasibility:* medium. Book a GPU ahead of time.

7. **On-device models**
   - Gemma 4 E2B/E4B: released 2 Apr 2026 under Apache 2.0. One talk reports about 40 tokens/s on an iPhone 17 Pro with MLX (https://ai.engineer/talks/running-gemma-4-on-device-40-tokens-s-on-iphone-with-mlx).
   - Apple's Foundation Models framework also runs offline (https://techcrunch.com/2025/06/09/apple-lets-developers-tap-into-its-offline-ai-models/).
   - *Magic moment:* switch on airplane mode on stage and the app keeps working, so the privacy claim is visible.
   - *Feasibility:* medium. Demo only on the device you rehearsed with.

8. **Wearables**
   - Oura API v2: OAuth2 only (personal access tokens deprecated Dec 2025), 10-user cap until approved. Terms effective 8 Jun 2026 reportedly require written consent to send data to AI models (https://tryterra.co/blog/oura-api-ai-apps-access-permissions-commercial-restrictions).
   - WHOOP v2: webhooks for recovery, sleep and workouts, 10-member developer cap (https://tryterra.co/blog/whoop-api-data-access-permissions-limitations-2026).
   - Muse Athena (EEG plus fNIRS): only through the unofficial OpenMuse project (https://github.com/DominiqueMakowski/OpenMuse).
   - Precedent: Fulcra Dynamics built a village-wide wellness dashboard at Esmeralda 2025 (https://edgeesmeralda2025.substack.com/p/edge-esmeralda-2025-month-in-review).
   - *Magic moment:* a picture of the whole village's signals that never exposes any one person.
   - *Feasibility:* low-medium, because of the user caps and licence terms.

9. **World AgentKit** (World is an Agent Village partner)
   - Beta. A verified human registers an agent's wallet in AgentBook through World App. It extends x402 so services can apply per-human limits (`@worldcoin/agentkit`) (https://docs.world.org/agents).
   - The June expansion added support for Claude Code, Codex, Hermes and OpenClaw (https://thedefiant.io/news/infrastructure/world-launches-agentkit-to-let-ai-agents-carry-proof-of-human-backing).
   - *Magic moment:* "one human, one agent, one voice" in a village process, without revealing who anyone is.
   - *Feasibility:* medium. Real residents have to verify in World App on site.

10. **zkTLS / TLSNotary**
    - Still alpha (alpha.14). Proxy mode was added in April 2026, and the browser extension is unaudited.
    - One team (Peer) moved to TEEs and cut latency from about 30 s to under 1 s (https://tlsnotary.org/blog/).
    - *Magic moment:* an agent's claim about its human carries a receipt from the original source. This answers V1's fabrication failure directly.
    - *Feasibility:* medium. The user can reuse fermata and webproof.

11. **FHE**
    - Fhenix CoFHE is reported in production on Ethereum and Arbitrum; the report is undated (https://hackernoon.com/fhenix-launches-cofhe-on-ethereum-and-arbitrum-for-confidential-smart-contracts).
    - Zama mainnet reportedly launched in late Dec 2025 (https://blockeden.xyz/blog/2026/01/05/zama-protocol/).
    - *Magic moment:* two agents agree a price, time or split without either side's number being revealed.
    - *Feasibility:* medium, reusing batna-protocol. It is hard to make clear in 3 minutes.

12. **Agent payments**
    - x402 (Coinbase; V2 Dec 2025) and MPP (Stripe and Tempo, 18 Mar 2026, with session spending limits) (https://workos.com/blog/x402-vs-stripe-mpp-how-to-choose-payment-infrastructure-for-ai-agents-and-mcp-tools-in-2026).
    - Adoption figures are vendor-reported, and I couldn't verify them.
    - *Magic moment:* pay-on-proof, where money moves only when evidence arrives.
    - *Feasibility:* high, reusing fermata.

13. **Agent Village stack** (live, with real residents)
    - Index MCP, the EdgeOS API and the av-approval gate, which fails closed (https://github.com/Edge-City/agentvillage).
    - Mini-apps are reviewed manifests with "no arbitrary code upload", and "`MINI_APPS_MANIFESTS` is off in production" (https://github.com/Edge-City/agentvillage/blob/main/mini-apps/README.md).
    - *Magic moment:* the demo runs on residents' real agents, not personas.
    - *Feasibility:* medium. Build against it and open a PR. INFERRED: don't count on staff approving it within 54 hours.

14. **Generative media** (for the non-technical track)
    - ElevenLabs Video-to-Music API (Oct 19) and Lyria 3.5 full-length songs (Sep 3).
    - *Feasibility:* high, but it is the least frontier-pushing option here.

## (b) Winning-craft principles

1. **Domain closeness beats technical flash.**
   - Four of the five Opus 4.6 hackathon winners were not professional developers: a lawyer (CrossBeam, building permits), a cardiologist, a road-infrastructure specialist and a musician (https://claude.com/blog/meet-the-winners-of-our-built-with-opus-4-6-claude-code-hackathon).
   - Most Opus 4.7 winners built for fields they worked in.
   - Implication: build for a problem that a named resident or local business actually has.

2. **Show a number.**
   - Opus 4.7 winners cited pilots (Medkit: three medical faculties plus a pharma company) and evaluations against expert judgment (MaestrIA: 74% to 81%) (4.7 URL above).
   - Sim Francisco, second at a 12-hour build day, predicted 81.3% against an actual 83.8% (https://claude.com/resources/articles/meet-the-winners-of-our-claude-opus-4-8-build-day-hackathon).

3. **One working path beats ambition.** A judge of three July 2026 hackathons (https://dev.to/kurbaitaev/what-judges-actually-score-notes-from-a-year-of-hackathon-judging-3p4l):
   - The questions that decided scores were "Who is this for, specifically?", "What part did you build this weekend?" and "What breaks first at scale?"
   - The first 30 seconds largely set the score.
   - UI polish beyond readability, framework choice, team size and slides did not affect scores.

4. **Honesty is scored.**
   - Say plainly what works. Pre-fill data and mock slow API calls so the demo can't stall. This is from the JetBrains judges' notes; I saw it only in search results because the page returned 403 to me (https://blog.jetbrains.com/ai/2026/06/how-to-win-a-hackathon-notes-from-the-judging-table/).
   - Edge City Lanna required builders to say how much was actually built during the week (https://edgecitylanna.substack.com/p/get-ready-for-the-edge-city-lanna). This matters because the user is reusing prior repos.

5. **Typical rubrics.**
   - ETHGlobal: Technicality, Originality, Practicality, Usability, WOW factor (https://ethglobal.com/events/agents/info/details).
   - A Devpost-hosted event (Okta): creativity, implementation and potential impact, weighted equally (https://devforum.okta.com/t/what-are-the-judging-criteria-for-the-hackathon/15842).
   - Edge Lanna: prizes for the "biggest vision and potential tech or non tech", plus a creativity prize and a community vote (Lanna URL above).

6. **What this rubric will probably weigh (INFERRED).**
   - The criteria came from a session with NYU's Ethical Intelligence Lab (https://build.edgecity.live/events/india-buildathon). The same lab is an Agent Village partner (https://agents.edgecity.live/).
   - Expect weight on autonomy, consent, faithful representation and collective benefit.
   - The V1 write-up supplies vocabulary the judges will recognise (https://blog.cosmos-institute.org/p/we-gave-a-village-personal-ai-agents):
     - "As soon as an agent claims to know its principal, people need to see what it believes, where the belief came from, and how to correct it."
     - "Individual alignment did not automatically produce collective alignment."
     - "Preserving autonomy will require the ability for people to inspect and confirm agent judgments."
     - "Core utility drives adoption, and fun sustains experimentation."
     - V2 asks whether users can "understand, correct, withdraw, or ratify consequential actions."

7. **Popup-city precedent: builds that use the village itself.**
   - Esmeralda 2025 experiments included Harmonica (Polis-style dialogue), Fulcra's village wellness dashboard, an off-grid solar datacenter that residents contributed hardware to, and Ante crowdfunding the next village (Esmeralda review URL above).
   - The Esmeralda hackathon theme was "Tools for Human Flourishing". Judges included Ivan Zhao, Omri Amirav-Drory and Yasmin Razavi (https://luma.com/3uv27g5v ; https://longevityxplorer.substack.com/p/longevity-rewarded-at-edge-esmeralda).

## (c) Advice for a 54-hour build and a 3-minute pitch

**Timeline**
- **Wed 11:30–18:00:**
  - Go to the kickoff and ask Timour for the rubric and how the top 3 are chosen; the event page doesn't say.
  - Lock one user, one path and one number.
  - Recruit 3–5 consenting residents or Goan businesses, possibly through Ground Floor.
- **Wed night to Thu noon:** build the core path end to end.
- **Thu afternoon and evening:** sessions with real users. Log each one; the logs are your evidence.
- **Fri:**
  - Freeze features at 12:00 IST.
  - Record a 2–3 minute video; it is both the backup and the submission.
  - Write a README with a table of what was built 28–30 Oct versus what was reused.
  - Submit by about 16:00 and keep editing until 18:00.

**Assume the written submission is what gets you selected (INFERRED).** The top 3 are probably chosen before Demo Day, so the video has to work without you in the room.

**3-minute structure**
- 0:00–0:15: one sentence on what it is.
- 0:15–0:45: a real person's problem, in their words and with their permission.
- 0:45–2:00: live demo of one path, with the magic moment around 1:30.
- 2:00–2:30: evidence: number of users, one measured result, one failure you caught.
- 2:30–3:00: the safeguard (a human yes, the ability to inspect and correct) and what comes next: Devcon Mumbai 3–6 Nov, Edge City Bhutan 11–19 Nov.

**Other advice**
- **Put the ethics in the interface, not on a slide.** Show provenance on every claim, an approval tap and an undo.
- **The field is small and the pull elsewhere is strong (INFERRED).** Only 2 teams were registered as of today. Hacker House Goa runs in parallel with $50K in AI and crypto bounties (https://edgecityindia2026.substack.com/p/programming-preview-for-edge-city). Stand out by putting the community first rather than chasing bounties.
- **Don't trust the wifi.** Have a local fallback, label cached responses as cached, and pin model IDs.

## (d) Pitfalls

1. **Over-scoping.** Even V1's live onstage setup failed (Cosmos URL above). Cut to one path.
2. **Fake data shown as real.** V1's headline failure was agents making things up about their people. A demo that invents a resident's views defeats itself. Label synthetic data on screen.
3. **Recording people.**
   - India's DPDP Rules were notified on 13 Nov 2025. Consent-manager rules apply from 13 Nov 2026 and full consent duties from 13 May 2027 (https://www.hoganlovells.com/en/publications/indias-digital-personal-data-protection-act-2023-brought-into-force-).
   - Always-on wearables are running into wiretap-law and bystander concerns (https://tech-insider.org/ai-wearables-wiretap-law-limits-2026/). WIRED found the Friend pendant alienated people around its wearers (https://getcoai.com/news/wired-tested-the-129-ai-necklace-that-alienates-users-and-fails-technically).
   - Use explicit opt-in, process on-device or temporarily, and never capture bystanders.
4. **Wearable licence traps.** Oura's terms reportedly restrict AI processing, and developer apps are capped at 10 users (tryterra URLs above).
5. **"AI wrapper" fatigue.**
   - Judges ask whether a project is a "novel use of AI, or another chatbot wrapper" (https://www.masaischool.com/blog/how-to-win-an-ai-hackathon-in-2026-full-guide/).
   - "AI chatbot for X" tops one list of ideas judges are tired of (https://blogs.reskilll.com/hackathon-ideas-that-won-2026-judges-actually-pick-examples/).
   - Answer it with verifiability, value for several people at once, or a measured outcome.
6. **Crypto skepticism.**
   - 63% of US adults have little or no confidence in crypto (Pew, survey from Feb 2024: https://www.pewresearch.org/short-reads/2025/04/10/majority-of-americans-arent-confident-in-the-safety-and-reliability-of-cryptocurrency/).
   - Lead with the human outcome. Use a chain or proof only where it removes a trust assumption you can name, and keep wallets off screen.
   - Have an answer ready on World's regulatory history (https://emelia.io/hub/world-agentkit-proof-of-human).
7. **Agents acting without a human yes, or draining shared resources.** Both happened in V1: Sims voted without their owners ratifying, and agents used up shared credits. Use approval gates and rate limits. INFERRED: don't flood residents' agents during the build.
8. **Relying on unreleased infrastructure.** Mini-apps need staff review, TLSNotary is pre-1.0 and unaudited, AgentKit is in beta, and Cartesia stops hosting Line agents on 1 Dec 2026.
9. **A sales pitch.** Edge norms say to avoid sales-focused behaviour, so pitch the benefit to the community, not a fundraise.

**Gaps:** I found no public source for resident credits. Nothing public shows what the NYU session produced.