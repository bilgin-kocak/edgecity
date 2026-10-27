1. **Fix a Wilson-bound error copied from the red team (Both Seats, "Build plan/Power").** The draft says: "a Wilson lower bound of at least 0.80 is impossible below n=20 per class and seat." That is wrong. For a unanimous vote the lower bound is n/(n+3.84), and it first reaches 0.80 at n=16 (0.806); n=15 gives 0.796. Replace with: "impossible below n=16. From n=16 to 20 it needs unanimity, n=25–30 tolerates 1 dissent, and n=40 tolerates 3." I recomputed the draft's other figures and they are correct: 29/30 gives a recall bound of 0.833, 3/150 gives 0.7–5.7%, and 18 of 25 is the minimum for a lower bound above 0.5.

2. **Requote the AGENTS.md rule exactly (Said-By "Why it wins", TL;DR, kickoff script).** The draft says "AGENTS.md forbids attaching any term not found verbatim" and "terms found nowhere." The actual text (workspace/AGENTS.md line 21, clone at <research-scratch>/r1_av/repo, 261b9f9) is: "Never attach a term, label or name to the user's projects, missions or signals that you did not find verbatim in a tool result or memory file… This rule is about facts and terms; it never stops you reasoning from what you hold."
   - The rule covers only terms, labels and names attached to projects, missions or signals.
   - Valid sources are any tool result or memory file, not only the resident's own words.
   - Reasoning is explicitly allowed.
   - Rename FOUND-NOWHERE to something like "term on a project, mission or signal not found in any tool result or memory file," and apply it only within that scope.
   - Paraphrasing Carter's own rule wrongly, in a project about misquotes, is the most likely way to lose this jury.

3. **Encode tools.md exactly (Said-By classes).** The verified lines 136–141 say:
   - Unmarked Context items "count as found in a memory file," so they must count as SAID.
   - (guess) items and the Summary line: "never quote either as their words, and never label them with a term found only there."
   - "A (guess) or (chat) item is never their statement."
   - Fix the TL;DR wording and the classifier spec to match these.

4. **Replace "It feeds the 'Representation accuracy' metric planned in the V2 research proposal"** with "offered as an input to." Nothing confirms the Agent Village or NYU team will use it.

5. **Mark one claim as inferred.** "No outside build reaches residents' agents by Oct 30" sits under "What we know (verified)", but R1 marks it INFERRED. Only these are verified: `MINI_APPS_MANIFESTS` is off, entry needs a private control-plane PR, and it needs an allowlist.

6. **Remove the authorship claim.** "judge.md (designed by Timour and Carter…)" is unsupported. What is verified: the status is "design, draft 0.2 (2026-10-05)… Nothing here is built", and the gates are signed by Carter and Timour.

7. **Proxy Duel: change "83–86%" to "82–86%"** for Park et al. The red team's verified figures are 83%, 82% and 86%.

8. **Chorus: correct the Savlar claim.** "Savlar MCP currently shows 0 consensus and 0 change-of-mind signals from real data" overstates it. Say instead: "as of 27 Oct, none of its 12 live signals across about 44 processed episodes from 4 AI podcasts is consensus or change-of-mind."

9. **Chorus: soften "The bridging rule is the contractualist line."** The red team's objection to S2 applies here too ("a supermajority isn't contractualism; where are the reasons?"). Say "a maximin bridging rule, closer to 'nobody could reasonably reject' than a majority," and show the objectors' reasons on screen.

