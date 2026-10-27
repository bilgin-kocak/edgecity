> Battle plan and red-team report from the workflow, written before the final fact-check pass. Where this file and [IDEAS.md](../IDEAS.md) differ, IDEAS.md is the corrected version.

# Where's the Line: the village decides which agent actions need a human yes (S2, agg 6.5)

VERDICT: FIXABLE. Both "fatal as framed" points are overclaims. Reframing the output as evidence for the people who sign the policy removes both.

## 1. Name and pitch
**Both Seats: who should say yes when your agent acts?**
Residents judge realistic agent actions twice: once as the person whose agent acts, and once as the person it acts on. They then read the other seat's reasons and may revise their answer. A sealed shadow judge is scored against them. There are two outputs: an evidence brief for the policy owners, and a personal checklist each resident applies to their own Approvals settings.

## 2. Why it wins
- **It answers Agent Village research question 03 word for word:** "What can agents do alone, and what needs a human yes?" It also addresses V1's Simocracy failure, where allocations were recorded with no final human yes.
- **It uses the NYU Ethical Intelligence Lab's methods correctly:**
  - The two seats put contractualism into practice ("agreements diverse stakeholders would endorse").
  - The revision round is virtual bargaining.
  - On stage we quote Levine & Awad's own limit: crowd input informs a decision, it is not "the final word."
- **It matches Timour and Carter's evidence culture:** sealed predictions, Wilson intervals, and a Gate A *dry run* for judge.md ("Nothing here is built"). The dry run is labelled unofficial, and Carter and Timour remain the only signers.
- **It respects existing rulings:**
  - It does not propose flipping message.send or opportunity.accept, which follows Carter's Oct 3 and Oct 7 attention rulings.
  - village.vote and treasury.* are sealed as never delegable, matching ODIN's affected-party rule.
- **Predicted rubric:** ethics built into the mechanism, real residents using it, and nontechnical participation.

## 3. 90-second demo script
- **0:00** "Your agent declines a meeting for you without asking. Fine? Now someone's agent declines *yours* without asking them. Still fine?"
- **0:15** The room scans a QR code and rates 3 practice cards from both seats. These go into a separate "room" column and are never mixed into the sealed data.
- **0:35** The week's result appears: for each class, actor-seat vs affected-seat endorsement with Wilson intervals. One big number: the **agreement gap**.
- **0:55** **The moment:** the top affected-seat objection appears, quoted word for word. People revise after reading it, and the room's own gap shrinks live. Beside it is the week's figure: "perspective-taking closed X of Y points."
- **1:15** Shadow-judge panel: the hash committed Thursday at 10:00 is recomputed live and matches. It shows dry-run metrics against constructed labels, including any card where the judge approved an intention the resident never stated.
- **1:30** "N residents changed a real setting themselves. Nothing was applied for them."

## 4. Real vs mocked
**Real:**
- labelled card corpus
- judge runs
- SHA-256 seals
- grading app
- resident grades and reasons
- statistics
- evidence brief
- consented self-reports of settings changes

**Synthetic or labelled as such:**
- Every card uses fictional people.
- There is no access to the agent fleet or the control plane.
- Gate A is an unofficial dry run on a synthetic set.
- Any APPROVAL.md YAML is a "what-if" illustration.
- The optional negotiator.ts guard runs only on a local replay.

## 5. Architecture and stack
- **Card generator (Python):** about 250 cards built from the APPROVAL.md classes and judge.md §3–§8.
  - At least 30 are constructed denials (wrong recipient, an intention the resident never stated), so the dry run never depends on recruiting.
  - The injection set stays private.
- **Scope:**
  - Judge-eligible classes: intent.publish.inferred.index and digest.share.
  - Classes with a counterparty: opportunity.accept, Gold Stars send, and a message to another person.
  - The agent's own tool rows are excluded.
- **Grading app (PWA):** Next.js, FastAPI and Postgres. Each grader sees every in-scope class once per seat, so the number of graders per class equals the total number of graders. Each card asks for a one-line reason and allows one revision.
- **Judge:** Claude Opus 5.5 pinned as `model:judge-shadow@0.1.0`, returning closed JSON. It is from a different model family than the fleet's gpt-6-luna.
- **Statistics:** scipy/statsmodels (Wilson intervals, kappa, bootstrap). Objections are clustered with LLM help; quotes stay word for word and are checked by a human.
- **Reused from the user's repos:**
  - **harness-lab:** reproducible runs, verifiers, gate statistics
  - **dress-rehearsal:** paper-twin card payloads, replay
  - **arcminute:** seal and reveal

