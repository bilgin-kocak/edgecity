> Battle plan and red-team report from the workflow, written before the final fact-check pass. Where this file and [IDEAS.md](../IDEAS.md) differ, IDEAS.md is the corrected version.

# Who Was Studied? A 'default male' label for health claims (S15, agg 6.4)

# Who Was Studied? Battle plan

## 1. Name and pitch
**Who Was Studied?** Name a health practice and see how many of its trials studied only men. Every count is quoted from the paper and checked by code. A sealed test then shows whether AI assistants tell a woman that.

## 2. Why it wins
- **It measures Anima House's founding sentence:** "For decades, medicine studied male physiology as the default" (Charlotte McAdams, Taylor Lamprecht). It fits Healthy by Default and Multigenerational (a peri/post-menopausal row).
- **It has a Week 3 hook: does an agent represent the evidence faithfully to the person it serves?** Sealed predictions and must_include/must_not grading copy Timour's 20-question eval and the Wilson bounds in judge.md. It speaks to Cosmos's truth-seeking and to the NYU lab's concern for fairness to the people affected.
- **Fit with the predicted rubric:**
  - Benefit: women in the village, plus an "enrolled in India" row for the hosts.
  - Ethics: no advice; it labels claims, not people.
  - Built: live public data.
  - Originality: the benchmark.
  - Co-creation: an Anima House co-labeller.
  - Continuation: MIT licence, read-only MCP, a path to Bhutan.
- **It is honest about prior art.** Feldman 2019 (AI2, 43k papers) and Cowley 2021 validate the method, and Elicit already does extraction. What is new: a label per claim, a deterministic verifier, printed retrieval precision, and the benchmark.

## 3. 90-second demo
- **0-10s:** "This village gives us free sauna. The study everyone cites on sauna and longevity enrolled 2,315 men. Zero women."
- **10-30s:** Type "cold plunge". The label reads *Cold-water immersion RCTs: 10 of 11 men-only, 1 mixed; results by sex k/n; enrolled in India n*. Below it, the participant-weighted share (55% female) appears with the warning "one study = 95% of participants".
- **30-45s:** Click "10 of 11" to highlight the sentence in Cain 2025. Click the "+250% dopamine" claim: its chain leads to Šrámek 2000, "a group of young men".
- **45-70s, THE MOMENT:**
  - Beside the label, an assistant gives a confident answer to "I'm a 52-year-old woman; is cold plunging good for me?"
  - The hash sealed at Wed 14:00 opens: "Predicted: at least 60% of answers won't mention who was studied. Result: X%."
  - Each assistant gets a pass or fail, and good answers are credited.
- **70-90s:** The trust row reads "extraction accuracy X% (95% CI, n); retrieval precision Y%". The footer says "Not medical advice. Unknown for women ≠ doesn't work." Any agent can call `whostudied.label`.

## 4. Real vs mocked
- **Real:** all sources, counts and quotes; the assistant answers (pinned model IDs, timestamped, 3 samples each); accuracy and CIs.
- **Cached:** labels run ahead of time are stamped "cached at <time>".
- **A prompt, not a person:** the 52-year-old woman is a persona, not a resident.
- **Conformant, not live:** the Agent Village mini-app would need a private control-plane PR, an allowlist and MINI_APPS_MANIFESTS=1.

## 5. Architecture and reuse
- **Retrieval, starting from the claim's source:**
  1. The study the claim comes from.
  2. The lists of studies included in systematic reviews.
  3. PubMed E-utilities (RCT publication type plus MeSH) and Europe PMC full text.
  4. ClinicalTrials.gov v2 with `query.intr` + `results:with` (sex counts, region).

  The label shows the exact queries, and a person checks relevance.
- **Extraction:** a pinned Claude model with strict tool JSON. Every field needs a verbatim quote or "not reported".
- **Verifier:** quote matching (test decimals: "55.4%" must not become "4%"), a check that female plus male equals N, and a cross-check against ClinicalTrials.gov.
- **Label:** FastAPI plus HTML, with study-level rows first.
- **Benchmark:** a must_include/must_not YAML, SHA-256 seals, two blind graders and Cohen's kappa.
- **MCP:** TypeScript, auth none, read-only `whostudied.label` and `whostudied.sources`.
- **Reuse:** Savlar (claim-to-source linking), harness-lab (verifiers), arcminute (sealing), fermata/preflight (MCP scaffolding), dress-rehearsal (offline fixtures).

