> Battle plan and red-team report from the workflow, written before the final fact-check pass. Where this file and [IDEAS.md](../IDEAS.md) differ, IDEAS.md is the corrected version.

# Proxy Test: does your agent know you better than your friend? (S3, agg 6.3)

VERDICT: FIXABLE. The five fatal flaws are protocol bugs, and each one is fixed below.

## 1. Proxy Duel: does your agent actually know you?
Before you answer 30 quick village questions, four proxies seal a guess about you: your Agent Village agent, the same model with no memory of you, the crowd, and optionally a friend. The seals open, and you fix what your agent got wrong.

## 2. Why it wins
- **It answers V2 question 06**, "Do agents beat people at this?", in Timour's own terms: "Honest predictions, written down before… so we can be wrong in public."
- **It completes PR #335 instead of rivalling it.** It runs #335's MIT `prediction_prompt` and adds the human and no-memory baselines that the lane lacks.
- **Its headlines survive a small n:**
  - "Did memory beat the same model without it?"
  - "X% of predictions above 0.8 confidence were wrong."
- **Predicted rubric:** the ethics sit in the mechanism, real residents use it, and the benefit is counted (how many agents were corrected). It is MIT with a verifier.
- **Hooks:**
  - The NYU lab (Levine, Walls) studies individual judgment.
  - Cosmos asks for "inspect and confirm agent judgments".
  - Carter's evals use dumb baselines.

## 3. 90-second demo
- **0:00** "Your agent has watched you for 2.5 weeks. Does it know you better than your friend does?"
- **0:10** A QR code links to Thursday's seal (a Telegram channel post plus OpenTimestamps). "Locked before anyone answered."
- **0:20** **Live duel.** Resident A and friend B are on stage. On Thursday, A's agent memory (the Context lane) and B sealed their predictions on three low-stakes items. The room votes by hand on who will be right.
- **0:35** Each seal opens after A answers. **The room reacts on the item where a proxy was most confident.**
- **1:00** The real aggregate: n, the memory gap with its 95% CI (said aloud even if inconclusive), and the confident-wrong rate.
- **1:20** "N residents fixed their agents. MIT, offered to the #335 team."

## 4. Real vs mocked
- Everything shown is real: residents, replies, seals and scores. Synthetic data appears only in test fixtures.
- Disclosed limitations:
  - The Context lane uses the Context-page text, not MEMORY.md.
  - The fleet model is unconfirmed. If it stays unconfirmed, the build uses `openai/gpt-6-luna` and says so.
  - The duel uses the Context lane, because the resident would see a live reply first.

## 5. Architecture and stack
Each session takes 5 minutes:
1. **Consent and inputs.** The resident consents and writes a short bio. Optionally, they paste their "What your agent knows" text and name a friend, who predicts via a separate link.
2. **Two prediction lanes, sealed before answering:**
   - Context lane: the #335 prompt, with no tools, on the fleet model via OpenRouter.
   - Cold lane: the same model, given only the bio.
   - Predictions are salted and hashed. The Merkle root goes to the channel and to OpenTimestamps **before the answer page unlocks**.
3. **The resident answers 30 items**, and the answers are committed immediately. 24 are practical and 6 are split value items. None touch the constitution, the referendum or MoralMod.
4. **Live-agent lane:**
   - The resident sends their agent a fixed prompt in a fresh session: "Quiz only. Do not save to memory or record intentions", plus a nonce.
   - They forward the reply to the bot. `forward_origin` proves which agent bot sent it and when.
   - Only the first reply after the nonce counts.
5. **Crowd lane:** a leave-one-out crowd prediction, computed after close.

**Scoring:**
- Measures: accuracy, Brier, calibration, confident-wrong rate and abstentions.
- Intervals: person-clustered bootstrap CIs.
- Normalisation: a Friday test-retest on 10 items.
- Target: n=25, which gives about 60% power for a 6-point gap.