## 6. Hour-by-hour
**Wed 28**
- **11:30–12:30** Kickoff asks (section 7); post the teammate call.
- **12:30–15:00** Read approval.md and judge.md. Write the preregistration:
  - H1: the affected seat endorses at least 15 points less than the actor seat on at least one class.
  - H2: the revision round narrows the gap.
  - H3: the judge's denial recall is lower on the co-author's cards.
  - Power: at 25 graders, "clear endorsement" (Wilson lower bound above 0.5) needs at least 18 of 25 (my calculation).
- **15:00–19:00** Card generator. The co-author writes at least half the bad-action cards without seeing the judge prompt.
- **19:00–24:00** Grading app with a consent screen and a "PRACTICE CARD – NOT A REAL REQUEST" banner. Seal the judge prompt and model ID.

**Thu 29**
- **08:00–09:30** Pilot with 3 people, one of them nontechnical; fix the wording.
- **09:30** Card authoring closes.
- **10:00** Run the judge, commit the verdict hash and the preregistration, and paste the hash into the submission draft.
- **10:00–20:00** Grading is open. Recruit in person at The Circle and Riva, plus one approved post. Target: 25 residents.
- **In parallel:** statistics and the report page.
- **Stretch:** a negotiator.ts guard on the receiving side that returns `{stall:{reason,suggestedAsk}}` when the affected seat has objected.

**Fri 30**
- **09:00** Grading closes. Reveal the verdicts, verify the hash, run final statistics, cluster the objections.
- **11:00** Evidence brief. Send each grader their checklist with a link to the real Approvals page. Send the brief and the injection corpus privately to Carter.
- **12:00** Feature freeze.
- **12:00–14:30** Video and README.
- **16:00** Submit; keep editing until 18:00.

**Cut line, in order:**
1. negotiator.ts guard
2. what-if YAML
3. Carter/Timour grading column

Never cut: the seals, two-seat grading, the revision round, the brief, the limitations section. If fewer than 15 residents have graded by Thu 20:00, present it as a pilot with intervals only.

## 7. Day-1 people and asks
- **Timour Kosters:**
  - What is the rubric, and how are the top 3 chosen?
  - Is it OK to add a crowd column beside the labelled set?
  - Permission for one recruiting post, never through the approvals bot.
- **Carter Crouch:**
  - Does the labelled set exist yet?
  - A quick check of the schema.
  - A channel for privately disclosing the injection corpus.
- **Sydney Levine / Logan Walls (NYU lab):**
  - Could grading contaminate the MoralMod arms, treasury H2 or the Habermas Machine study?
  - Would they review the preregistration?
- **Teammate post (buildathon page):** "Builder (agent evals, sealed predictions) seeks 1–2 teammates for *Both Seats*: residents decide which agent actions need a human yes, from both sides. Need someone in Goa to recruit 25 residents for 4 minutes each, and a nontechnical co-author for half the 'bad agent action' cards. No code needed."

If the Agent Village or NYU leads say no, pivot to a "shadow-judge eval and two-seat study" with no policy framing.

## 8. Safeguards
- **Data handling:**
  - The project's own consent screen.
  - Adults only.
  - Pseudonymous.
  - No Telegram or EdgeOS IDs.
  - Aggregates only.
  - All data deleted by 30 Nov 2026.
- **No confusion with real requests:** nothing is sent through the approvals bot, and practice cards look visibly different from real ones.
- **No real people on cards:** fictional names and intentions only.
- **No attack kit:** the injection corpus stays private. Only its taxonomy, counts and hashes are published.
- **Honest scope:**
  - Report n, who took part, and the self-selection; never say "the village decided."
  - Graders are mostly visitors (about 65% from outside India), so the result does not speak for the Goan host community, and the pitch says so.
- **No moral grading of people:** it measures the judge and the policy, never people's morals. No per-person results are shown.

## 9. Submission package
- **Description:** pitch, findings, links to the preregistration and hash, a built-vs-reused table, limitations.
- **Video (2–3 min):** one human story, the agreement gap, hash verification, one failure.
- **Repo (MIT):** app, card generator, judge runner, statistics, preregistration, report.
- **Image:** a chart of actor vs affected endorsement showing the gap.