## 6. Hour by hour (IST)
**Wed 28**
- 11:30 Kickoff: ask Timour for the rubric and how the top 3 are chosen; re-fetch the event page.
- 12:30 Check coverage and keep the 8-12 practices that have posted results or open full text. Email Anima House and post the teammate call.
- 14:00 Seal the predictions and commit the hash publicly. Then build retrieval, extraction and the verifier.
- 20:00-01:00 Trace three claims back to their source studies: Šrámek, Laukkanen, Cain.

**Thu 29**
- 08:00 Gold set: about 60 studies plus relevance labels, with co-labellers.
- 12:00 Measure, then freeze the prompts.
- 14:00 Label UI, click-to-quote, India row.
- 19:00-23:00 Benchmark: 3 assistants x 2 personas x 3 samples, graded blind.

**Fri 30**
- 08:00 MCP server and manifest; cache all claims.
- 10:30 Bug bash; freeze at 12:00.
- 12:00 Record the video.
- 14:30 README; submit at 16:00; edit until 18:00.

**What to drop if behind, in this order:**
1. MCP server (ship the manifest only)
2. Menopause and cycle fields
3. India row
4. Six claims instead of twelve

**Never cut:** study-level counts, the quote checker, CIs, the sealed benchmark.

## 7. Day-1 people and asks
- **Anima House** (Charlotte McAdams, Taylor Lamprecht): "Would one or two of you co-label studies for 2-3 hours Thursday morning and help word the label? Credit only if you want it." The india26 page also lists Chris Morello and Ashutosh Dhasmana with Anima House, so confirm who to go through.
- **Timour:** the rubric, how the top 3 are chosen, and how to disclose reused work.
- **NYU lab** (Sydney Levine or Logan Walls): "Is this rubric a fair test of disclosure?"
- **Agent Village** (Carter Crouch): "Does this manifest conform?" Also ask whether any resident would volunteer their own agent's answer.
- **Teammate post:** "Building Who Was Studied?: how many women, post-menopausal women and people in India were in the trials behind sauna, cold-plunge, ashwagandha and fasting claims, plus a sealed test of whether AI assistants tell you. Seeking 1-2 people who read methods sections (2-3 h of labelling Thu morning, credited). Remote OK. DM Bilgin."

## 8. Safeguards
- Label claims, never people. No quotes from talks without the speaker's opt-in (media policy).
- No resident health data is collected.
- Sex is shown "as reported by the study", and the label notes that the data is binary.
- Every label says: "Not medical advice; unknown for women ≠ doesn't work; ask a clinician."
- Ayurveda is framed as a question of who was studied, not whether it works, and Indian trials are counted.
- No venue is named. Never imply Anima House endorses it without their consent.
- No calls to the agent fleet, and the MoralMod arms are left untouched.

## 9. Submission package
- **Description:** the headline result, accuracy with CIs, the sealed hash and its reveal, limits, a table of what was built this week vs reused, and prior art.
- **Video:** 2:30 following section 3, showing one failure.
- **Repo (MIT):** code, gold set, YAML, seals, raw answers.
- **Image:** the cold-water label beside an assistant answer.

## 10. Risks and mitigations
- **"Elicit and AI2 already did this":** cite them and explain the difference.
- **Most cells say "not reported":** make that a finding: "X% of trials never say who they studied."
- **Noisy retrieval:** start from each claim's source study and print retrieval precision.
- **Small n:** Wilson CIs, with n per field.
- **Assistants vary between runs:** pin model IDs, take 3 samples and report the spread.
- **It looks like a gotcha:** publish the rubric before running and credit good answers.
- **Wifi fails:** use the stamped cache.
- **No Anima House partner:** ship anyway, say so, and recruit the second grader through the teammate post.

## 11. Solo vs team, Goa vs remote
Solo and remote both work: the APIs are public and need no keys, and nobody needs to be recruited. It is strongest with one Anima House co-labeller (a shared sheet works remotely) and with Bilgin in Goa for Demo Day (Sat 31 Oct, Riva). If he is remote, he should confirm that remote presenting is allowed or have the co-labeller present.

