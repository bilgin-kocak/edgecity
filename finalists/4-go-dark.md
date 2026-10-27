> Battle plan and red-team report from the workflow, written before the final fact-check pass. Where this file and [IDEAS.md](../IDEAS.md) differ, IDEAS.md is the corrected version.

# Go Dark: the whole Demo Day room saves the hatchlings (S13, agg 6.4)

# Go Dark: battle plan (verdict: fixable)

## 1. Name and pitch
**Go Dark: our lights, their beach.** Every phone in the room is a light on Edge's own part of the Mandrem shore. An "agent" keeps each light on for a good private reason. The hatchlings reach the sea only when the room agrees to a shared rule and goes dark together. Edge then measures its real beachfront lights before and after.

## 2. Why it wins
- **It makes universalization physical.** NYU's Ethical Intelligence Lab helped shape the rubric, and the lab's PNAS 2020 paper asks "what if everyone did that?" By design, one phone has no visible effect, and each phone shows what would happen if everyone did the same.
- **It plays out V1's lesson without touching the fleet.** V1 found that "Individual alignment did not automatically produce collective alignment." In the game, each agent serves its owner and turns dark only after its human says yes. Nothing touches Agent Village or MoralMod.
- **It produces measurements:**
  - the Thursday live run: join rate, time to dark, hatchlings saved
  - Riva's beachfront lux before and after a Dark Hours trial
  - a sealed prediction opened on stage, in the spirit of Timour's "be wrong in public"
- **It respects the hosts.** The map shows only Edge's lights, with consent: "these are our lights." No shacks, no enforcement.
- **It works across generations.** Kids can play, and the call invites games. The crowd reviewer scored it 8/10.

## 3. 90-second demo
- **Break before the slot:** a QR code on screen opens a plain web page with no permission prompts. Sessions resume when a phone is unlocked.
- **0:00–0:12.** "This village sits on a turtle beach. Morjim–Mandrem nests went from 8 to 276 in a decade. Last season's first nests came in December. These lights are ours: Riva's, with permission." The prediction's seal (hash) is shown.
- **0:12–0:32, agents on.** "Unlock." Each card shows its agent's reason, for example "kept your screen lit to find your room." Hatchlings stream toward the audience. Each phone reads: "Alone: 0 lost. If every agent did this: N lost."
- **0:32–0:50, agree to the rule.** Phones ask: "Shared rule: no lights toward the shore after dusk. Yes/No." Each yes turns that screen black. "Your agent can't decide this. You can."
- **0:50–1:10, THE MOMENT.** "Now lock your phones." The hall goes dark. The swarm turns toward the moonlit water and the "reached the sea" counter climbs. A live threshold curve shows most hatchlings lost at 70% dark and most saved at 95%. "No single phone mattered. All of them did."
- **1:10–1:30, reveal.** The sealed prediction is opened and compared with the result. Then: "Thursday night, light at Riva's waterline went from X to Y lux. Here's the playbook Edge keeps."

## 4. Real vs mocked
- **Real:**
  - each phone's live state
  - the room's choices
  - logged playtest data
  - the sealed prediction
  - relative lux readings (same phone, fixed exposure)
- **Simplified:**
  - Hatchlings follow one rule: crawl toward the brightest horizon, plus noise.
  - The agents are scripted policies, not LLM agents or Agent Village agents.
  - The map is stylized from venue photos taken with consent.
- **Not claimed:**
  - that phones in a hall affect any turtle
  - any role for sound: hatchlings respond to light, and the alleged Morjim turn-back is left out
  - any nest locations

## 5. Architecture
- **Server:** Node 20 with `ws` on Fly or Railway. It broadcasts about 40 bytes twice a second, using anonymous ids.
- **Phone:** vanilla JS. A phone counts as dark if any of these is true:
  - it has said yes to the rule (black page)
  - `visibilitychange` reports it hidden
  - its heartbeat has been silent for 3 s

  No mic, camera, motion sensors or Wake Lock.
