> Battle plan and red-team report from the workflow, written before the final fact-check pass. Where this file and [IDEAS.md](../IDEAS.md) differ, IDEAS.md is the corrected version.

# Chorus (with receipts) (S12, agg 6.4)

# S12 battle plan: Chorus, with receipts

## 1. Name and pitch
**Chorus, with receipts.** The song Edge India earned. Every sung line is a resident's own words, used with their consent. The chorus is the one line that the people who disagreed most both signed. An AI's summary of the village gets stamped wherever residents never said what it claims.

## 2. Why it wins
- **Predicted rubric:** co-creation (25+ voice notes, 80+ voters), ethics built into the mechanism, a vote and verifier that work live, Push the Edge.
- **NYU Ethical Intelligence Lab:** the chorus is chosen by a bridging rule: the highest *minimum* agreement across opinion clusters. That makes it the contractualist line nobody could reasonably reject, not a majority pick. We cite Awad and Levine's caveat ("do not guarantee representative samples") before the judges can.
- **Timour:** agreement is reported as a Wilson 95% lower bound, the same gate `judge.md` uses. The prologue acts out his line "people need to see what it believes, where the belief came from, and how to correct it."
- **Continuity:** the map, vote data and method feed the roadmap's "shared archive of experiments" and become a template for Bhutan (Nov 11–19).
- **Against Harmonica, Talk to the City and the Habermas Machine:** lyrics are verbatim only, consent covers where a line is placed, and the room sings the result.

## 3. 90-second demo
- **0:00** Scope card: "N notes, M voters, of ~800 residents. Who took part, not the village."
- **0:10 Prologue.** A frontier model's unprompted summary of Edge India, written from the public Substack and wiki, scrolls past. The verifier stamps NOT IN WHAT RESIDENTS TOLD US on unsupported lines and cuts them off mid-word. A footer shows how often the verifier agreed with 30 hand labels (the real figure).
- **0:30 Verse.** The musician sings resident A's line, and resident B's opposing line answers it. Each is credited with the second it was said. Both residents approved being paired.
- **0:50 Bridge.** A line labelled "self-reported change of mind".
- **1:05 Reveal.** The vote matrix splits into two clusters, and one line lights up in both: "both sides signed this."
- **1:15 THE MOMENT.** The musician teaches the chorus (10 words or fewer) once, and the room sings its own members' words.
  - If no line clears the preregistered threshold, the chorus plays as an instrumental and the screen reads "We did not agree on one thing." This ending is rehearsed too.
- **1:25** The preregistration hash is shown and matches the one posted on Wednesday.

## 4. Real vs mocked
- **Real:** voice drop, consent store, transcripts, vote, clustering, chorus computation, verifier accuracy, preregistration hash, live performance.
- **Done by hand and logged:** quote trims and the melody.
- **Not claimed:**
  - that the chorus represents the village
  - that lyric fidelity is certified by speech recognition (contributors approve their sung line by ear instead)
  - that changes of mind were computed (they are self-reported)
- **AI vocals (fallback only):** labelled synthetic and C2PA-signed.

## 5. Architecture
- **Voice drop:** Next.js and MediaRecorder, reused from **ns-steward**. A SQLite consent store keeps three flags per line: quote, placement and publication.
- **Speech-to-text:** a Whisper-class model, plus Sarvam Saaras `kok-IN` for Konkani.
- **Candidate lines:** claim extraction from **Savlar / intelligence-layer**, adapted to short notes.
- **Vote:** a Polis-style agree / disagree / pass page, with PCA and k-means on the vote matrix.
  - Bridging score = the lowest, across clusters, of the Wilson lower bound on the agree rate.
  - Verses = the lines the clusters split on most.
- **Verifier:** **harness-lab**'s independent-verifier pattern. Claude Opus 5.5 narrates, and a model from a different vendor checks.
- **Preregistration:** SHA-256 sealing from **arcminute**.
- **Output:** a Remotion lyric video and a static map page, MIT licence.
- **Fallback:** ElevenLabs Music API (Creator plan, `composition_plan`, `sign_with_c2pa`).