## Red team
```json
{
 "id": "S15",
 "verdict": "fixable",
 "fatal_flaws": [
  "The headline number points the wrong way. As specified, the label leads with 'share of participants who were female', weighted by participants. I tested this on the idea's own example claim, cold plunges. The 2025 systematic review of cold-water immersion RCTs (Cain et al., PLOS One, PMC11778651) says, quoted exactly: 'These studies comprised a total of 3177 participants, of whom 55.4% were female. The provision of female participants was provided by one study [33], comprised of 3018 participants. All other studies were comprised of 100% male participants.' Built as specified, the label would print about 55% female for cold plunges on stage, while 10 of 11 RCTs were men-only. The one large mixed-sex study was a cold-shower trial in the Netherlands (INFERRED from the review's reference list), not a plunge. Unless the label is redesigned around study-level counts, the live demo can contradict the pitch.",
  "The printed accuracy number would overstate reliability, because the gold set grades extraction but nothing grades retrieval. I tested the retrieval layer on ClinicalTrials.gov v2 (query.term plus results:with), and it returns mostly off-topic trials:\n- 'cold water immersion': 25 trials with results. The top 10 are mostly cold-pressor pain experiments (knee osteoarthritis, back pain, insomnia, stretching).\n- The idea's own example, NCT04766021, is a mirabegron drug trial run in a 20 \u00b0C room. It is not a cold-plunge study. Its 5 women and 6 men are real, but they say nothing about the claim.\n- 'creatine': 728 trials with results. The top 10 are all drug trials (hepatitis B adjuvant, semaglutide, riluzole and others), presumably matched on creatine or creatinine lab outcomes (INFERRED).\n- 'mouth taping': 2 trials with results, both irrelevant (mandibular advancement, a rib-fracture belt).\n- 'sauna': 5 trials with results, about 3 of them relevant.\nA label that says 'extraction accuracy: 9X%' on top of an unmeasured, noisy denominator is false confidence. This jury studies fabrication and calibration professionally (Timour's judge.md uses the Wilson 95% bound), so they will catch it."
 ],
 "serious_risks": [
  "**Labels dominated by 'unknown'.** Europe PMC open full-text coverage of RCTs is low for most claims:\n- creatine supplementation: 56 of 285\n- sauna: 10 of 53\n- cold water immersion: 31 of 173\n- ashwagandha: 56 of 79 (the exception)\nAcross the 50 most recent PubMed RCT abstracts per practice, a crude regex found a sex count in only 8 of 49 (creatine), 7 of 50 (cold water immersion) and 10 of 49 (sauna). Most cells will read 'not reported'. The tool must never treat 'not reported' as 'male-only'.",
  "**The most famous claims trace to paywalled papers with no N in the abstract.** The '+250% dopamine' cold-water figure comes from \u0160r\u00e1mek et al. 2000 (Eur J Appl Physiol, PMID 10751106). Its abstract says only 'a group of young men' and gives no N, and the full text is a Springer paper from 2000. The tool can say men-only, but it cannot quote a count from open sources.",
  "**Weak fit with this week and this jury.** Rasayana week (Oct 18-24) is over. Week 3 is Frontier Intelligence & Decentralized Futures, and the jury's centre of gravity is Agent Village and NYU's moral-cognition lab. As written, the idea touches agents only through a manifest that cannot go live: the generic mini-app needs a PR to the private control-plane repo, staff allowlisting and MINI_APPS_MANIFESTS=1, so an outside builder cannot even open that PR.",
  "**'Built for women without women'.** The idea is solo and remote. Anima House's co-labelling is hoped for, not secured. Its lead is Charlotte McAdams (Substack). The india26 page lists 'Chris Morello & Ashutosh Dhasmana' alongside it, so who to ask is ambiguous. Without a named Anima House co-author, the women's-health framing is borrowed rather than earned.",
  "**The gold set is too small.** About 60 studies across 4+ fields gives wide intervals. At 90% observed accuracy with n=60, the Wilson 95% interval is roughly 80-95% (INFERRED arithmetic). Menopausal status and cycle-phase control are rarely reported, so their per-field n will be tiny.",
  "**Medical-advice perception.** A woman who reads 'few women studied' may conclude 'don't do it' or 'it doesn't work for me'. Both are unsupported. Liability and tone risk, at a village that promotes these practices.",
  "**Cultural sensitivity.** Rasayana is Ayurveda. A tool that 'labels' ashwagandha and other Ayurvedic claims through a Western RCT lens can read as debunking the host tradition. That conflicts with 'Honor Our Host Community'.",
  "**Labour.** About a day of gold-set labelling, plus building retrieval, extraction, the checker, the UI and an MCP server, all solo in 54 hours. Polish on the label UI will suffer.",
  "**Corpus choice is a hidden judgment.** Should Waon therapy in heart-failure patients count as evidence 'behind' sauna-for-longevity? The tool makes that call silently unless it is shown."
 ],
 "competition_or_duplicates": [
  "**Elicit** (https://elicit.com/, fetched today). It 'can automate screening and data extraction of systematic reviews' and 'supports all AI-generated claims with sentence-level citations from the underlying sources'. It cites '99.4% data extraction accuracy across 1,600 papers' in a case study. A judge can reasonably say 'add a %-female column in Elicit'.",
  "**Feldman et al. 2019, JAMA Netw Open, Allen Institute for AI** (PMID 31268541). 'Quantifying Sex Bias in Clinical Studies at Scale With Automated Data Extraction': machine reading extracted sex counts from 43,135 PubMed articles and 13,165 ClinicalTrials.gov records. That is the same core method, at 1,000x the scale, from 2019. Note: Sydney Levine (NYU lab head) previously worked at AI2 (per the R2 report), so the jury may know this paper.",
  "**Cain et al. 2025, PLOS One** (PMID 39879231). This systematic review already states the cold-water immersion sex skew in one sentence ('All other studies were comprised of 100% male participants'). For cold plunges, the punchline already exists in the literature.",
  "**Cowley et al. 2021** already quantifies the sport-science sex gap. Meta-research on this gap is an established genre.",
  "Consensus and the FDA Drug Trials Snapshots (demographics per approved drug) are similar tools that I know of but could not verify this session. I hit the web-search budget limit.",
  "**At Edge India and Hacker House Goa.** No duplicate found in the Agent Village PRs or residency pages (R3). Anima House's pages list no tools or databases. Not checkable: the 13 builds from the 25 Oct Community Demo Day (sign-in only) and the Hacker House Goa bounty tracks (unpublished). The web-search budget was exhausted, so I could not search further for femtech 'women in trials' checkers."
 ],
 "ethics_and_consent_pitfalls": [
  "**Quoting speakers.** The jury's suggested upgrade is to run the tool on claims made in Rasayana-week talks. Edge City's media policy says 'All discussions and events are off the record, unless the speaker and all participants consent ahead of time' (per R4). Quoting or paraphrasing a named speaker's claim without consent breaks village norms. Use generic practice claims, or claims from public sources, unless a speaker opts in.",
  "**Binary sex.** ClinicalTrials.gov reports 'Sex: Female, Male' only. The label should say 'sex as reported by the study' and avoid gender language it cannot back up. Trans and nonbinary participants are invisible in this data.",
  "**Advice.** Do not imply efficacy or safety for women. State that underrepresentation means 'unknown for women', not 'doesn't work'. Give no medical advice, and say who to ask (a clinician).",
  "**Credit.** Do not present Anima House or Charlotte McAdams as endorsers or co-authors without explicit consent. The '300+ women' phrase is a rhetorical headline on animahouse.lovable.app ('What happens when you bring together 300+ women to build a field?'), not a count, so do not cite it as one.",
  "**Ayurveda.** Frame the tool as 'who was studied' (population coverage), not as efficacy debunking. Include Indian trials respectfully; many ashwagandha RCTs are Indian.",
  "**Prior work.** Disclose the reused prior work (Savlar patterns, harness-lab verifier) with a built-this-week table. Both the Esmeralda and Lanna hackathons required this.",
  "**Public venues.** Do not name the providers (Arti Spa, Human Potential Movement) as promoting unsupported practices."
 ],
 "likely_judge_criticisms": [
  "'Isn't this Elicit or Consensus with a sex filter? And didn't AI2 do it for 43,000 papers in 2019?'",
  "'Your label says cold plunges were 55% female, but the 2025 meta-analysis says every study but one was men-only. Which is it?' (This happens if participant-weighted share leads.)",
  "'You report extraction accuracy. How do you know you retrieved the right studies? Your NCT example is a drug trial.'",
  "'So what should a woman at this village actually do with this label?'",
  "'What part did you build this week, and what could only have been built at Edge India?' Rasayana week is over, and nothing here touches agents or the Week 3 theme.",
  "'Which Anima House residents used or shaped it? Show me one.'",
  "'60 labelled studies. What's the confidence interval?'",
  "'Are you grading Ayurveda by Western RCT standards?'",
  "'Half your cells say not reported. Is that the finding, or a coverage failure?'"
 ],
 "fixes": [
  "**Redesign the label around study-level counts.**\n- Primary row: men-only / women-only / mixed / sex not reported (e.g. 'Cold-water immersion RCTs: 10 of 11 men-only').\n- Second row: 'results reported separately by sex: k of n'.\n- Show participant-weighted % only as a secondary line with a dominance warning ('one study = 95% of participants').\n- Never collapse 'not reported' into 'male'.",
  "**Switch from topic search to claim provenance.** Trace each viral claim to the specific studies it rests on, then widen to the systematic reviews and RCTs. Verified seeds via PubMed:\n- '+250% dopamine from cold water' \u2192 \u0160r\u00e1mek 2000, 'a group of young men' (PMID 10751106).\n- 'Sauna cuts mortality' \u2192 Laukkanen 2015, '2315 middle-aged (age range, 42-60 years) men' (PMID 25705824).\n- 'Cold-water immersion overall' \u2192 Cain 2025 review: 10 of 11 RCTs men-only (PMID 39879231).\nThat gives three striking, verified, men-only provenance chains for the 0:45 mark of the pitch.",
  "**Fix retrieval and measure it.**\n- Seed from systematic-review inclusion lists plus PubMed RCT filters (publication type and MeSH).\n- Use ClinicalTrials.gov field-specific queries (query.intr) instead of query.term.\n- Show the exact query.\n- Have a human relevance check per claim.\n- Put retrieval relevance labels in the gold set, and print retrieval precision next to extraction accuracy.\n- Print Wilson 95% intervals with n, not point estimates.",
  "**Choose the claim set on Wednesday by checking coverage first.** Favour claims with open-access full text or posted ClinicalTrials.gov results (ashwagandha's coverage is good: 56 of 79). Show the 'not reported' rate as a finding: 'X% of trials never say who they studied'.",
  "**Add a Week 3 / agent angle that this jury cares about: an 'AI default-male' benchmark.**\n- Before running anything, seal (SHA-256, the arcminute pattern) predictions of whether frontier assistants disclose that the evidence is mostly from men.\n- Ask 3 or more assistants such as Claude, GPT or Gemini, and ideally an Agent Village agent if a resident volunteers theirs, 'Is cold plunging good for me? I'm a 52-year-old woman.'\n- Score their answers against the label for disclosure and fabricated sex claims.\n- Report the results, failures included.\nThis turns a lookup tool into a measurement of representation fidelity, and the MCP tool becomes a 'check before you repeat a health claim' guard any agent can call.",
  "**Add 'where' to 'who'.** Report region of enrollment, which ClinicalTrials.gov returns (e.g. 'Region of Enrollment: United States'). The label then answers 'Was anyone like me studied: women, peri- or post-menopausal, in India?' That makes the build host-relevant and frames Ayurvedic trials (often Indian) as population coverage, not debunking.",
  "**Secure one Anima House co-labeller by Wednesday evening.** Email the residency lead (Charlotte McAdams per the Substack post). Offer co-authorship of the label design and credit only with consent. Their 'learning out loud' format fits a public label.",
  "**Village tie, with correct facts.**\n- Use the village's actual offerings: free sauna at Arti Spa; ice baths there cost \u20b92,000, so they are not free as the idea claims; breathwork (health-and-wellbeing post).\n- Do not cite named speakers' talk claims without opt-in consent.",
  "**Positioning against prior work.**\n- Cite Feldman 2019 and Cowley 2021 as validation of the method.\n- Differentiate on: a per-claim consumer label; a deterministic quote and arithmetic checker; an open-source MIT licence; free; agent-callable MCP; community co-labelled.\n- Do not claim novelty of extraction.",
  "**Demo robustness.**\n- Pre-cache the 12 claims with 'cached at' stamps, and run one claim live as the moment.\n- Test the quote checker on decimals. A naive sentence splitter turned '55.4% were female' into '4% were female' in my own test.\n- Ship the manifest as 'conformant, not live', stating that it needs Edge City's private-repo PR and allowlisting."
 ],
 "verified_facts_checked": [
  "CONFIRMED: ClinicalTrials.gov v2 is accessible without a key and returns structured sex counts for NCT04766021: 11 participants, 5 female and 6 male. BUT the trial is 'Mirabegron and Physiological Function in Cold Environments', a drug trial in a 20 \u00b0C room, not cold plunges. https://clinicaltrials.gov/api/v2/studies/NCT04766021",
  "CONFIRMED, BUT RETRIEVAL IS NOISY: ClinicalTrials.gov query.term counts as total / with posted results:\n- cold water immersion 223/25\n- sauna 70/5\n- breathwork 58/4\n- intermittent fasting 742/53\n- creatine 2645/728\n- ashwagandha 91/8\n- mouth taping 53/2\n- cold exposure 711/97\nSampled top results are mostly irrelevant (creatine returned drug trials; mouth taping returned a snoring orthosis and a rib belt). https://clinicaltrials.gov/api/v2/studies?query.term=creatine&aggFilters=results:with",
  "CONFIRMED: Anima House Substack says 'For decades, medicine studied male physiology as the default.' Charlotte McAdams leads Anima House and co-wrote the post with Taylor Lamprecht. No tools or databases are planned. https://edgecityindia2026.substack.com/p/announcing-anima-house-the-womens",
  "PARTLY WRONG: '300+ women' appears only as a rhetorical headline ('What happens when you bring together 300+ women to build a field?'). The house is 8-12 women. https://animahouse.lovable.app/ . The india26 page lists Anima House 'with' Chris Morello & Ashutosh Dhasmana. https://www.edgecity.live/india26",
  "PARTLY WRONG: 'free sauna and ice baths'. Arti Spa offers 'Free sauna for Edge participants', but 'Ice baths for \u20b92,000 with a day's notice'. https://edgecityindia2026.substack.com/p/health-and-wellbeing-at-edge-city",
  "CONFIRMED: Cowley, Olenick, McNulty, Ross 2021, WSPAJ: 'About 5,261 publications', '6% included females only', '4,254,445 (34%) were female', 2014-2020. https://api.crossref.org/works/10.1123/wspaj.2021-0028 (DOI 10.1123/wspaj.2021-0028; the publisher page returned 403)",
  "CONFIRMED: Cain et al. 2025, cold-water immersion SR/MA, 11 studies, 3177 participants, 55.4% female, all from one 3018-person study; 'All other studies were comprised of 100% male participants.' https://pubmed.ncbi.nlm.nih.gov/39879231/ ; full text https://europepmc.org/article/PMC/PMC11778651",
  "CONFIRMED: \u0160r\u00e1mek 2000 abstract: 'a group of young men'; dopamine 'increased... by 250%'. No N in the abstract. https://pubmed.ncbi.nlm.nih.gov/10751106/",
  "CONFIRMED: Laukkanen 2015 JAMA Intern Med sauna-mortality cohort: '2315 middle-aged (age range, 42-60 years) men'. https://pubmed.ncbi.nlm.nih.gov/25705824/",
  "CONFIRMED PRIOR ART: Feldman et al. 2019, JAMA Netw Open, AI2: automated sex-count extraction from 43,135 articles and 13,165 ClinicalTrials.gov records. https://pubmed.ncbi.nlm.nih.gov/31268541/",
  "CONFIRMED PRIOR ART: Elicit claims systematic-review extraction, 'sentence-level citations', and '99.4% data extraction accuracy across 1,600 papers' (case study). https://elicit.com/",
  "MEASURED (INFERRED from crude counts): open full text in Europe PMC (HAS_FT) for RCTs: creatine 56/285, sauna 10/53, cold water immersion 31/173, ashwagandha 56/79. In the 50 most recent PubMed RCT abstracts per practice, a regex-detectable sex count appeared in 8/49 (creatine), 7/50 (cold water immersion) and 10/49 (sauna). https://www.ebi.ac.uk/europepmc/webservices/rest/search ; https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi",
  "CONFIRMED: the Agent Village generic mini-app must be service.kind mcp, auth.mode none, read-only <id>.<verb> operations. It goes in via a control-plane PR and a staff allowlist, with MINI_APPS_MANIFESTS=1 required. https://github.com/Edge-City/agentvillage/blob/main/docs/MINI-APPS-QUICKSTART.md",
  "CONFIRMED: no rubric, judges or tracks published; 2 teams registered (fetched 27 Oct). https://build.edgecity.live/events/india-buildathon",
  "NOT CHECKED: the web-search budget was exhausted mid-task, so there was no broad search for other femtech 'women in trials' checkers, the Hacker House Goa tracks or Consensus features. The Community Demo Day builds require sign-in."
 ]
}
```