- **Projection:** PixiJS with about 800 hatchlings. The light field combines Edge's lights, the phones (each weighted 1/N) and the moon. A sigmoid is tuned so the room must be about 90% dark.
- **Reuse:**
  - arcminute: SHA-256 commit-reveal and phone-camera measurement (Python/OpenCV)
  - dress-rehearsal: simulated clients for a 150-client load test
  - harness-lab: a README that separates what was built this week from what was reused
  - The game itself is new.

## 6. Hour-by-hour (IST)
**Wed 28**
- 11:30–12:30 Kickoff. Ask about the rubric, how the top 3 are picked, slot length, whether Garden Oasis is indoors, and the projector. Post the teammate ask.
- 12:30–14:00 The asks in section 7.
- 14:00–20:00 Server, client, projection, light-following (phototaxis).
- 20:00–22:00 Load test on cellular.
- 22:00–23:00 With Riva's OK and an escort: baseline lux at 3 waterline points. No people in frame.

**Thu 29**
- 08:00–12:00 Rounds, the yes/no vote, per-phone counterfactuals, threshold curve, sealing, CSV logging.
- 12:00–14:00 Light map.
- 14:00–16:00 Playtest with 5–10 residents and Edge Tomorrow kids at The Circle. Fix iOS quirks.
- 16:00–19:00 Polish. Add a single-phone QR mode for shack tables, in English and Hindi.
- 19:00–21:00 **Full run at a village gathering**, with organizer OK and consent announced, filmed from behind. This run is the submission.
- 22:00–23:00 Lux during the Dark Hours trial.

**Fri 30**
- 08:00–12:00 Analysis, README, one-page playbook. **Freeze at 12:00.**
- 12:00–15:00 Video, image, description.
- 16:00 Submit, then keep editing until 18:00.

**Cut line (drop in this order if behind):**
1. single-phone mode
2. agent round (keep the yes/no tap)
3. Dark Hours trial (report that it was asked for)
4. light map (fall back to a gradient)

Never cut the permission-free join, the Thursday run or the honest README.

## 7. Day-1 asks
- **Timour Kosters:** the kickoff questions, plus a 10-minute slot at a Thursday gathering.
- **Edge ops and Riva management:** dim or shield the beachfront lights after 22:00 Thursday (ideally also 30–31), with consent to measure. If they say no, there is no trial.
- **Ground Floor:** an introduction to turtle volunteers. Ask whether an outreach version would help them. Do a Konkani version only if it is made together with them.
- **Sydney Levine or Logan Walls (NYU), if they are on site:** "Is this a fair dramatization of universalization?"
- **Edge Tomorrow:** a kids' playtest with parents' consent.
- **Creator Residency:** film Thursday's run.
- **Teammate post:** "Building Go Dark, a room-scale phone game about Edge's own beach lights and olive ridley hatchlings. Looking for 1–2 people in Mandrem to help run and film Thursday's playtest. Designers and Hindi/Konkani speakers welcome. MIT code."

## 8. Safeguards
- **Data:** no mic, camera or motion access. Players see what is logged (anonymous id, state, timestamps) before they join.
- **What is shown:** no nest locations, no non-Edge businesses, no faces. A venue's lights appear only with that venue's consent.
- **Framing:** no enforcement angle. Never claim the Forest Department or volunteers endorse it without their written OK. Stay neutral in the run-up to the 2027 election.
- **Media policy:** get consent from everyone in frame. Work on the beach at night only with an escort.
- **Sources:** every figure is sourced, and claims are marked "alleged" where the source says so.

## 9. Submission
- **Description:** the pitch, the three measured numbers, a built-versus-reused table, and the limitations.
- **Video:** the Thursday run, 2–3 minutes, ending on the lux before and after.
- **Repo:** MIT licence, with the game, analysis scripts, round CSVs, the sealed prediction and its reveal, and the playbook.
- **Image:** a still of the swarm with the counter and threshold curve.