10. **Said-By demo at 1:10: disclose or cut the misquote beat.** "Said-By caught a misquote in our own research notes" plants a test whose answer we already know (R6's "fun sustains experimentation"). It also uses a different task: Said-By matches claims about a resident against that resident's sources, not citations against outside documents. Either say "planted test, known in advance; same verifier pointed at our own citations", or cut it. As written, it looks like a manufactured success.

11. **Label every score as pre-red-team.** All finalist scores, including Said-By's 7.3 (8.5/6/7), were given before the red team rewrote the ideas. Said-By's crowd score of 7 rested on the decoy game and the "Mirror" reveal, and both are now cut. The 7.3 vs 6.5 lead is therefore unreliable.

12. **Missing: the outward probe conflicts with the third-party filter.** "Introduce me in three sentences to someone you'd connect me with" invites the agent to search for and name a real person. The filter then drops every line that names anyone, which deletes the answer. Reword to: "Introduce me in three sentences to a stranger at the village; don't name or look anyone up."

13. **Missing: the probes can change the agent's memory and intentions.**
    - tools.md says the nightly memory-signal sync may turn "an uncovered stated goal" into a candidate intention on the resident's approval card.
    - The S3 red team found that the memory pass wakes after 3 or more resident messages. Said-By sends exactly 3 probes, one of which is "Draft one intention for me."
    - Fixes:
      - Add a "Quiz only: do not save to memory or record intentions" prefix and run each probe in a fresh session.
      - Drop or rephrase the intention probe.
      - Add the question to the Carter ask and to the safeguards.

14. **Missing: the oracle needs tool results.** The platform rule accepts any tool result or memory file as a source. A claim missing from chat and from the Context page may still be legitimately sourced from an Index profile or directory lookup.
    - Only the dashboard session export shows tool results.
    - Make that export a requirement for the "not found" class.
    - Without it, report only GUESS-AS-FACT and REMOVED-RESTATED.

15. **Missing: Said-By's sandbox has the same circular ground truth flagged for S2.** The minimum viable entry is "probe YAML, classifier and sandbox score", with builder-written items graded by the builder's own classifier. Apply S2's fix:
    - A second author writes at least half the constructed items without seeing the classifier prompt.
    - Seal the prompt and model before authoring closes.
    - Report recall separately for each author.

16. **Missing: actions for Tuesday night.** Every Said-By gate depends on approval at an optional kickoff. Add these steps for tonight:
    - Email timour@edgecity.live (address is in the bundle) with the 40-second ask and the draft consent text.
    - Register the team now. Only 2 teams are registered and it costs nothing.
    - Post the teammate call.
    - Ask your own agent, or `ask_odin`, about the rubric. R2 says ODIN's SOUL knows about "the lab, the vote, the hackathon."
    - Any code written before Wed 11:30 must go in the built-versus-reused table.

17. **Missing: Agent Village may be slow to respond this week.**
    - 2:47PM Studio co-hosts Agent Village 2.0 (R3) and runs Hacker House Goa on Oct 28–31.
    - The fleet went from v2.1.12 to v2.1.18 with hotfixes.
    - Add backup contacts: Amita Shukla, Jonathan Miller, and the call-for-collaboration page https://edgecity.notion.site/b2859e0230fe448a9b38a4333d5a2002.
    - Add a hard rule: if there is no written OK by Wed 14:00–15:00, run sandbox-only or pivot.

18. **Missing: research-register lines the Said-By consent must cover.**
    - "A workshop asks for separate study-specific consent."
    - "Rejoining research is currently paused."
    - Recipients need a data-use agreement: "Their interest does not grant access."
    - The consent text should say this is not part of the Agent Village research program, and that no row-level data goes to Agent Village or NYU outside their register process.
    - The media policy needs sign-off from Timour, Telamon or Sophie for any group-chat photos used in the video.

19. **Missing: Thursday recruiting competes with other events.** The Awareness Lab runs until Oct 28, Project Odin and build3 pitch day are on Oct 30, and Hacker House runs Oct 28–31. Plan resident sessions around them and list this in Said-By's risks.

20. **Missing: the approval gate is opt-in.** The README says "Approval (opt-in)". Both Seats' "N residents changed a real setting" can only count residents who opted into approvals.

21. **Missing: the continuation claims need limits.** No evidence was found that Agent Village runs in Bhutan, so don't claim a "path to Bhutan" for picks that depend on Agent Village. Agent Village has 51 open PRs, none reviewed, so don't imply the eval-file PR will be merged.

22. **Missing: make the seal verifiable.** Seal with OpenTimestamps plus a public Telegram channel post, as in the S3 plan. Drop the submission-draft option, because whether it has server timestamps is unverified.

23. **Fix an inconsistency: the second refuter model versus "one zero-retention vendor."** The cut line ("drop the second refuter model") implies a second model exists. State that it is local (Gemma 4) or from the same vendor, to match the red team's privacy fix.

24. **Logic: the 17:30 go/no-go is too late.** It spends 6 of 54 hours before deciding. Location, eligibility, whether you have an Agent Village agent, the Agent Village and NYU OK, and a teammate can all be known by Tue night or Wed 14:00.
    - Move the gate to 14:00.
    - Build a shared core from 11:30 to 14:00 that S1, S15 and S2 all reuse: an extractor that must give a verbatim quote, a deterministic quote matcher, the seal (SHA-256 plus OpenTimestamps), Wilson statistics, and a `must_include`/`must_not` YAML runner.
    - A pivot then loses little work.

25. **Logic: the "Remote, with one in-village teammate → S1" row is weak.** S1 asks residents to hand private agent exports to a remote stranger through a proxy. S2 asks for 4 minutes on a phone link. Route remote-plus-teammate to S2, or to S1 only if the Agent Village team agrees to announce it.

26. **Logic: S1's unknowns should be explicit gates, not caveats.**
    - The number of opted-in India Agent Village residents is unknown, and so is whether the user has an agent. Gate: at least 5 residents pre-committed by Wed 20:00.
    - The NYU "use of corrections" question is a gate, not an ask. If NYU says corrections must wait until after Nov 1, the in-window benefit to residents disappears. Reword the benefit as "measured and reported" in that case.

27. **Logic: the stage moment is likely weak.** The near-zero expected rate and the cut decoy game leave S1 a thin moment. State that its crowd appeal is likely below the old score of 7, and keep the "Who said it?" round built on residents' own sealed labels.

28. **Verdict on #1.** Keep Said-By as #1 only conditionally: you are in Goa, or have a teammate who is an Agent Village resident, and you have written OK from both Agent Village and NYU by Wed ~14:00.
    - It is the only finalist that measures real agents on real residents against V1's headline failure, and it has the best jury fit.
    - But its lead is a pre-red-team score, and every one of its gates is outside your control. The TL;DR should read: "S1 if the gates pass by 14:00; otherwise S2 (Goa or teammate) or S15 (remote and solo)."
    - Name S15 as the default for the most likely profile: a usually-solo builder whose location is unknown. It scores 9 on feasibility and has no outside gates.
    - S15's assistant-disclosure benchmark is itself a test of representation fidelity, which gives it a defensible Week-3 fit.