**Stack:** FastAPI, SQLite, server-rendered pages, python-telegram-bot, OpenRouter, opentimestamps-client and numpy/scipy.

**Reused:**
- arcminute: commit-reveal, rival predictors.
- harness-lab: config hashes, verifier.
- ns-steward: the bot.
- dress-rehearsal: a fake agent bot for tests.

## 6. Hour by hour (IST)
**Wed 28**
- 11:30–13:00: kickoff and the asks in §7.
- 13:00–16:00: items, consent and prompt. Pilot with 3 residents (one nontechnical).
- 16:00–21:00: commit service, channel, forwarding bot and answer page.
- 21:00–24:00: Context and cold lanes. Timestamp the pre-registration (hypotheses, MDE, headlines, exclusions).

**Thu 29**
- 09:00–18:00: session waves at The Circle, target n=25.
- 14:00: seal the duel items.
- 18:00–22:00: reveal pages and dashboard. If n<15, add Friday-morning sessions.

**Fri 30**
- 08:00–10:00: retest and the last sessions.
- 10:00: reveal, score, and verify from a clean clone.
- 11:00: send results privately to Timour and Carter.
- 12:00: freeze. Video until 14:30, README until 16:00, then submit. Edits are allowed until 18:00.

**Cut line, in this order:**
1. Friend lane.
2. Test-retest.
3. OpenTimestamps.
4. Live-agent lane. Context against cold still answers the memory question.

**Never cut:** seal-before-answer, consent, the leave-one-out crowd, honest n.

## 7. Day-1 asks
- **Timour Kosters:**
  - The rubric and how the top 3 are chosen.
  - Whether a #335 referendum runs 28–31 Oct. If it does, offer sealed friend, crowd and cold baselines for a joint scoreboard.
  - Agreement to run, with results shown to him first.
- **Carter Crouch:**
  - Which model the fleet runs.
  - Whether a quiz-only prompt still writes MEMORY.md or ambient intentions.
  - Any conflicts with MoralMod or GC-ELICIT.
- **Sydney Levine or Logan Walls (NYU lab):** a 20-minute review of the items and the consent text.
- **Teammate post:** "Proxy Duel: does your agent know you better than your friend? Seeking one on-site facilitator, Thu–Fri, to run 5-minute consented sessions and the Demo Day duel. No code needed. Co-credit."

## 8. Safeguards
- **Framing and consent:**
  - Framed as a consented community game, not research.
  - Consent is specific to this study, and the friend consents separately.
  - Participants are told the quiz enters their Agent Village conversation.
  - No one takes part during an open referendum.
- **Data handling:**
  - Context text and bios are processed ephemerally.
  - Raw data is deleted by 1 Nov.
- **Publication:**
  - Only aggregates are published, with no subgroup or MoralMod-arm splits.
  - No one is asked which arm they are in.
  - Friends see only the aggregate.
- **Host community and media policy:**
  - No items about Goans, local spending or politics.
  - No recording.
  - Duel participants consent to be on stage, per the media policy.

## 9. Submission
- **Description:** a built-versus-reused table, results with CIs, limitations, and prior art (Youyou 2015; Park et al. 2024).
- **Video:** 2:30.
- **MIT repo:**
  - The pre-registration as the first commit.
  - `verify.py`, which recomputes the roots and checks the OTS proofs and channel timestamps.
  - The scoring notebook.
- **Image:** a calibration chart with the seal QR.

## 10. Risks
- **Low n:** the friend is optional, there is a Friday catch-up, and the MDE is reported.
- **Overlap with Agent Village's own work:** offer the joint scoreboard and credit #335.
- **Memory contamination:** use the quiz-only prompt and get Carter's check. Failing that, run only the Context and cold lanes.
- **Coaching or refusals:** refusals count as abstentions. The clean Context lane is the primary comparison.
- **Wifi:** results are cached and the verifier runs offline.