## 10. Risks
- **The top 3 may be chosen before any room plays it.** The Thursday video has to make the case.
- **Low join rate.** Thresholds use the fraction of phones that joined. Never add bots to a live round.
- **Wifi, projector or a daylit hall.** Use cellular data, high-contrast visuals and a recorded fallback.
- **"It's Earth Hour with a projector."** Answer with the measured lux, the yes/no mechanic and the sealed prediction.
- **Riva declines.** Report that you asked. The playbook still stands.
- **Off-theme for Week 3.** The agent round connects it to the week's theme.

## 11. Viability
- **Solo in Goa:** feasible. A helper makes Thursday's run better.
- **Remote:** weak. The Thursday run, the lux trial and the conversation with Riva all need someone in Mandrem. Without a teammate in Goa by Wednesday evening, it is at best a community-vote contender, so pick an idea that works remotely instead.

## Red team
```json
{
 "id": "S13",
 "verdict": "fixable",
 "fatal_flaws": [
  "Nothing is strictly fatal: there are no API, data-access or resident-consent blockers. Two flaws would sink it if left as written.",
  "(1) The signature moment only happens after selection. The page says only that the 'three top projects present' at Demo Day. It does not say who picks them, when, or how long each slot is, and it mentions no audience vote (https://build.edgecity.live/events/india-buildathon). INFERRED: the top 3 are picked from the written submission and video. A room-scale game that is only described, or shown with 10-30 people, can lose before the room ever plays it.",
  "(2) The 'one holdout flips a phone on and a cluster veers inland' beat contradicts the universalization claim the pitch rests on. Universalization is about acts that are harmless alone and harmful only if everyone does them (Levine, Kleiman-Weiner, Schulz, Tenenbaum, Cushman, 'The logic of universalization guides moral judgment', PNAS 117(42), 2020: https://api.crossref.org/works/10.1073/pnas.2014505117). A visible harm caused by a single phone is direct causation, not universalization. A member of the lab that co-ran the criteria session could point this out on stage."
 ],
 "serious_risks": [
  "**Thin measurable benefit (the 'awareness game' problem).** Turning phones over in a banquet hall changes no real light on Mandrem beach. The village ends 1 Nov, and last season's first nests were in December: Agonda on 11 Dec, and Morjim's first nest reported 28 Dec 2025, laid the Friday before (about 26 Dec, INFERRED) (https://www.thegoan.net/goa-news/morjim-beach-gets-season\u2019s-first-turtle-nesting-pit-with-99-eggs/141110.html). So an Edge 'Dark Hours' pledge has almost no runway left on this beach. This is exactly the gimmick-with-thin-benefit profile the jury is predicted to dislike.",
  "**The 'real Mandrem shoreline light map' shames identifiable local businesses.** Names are not needed: a short, well-known stretch of beach makes each light recognizable to locals. The demo venue itself is a candidate light source. Riva Beach Resort is on Mandrem Beach, is Edge's community hub, is open 24/7, and offers candlelight dinners on the shore (https://www.rivaresorts.com/, and the edge-india SKILL newsletter in the agentvillage repo). INFERRED: a projected map in which the host venue's or neighbouring shacks' lights pull hatchlings inland amounts to enforcement-by-shame aimed at hosts and partners, whatever the pitch says.",
  "**Asking about 100 people for microphone permission, in front of a jury shaped by AI ethics, is bad optics.** Edge's media policy is that everything is 'off the record' unless everyone consents (R4, citing https://edgecity.notion.site/Edge-City-Media-Policy-Shared-263d45cdfc59803cbf30f181bb164955). 'No audio leaves the phone' cannot be verified by the audience. The mic step also adds a second permission prompt that will cut participation.",
  "**Fragile room-scale tech.**\n- iOS requires DeviceOrientationEvent.requestPermission() from a user gesture, over HTTPS; the call otherwise rejects (https://developer.mozilla.org/en-US/docs/Web/API/DeviceOrientationEvent/requestPermission_static).\n- A face-down phone can sleep. Its JS and WebSocket then suspend unless the Screen Wake Lock API holds the screen on. That API is only 'Baseline 2025' and is released on visibility change, low battery or power-save mode (https://developer.mozilla.org/en-US/docs/Web/API/Screen_Wake_Lock_API).\n- About 100 clients on venue wifi or patchy cellular data.\n- If only 20 phones join, the darkness moment fizzles.",
  "**Venue and timing are unknown.** The Demo Day time is TBC. The venue is the 'Garden Oasis Banquet Hall' at Riva, and whether it is indoor or outdoor is unknown (https://build.edgecity.live/events/india-buildathon). Riva's site lists banquet halls but no capacity or Garden Oasis details (https://www.rivaresorts.com/). A daytime or garden setting would wash out a projector. Projector availability is unconfirmed.",
  "**Biological accuracy.**\n- Light is well supported: hatchlings are 'often fatally attracted to landward lights' and lights 'repel nesting sea turtle mothers' (https://en.wikipedia.org/wiki/Ecological_light_pollution).\n- Noise is not supported for hatchlings in the sources I checked: neither Wikipedia nor Florida FWC's lighting guidance mentions it (https://myfwc.com/wildlifehabitats/wildlife/sea-turtle/lighting/).\n- If silence affects hatchlings in the sim, a conservation-literate judge can call it invented.\n- The Morjim 'turn-back' was an allegation by 'turtle enthusiasts', blamed on noise AND lights (https://www.thegoan.net/goa-news/turtle-nesting-boom-on-goa-beaches-despite-tourism-rush/148613.html).",
  "**The leave-behind does not fit its user.** A game that needs a projector and a crowd is not a tool Forest Department volunteers can use during shack season. Konkani strings would mostly reach locals, which reintroduces the 'policing hosts' framing. Shack-season visitors are mostly Hindi or English speakers (INFERRED).",
  "**Agent Village is the jury's main research thread, and this idea has no tie to it.** INFERRED: if the NYU lab, Timour or Carter weight agent fidelity, the idea may look off-theme for Week 3 (Frontier Intelligence and Decentralized Futures). The jury's own score was 5.5 out of 10.",
  "**Practical presence dependencies.** The night shoot and the playtest need someone in Goa. A night on the beach needs an escort. The builder's location is UNKNOWN."
 ],
 "competition_or_duplicates": [
  "**Collective lights-off.** Earth Hour has done 'symbolic lights off' as a global collective act since 2007; the 2026 edition was 28 March at 8:30pm (https://www.earthhour.org/). Expect the judge line 'this is Earth Hour as a game'.",
  "**Audience phone participation.** Phones as lights and audience-controlled games are an established genre (concert phone-light moments, Jackbox-style audience play). INFERRED, not freshly verified: the WebSearch budget for this turn was exhausted.",
  "**Turtle light-pollution games and simulations.** I could not check for existing turtle-hatchling light-pollution games because the WebSearch budget was used up. Assume some exist and claim novelty only for the live, room-scale, real-shoreline combination.",
  "**Edge India.** I found no turtle, hatchling or olive ridley project in the Agent Village repo clones, Substack dumps or wiki captures in the scratchpad. The only mention is the newsletter line 'south to Morjim's turtle-nesting beach' (agentvillage `skills/edge-india/references/newsletter/a-typical-day-and-week-at-edge-city.md`). The 25 Oct Community Demo Day list (13 builds) is sign-in only and was not checked.",
  "**Hacker House Goa.** Bounty tracks are unpublished (R3: https://hacker-house-goa-2026.devfolio.co/). I found no evidence of an environmental or crowd-game track. Duplicate risk is low."
 ],
 "ethics_and_consent_pitfalls": [
  "**Phone microphones.** Mass mic access from audience phones conflicts with Edge's off-the-record norm and is unverifiable to the audience. Drop it. Use one announced laptop mic for room loudness, or no audio at all.",
  "**Shoreline footage.** Footage of real businesses' lights is an implicit accusation against hosts. Use a stylized map, or include only lights whose owners consent, starting with Edge's own venues (Riva, The Circle) and with their permission.",
  "**Nest and hatchery locations.** Do not show nest or hatchery locations. The Morjim hatchery is publicly reported at Temwada, but the game should still never place nests.",
  "**Political timing.** This is a politically charged period, with Goa Assembly elections around Feb-Mar 2027 (R5: https://en.wikipedia.org/wiki/Next_Goa_Legislative_Assembly_election). Avoid any framing of GSPCB, shacks or the Forest Department that reads as taking sides. Never imply that the Forest Department or volunteers endorse the project without written OK.",
  "**Factual framing.**\n- Say 'alleged' for the Morjim turn-back incident.\n- Label the simulation as illustrative.\n- Do not imply that phone lights in a hall affect turtles, or that one person's light kills hatchlings.",
  "**Playtest data.** Anonymous session states are fine. Tell players what is logged (join count, time-to-dark) before they join. Filming players for the submission video needs consent from everyone in frame, per the media policy.",
  "**Greenwashing.** Edge brought roughly 800 people to a turtle beach (R4: https://sugermint.com/goa-to-host-indias-first-edge-city/). A feel-good game with no real-world change can read as performative unless it ends in a concrete commitment by Edge itself."
 ],
 "likely_judge_criticisms": [
  "'What changed on the actual beach because of this? Did a single light go off?'",
  "'This is Earth Hour with a projector.'",
  "'Your holdout scene shows one person causing harm. That's direct causation, not universalization.' (from a Levine-lab perspective)",
  "'Who asked for this? Did the turtle volunteers or the Forest Department co-design it, or are you speaking for them?'",
  "'Is that Riva's light in your map? Whose businesses are you projecting as the problem?'",
  "'Why do you need 100 people's microphones?'",
  "'Noise doesn't misorient hatchlings, does it? What's real in the model and what's made up?'",
  "'How does this relate to anything we're researching this week (agents, representation, collective alignment)?'",
  "'What did you build in 54 hours versus reuse?' (mostly new work here, which is good, but say so)",
  "'It's fun, but is it a community-vote prize rather than a top prize?'"
 ],
 "fixes": [
  "**1. Make the demo permission-free.**\n- 'Go dark' = lock your phone. Send 'dark' on the visibilitychange event and use a server heartbeat timeout, so a disconnected phone also counts as dark.\n- Keep an optional tap-to-black-screen toggle.\n- Drop the phone mic. Measure room loudness with one laptop mic and announce it, or remove sound from the hatchling mechanic. Use sound only in the mother-turtle opening, labelled 'alleged'.\n- This removes iOS motion permission, Wake Lock and mic consent issues in one move.",
  "**2. Fix the moral model so it really is universalization.**\n- Make a single phone's effect imperceptible on the projected shore.\n- Give each phone its own 'If everyone in this room did what you just did: N hatchlings lost' counterfactual.\n- Replace the 'one holdout ruins it' beat with 'small fractions matter only at scale', and show the threshold curve live.\n- Seal the room's prediction of hatchlings saved (SHA-256, the arcminute pattern) before round 2 and reveal it after.",
  "**3. Win selection without the room.**\n- Run the full room-scale version at a real village gathering on Thu 29 Oct, such as a community dinner or an evening salon, with organizer OK and on-camera consent.\n- Film it as the submission video.\n- Report join rate, time-to-dark and saved/lost per round.\n- The video, not the Demo Day slot, is what earns the top-3 spot.",
  "**4. Replace the real-shoreline shame map.**\n- Use a stylized light map built from public imagery.\n- Or map only Edge-controlled lights (Riva's beachfront, The Circle at Ashvem), with their consent.\n- Make the self-critique explicit: 'these are our lights'.",
  "**5. Attach one real, measured commitment by Edge itself.**\n- Ask organizers and Riva for a 'Dark Hours' trial on the nights of 30-31 Oct: beachfront lights dimmed or shielded after a set hour.\n- Measure lux with phone cameras before and after at fixed points; this reuses arcminute.\n- Put the policy in Edge's coastal-venue playbook for future villages, and show the vote or ratification on stage.\n- Cite the Bombay HC's 2023 crackdown on beach parties near Morjim/Ashvem nesting sites (per https://en.wikipedia.org/wiki/Morjim) rather than the unverified '8 pm shack lights' order.",
  "**6. Re-target the leave-behind.**\n- Build a single-phone mode with a QR code for shack tables and guesthouse rooms, aimed at shack-season tourists (English and Hindi).\n- Offer it to the Forest Department's stipended local volunteers (https://en.wikipedia.org/wiki/Morjim) only if they ask, with a Konkani version co-made with them.\n- Make the README's 'what is simplified' section explicit.",
  "**7. Optional bridge to the jury's research (if time allows).**\n- Add a round 3 where each phone is played by a 'personal agent' that keeps its owner's light on for private benefit, so the swarm fails.\n- The room then ratifies a shared rule, and only that rule saves the hatchlings.\n- This dramatizes the V1 line 'Individual alignment did not automatically produce collective alignment' (https://blog.cosmos-institute.org/p/we-gave-a-village-personal-ai-agents) without touching the live fleet.",
  "**8. Logistics.**\n- Get the QR code shown during the break before your slot through the MC, without asking people to keep screens lit during others' pitches.\n- Confirm projector, house-light dimming and whether the Garden Oasis hall is indoor or outdoor at kickoff.\n- Keep a pre-recorded run as fallback.",
  "**9. Fact hygiene.**\n- 'Morjim-Mandrem nests 8 to 276; hatchlings 331 to 12,857': verified.\n- 'Last season's first nests appeared in December': verified.\n- Replace 'about six weeks after the village leaves' with that December wording.\n- Mark the 8 pm shack-lights order and the Herald Goa hatchling claim as unverified, or drop them."
 ],
 "verified_facts_checked": [
  "**VERIFIED: Morjim-Mandrem nest and hatchling numbers.** Nests rose from 8 (2014-15) to 276 (2024-25) and hatchlings from 331 to 12,857. Jan-Mar 2026: Morjim had 36 nests and 3,905 eggs, Mandrem 17 nests and 1,633 eggs. Named threats are artificial lighting from shacks and resorts, loud music, beach events, human movement, and illegal shacks in protection zones. The Goan, 23 May 2026: https://www.thegoan.net/goa-news/turtle-nesting-boom-on-goa-beaches-despite-tourism-rush/148613.html",
  "**PARTLY VERIFIED: the 'mother turtle turned back' incident.** The source says 'turtle enthusiasts alleged' that noise and lights at Morjim forced a turtle back to sea without nesting 'this season'. It is an allegation and blames lights as well as noise. Same URL.",
  "**VERIFIED, with a correction: Morjim's first nest.** It was reported 28 Dec 2025 (article date): 99 eggs at Temwada, laid on 'Friday', i.e. about 26 Dec (INFERRED). Agonda's first nest was 11 Dec. Morjim and Mandrem are 'sensitive zones'. The campaign has run since 1997. https://www.thegoan.net/goa-news/morjim-beach-gets-season\u2019s-first-turtle-nesting-pit-with-99-eggs/141110.html",
  "**VERIFIED: universalization paper.** 'The logic of universalization guides moral judgment', Levine, Kleiman-Weiner, Schulz, Tenenbaum, Cushman, PNAS 117(42):26158-26169, 2020. https://api.crossref.org/works/10.1073/pnas.2014505117 (the PNAS page itself returned 403).",
  "**VERIFIED: Royal Tomato enforcement.** GSPCB fined Royal Tomato, Vittaldas Wado, Morjim, Rs 21 lakh and shut it for 2 months. Monitoring logged 70 exceedances between 1 Jan and 5 Feb 2026. The club is in a Silent Zone near a turtle nesting site. The Goan, 10 Feb 2026: https://www.thegoan.net/goa-news/morjim-nightclub-near-turtle-nesting-site-shut-fined-rs-21l-for-violations/143290.html",
  "**VERIFIED: GSPCB monitoring gap.** Board minutes: 'the Real Time Online Noise Monitoring Systems cannot identify the source of the sound'; 38 stations. The Goan, 22 Jun 2026: https://www.thegoan.net/goa-news/noise-meters-come-under-pollution-watchdog-lens/149973.html",
  "**VERIFIED from Wikipedia (secondary source): rules on lights and parties.** The Tourism Department limits shacks to daytime operation with furniture removed after dark. The Bombay HC ordered a crackdown on beach parties near nesting sites in March 2023, with an inquiry into late-night parties at Morjim and Ashvem. The Forest Department pays stipends to local volunteers. https://en.wikipedia.org/wiki/Morjim",
  "**NOT VERIFIED: the 'Forest Department ordered shack lights out by 8 pm' precedent.** No source was given and the search budget was exhausted. Wikipedia instead mentions Tourism Department daytime-only shack rules.",
  "**VERIFIED: light-only phototaxis.** Hatchlings are 'often fatally attracted to landward lights', and lights 'repel nesting sea turtle mothers'. Noise is not mentioned for turtles (https://en.wikipedia.org/wiki/Ecological_light_pollution). Florida FWC lighting guidance also omits noise (https://myfwc.com/wildlifehabitats/wildlife/sea-turtle/lighting/). The game's sound mechanic is therefore unsupported for hatchlings.",
  "**VERIFIED: Demo Day details.** Riva, Garden Oasis Banquet Hall; time TBC; three top projects present; slot length, selectors and audience vote are not stated; rubric still unpublished; 2 teams registered. https://build.edgecity.live/events/india-buildathon (fetched 27 Oct).",
  "**VERIFIED: Riva's location and role.** Riva Beach Resort is on Mandrem Beach, where the Arabian Sea meets the Mandrem rivulet. Its site lists banquet halls (no capacity or indoor/outdoor details) and candlelight dinners on the shore (https://www.rivaresorts.com/). The Edge newsletter in the agentvillage repo calls Riva the 24/7 community hub on Mandrem Beach with direct beach access, and The Circle sits on Ashvem Beach road.",
  "**VERIFIED: iOS motion permission.** DeviceOrientationEvent.requestPermission needs a user gesture and HTTPS, and rejects with NotAllowedError otherwise. https://developer.mozilla.org/en-US/docs/Web/API/DeviceOrientationEvent/requestPermission_static",
  "**VERIFIED: Screen Wake Lock limits.** The API is Baseline 2025, HTTPS-only, and is released on visibility change, low battery or power-save mode. https://developer.mozilla.org/en-US/docs/Web/API/Screen_Wake_Lock_API",
  "**VERIFIED: Earth Hour precedent.** Earth Hour has used 'symbolic lights off' since 2007. https://www.earthhour.org/",
  "**CHECKED: no duplicate project found locally.** A local grep of the Agent Village clones and the Substack and wiki captures in the scratchpad found no turtle, hatchling or olive ridley project. Web searches for duplicates and for the November season start could not run because the turn's WebSearch limit of 200 was used up."
 ]
}
```
