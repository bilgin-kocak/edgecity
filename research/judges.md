# R2 report: who judges the Edge India Buildathon, the likely rubric, and what this jury rewards

## (a) Verified facts about the rubric process

- **No rubric has been published.** The live buildathon page (fetched 27 Oct) still says: "The community explored the judging criteria in an AI-assisted session with NYU's Ethical Intelligence Lab. The final rubric and the prize split will be published separately." The prize table says "final adopted rubric and distribution published separately." No judges are named. The page also says "Organizers award the prizes and publish the results" (Sat 31 Oct, 20:00) and "Every build and team goes public with the results." "Submission instructions will follow before the deadline." https://build.edgecity.live/events/india-buildathon
- **Searches for the rubric found nothing.** I checked the Edge City India Substack archive (latest post 9 Oct), the Agent Village repo (its code and docs, plus the first 25 of 518 PR titles), web, X, LinkedIn and Notion. None of them mention the session, the criteria the community proposed, or a rubric. https://edgecityindia2026.substack.com
- **The NYU Ethical Intelligence Lab is real.** It is run by Sydney Levine (Assistant Professor, NYU Psychology; part-time Visiting Research Scientist at Google DeepMind; formerly Allen Institute for AI). It officially opened at NYU in Jan 2026. Members: Logan Walls (postdoc), Julien Lie-Panis (visiting postdoc), Ziyi Meng (lab manager), and PhD students Misha O'Keeffe and Ben Sterling. Mission: "characterize the human moral mind in computational terms" and build AI that is safe, transparently aligned and supportive of human flourishing. https://www.ethicalintelligencelab.org/team , https://www.ethicalintelligencelab.org/home , https://sites.google.com/site/sydneymlevine/ . (A different "Ethical Intelligence" consultancy exists; it is unrelated.)
- **The lab runs a live experiment in Agent Village.** Lab news for Oct 2026 says "MoralMod was deployed in the Agent Village at EdgeCity India." The paper is "MoralMod: An auditable & steerable moral module for AI systems" (Walls, Chiu, Collins, Tenenbaum, Leshinskaya, Levine; COLM 2026 Lifelong Agents workshop): https://www.ethicalintelligencelab.org/publications . In the repo, MoralMod is a randomized arm (`AV_MORALMOD_ARM=on|off`). For ON residents it replaces the Index Network negotiator, under a `DECISION_EXPERIMENT_ID`, and "NYU supplies the exact release." https://github.com/Edge-City/agentvillage/blob/main/docs/moralmod_lifecycle.md . Agent Village lists Sydney Levine and Logan Walls as collaborators. https://agents.edgecity.live/
- **The lab's core frameworks:**
  - Resource-Rational Contractualism: AI should approximate "agreements that diverse stakeholders would endorse" using cheap heuristics. https://arxiv.org/abs/2506.17434
  - Virtual bargaining, i.e. what both parties would agree to. https://doi.org/10.1016/j.cognition.2024.105790
  - Universalization ("what if everyone did that"). https://doi.org/10.1073/pnas.2014505117
  - Pluralism. MoReBench grades the reasoning process, not only the conclusion, with expert rubric criteria "essential to include (or avoid)." https://morebench.github.io/
  - "Intuitions of compromise" (Cognition).
  - "Why We Should Crowdsource AI Ethics (and How to Do So Responsibly)" (Levine & Awad, 2020). https://behavioralscientist.org/why-we-should-crowdsource-ai-ethics-and-how-to-do-so-responsibly/
- **The village has a precedent for AI-assisted collective decisions.** A "Village constitution" was set by resident vote. In the authors round, 30 statements were rated blind: 15 written by residents' agents and 15 by ODIN, the "village god agent." Ballot text: "Private: only you and the research team see your ratings." It closed Sun 25 Oct. ODIN's instructions say it knows about "the lab, the vote, the hackathon." https://github.com/Edge-City/agentvillage/blob/main/docs/GODCONST-TELEGRAM-BALLOT.md , https://github.com/Edge-City/agentvillage/blob/main/workspace/odin/SOUL.md
- **How earlier Edge City hackathons were judged:**
  - Edge Esmeralda 2024: theme "Tools for Human Flourishing." Rule: "Each winning entry should embody the spirit of human flourishing." You could demo anything "built or meaningfully progressed" at the village but had to say how long you had worked on it. Judges were mostly investors and founders (Ivan Zhao, Justin Mares of Long Journey, Yasmin Razavi, NFX, Aztec, Bun, 1517). Hosts: Zelda Poem and Timour Kosters. No published rubric. https://edgecity.notion.site/Edge-Esmeralda-Final-Demo-Hackathon-Saturday-June-29th-799ceb44de364dfeb57a4bf0e3f066a6 , https://luma.com/3uv27g5v
  - Edge Lanna 2024: main prizes went to "the biggest vision and potential tech or non tech." There was also a $1K Community Prize decided by community vote and a $1K Most Creative Project prize. Builders had to disclose how long they had worked on the project. https://edgecitylanna.substack.com/p/get-ready-for-the-edge-city-lanna , https://edgecitylanna.substack.com/p/announcing-the-edge-city-lanna-hackathon
  - I found nothing published for Edge Patagonia or Edge Esmeralda 2025/2026.