## 10. Risks and mitigations
| Risk | Mitigation |
|---|---|
| Too few graders | In-person recruiting, a teammate in Goa, pilot framing |
| Circular ground truth | Co-author writes cards blind; recall reported per author |
| Nothing flips live | The headline is the gap and the revision, not flips |
| Rubric differs | Re-fetch the page Wednesday; reorder the pitch |
| Wifi fails | Cached replay, labelled as cached |

## 11. Solo/team, Goa/remote
One person can do the build, remotely if needed. Recruiting and the live demo need someone in Goa. A remote solo builder will get a pilot-size sample unless there is a teammate in Goa or an approved recruiting post. The best setup is being in Goa with one nontechnical co-author.

## Red team
```json
{
 "id": "S2",
 "verdict": "fixable",
 "fatal_flaws": [
  "FATAL AS FRAMED: the idea cites a paper that argues against its own core mechanism. It cites Levine and Awad's 'Why We Should Crowdsource AI Ethics (and How to Do So Responsibly)' as support for the 'compiler' that turns crowd grades directly into an APPROVAL.md diff. That article says crowd preferences should not be 'directly translated into policy or handed off to engineers' and should not be 'the final word'. It also warns that online participants are 'self-selected, tech-savvy volunteers' (https://behavioralscientist.org/why-we-should-crowdsource-ai-ethics-and-how-to-do-so-responsibly/). Sydney Levine runs the lab that framed the rubric, so a lab member could undo the pitch in a single sentence. Fix: reframe the output as evidence that informs the signers, not as a compiler.",
  "FATAL AS FRAMED: the 'Gate A report' and the 'GATE A: FAIL' panel claim an authority the builder does not have.\n- judge.md says each gate is 'a written sign-off by Carter and Timour\u2026 No other signature is needed' (decision 13).\n- Its labelled set is 'about 200 recorded card payloads, each graded independently by Carter and Timour'. These are recorded cards, not synthetic ones.\n- Decision 6 counts team tenants and that labelled set. Resident-graded pairs come only from residents' own supervised-retro samples.\n- Crowd grades on synthetic cards about hypothetical strangers are not Gate A pairs (https://github.com/Edge-City/agentvillage/blob/main/docs/design/judge.md).\n- The closing line 'This room just amended the village's agent policy' is also false. Any template change means 'a change to every tenant's policy bytes, and so a re-attestation', and 'Every later change needs the resident's acceptance' (https://github.com/Edge-City/agentvillage/blob/main/skills/approval/templates/APPROVAL.md). The village ends Nov 1, and I found no evidence that Agent Village runs in Bhutan.\n- The jury studies agents that overstate what they did. Overclaiming here is the exact failure the project says it measures."
 ],
 "serious_risks": [
  "The sealed rule mostly decides the result in advance, so sealing it proves little. My own Wilson 95% calculation:\n- With fewer than 20 graders per class per seat, no class can ever reach a lower bound of 0.80.\n- With exactly 20 graders it needs unanimity. With 30 it tolerates 1 dissent; with 40, 3 dissents.\n- The idea also says 'An objection from the affected party keeps it manual'. That reads as a single-veto rule, which contradicts the 0.80 rule.\n- With 20 to 60 graders spread over 6 or more classes and 2 seats, nearly every class will come out manual. A skeptic will say the outcome was known before any data arrived.",
  "The 'proposed diff' would reverse explicit, reasoned rulings by the policy owner:\n- message.send and the other Hermes tool rows are autonomous because of Carter's 'recorder' ruling (Oct 3): making them manual 'would have held every curl and every routed tool\u2026 behind a tap'.\n- opportunity.accept is autonomous because of Carter's Oct 7 ruling: 'a second gate would ask twice'.\n- judge.md opens with 'A resident's attention is the scarcest thing approval.md spends.'\nA fail-closed diff that flips these to manual is dead on arrival and looks naive about the system (https://github.com/Edge-City/agentvillage/blob/main/skills/approval/templates/APPROVAL.md).",
  "It mixes two different levers. Class autonomy is a policy row. The judge decides instance by instance inside manual classes. judge.md says: 'Delegation never changes a class's autonomy.' Pooling instance-level grades (which mostly come back 'depends') into class-level autonomy decisions is not defined, and 'depends' has no rule in the compiler. Decision 8 also limits the judge to intent.publish.inferred.index and then digest.share, and says 'Never village.vote and never treasury.*'. Most of the proposed classes are therefore outside the judge's scope (judge.md \u00a77).",
  "The ground truth is circular. One builder writes the bad-action cards, the plain-language seat wording and the judge prompt. Recall on constructed denials will be inflated, and a 'pass' will be suspect. A 'fail' is also near-certain:\n- At 30 denials, one miss gives a recall lower bound of 0.833, below the 0.85 required (my calculation).\n- Gate A also allows 'zero' oks on irreversible or misattributed actions.\nEither outcome is weak evidence.",
  "Recruiting graders from a fatigued village is the binding constraint. Residents are already asked to:\n- complete the GODCONST ballot (closed Oct 25)\n- answer GC-ELICIT follow-up interviews 'over a few days' after the pool closes (https://github.com/Edge-City/agentvillage/blob/main/plugins/av-elicit/README.md)\n- rate suggestions on av-rate cards\n- vote in the daily treasury ballot (APPROVAL.md village.vote row)\n- rank plans in NYU's Habermas Machine community-fund experiment in Goa (https://github.com/The-Cybernetic-Society/edge-city-nyu/blob/main/NOTES.md)\nAll of this runs during the Hacker House, the Buildathon and Demo Day week. Getting 200 or more paired grades with 30 or more denials from residents in about 30 hours is uncertain.",
  "There is little measurable benefit to the community this week. Nobody's agent behaves differently by Oct 30.\n- Residents can already change their own rows on the app's Approvals settings page: 'the settings page offers ask and never' for opportunity.accept, and the Hermes rows 'ask only if the resident sets their row to ask'. 'Personal override files' therefore duplicate an existing feature.\n- The approval gate itself is opt-in ('Approval (opt-in)', https://github.com/Edge-City/agentvillage/blob/main/README.md). Many residents may have no gate for a policy to change. INFERRED, but DATA-444's 'Connect-approvals reminder' points that way.",
  "Stated versus revealed preference. The AV team already logs real approve and deny taps (approval.card_resolved events, PR #292). For research question 3, Timour can argue that real taps on real cards outrank hypothetical grades on synthetic cards. The only thing their data cannot give is the affected-party seat, so the whole pitch rests on that one point.",
  "Grading could contaminate the live experiments. Prompting 20 to 60 residents to reflect on what their agent may do without asking, in the final days of the randomized MoralMod ON/OFF arm and the treasury preregistration (H2), could shift real approval behaviour and settings changes. This needs explicit clearance from the AV and NYU leads.",
  "Demo risk. With a room-sized n, almost nothing will flip live, so the 'recompile' moment may show no change. Adding Demo Day audience grades to a sealed, preregistered dataset also breaks the preregistration. Only the top 3 present on Oct 31, so the submission video has to carry the project alone. 'needs_physical_presence: false' understates this: remote recruitment of residents and the live room demo both effectively need someone in Goa.",
  "The feasibility upgrade suggests adding Hacker House Goa participants and 'anyone reachable by link' to the grader pool. They are not the affected community, so this dilutes the 'the village decides' claim. Report them only as a separate, labelled column, or leave them out."
 ],
 "competition_or_duplicates": [
  "The judge's 'offline labelled set and the injection corpus, graded by Carter and Timour' is a planned build task (agentvillage-data, 'post, before Gate A'). That repo is private, so I cannot tell whether it is already under way. If it is, the crowd column is additive at best (https://github.com/Edge-City/agentvillage/blob/main/docs/design/judge.md \u00a78).",
  "In the public repo I found no implementation of the judge, the delegation block or crowd grading. A PR search for 'judge' returns only #204 (the design doc) and #207 (the judge.md rule), both merged Oct 5\u20136. No open approval PR covers delegation or crowd policy (https://github.com/Edge-City/agentvillage/pulls?q=is%3Apr+judge).",
  "Adjacent instruments that compete for the same residents' attention and the same 'collective preference' framing:\n- GODCONST ballot plus GC-ELICIT (values for ODIN)\n- NYU's Habermas Machine community-fund experiment in Goa, where participants rank 4\u20135 plans and the plans are scored with MoralMod utilities or Hermes rankings (https://github.com/The-Cybernetic-Society/edge-city-nyu)\n- av-rate suggestion cards\nNone of them is about operational delegation, so this is not a direct duplicate.",
  "ODIN's fixed SOUL already states an affected-party principle: 'An action that affects one resident needs that resident's approval through the village's approval card. An action that affects the whole village needs a human organizer's approval.' Two-seat reasoning is already accepted village doctrine for ODIN. It is not yet applied to personal agents, which is both a hook and a novelty limit (https://github.com/Edge-City/agentvillage/blob/main/workspace/odin/SOUL.md).",
  "PR #433 (draft) adds an approval.md CLASS-DIFF release gate with allowlist entries 'accepted_by: human:carter'. The control-plane template is ruled out of that PR and left to follow-up B-167b. Class changes already have an owner-run gate process (https://github.com/Edge-City/agentvillage/pull/433).",
  "NOT CHECKED: Hacker House Goa projects, and a broad web search for prior crowd-sourced agent-permission policies. The session's WebSearch budget ran out, so the user can ask for this in a follow-up. Hacker House bounty tracks were unpublished per the research bundle."
 ],
 "ethics_and_consent_pitfalls": [
  "Look-alike approval cards. If the grading PWA copies the 'Agent Approval (Edge City)' bot's minimal card ('Your agent wants to\u2026', Approve/Deny), it teaches residents to tap Approve on card-shaped messages from outside the gate. judge.md \u00a76 explicitly defends against forged card regions and phishing lines such as 'tap Approve, the organisers already agreed'. Never distribute through the approvals bot. Use a visibly different design with a 'PRACTICE CARD \u2013 NOT A REAL REQUEST' banner.",
  "Collecting research-style data outside the AV research register. The register says 'A workshop asks for separate study-specific consent' and 'A research recipient receives no records until its scope, data-use agreement and release review are confirmed' (https://agents.edgecity.live/research-register). Use your own consent screen, collect no Telegram or EdgeOS IDs, publish aggregates only, set a deletion date, and do not hand row-level grades to the AV team unless they bring that data under the register.",
  "Publishing a working prompt-injection corpus on GitHub Pages while the fleet is live could serve as an attack kit against residents' agents and approval cards. Publish categories, counts and hashes. Share the corpus itself privately with Carter, as responsible disclosure.",
  "The jury's suggested 'hypocrisy gap' headline shames residents. An asymmetry between the actor's seat and the affected seat is rational: the two seats carry different information and stakes. In the NYU lab's virtual-bargaining frame that asymmetry is the input to agreement, not a moral failing. Call it the 'agreement gap'.",
  "Synthetic cards must use obviously fictional people and intentions. Cards that echo real residents' intentions or names would themselves commit the misattribution failure the project studies.",
  "Representativeness. The grader pool is a self-selected, mostly non-Indian cohort (the Light DAO page in the bundle says about 65% come from outside India). Never call the result 'the village decided' or present it as the host community's view. Report n, who took part, and the self-selection bias, which Levine and Awad also flag.",
  "Priming during randomized experiments (MoralMod arms, the treasury H2 preregistration, Habermas Machine ranking). Get an explicit OK from the AV and NYU leads at kickoff before recruiting from AV channels.",
  "Frame it as measuring the judge and the policy, never people's morals. Do not show per-person results on stage."
 ],
 "likely_judge_criticisms": [
  "Levine-lab member: 'Our article says crowd preferences shouldn't be translated directly into policy. Why does your compiler do exactly that?'",
  "Contractualist objection: 'An 80% supermajority isn't contractualism. Contractualism asks whether anyone could reasonably reject the action. Where are the reasons the objectors gave?' The RRC paper speaks of agreements stakeholders 'would endorse under the right conditions', and a one-shot survey involves no deliberation (https://arxiv.org/abs/2506.17434).",
  "Timour or Carter: 'Only Carter and Timour sign Gate A, and the labelled set is recorded payloads. This is a dry run on synthetic cards, so why does the slide say GATE A?'",
  "Carter: 'Your diff makes message.send and opportunity.accept manual. We ruled against that on Oct 3 and Oct 7, for attention reasons you don't address.'",
  "'Residents can already set ask or never per class in the app. What does a personal override file add?'",
  "'You wrote the bad cards and the judge prompt. Why is recall on your own constructed denials evidence of anything?'",
  "'We have thousands of real taps on real cards. Why should stated preferences on synthetic cards outrank them?'",
  "'With 25 graders a single dissent keeps a class manual. Your sealed rule decided the outcome before anyone graded.'",
  "'Who is better off this week because of this?'",
  "Audience: 'It's a poll and a YAML file.' The crowd juror's 3/10 reflects this."
 ],
 "fixes": [
  "Reframe the output from 'compiled APPROVAL.md diff' to 'Evidence brief for the policy owners: where both sides agree, where they don't, and why'. Quote Levine and Awad's own limit on stage: crowd input informs and breaks ties, it does not dictate. Show any YAML only as a 'what-if' illustration, never as 'the policy'.",
  "Rename the gate panel 'Gate A dry run (unofficial, synthetic set, signers: Carter and Timour)'. Report the crowd-versus-judge numbers next to a constructed-label ground truth: wrong recipient, an intention the resident never stated, injection. Drop the claim that the room 'amended the policy'. Any change would apply to the next Agent Village deployment, after re-attestation.",
  "Scope to open questions only, and hard-code the floors.\n- In scope: (a) the two judge-eligible classes, intent.publish.inferred.index and digest.share, for the judge evaluation; (b) the currently autonomous classes that have a counterparty (opportunity.accept, Gold Stars send, a message to another person) for the two-seat question.\n- Seal these as never delegable: village.vote, treasury.*, the human-only rows (judge.md decision 8; ODIN's fixed rule).\n- Leave the agent's own tool rows (network.call, read.web, cron and so on) out entirely.",
  "Replace the Wilson \u22650.80 headcount rule with a two-part, contractualist-flavoured readout:\n- For each class and seat: the endorsement share with its Wilson interval.\n- A 'reasonable rejection' list: the affected-party objections, quoted verbatim and clustered.\nState the power math in advance (n \u2265 20 per class-seat to say anything at all). Design card allocation so every grader sees every in-scope class once from each seat, which makes the per-class n equal to the number of graders.",
  "Add one virtual-bargaining round. After grading, each person sees the other seat's distribution and its top objection reasons, then may revise one answer. The headline becomes 'perspective-taking closed X of the Y-point agreement gap'. That fits Levine's virtual-bargaining and RRC work and works better as the crowd moment than a 'hypocrisy' number.",
  "Break the circularity:\n- A second author, ideally a nontechnical resident, writes at least half of the bad-action cards without seeing the judge prompt.\n- Seal the judge prompt and model snapshot before card authoring ends.\n- Report recall separately for each author's cards.",
  "Give residents something real they can use this week, under their own control:\n- On finishing, each grader gets their answers as a checklist and a deep link to the real Approvals settings page, where they change rows themselves. The builder never applies anything.\n- With consent, count how many changed a real setting. That is a behavioural outcome, not only a survey.\n- Optionally ship a receiver-side guard: a negotiator.ts that stalls (`{stall:{reason,suggestedAsk}}`) on actions the affected-party seat objected to. approval.md has no channel for the receiver's consent, and this fills that gap without touching the live fleet (https://github.com/Edge-City/agentvillage/blob/main/docs/negotiator.md).",
  "At the Wed 11:30 kickoff:\n- Get Carter and Timour's yes to the crowd column, and ask whether the labelled set already exists.\n- Get the AV and NYU leads' OK on contamination.\n- Get permission for one recruiting post in a buildathon or general channel, never the approvals bot.\nIf they say no, pivot to a 'shadow judge eval and two-seat study' with no policy framing.",
  "Recruit in person on Wed and Thu at The Circle and Riva, with a teammate in Goa if the user is remote. Pre-commit a minimum sample: 25 residents, which allows a meaningful class-level result for 3\u20134 classes. Keep non-resident graders out of the 'village' column, or label them separately.",
  "Keep the injection corpus private and publish only its taxonomy and hashes. Give the practice cards a clearly different design from the real approval bot's cards.",
  "Build the pitch around one human story: 'Your agent declined a meeting for you' against 'someone's agent declined yours', with the agreement gap and the quoted objections. The judge panel comes second. Pre-record a 2\u20133 minute video, because only the top 3 demo live. Include a table separating what was built Oct 28\u201330 from what came from harness-lab, dress-rehearsal and arcminute."
 ],
 "verified_facts_checked": [
  "VERIFIED: judge.md says 'Nothing here is built'. Its Gate A thresholds match the idea exactly: \u2265200 paired grades, \u226530 human denials, \u226590% agreement, kappa \u22650.6, Wilson lower bound \u22650.85 on denial recall, zero ok on irreversible or misattributed actions, zero forced ok on the injection corpus. BUT the gates are signed by Carter and Timour alone (decision 13), the labelled set is 'about 200 recorded card payloads' graded by Carter and Timour, the thresholds are 'still proposals', and only intent.publish.inferred.index and digest.share are eligible for delegation (decision 8). Source: https://github.com/Edge-City/agentvillage/blob/main/docs/design/judge.md (local clone at 261b9f9).",
  "VERIFIED: the APPROVAL.md day-one template.\n- It is an 'operator attestation'.\n- opportunity.accept and message.send are autonomous; intent.publish.inferred.index, digest.share, village.vote, treasury.propose and resource.allocate are manual.\n- The 'recorder' shape (Carter, Oct 3) and the opportunity.accept ruling (Oct 7) give explicit attention-cost reasons for the autonomous defaults.\n- 'Every later change needs the resident's acceptance in the app or their tap', and the settings page already lets residents choose ask or never per row.\nSource: https://github.com/Edge-City/agentvillage/blob/main/skills/approval/templates/APPROVAL.md",
  "VERIFIED: the approval gate is opt-in ('Approval (opt-in)\u2026 For residents who opt in'). Source: https://github.com/Edge-City/agentvillage/blob/main/README.md",
  "VERIFIED: research question 03 reads verbatim 'What can agents do alone, and what needs a human yes?' Also on the page: 'Which actions need a human yes, and which can be delegated'. Source: https://agents.edgecity.live/",
  "VERIFIED, and it CONTRADICTS the idea's use of it: Awad and Levine (Sep 7, 2020) say crowd preferences should not be 'directly translated into policy or handed off to engineers' and are not 'the final word'. Source: https://behavioralscientist.org/why-we-should-crowdsource-ai-ethics-and-how-to-do-so-responsibly/",
  "VERIFIED: 'Resource Rational Contractualism Should Guide AI Alignment' lists Sydney Levine as first author. The paper speaks of 'agreements that diverse stakeholders would endorse under the right conditions'. Source: https://arxiv.org/abs/2506.17434",
  "VERIFIED: the buildathon rubric and prize split are still unpublished, no judges are named, and 2 teams are registered (fetched Oct 27). Source: https://build.edgecity.live/events/india-buildathon",
  "VERIFIED: NYU's Goa community-fund experiment runs Habermas Machine arms in which participants rank plans. It is another concurrent ask on residents. Source: https://github.com/The-Cybernetic-Society/edge-city-nyu/blob/main/NOTES.md",
  "VERIFIED: GC-ELICIT has residents' agents interview them 'over a few days' after the GODCONST pool closes, so it overlaps the build window. Source: https://github.com/Edge-City/agentvillage/blob/main/plugins/av-elicit/README.md",
  "VERIFIED: ODIN's fixed rule: 'An action that affects one resident needs that resident's approval\u2026 An action that affects the whole village needs a human organizer's approval.' Source: https://github.com/Edge-City/agentvillage/blob/main/workspace/odin/SOUL.md",
  "VERIFIED: no public PR implements the judge or a labelled set. Only #204 and #207 (design docs) match 'judge'. The private agentvillage-data and control-plane repos could not be checked. Source: https://github.com/Edge-City/agentvillage/pulls?q=is%3Apr+judge",
  "VERIFIED: PR #433's CLASS-DIFF gate needs Carter's 'accepted_by: human:carter' allowlist entries, and the control-plane template is deferred to B-167b. Source: https://github.com/Edge-City/agentvillage/pull/433",
  "VERIFIED: the research register says 'A workshop asks for separate study-specific consent' and 'Rejoining research is currently paused'. Source: https://agents.edgecity.live/research-register",
  "COMPUTED (my own Wilson 95% calculation; not from any source):\n- A lower bound \u22650.80 is impossible below n=20, needs 20/20 at n=20, and allows 1 dissent at n=25\u201330 and 3 at n=40.\n- Denial recall at 29/30 gives a lower bound of 0.833, below the 0.85 bar.",
  "NOT FOUND: any evidence that Agent Village continues at Edge City Bhutan (Nov 11\u201319), so the proposed diff has no confirmed next deployment.",
  "NOT CHECKED: Hacker House Goa projects and a broad web search for duplicates. The WebSearch budget for this turn ran out."
 ]
}
```