## 6. Hour-by-hour (IST)
**Wed 28**
- **11:30** Kickoff asks (section 7).
- **12:30–15:00** Write and seal the preregistration: prompts, cluster method, thresholds, trim and exclusion rules, selection code. Post the hash and launch the voice drop.
- **15:00–20:00** Recruit a musician and an organizer. Set up a quiet recording corner at The Circle and post the call.
- **20:00–02:00** Build ingestion, transcription, extraction and the line selector.

**Thu 29**
- **09:00–12:00** Build the vote page. Run the prologue and hand-label 30 sentences.
- **12:00** Voice notes close. **12:30** Freeze 15–25 candidate lines using the sealed rule.
- **13:00** Open the vote and promote it at dinners. The musician builds a melodic frame with a slot for the chorus.
- **18:00–23:00** Send placement-consent requests. Build the lyric renderer.

**Fri 30**
- **09:00** Vote closes; compute results. **10:00** Consent lock: anyone who has not replied is excluded.
- **10:00–13:00** Finalize the lyric sheet. Contributors approve their sung lines.
- **13:00–15:00** Record the performance and the video. Write the README with the reuse table.
- **16:00** Submit, and keep editing until 18:00.

**Cut line, in this order:**
1. AI music fallback
2. Konkani
3. Remotion polish (screen-record the HTML instead)
4. Interactive map (use a static table instead)

**Never cut:** consent, preregistration, the vote, verifier accuracy, scope labels.

## 7. Day-1 people and asks
- **Timour (at kickoff):** the rubric, how the top 3 are chosen, how long a slot is, and whether a one-line call can go on the main Telegram.
- **Agent Village team (Carter Crouch):** can the call go in the 08:00 brief? We will not touch any agents or ODIN.
- **Creator Residency / LocalhostHQ:** a musician to arrange and sing. This counts toward their required resident collaboration.
- **Community Builders (Odd Table, Jungli):** spread the vote link.
- **Ground Floor:** invite Goan voices, in their own language.
- **ElevenLabs contact:** credits, plus written OK if the video is entered as a film.
- **Teammate post:** "Building a song from residents' own words, with receipts: the chorus is the line people who disagreed both signed. Need a musician or singer for a live Demo Day performance, and an organizer to get 80 people to a 2-minute vote. Everything open; everyone credited."

## 8. Safeguards
- **Three consents:** the quote itself, its placement (the contributor sees the line it is paired with), and performance plus publication. People can withdraw until Fri 10:00. After publication, takedown requests are honoured within 24 hours.
- **Audio and anonymity:** raw audio is deleted after transcription. Anonymous lines are checked for whether they could identify the speaker.
- **Excluded:**
  - group-chat text
  - named third parties, including complaints about staff or locals (a sealed rule)
  - minors
  - bystanders (headset mic, quiet corner)
- **Host community:** this is the visitors' song. No line describes Goans unless a Goan said it, and there are no synthetic Konkani voices.
- **Prologue:** never uses ODIN or residents' agents. A stamp means "not in what residents told us", not "false".

## 9. Submission package
- **Description:** the pitch, the scope numbers, and what was reused versus built 28–30 Oct.
- **Video (3 minutes or less):** the performance plus the method.
- **Repo (MIT):** code, preregistration and hash, the anonymised vote matrix, consent counts.
- **Image:** the lyric sheet with each line's source second and each cluster's agreement bars.

## 10. Risks and mitigations
- **Too few contributors:** show n on screen. Voting takes only 2 minutes.
- **No chorus:** the rehearsed ending makes honesty the climax.
- **Musician doesn't show:** use the AI fallback, with contributors approving their lines.
- **Disagreement attributed wrongly:** pairs come from the votes, not model inference, and both people approve the pairing.
- **"Gimmick" critique:** the deliverable is the method, the data and the Bhutan template; the song is how they are performed.

## 11. Solo vs team, Goa vs remote
- Needs presence in Goa, or a teammate there, for recording, recruiting and the performance. Working remote and solo is not viable.
- Best team: a builder, a musician and an organizer.