- **Competition context.** Two teams were registered as of 27 Oct (buildathon page). Hacker House Goa runs in parallel (Oct 28–31, $50K bounties, 247 builders, on-site judges plus visitor voting) and will pull builders away. https://x.com/JoinEdgeCity/status/2092681113789411697
- **The Savlar MCP has nothing on this jury.** It indexes only 4 AI podcasts: Dwarkesh, Latent Space, MLST and No Priors. Searches for Timour Kosters (no identified speaker), Edge City, Zuzalu, network state, society incubator and Cosmos Institute returned no matching claims. The only tangentially related quotes are on agent-to-agent interaction (e.g. Rune Kvist: "you'll start to see true agent to agent interactions that are not mediated by humans": https://podcasts.beehiiv.com/3967c1f2-cb97-4eb0-a5c0-21a1d2579408/01a15fdf-0e93-7e1a-880d-d73752a1f915/01a15fdf-707a-7768-8014-cca95e62c689/01a15fdf-748f-7fd0-9052-e2b71649f20c.mp3#t=3471). Not useful for judge profiling.

## (b) Predicted rubric (INFERRED, not published)

**What the prediction rests on:**
- The criteria came from a community session run by a moral-cognition lab. That lab's method is crowdsourced, pluralistic, process-graded rubrics with things that must be included or avoided (MoReBench).
- The word "adopted" suggests the residents voted on the criteria, as they did for the constitution.
- Edge City's own values and the "helps the community" wording on the page.
- Past Edge prizes centred on human flourishing, "vision and potential," community vote and creativity.
- Timour's demonstrated habit of eval-driven checking (see c).

| # | Dimension (INFERRED) | Weight | What a top score likely looks like |
|---|---|---|---|
| 1 | **Benefit to people / the community** (flourishing, helps Edge India residents and/or the Goan host community) | 25% | Named real users this week. A concrete before/after. Serves locals, not only visitors. |
| 2 | **Ethics in the design** (consent, privacy, honesty, human autonomy, a human yes for consequential acts, no manipulation, fairness to people affected) | 20% | Safeguards are built into the mechanism, not added as a disclaimer. Considers all affected parties, not only the user. |
| 3 | **Built and working** (built or meaningfully progressed in the window; live demo) | 20% | Live, not a mock-up. Prior work disclosed honestly. |
| 4 | **Originality / "Push the Edge" / interesting** | 15% | A new idea someone could only have built at this village, this week. |
| 5 | **Co-creation and inclusiveness** (multidisciplinary, accessible to nontechnical people, helped others) | 10% | Residents or locals shaped it. Nontechnical people can use it. |
| 6 | **Continuation and openness** (open source, documented, others can build on it, plugs into village infrastructure) | 10% | MIT licence, a README with limitations, a path to Bhutan (11–19 Nov) or the Agent Village. |

There may also be a separate community or audience vote, given the Lanna precedent and the community-authored criteria (INFERRED). Expect the rubric to be published around kickoff (Wed 11:30) or before the deadline (INFERRED). **Action: re-fetch the buildathon page on Wed morning, ask Timour at kickoff, and ask ODIN or your own agent, since ODIN is briefed on "the hackathon."**

## (c) Likely judges (none confirmed; "organizers award the prizes")

**Timour Kosters, co-founder.** He runs the kickoff and co-hosted the Esmeralda 2024 hackathon. Very likely a judge (INFERRED).
- Background: Artsy, Kama (health tech), Impact, partner at Seed Club Ventures, founder of the experiential agency Excetera. https://www.edgecity.live/about
- He frames Edge City as a "society incubator": 7 villages, 11,000+ participants, $1M in grants, 50+ startups. https://www.castfox.net/podcast/edge-city-7020458/episode/the-story-and-impact-of-edge-city-in-5-min-timour-kosters-the-network-state-conference-2025-423975
- He traces popup cities back to salons, Chautauqua, Black Mountain College, Santa Fe Institute and Burning Man. https://wiki.p2pfoundation.net/Timour_Kosters_on_the_Lineage_of_Web3_Popup_Cities
- He is the first author of the V1 Agent Village write-up with Harry Law and Ivan Vendrov. Its stated test of success: "The measure of success is whether agents enable us to live more fulfilling, human lives." It warns "Individual alignment did not automatically produce collective alignment." It argues for "cosmos vs. taxis" (order that emerges from decentralized interaction) and says "people need to see what it believes, where the belief came from, and how to correct it." https://blog.cosmos-institute.org/p/we-gave-a-village-personal-ai-agents
- He is personally rigorous about evals. He proposed the 20-question eval, where each answer has must_include and must_not lists and is scored on whether it is grounded, safe and cited. https://github.com/Edge-City/agentvillage/blob/main/docs/evals/edge-india-village-20.yaml . He and Carter grade a ~200-item labelled set, constructed bad actions included ("an intention the resident never stated"), and sign evidence gates judged "by the Wilson 95% bound, not the point estimate." https://github.com/Edge-City/agentvillage/blob/main/docs/design/judge.md
- **Taste (INFERRED):** measured outcomes, refutation, honesty, agents as faithful representatives.

**Janine Leger, co-founder.** Drove Zuzalu Montenegro and ZuConnect, led Gitcoin's public goods funding workstream, and built popup co-living communities. https://www.edgecity.live/about . **Taste (INFERRED):** public goods, community governance, things a community actually adopts. I found no podcast transcript in this session. A Leger and Kosters co-founders episode is listed but unconfirmed (https://player.fm/1BFKPkK).

**NYU lab (Sydney Levine, Logan Walls, possibly others)** ran the criteria session. Whether they judge is unknown.
- Levine's agenda: align AI "with the plurality of human moral values" while staying interpretable and steerable.
- **Taste (INFERRED):** contractualist agreement (would all affected parties endorse this?), universalization (what if every agent did this?), pluralism, and a reasoning process you can inspect.
- Walls: resource-rational moral reasoning, MoralMod. Meng: "how institutional design can support" human–AI cooperation. Sterling: norms and institutions. Lie-Panis: large-scale cooperation, game theory. https://www.ethicalintelligencelab.org/team

**Cosmos Institute (Harry Law, principal researcher; Ivan Vendrov).** Possible judges or advisers (INFERRED).
- Cosmos pillars: "Truth-seeking (the ability to inquire openly and correct our errors)," "Decentralization (systems that resist coercion, capture, and control)," "Human autonomy (the cultivated capacity for self-direction)." https://www.cosmos-institute.org/faq
- Philosopher-builders treat "what should I build for?" as their first duty.
- "we must build AI that encourages inquiry over complacency." https://blog.cosmos-institute.org/p/introducing-the-cosmos-institute
- Harry Law's role: https://worksinprogress.co/our-authors/harry-law/

**Agent Village builders (Carter Crouch, the engineering owner; Amita Shukla; Jonathan Miller; Index Network's Seref Yarar and Seren Sandikci).** Possible judges (INFERRED). Their docs show a culture of fail-closed approval gates, reviewed mini-app contracts, and never presenting a model's decision as a human grant. https://agents.edgecity.live/ , https://github.com/Edge-City/agentvillage

**Partner and sponsor guests (Microsoft, Long Journey, Protocol Labs, Sarvam, ElevenLabs).** Unknown. Long Journey's Justin Mares judged in 2024.

## (d) Signals for this jury

**Signals that win (INFERRED, each tied to evidence above):**
1. **Measured real-world outcome during the window.** Real residents or Goan locals used it, with numbers and a funnel. This mirrors Agent Village's "verified useful outcomes for each intention."
2. **Fixes a named V1 failure mode with a mechanism plus evidence.** The failure modes are agents fabricating facts about their people, attributing ideas they never had, depleting shared resources, and fund decisions without a final human yes. Show an eval with must and must-not cases, a labelled set that includes constructed bad actions, and a refutation section. This is exactly how Timour works.
3. **Agreement-based design: act only on terms all affected parties would endorse.** It maps one-to-one onto Levine's contractualism and virtual bargaining. Shared-resource depletion is literally a universalization problem. Bilgin's batna-protocol (privately finding agreement without revealing reservation prices) is the closest existing asset.
4. **Inspectable, correctable, revocable.** People can see what the system believes, where the belief came from, and how to correct it, with consent and withdrawal built in.
5. **Plugs into village infrastructure without contaminating the MoralMod randomized arms.** For example a mini-app under the builder contract, a skill, or a read-only evidence layer. This gives continuity and shows respect for the research.
6. **Honest documentation.** Disclose prior work and time spent (both Esmeralda and Lanna required this) and state limitations and failures. Sealed or pre-registered predictions (the arcminute style) fit the "truth-seeking" ethos.
7. **Legible to nontechnical judges and the audience.** A 90-second human story beats architecture slides, and the buildathon explicitly invites artists and community organizers.
8. **Serves the host community** (Ground Floor's Goan businesses) and is multigenerational, which fits Edge City values. https://www.edgecity.live/india26

**Signals that lose (INFERRED):**
1. Agents taking consequential actions (money, messages, sign-ups) without a human yes, or a model decision presented as a human approval.
2. Any fabricated or inflated claim in the demo. This jury studies fabrication professionally.
3. Sales or token-first pitches. Edge City norms say to avoid sales-focused behaviour.
4. Profiling residents, using the directory or private context without consent, or wearables surveillance.
5. A moralizing "AI grades your ethics" product. It conflicts with pluralism and autonomy.
6. A generic chatbot or wrapper, or a pre-built project with a thin new layer and no disclosure.
7. Interfering with the running experiments, i.e. the negotiator or MoralMod arms.
8. Ignoring Goan locals, or building something extractive.

## (e) The one sentence a winning pitch should make true

"This week, real Edge India residents used it to get something done together. Their agents acted only on terms everyone affected could see, correct and would have agreed to. Here is the measured evidence, including where it failed."