## 11. Solo/team, Goa/remote
Being in Goa is effectively required, because recruitment, the sessions and Demo Day at Riva are all in person.
- **Solo in Goa:** feasible. The build is about one day, with sessions on Thursday.
- **Remote:** works only with an on-site facilitator.
- **Best setup:** the builder plus one facilitator.

## Red team
```json
{
 "id": "S3",
 "verdict": "fixable",
 "fatal_flaws": [
  "The agent arm is contaminated by the order of steps. The resident pastes the dilemmas into their own agent and pastes its reply back before answering. They therefore read their agent's prediction first (anchoring), and they are the only link between agent and page, so they can edit or re-roll the reply. The SHA-256 seal guards against the builder, but the leak runs through the resident. As written, this inflates agent accuracy, and any 'agents beat friends' result will be dismissed on stage.",
  "The seal timing contradicts itself. The description says the Merkle root is committed before the resident answers, but the build plan says 'Commit roots nightly'. Thursday's predictions would be committed Thursday night, after the answers, so the seal proves nothing for same-day sessions. GitHub commit dates do not rescue it: git lets the author set them with --date and GIT_COMMITTER_DATE (https://git-scm.com/docs/git-commit).",
  "The inner-state ping arm cannot be built without fleet access. Telegram says 'bots will not be able to see messages from other bots regardless of mode' (https://core.telegram.org/bots/faq), so a Proxy Test bot cannot ask the resident's agent bot for a sealed guess before each ping. The resident would have to ask their own agent six times a day. That leaks the guess to them, as in flaw 1, and adds a heavy burden. Cut this arm.",
  "The core novelty claim is not true as stated. Timour's own draft PR #335 (opened 14 Oct) already contains what its code calls 'the sealed prediction lane'. Its prompt reads 'Predict this resident's preference before they see the referendum. This is research only.' It enforces sourceCutoffAt <= frozenAt, runs with an empty toolset, outputs probabilities, confidence, abstention and evidence, and records promptSha256 and sourceSha256 (https://raw.githubusercontent.com/Edge-City/agentvillage/codex/referendum-runtime/plugins/av-events/referendum_predict.py). The public PR text mentions no scoring, but its companion PRs sit in private repos (agentvillage-app #238), so 'nothing scores those predictions' cannot be verified and is probably wrong (INFERRED). A pasted Telegram prompt is a weaker copy of the likely head judge's own leak-free design.",
  "The power is too low for the headline to hold whichever way it lands. I simulated 12 binary items with person-clustered bootstrap (INFERRED assumptions; script at <research-scratch>/s3_rt/power.py). With n=15 and a true friend-agent gap of 6 points, the 95% CI resolves the gap only about 27% of the time, and the CI is about 0.19 wide. With n=10 it resolves about 23% of the time. The most likely outcome is 'inconclusive', which is not a headline."
 ],
 "serious_risks": [
  "Recruitment carries the whole project. Each participant needs an active Agent Village (AV) agent, 10 minutes and a consenting friend, during the busiest week: the Buildathon, Hacker House Goa, Project Odin, build3 and Demo Day all fall on 28 to 31 Oct. A remote builder cannot recruit or run sessions, so `needs_physical_presence: false` is effectively wrong. An on-site facilitator is required, and a top-3 finish means presenting in person at Riva on 31 Oct.",
  "Agents probably know too little to beat a cold model. V1 had 4,866 resident messages across 239 agents, about 20 per agent over four weeks (https://blog.cosmos-institute.org/p/we-gave-a-village-personal-ai-agents). Park et al. found that demographics-only agents already reach 74% of test-retest, against 83 to 86% for interview-grounded ones (https://arxiv.org/abs/2411.10109). Expect agent \u2248 cold model \u2248 crowd, which is a null that judges can predict.",
  "The baselines are confounded as specified. (1) The cold model is Claude Sonnet 5.5, while the agent runs whatever model the control plane sets, with openai/gpt-6-luna as fallback (README line 292). Any gap mixes model differences with memory. (2) If the crowd majority includes the resident's own answer, that answer leaks into the baseline; it must be leave-one-out. (3) Without a test-retest ceiling, accuracy cannot be interpreted, because humans are not fully self-consistent (Park et al.).",
  "It may contaminate the organizers' own research. #335's lane reads SOUL.md, USER.md, MEMORY.md and similar files modified before the cutoff. A 12-dilemma session about values can lead the agent to write memory notes, which would then feed future #335 referendum predictions on the same topics (shared resources, local spending). The nightly memory-signals pass also wakes after 3 or more resident messages and may record an 'ambient' intention (skills/index-network/prompts/memory-signals.md). All of this is INFERRED risk.",
  "It overlaps planned NYU and AV studies on the same cohort. The V2 proposal says 'Planned studies cover representation accuracy, use of corrections\u2026' and 'Additional studies are being prepared to compare human coordination with agent-assisted coordination, representation\u2026' (https://edgecity.notion.site/Research-Partner-Proposal-Agent-Village-V2-at-Edge-City-India-Shared-3c1d45cdfc5981d7b7bac1e216f3678b). An outsider running a quick version on the same participants can look like pre-empting or contaminating their pool.",
  "The moral-dilemma items fall squarely in the jury's own field. Without a lab co-author, 12 builder-written 'neutral' items will likely be leading, double-barrelled or near-consensus. Near-consensus items hand the crowd baseline the win and make the comparison uninformative.",
  "The benefit to the community is weak. It serves Agent Village's research question, not residents' lives or the Goan host community. On the predicted 'benefit to people' and 'host community' dimensions it scores low unless reframed.",
  "The stage payoff is a dashboard. Bars, Brier scores and a Merkle root mean little to nontechnical judges, and small n makes them soft.",
  "The parsing is fragile. AGENTS.md tells agents to give 'a lean\u2026 say it is your guess', not strict JSON, so free-text replies pasted by hand will vary. The agent may also call tools such as query_village (main-group messages) and cite other residents.",
  "The token-budget claim is mis-cited. Issue #100 (HTTP 402 from the heartbeat cron, about 57k input tokens per turn) dates from 15 June 2026, the Esmeralda era, not India (https://github.com/Edge-City/agentvillage/issues/100). One prompt per resident costs little, but the cited evidence is stale."
 ],
 "competition_or_duplicates": [
  "PR #335, 'Add scoped referendum adapters to the Hermes runtime' (timkosters, draft, 14 Oct). Its 'sealed prediction lane' makes tool-free, cutoff-aware, hashed preference predictions with abstention. This is the agent arm of S3, built better by the likely head judge (https://github.com/Edge-City/agentvillage/pull/335).",
  "The 'What your agent knows' Context page is already shipped. The agent's USER.md entry, marked (guess) or (chat), plus a 'Removed by you' correction list, is shown to the resident (skills/index-network/tools.md line 136; PR #250 by timkosters, merged 8 Oct). It largely duplicates S3's 'inspect and correct' card.",
  "The MoralMod Decisions tab. 'Participants with MoralMod ON and approved research consent can inspect and correct their own assessments in the Decisions tab' (https://agents.edgecity.live/research-register). NYU already runs representation-and-correction tooling.",
  "Mosaic, added to the register on 22 Oct, 'write[s] an AI summary of you, adds what it learns to your agent's Context' (https://agents.edgecity.live/research-register). The AV team owns another layer of 'agent believes X about you'.",
  "Planned NYU and AV representation-accuracy studies, plus the 'Representation accuracy' metric on the safety dashboard (research proposal URL above).",
  "V1 Simocracy, where Sims voted and owners judged and corrected them: one 'did vote pretty much how I would have', another corrected one vote (https://blog.cosmos-institute.org/p/we-gave-a-village-personal-ai-agents).",
  "Prior art that settles the general question. Algorithms beat friends at judging personality, r=0.56 against 0.49 (Youyou, Kosinski & Stillwell, PNAS 2015, https://pmc.ncbi.nlm.nih.gov/articles/PMC4313801/). Interview-grounded LLM agents reach 83 to 86% of test-retest (Park et al., https://arxiv.org/abs/2411.10109). Only the in-situ, deployed-agent angle is new.",
  "No AV PR titles match 'predict' or 'representation' (GitHub title search returned 0). The NYU repo edge-city-nyu covers allocation rules only, with no prediction scoring (https://github.com/The-Cybernetic-Society/edge-city-nyu).",
  "Hacker House Goa and other in-village projects are NOT VERIFIED. The web search budget ran out, so I could not check them."
 ],
 "ethics_and_consent_pitfalls": [
  "The pasted prompt and the agent's reply become part of the resident's AV conversation. Under their AV consent, that conversation can be research data, and NYU training data if they opted in ('NYU may receive selected, de-identified agent conversations\u2026', https://agents.edgecity.live/research-register). Participants must be told, and the study needs its own consent: the register notes 'A workshop asks for separate study-specific consent.'",
  "There is no IRB or protocol, yet it is presented as a 'pre-registered study' to a moral-psychology lab whose own studies remain 'subject to its protocol, consent, and applicable institutional review'. Frame it as a consented community game or demo, not research, unless the AV team or NYU adopts it.",
  "The friend's predictions are third-party personal data. If a friend sees item-level scores, they can work out the resident's moral answers. Show friends only an aggregate score, and only with both people's consent.",
  "Village aggregates can identify people. In a village where participants and friend pairs are known, n\u22655 is a weak threshold. Avoid per-subgroup breakdowns, and never break results down by MoralMod arm; asking residents their arm could also break the experiment's blinding.",
  "The 'cold model sees a public profile' arm must not scrape LinkedIn or the directory; partner keys cannot read the directory anyway. Use a bio the resident writes, with consent.",
  "If residents export their Context or Mosaic summary for a #335-style lane, that is sensitive data. Process it ephemerally, delete it by 1 Nov, and never log it.",
  "The inner-state pings collect mood and energy data six times a day, which is health-adjacent and surveillance-flavoured. Drop them.",
  "Pasted dilemmas can plant value-laden 'memories' or ambient intentions in residents' agents. The prompt must say 'quiz only: do not save or record anything', and the resident should run it in a fresh session.",
  "A public 'AV agents lose to a cold model' number about the organizers' flagship experiment needs a heads-up to Timour and Carter first. Every build 'goes public with the results' (https://build.edgecity.live/events/india-buildathon).",
  "Items about 'local vs visitor spending' and Goa are answered only by visitors. Avoid reporting results that read as a verdict on the host community."
 ],
 "likely_judge_criticisms": [
  "Timour, or anyone from the AV team: 'My PR #335 already is a sealed prediction lane, tool-free and cutoff-aware. Yours pipes a pasted prompt through a chatty agent with tools, with the human in the middle reading its answer first. What did you measure?'",
  "'n=15 with confidence intervals of plus or minus 9 points. Your headline is noise.'",
  "An NYU lab member: 'Who validated these dilemmas? Several are leading or near-consensus. Where is your test-retest ceiling?'",
  "'We already know Facebook Likes beat friends (Youyou 2015) and interview-grounded agents reach about 85% of test-retest (Park et al.). What is new besides the location?'",
  "'Your seal was committed nightly, after people answered, and git commit dates can be set by hand. The cryptography is theatre.'",
  "'Hypothetical dilemmas are not representation. Agents represent people in consequential choices: votes, RSVPs, funds.'",
  "'The inspect-and-correct card already exists. It is the Context page, \"What your agent knows\", and the MoralMod Decisions tab.'",
  "'How does this help a resident or a Goan this week?'",
  "'Did you just plant 12 moral dilemmas into the agents' memory in the middle of our experiment?'",
  "'The friend arm: these people have known each other for two weeks.'"
 ],
 "fixes": [
  "Reverse the order. (1) The resident answers first, and the answers are committed immediately and hidden. (2) Only then do they send the fixed prompt to their agent. (3) They forward the agent's reply to the Proxy Test bot instead of pasting it. Telegram's forward_origin carries sender_user and the original date (https://core.telegram.org/bots/api#messageoriginuser), which proves the reply came from their agent bot after a session nonce. Count only the first reply after the nonce, so re-rolls do not count.",
  "Commit per session, not nightly. Push the salted Merkle root before the answer phase opens: OpenTimestamps plus a post to a public Telegram channel, whose dates are set by Telegram's server. Put a QR code of the root on screen so anyone can verify it.",
  "Cut the inner-state ping arm and the camera arm entirely.",
  "Become #335's human-baseline arm instead of a rival agent predictor. At kickoff, ask Timour whether a referendum runs Oct 28\u201331 with the sealed lane on. If one does, offer to collect sealed friend, crowd (leave-one-out) and cold-model predictions on the same questions before the vote, and to publish a joint scoreboard. That answers V2 question 06, 'Do agents beat people at this?', for their real system.",
  "If there is no live referendum, add a lane that matches #335 without fleet access. With consent, the resident copies their 'What your agent knows' Context text, and the builder runs #335's exact prediction_prompt (MIT licence) on the same model the fleet uses through OpenRouter, with no tools. The cold baseline then uses the same model with only a self-written bio. Comparing live agent, Context lane and cold model isolates whether memory adds anything.",
  "Fix the statistics. Use about 30 quick items, binary or 5-point, in 5 minutes, and make the friend optional. My simulation gives about 60% power for a 6-point gap at n=25 with 30 items, against about 27% at n=15 with 12 items. Pre-register the minimum detectable effect. Re-ask 10 items on Friday as a test-retest ceiling and report normalized accuracy, as Park et al. do.",
  "Choose a headline that survives small n: 'X% of agent predictions were confident (above 0.8) and wrong' and 'Did 2.5 weeks of memory beat the same model without it?' Avoid a winner-takes-all agent-versus-friend claim.",
  "Have an NYU lab member, or at least Carter or Timour, review the items. Prefer practical village preferences (which session, venue, food, noise, shuttle) plus a few value items with real splits. Never use constitution, referendum or MoralMod-domain items without coordination.",
  "Write the prompt as 'quiz only: do not save to memory, do not record intentions'. Ask residents to run it in a fresh session. Do not run it for anyone in an open referendum window.",
  "Reuse the existing correction surface instead of building a new card. Each resident gets a private link to their Context page to fix what the agent got wrong. Count the corrections they report making; that is the community-benefit number.",
  "On stage, run a live duel (crowd judge's upgrade). A resident and a friend take on the resident's agent across 3 low-stakes items sealed the day before. Open them one at a time while the room guesses, then show the honest aggregate.",
  "Fix logistics and honesty. Recruit an on-site facilitator. Get explicit study-specific consent, including the friend's. Delete raw data by 1 Nov. Cite Youyou 2015 and Park et al. in the README, alongside a table of what was built versus reused."
 ],
 "verified_facts_checked": [
  "PR #335 is real: 'Add scoped referendum adapters to the Hermes runtime', by timkosters, draft, opened 14 Oct 2026. Its description mentions no Brier, accuracy or scoring against votes, and its companion PRs are in private repos. https://github.com/Edge-City/agentvillage/pull/335",
  "PR #335's code calls itself 'the sealed prediction lane'. Its prompt reads 'Predict this resident's preference before they see the referendum. This is research only.' It enforces sourceCutoffAt <= frozenAt, runs with an empty toolset, outputs status, probabilities, confidence, abstentionReason and evidence, and records promptSha256 and sourceSha256. It reads SOUL.md, USER.md, AGENTS.md and MEMORY.md, filtered by mtime cutoff. https://raw.githubusercontent.com/Edge-City/agentvillage/codex/referendum-runtime/plugins/av-events/referendum_predict.py",
  "Confirmed: 'Do agents beat people at this?' is research question 06 on https://agents.edgecity.live/",
  "Confirmed in the V1 write-up: a Sim owner said it 'did vote pretty much how I would have', and another owner corrected one vote. V1 had 4,866 messages across 239 agents, about 20 per agent (computed). https://blog.cosmos-institute.org/p/we-gave-a-village-personal-ai-agents",
  "Confirmed: Timour wrote 'Honest predictions, written down before the village starts, so we can be wrong in public.' https://www.edgecity.live/blog/the-agent-village-experiment-at-edge-esmeralda-2026",
  "Confirmed: the V2 research proposal says 'Planned studies cover representation accuracy, use of corrections\u2026' and lists 'Representation accuracy' on its safety dashboard. https://edgecity.notion.site/Research-Partner-Proposal-Agent-Village-V2-at-Edge-City-India-Shared-3c1d45cdfc5981d7b7bac1e216f3678b",
  "Confirmed in the research register: the MoralMod Decisions tab lets people inspect and correct; Mosaic writes an AI summary into the agent's Context (22 Oct); NYU may receive de-identified conversations if the resident opts in to training; 'A workshop asks for separate study-specific consent.' https://agents.edgecity.live/research-register",
  "Confirmed: the 'What your agent knows' Context page already exists, with (guess) items and a 'Removed by you' list (skills/index-network/tools.md line 136). PR #250 by timkosters, 'AGENTS.md: how to use the \"What your agent knows\" entry', was merged 8 Oct. https://github.com/Edge-City/agentvillage/pulls?q=is%3Apr+eval",
  "Issue #100 exists but dates from 15 June 2026 (Esmeralda era) and concerns the heartbeat cron's 402s. S3 presents it as current. https://github.com/Edge-City/agentvillage/issues/100",
  "Telegram bots cannot see messages from other bots (https://core.telegram.org/bots/faq). forward_origin carries the original sender_user and date (https://core.telegram.org/bots/api#messageoriginuser).",
  "Git commit dates can be overridden with --date, GIT_AUTHOR_DATE and GIT_COMMITTER_DATE. https://git-scm.com/docs/git-commit",
  "Prior art: interview-grounded agents reach 83%, 82% and 86% of participants' own test-retest consistency, and demographics-only agents 74% (Park et al., https://arxiv.org/abs/2411.10109). Computer judgments beat friends', r=0.56 against 0.49 (https://pmc.ncbi.nlm.nih.gov/articles/PMC4313801/).",
  "Confirmed on the buildathon page: still no rubric and no named judges, 2 teams registered, and 'Every build and team goes public with the results.' https://build.edgecity.live/events/india-buildathon",
  "GitHub PR title searches for 'predict' and 'representation' in Edge-City/agentvillage return 0 results. The NYU edge-city-nyu repo contains only allocation rules, with no prediction scoring. https://github.com/The-Cybernetic-Society/edge-city-nyu",
  "Each resident's agent is its own Telegram bot (BotFather /newbot path in docs/tester-walkthrough.md; INFERRED). The fleet fallback model is openai/gpt-6-luna, and the control plane sets the primary model (README line 292). Both are from the repo clone at commit 261b9f9.",
  "My own power simulation (INFERRED assumptions): with 12 items and n=15, a 6-point gap is resolved about 27% of the time with a CI about 0.19 wide; with 30 items and n=25, about 60%. Script: <research-scratch>/s3_rt/power.py",
  "NOT CHECKED: the WebSearch budget ran out, so I could not search for duplicates at Hacker House Goa or among the 25 Oct Community Demo Day builds, which are visible only to signed-in users."
 ]
}
```