## Red team
```json
{
 "id": "S12",
 "verdict": "fixable",
 "fatal_flaws": [
  "These four flaws would sink the idea as written, but each can be fixed. (1) The project fails its own test. The chorus is billed as 'the one thing most of the village agreed on', but it comes from 20 to 40 self-selected contributors out of about 800 residents (sugermint, per R4). Under the project's own verifier standard, that headline sentence is UNSUPPORTED. The jury's own reference makes the point: Awad and Levine write that crowdsourcing platforms 'do not guarantee representative samples' (https://behavioralscientist.org/why-we-should-crowdsource-ai-ethics-and-how-to-do-so-responsibly/). On stage, an NYU judge would stamp the chorus the same way the prologue stamps the narrator.",
  "(2) The 'computed structure' rests on Savlar signals that Savlar has never produced from real data. Today's Savlar MCP get_brief shows 12 live signals across about 44 processed long-form episodes. Of those, 0 are EMERGING_CONSENSUS and 0 are change-of-mind signals. Savlar defines a change of mind as 'one person at two moments', so a single 60 to 90 second voice note can never yield a detected change of mind. The bridge is therefore elicited by prompt 3 ('what did you change your mind about?'), not computed. Convergence across short notes answering open prompts may not clear any honest threshold. If it doesn't, the climax ('the hall sings the chorus') disappears, by the project's own rules.",
  "(3) The lyric-fidelity verifier cannot certify that sung lines are verbatim. Automatic lyrics transcription is still error-prone: LyricWhiz, the best system in its comparison, reports 24.25% WER on Jamendo (https://arxiv.org/html/2306.17103; 2026 figures not checked). With exact matching, the verifier would reject almost every take. With a tolerance, it can't tell a model's word change from an ASR error. The central claim, 'every sung line is a verbatim quote', would then rest on a check that can't be relied on. For a project whose whole pitch is receipts, that is self-defeating.",
  "(4) 'needs_physical_presence: false' contradicts the demo. 'Both people are in the room' and 'the hall sings the chorus' both require someone in Goa. So do the in-person recording at The Circle and a Demo Day performance. Recruiting 20 to 40 contributors by link in a crowded final week, without being on site or having organizer channels, is the most likely way this fails."
 ],
 "serious_risks": [
  "Volume and the approval loop. Collection closes Thu 16:00 and every line needs its contributor's approval by Friday, in the same week as Hacker House Goa, Project Odin, build3 pitch day and the Awareness Lab. If one side of a verse pair doesn't reply or withdraws, that verse collapses. With only 2 teams registered (https://build.edgecity.live/events/india-buildathon), residents' attention is clearly scarce.",
  "The builder makes the real choices, even though the structure is called 'mechanical'. The prompts, embedding model, clustering, thresholds, which excerpts are picked from 40 notes, and the trims are all the builder's decisions. Without preregistration this is a garden of forking paths, and a skeptical judge will ask who actually chose the chorus.",
  "Verse pairs make a relation claim that a model generated: 'A disagrees with B.' Savlar's live brief already shows a misfiled quote: a Kokotajlo line about Claudes forming companies sits under 'AI expansion into physical work'. Pairing two named residents as opponents who don't actually disagree is the very V1 failure, 'attributed invented ideas to their principals' (https://blog.cosmos-institute.org/p/we-gave-a-village-personal-ai-agents).",
  "Spoken prose sung by a synthetic voice tends to sound stilted. Savlar's own verbatim quotes are disfluent fragments (for example 'it'll come yeah that's gonna be the next thing'), so trimmed voice notes will read like that too. If the melody is forgettable or heard only once, a room will not spontaneously sing it.",
  "AI-music fatigue in this particular room. LocalhostHQ, the village's media-lab partner, 'runs India's largest AI film festivals' (https://www.edgecity.live/india26). The Creator Residency explicitly expects 'an anchor piece (for filmmakers, artists, musicians)'. An AI-sung lyric video is unlikely to impress either group, so the provenance layer has to carry the whole entry.",
  "ElevenLabs licensing. On every plan from Free to Business, media rights read 'All online and offline commercial use permitted, except film, TV, radio, and Studio Games'. Free through Pro are 'For Individual Use Only'. Starter caps downloads at 30 min/month. Inputs may not name 'any artist's real name or stage name' or song titles (https://elevenlabs.io/music-terms). Calling the lyric video a 'short-film entry', or having Edge City (an organization) reuse it, sits awkwardly with those terms. A resident quote that names a musician or song would be a prohibited input.",
  "Weak rubric fit on benefit. The likely top-weighted criterion is benefit to the community (R2, INFERRED). As specified, the main output is a performance; the cultural-memory value only becomes concrete if the map and data are handed over as a durable archive.",
  "The prologue reads as a strawman. An AI narrator told to write a 'confident summary' and then caught out is a staged failure. Judges who study fabrication will ask whether the narrator was set up to fail, and whether 'UNSUPPORTED' means false or only 'not in our 30 notes'.",
  "The 'sealed chorus guess' proves nothing. The builder seals a guess and then controls the pipeline and thresholds that produce the answer, so a right or wrong reveal shows nothing. It undercuts the arcminute credibility the user is borrowing.",
  "Misapplied quote. 'Individual alignment did not automatically produce collective alignment' refers to agents built around individual users causing village-level problems (verified in the Cosmos post). It is not about humans disagreeing. Its author, Timour, is the most likely judge and will notice the stretch.",
  "The 'what did it get wrong?' prompt will draw complaints about taxis, noise, locals, staff and organizers. Singing those at a closing event in Goa risks breaching 'Honor Our Host Community' (https://www.edgecity.live/india26). Filtering them out risks the opposite charge of censoring disagreement.",
  "Demo Day format is unknown. The page doesn't say how long each top-3 presentation is or how the top 3 are chosen (https://build.edgecity.live/events/india-buildathon). A 2 to 3 minute song may take the whole slot and leave no time to explain the method."
 ],
 "competition_or_duplicates": [
  "Harmonica at Edge Esmeralda 2025 'prototyped a new format for structured, async dialogue using AI moderation and tools like Polis to surface collective views about human flourishing in the village' (https://www.edgecity.live/blog/edge-esmeralda-2025-month-in-review). The mapping half has already been done at an Edge village, and the organizers know it.",
  "Talk to the City (AI Objectives Institute) is open source. It clusters opinions and themes from interviews and has been used for Taiwan's MODA consultations, among others (https://ai.objectives.institute/talk-to-the-city).",
  "The Habermas Machine (Tessler et al., Science 2024, N=5,734) generates common-ground group statements and found that good ones 'incorporated dissenting voices while respecting the majority position' (https://doi.org/10.1126/science.adq2852; metadata confirmed via Semantic Scholar). Levine is a part-time DeepMind visiting researcher (R2), so judges likely know it. The real differentiators are verbatim-only lyrics and song form.",
  "The Agent Village constitution ballot (GODCONST) already had residents blind-rate 30 statements, 15 written by agents and 15 by ODIN, about what the village believes. It closed 25 Oct (https://github.com/Edge-City/agentvillage/blob/main/docs/GODCONST-TELEGRAM-BALLOT.md). Expect judges to say 'we just did collective statements this month'.",
  "Village Digest, a read-only summary of village Telegram (PR #276), and Edge Library, a knowledge graph with passage-level provenance (PR #506): https://github.com/Edge-City/agentvillage/pulls.",
  "Creator Residency anchor pieces from filmmakers, artists and musicians, required to publish on Edge City's channels (edgecity.live blog via repo mirror skills/edge-india/references/newsletter/creative-residency-edge-city-modern.md), plus LocalhostHQ's AI-film scene. A resident musician may already be writing a village song. UNKNOWN.",
  "Art prior art: Listening Post (Ben Rubin and Mark Hansen, 2002\u201305) voiced and sang fragments of real people's online chat. It is in the collection of the San Jose Museum of Art and the Science Museum Group (https://en.wikipedia.org/wiki/Listening_Post_(artwork)). Turning 'real people's words into song' is not new in itself; the consent and provenance layer is.",
  "NOT CHECKED: the 13 builds at the 25 Oct Community Demo Day (sign-in only), and whether anyone at Edge India or Hacker House Goa is making a village song or anthem. My web search budget was used up, so I could not search for these."
 ],
 "ethics_and_consent_pitfalls": [
  "Consenting to a quote is not consenting to where it is placed. Being set against another named resident as an opponent in a public performance needs its own consent, and the contributor should see the paired line before approving.",
  "Anonymous credit does not make a line unidentifiable. The AV research register warns: 'A distinctive story, event or combination of details can still identify you' (https://agents.edgecity.live/research-register). In a village of about 800, a verbatim 'what I changed my mind about' line can be traced to its author.",
  "Publication is permanent. 'Every build and team goes public with the results' (buildathon page). Contributors need a withdrawal path both before and after publication, and should know the lyric video will stay online.",
  "Voice is personal data. Keep raw audio only until transcription, then delete it. Store the minimum. DPDP consent duties take full effect 13 May 2027 (R6), but the jury will judge the ethics, not legal compliance.",
  "Recording at The Circle risks catching bystanders. The media policy says 'All discussions and events are off the record, unless the speaker and all participants consent ahead of time' (via R4; I could not re-fetch the Notion page). Record in a quiet corner with a headset mic.",
  "Use no group-chat text. Research use of Telegram messages requires 'separate, active research consent' (https://agents.edgecity.live/research-register). The idea already excludes it; keep it that way.",
  "No named third parties in lyrics, including staff, organizers and locals, unless that person approves. No minors from Edge Tomorrow without explicit parental consent; simpler to exclude them.",
  "Host community. This is the visitors' song and must not claim to speak for Mandrem or Goa. Lines that describe Goans should come only from Goans who chose to contribute.",
  "Disclose the AI. Label the vocals as synthetic and sign the audio with C2PA (`sign_with_c2pa` exists on the compose endpoint: https://elevenlabs.io/docs/api-reference/music/compose). Make sure no synthetic voice can be mistaken for a resident's.",
  "The prologue must not target anyone. Don't use ODIN or residents' agents as the 'confident AI' without the Agent Village team's consent, and stamp lines as 'not in what residents told us', not 'false'."
 ],
 "likely_judge_criticisms": [
  "'Your chorus is 31 people, not the village. You stamped the AI for that exact overclaim.'",
  "'Prompt 3 guarantees a bridge. That's elicited, not detected. What did the AI actually compute that a good songwriter with a spreadsheet couldn't?'",
  "'Isn't this Harmonica, Polis or Talk to the City with a soundtrack?'",
  "'You set the narrator up to hallucinate. Show me an unstaged AI summary failing, and your verifier's error rate against human labels.'",
  "'How do you know the sung words match? What's your lyric-ASR error rate?'",
  "'Did these two residents agree to be presented as opponents on stage?'",
  "'Why should the chorus be what most people said? Our compromise work (Moore, Choi and Levine, \"Intuitions of compromise: Utilitarianism, egalitarianism, contractualism\", Cognition, forthcoming: https://www.ethicalintelligencelab.org/publications) asks which aggregation rule is fair. Why majority and not something nobody could reasonably reject?'",
  "'You sealed a guess about a pipeline you control. What does the seal prove?'",
  "'What does the village have on Sunday besides a song? What carries forward to Bhutan?'",
  "'What was built this week, and what is Savlar?'",
  "'An AI singing a human community's words: is that flourishing, or an uncanny valley?'",
  "'That V1 quote was about agents, not people disagreeing.'"
 ],
 "fixes": [
  "Measure agreement instead of inferring it. Run two stages. (a) Voice notes, target 25 or more. (b) A 2-minute agree/disagree/pass web vote on 15 to 25 candidate verbatim lines, target 80 or more voters; this is far cheaper per person than recording. Chorus is the line with the highest minimum agreement across opinion clusters (bridging/maximin), so it reads: 'the people who disagreed most both signed this'. That also answers the contractualism and compromise question. Verses are the most polarized lines. The bridge is labelled 'self-reported change of mind'.",
  "Preregister before collection opens Wed. SHA-256-seal the prompts, cluster method, thresholds, selection code and trim rules, then publish the hash. This replaces the 'sealed chorus guess', which proves nothing. Ship a selection log so every contributor can see why their line was or wasn't used.",
  "Put the scope on screen everywhere: 'what N of ~800 residents who took part agreed on, 95% interval', plus who is missing (locals, staff, people who didn't take part). Cite Awad and Levine's representativeness caveat yourself before a judge does.",
  "Have humans perform it. Recruit a Creator Residency musician, whose residency requires 'at least one collaboration with another resident or with the community', to set the computed lyric sheet and sing it live. The AI music API becomes a fallback or backing track. Each contributor signs off their own sung line by listening to it. Forced alignment on a separated vocal stem is a secondary check only. Never claim fidelity is ASR-certified.",
  "If the AI vocals are kept: use the Creator plan ($22/mo; Music API is $0.15/min per https://elevenlabs.io/pricing/api), not Starter with its 30-min download cap. Regenerate only the failing sections with composition_plan v1 plus inpainting (`store_for_inpainting`, `source_from`). Turn on `sign_with_c2pa`. Strip artist and song names from lyrics. Don't call it a 'film' unless ElevenLabs gives written OK via the partner contact.",
  "Make the prologue unstaged. Give a frontier model the public Substack and wiki plus the corpus and ask for a summary of the village, with no instruction to be confident. Verify each sentence, and report the verifier's agreement with your own hand labels on about 30 sentences. Stamp lines 'NOT IN WHAT RESIDENTS TOLD US'. Leave ODIN and residents' agents out unless the AV team agrees.",
  "Use three layers of consent: the quote, the placement (show the paired line), and performance plus publication. Missing replies by Fri 10:00 IST default to exclusion. Delete raw audio after transcription, run a re-identification check on anonymous lines, allow no named third parties or minors, and use a quiet recording corner.",
  "Make the song survive dropouts. Keep 2 to 3 backup pairs per verse. Write and rehearse a 'no chorus' ending as well, for example an instrumental chorus with the on-screen line 'We did not agree on one thing', so honesty doesn't kill the demo.",
  "Handle the host community: call it the visitors' song. Exclude lines characterizing Goans unless a Goan said them. Optionally invite Goan contributors via Ground Floor in their own language (Sarvam Saaras supports kok-IN per R5). Never put words in their mouths through synthetic Konkani.",
  "Make the durable deliverable the open, consented map plus agreement data plus method, offered to Edge City as an entry in the 'shared archive of experiments' (https://www.edgecity.live/roadmap) and as a reusable template for Bhutan, Nov 11\u201319. The song becomes its performance layer. This scores on community benefit and continuity, not only spectacle.",
  "Change the presence flag to 'needs presence, or an in-Goa teammate'. At Wed kickoff, ask Timour for an organizer-approved call for contributions (main Telegram or the agent morning brief) and for how long a top-3 slot runs.",
  "Keep the chorus singable: one verbatim line of 10 words or fewer, repeated, taught to the room by the live musician before it is sung.",
  "Fix the pitch quotes. Use 'As soon as an agent claims to know its principal, people need to see what it believes, where the belief came from, and how to correct it' (verified) for the prologue. Drop the 'individual alignment' line or apply it correctly. Add a table separating what was reused from Savlar from what was built 28\u201330 Oct."
 ],
 "verified_facts_checked": [
  "CONFIRMED: the ElevenLabs compose endpoint takes a composition_plan. In music_v1, sections have positive/negative local styles, lines and duration_ms (3\u2013120 s), with at most 30 lines per section and 200 characters per line. Models are music_v1, v2 and v2.5. The endpoint also offers inpainting and `sign_with_c2pa`. The page describes no lyric-fidelity guarantee and no content moderation. https://elevenlabs.io/docs/api-reference/music/compose",
  "CONFIRMED: the Music API is for paid subscribers and costs $0.15/min. Starter is $6/mo, Creator $22/mo, Pro $99/mo. Generation cost is not a real blocker; licensing terms are. https://elevenlabs.io/docs/overview/capabilities/music , https://elevenlabs.io/pricing/api",
  "CONFIRMED in the music terms, Exhibit A: Free through Business allow commercial use 'except film, TV, radio, and Studio Games'. Free through Pro are 'For Individual Use Only'. Free and Starter prohibit streaming distribution, Free allows no downloads, and Starter caps downloads at 30 min/month. \u00a72.1 bans artist names, songwriter names and song titles in inputs. Free requires attribution. https://elevenlabs.io/music-terms",
  "CONFIRMED: ElevenLabs appears on the Edge India partner strip as a logo only. No role or resident credits are stated. https://www.edgecity.live/india26",
  "CONFIRMED: the buildathon page lists 2 teams. The rubric and prize split are unpublished. 'A song' and 'a short film' are welcome. It doesn't say how long top-3 presentations run or how the top 3 are chosen. https://build.edgecity.live/events/india-buildathon",
  "CONFIRMED: the newest Edge City India Substack post is still 9 Oct ('The First Three Days at Edge City India'). https://edgecityindia2026.substack.com/api/v1/archive",
  "CONFIRMED via the Savlar MCP (get_brief, list_sources, 27 Oct): about 44 of 887 episodes processed, 12 live signals, 0 EMERGING_CONSENSUS, 0 change-of-mind. A change of mind requires 'one person at two moments'; consensus requires 'at least 3 speakers on at least 2 shows'. https://savlar.com/intelligence",
  "CONFIRMED, though the idea's use is a stretch: in the Cosmos V1 post, 'Individual alignment did not automatically produce collective alignment' refers to agents built around individuals, and 'As soon as an agent claims to know its principal, people need to see what it believes, where the belief came from, and how to correct it' is verbatim. https://blog.cosmos-institute.org/p/we-gave-a-village-personal-ai-agents",
  "CONFIRMED: Awad and Levine (2020) say crowdsourcing platforms 'do not guarantee representative samples' and should 'qualitatively inform', not dictate. https://behavioralscientist.org/why-we-should-crowdsource-ai-ethics-and-how-to-do-so-responsibly/",
  "CONFIRMED: 'Intuitions of compromise: Utilitarianism, egalitarianism, contractualism' by Moore, Choi and Levine is listed as forthcoming in Cognition. https://www.ethicalintelligencelab.org/publications",
  "CONFIRMED: lyrics transcription is error-prone. LyricWhiz reports 24.25% WER on Jamendo and other prior systems 33% or more (2023 paper; current state of the art not checked). https://arxiv.org/html/2306.17103",
  "CONFIRMED: the AV research register says research use of group messages needs 'separate, active research consent', that 'A distinctive story, event or combination of details can still identify you', and that copies will be deleted by 1 Dec 2026. https://agents.edgecity.live/research-register",
  "CONFIRMED: Harmonica (Polis-style, AI-moderated) surfaced collective views about flourishing at Edge Esmeralda 2025. https://www.edgecity.live/blog/edge-esmeralda-2025-month-in-review",
  "CONFIRMED: Talk to the City is open source and used by Taiwan's MODA. https://ai.objectives.institute/talk-to-the-city . The Habermas Machine paper is Science 2024, N=5,734 (Semantic Scholar metadata). https://doi.org/10.1126/science.adq2852",
  "CONFIRMED: the Creator Residency expects an anchor piece 'for filmmakers, artists, musicians' and at least one collaboration with another resident or the community (repo mirror of the edgecity.live blog post 'creator-residency-goa-modern-renaissance'). LocalhostHQ 'runs India's largest AI film festivals' (https://www.edgecity.live/india26).",
  "CONFIRMED: Listening Post (Rubin and Hansen, 2002\u201305) voiced and sang fragments of real chat text. https://en.wikipedia.org/wiki/Listening_Post_(artwork)",
  "NOT RE-VERIFIED: the media policy wording 'All discussions and events are off the record, unless the speaker and all participants consent ahead of time'. The Notion page rendered empty to WebFetch, so I am relying on R4.",
  "NOT CHECKED: the web search budget was used up this turn. I could not search for existing Edge India or Hacker House village-song projects, independent reports on ElevenLabs lyric adherence, or the 25 Oct Community Demo Day builds (sign-in only)."
 ]
}
```
