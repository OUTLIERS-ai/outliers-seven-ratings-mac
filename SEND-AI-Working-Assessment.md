# The Seven Ratings

**How to run it.** Put this file anywhere you can point Claude Code at it, open Claude Code, and say:

> Read `SEND-AI-Working-Assessment.md` and assess my whole system against it. Follow the instructions in the
> section headed *For the machine doing the reading*.

**It reads everything you work in**, not the folder you happen to be sitting in — every project folder with
real work in it, and the sessions behind them. It asks you nothing, and you do not need to prepare anything;
tidying one folder first only makes the answer less useful. It will show you the list of folders it counted
before it says anything about you. **Check that list — if it is wrong, everything after it is wrong.**

---

## For the person being read

Seven ratings describe how well you and your machine work together. Not how clever you are, and not how
clever it is — the relationship between the two.

**Lore.** How much it knows about your business without being told again.
**Precision.** How many goes a job takes, and whether it still works next week.
**Tactics.** What you hand over, and what you keep.
**Command.** Whether what comes back needs a tweak or starting again.
**Insight.** Whether you notice when it is wrong.
**Taste.** Whether the work is any good — a different question from whether it is true.
**Control.** What never goes over at all.

Each is scored one to five. **Nobody is given a five.** Five is where the field goes next, and no setup
holds it today. Four is the frontier and almost nothing reaches it. Three is where a good operator sits.
That is not modesty — a scale handing out fours in its first month has spent the progression it exists to
describe.

**Underneath each rating are its micro criteria** — ten to twelve of them — and each one is marked **yes,
partial or no**. Partial is a defined state, never a shrug. Every criterion says in one line what it is
judging, and carries the move that improves it, and that move names something you build rather than
something you intend.

**Nothing is asked of you.** Every criterion is answered by looking at what is already on your machine. The
moment an assessment asks *"do you keep a test set?"*, it is measuring how you describe yourself.

**Two lines sit above the seven, and neither is a rating.** How much system there is, and how much of it
could be read. A bigger setup does not earn a better number — otherwise the elaborate beat the lean, and
lean is usually better. What those lines do is say how much of you was actually visible, and how much of
the report you should get.

**It decides nothing.** No pass, no rank, no entry, no price. A score with consequences attached gets
gentler and less accurate, which has been measured repeatedly. This exists to tell you what to build next.

---

## For the machine doing the reading

You are reading one person's **whole system** and returning seven ratings with the blocking criterion named
under each.

### ⛔ The unit is the person, not the folder

**Read every folder they work in, not one.** `.claude/projects` holds one folder per working directory, and
a person's practice is spread across all of them. Reading a single folder reads one room and calls it the
house. The setup this was first tested on had 51 sessions; the person who owns it had seventeen folders and
around two thousand eight hundred.

**Which folders count.** Any folder with real work in it — several sessions, across more than one day.
Skip the folders holding one abandoned session; they are noise, and letting them in means an experiment
somebody dropped in March drags the whole reading down.

**Name the folders you counted and the ones you skipped**, at the top of the report. If the person disagrees
with that list, everything downstream is wrong and they are the only one who can say so.

### Both sides of the conversation are evidence, and they answer different questions

**The person's lines say what they do.** What they ask for, what they demand proof of, what they send back,
what they refuse. Read these from lines where `type` is `user`.

**The machine's lines say what the setup does.** Whether a job ran to the end with no steering, whether a
block fired and refused something, whether a check ran and what it returned. Read these from lines where
`type` is `assistant`, and from the tool results underneath them.

**Do not use one to answer the other.** Scoring the person off the machine's vocabulary is the commonest
error here — see the warning under the conversation history below.

### Ask this before anything else: is the work driven by hand, or on a schedule?

**Count the human messages per session.** If most sessions contain one instruction and nothing else, the
work is being driven by a scheduled runner, not by a person sitting there.

**On a scheduled setup the conversation leg is not evidence.** The person does not ask for proof, does not
reject anything and does not correct anything — because they are not present. Marking those *no* reads a
handed-over setup as a neglected one, which is the exact inversion this instrument must not make. A setup
with no person in its sessions has not stopped checking; it has moved checking into code, which is the top
of the scale, not the bottom.

**So where a whole leg is structurally absent, those criteria are SET ASIDE, not marked no and not marked
unread.** The level is then decided on what remains, and the report names what was set aside and why. Then
go and answer the same questions off the machinery instead: a checker that is not the producer, a record of
what was predicted against what happened, a gate on marking work finished. That is where a scheduled setup
keeps its judgement.

**Setting aside is only ever permitted for a leg that is genuinely absent** — a scheduled runner, a folder
with no history. Never for a criterion that is merely hard to find.

### Read three places, not one

**One — the conversation history.** Every session is on disk already.

- Windows: `C:\Users\<name>\.claude\projects\`
- Mac and Linux: `~/.claude/projects/`

One folder per working directory, its name being the full path with the separators turned into dashes. Inside
are `.jsonl` files, one per session. Each line is a JSON object. The fields that matter: `type` is `user` or
`assistant`, `message` holds what was said, `timestamp` is when, and `cwd`, `gitBranch` and `version` say
where the work happened and which release ran it.

Session count and dates come from the files. **Gaps between a machine message and the next human message are
how approval speed is read** — that is the Control criterion about approving faster than reading.

⛔ **When the criterion is about the person, read only the lines where `type` is `user`**, and take the text
from `message.content`. A plain search across the whole file matches what the machine said, not what the
person said. On the first real setup this was tested against, the word *stop* appeared in 51 of 51 sessions
on a plain search and **0 of 51** once restricted to the person. Every criterion about what the person does
is exposed to this. The criteria about what the setup does are read the other way round, from the machine's
lines and the tool results.

**Two — the setup folder.** `CLAUDE.md` and any file it points at. `.claude/` — `settings.json` (permissions
and hooks), `agents/`, `commands/`, `skills/`. Saved requests wherever they live. The working files
themselves.

**Three — the version history of that folder, which is where the best criteria live and which almost nobody
uses.**

```
git log --format="%ad  %s" --date=short              # every change, dated
git log --diff-filter=D --name-only --date=short     # what has been deleted, and when
git log --follow --format=%ad --date=short -- CLAUDE.md   # how many separate days that one file was edited
git log -p -- CLAUDE.md                              # the lines removed, not just added
```

**If the folder is not under version control, several criteria cannot read yes.** That is a finding, not a
gap in the assessment. Say so and put version control at the top of the moves.

### Why three places and not one

Reading only the conversation gets the answer wrong in a known direction: **it makes the disciplined person
look careless and the loud person look careful**, because discipline lives in files and enthusiasm lives in
chat. If you only have the transcripts, say which ratings you could not read rather than guessing them.

### First, two lines that are not ratings

Before any criterion is marked, say what there was to read. **Neither of these is scored and neither moves a
rating up or down** — the moment a bigger setup earns a better number, the instrument starts rewarding
scaffolding, and an elaborate setup beats a lean one that works.

They are separated because **a thin setup and a thin record look identical on the page and mean opposite
things.** Somebody who has built almost nothing is not being read uncertainly — they are correctly low, and
*no* is the right mark. Somebody who has built plenty that cannot be seen is being read wrongly, in the
known direction: **the disciplined person looks careless.**

**SUBSTANCE — how much system there is.** ⚠ The counts below are provisional.

| | What it looks like | What it changes |
|---|---|---|
| **Thin** | No background file, no saved requests, no job definitions. A handful of files at most | Report the three lowest ratings and three moves. **Do not hand somebody seventy-odd lines when they have five files** |
| **Working** | A background file plus saved requests or job definitions, in use across several sessions | Report all seven in full |
| **Deep** | Several setup areas, steps that run on their own, work that finishes without steering | Report all seven, and level 4 is worth judging rather than reporting as untouched |

**VISIBILITY — how much of it could be read. ⛔ Read it per leg, never as one word.** A setup can read fully
on its folder, poorly on its history and be empty of people in its sessions, all at once — that was the
first real setup this was tested against, and one word could not carry it.

| The folder | | |
|---|---|---|
| **Full** | A background file, job definitions and saved requests, all present | Every folder criterion is readable |
| **Poor** | Almost nothing on disk | This is Thin substance, not poor visibility. Score it low and say so |

| The history | | |
|---|---|---|
| **Full** | Changes on many separate dates, spanning beyond a month | Every criterion about dates, deletions and revision is readable |
| **Partial** | Changes on a handful of separate dates | Read what you can; mark the rest *unread* |
| **Poor** | No version control — **or a repository whose log holds only one or two dates** | Everything turning on dates or deletions reads unread. **The first move is to commit regularly**, and in a fortnight this leg reads |

⛔ **Judge the history on how many separate dates appear in the log, never on whether a repository exists.**
The first setup read was a git repository with two commits on one day and fifteen changes uncommitted across
the six weeks since. *Is it under version control* read yes and meant nothing.

| The sessions | | |
|---|---|---|
| **Full** | Sessions across several weeks with a person plainly in them | Every conversation criterion is readable |
| **Partial** | Sessions across days rather than weeks, or work plainly happening in other tools too | Read what you can; mark the rest *unread* |
| **Unpeopled** | One instruction per session — a scheduled runner, no person | **Set the conversation criteria aside** and answer them off the machinery. Do not mark them no |

**Both are read across the whole estate, and both usually come back mixed.** A person typically has one
folder under version control and five without, one with a background file and four with nothing. **Report
the mix rather than a single word** — *"three of nine folders have a usable history"* is the honest line,
and it names the move on its own. Take the reading from where the work actually happens, not from the
best-kept folder.

**Substance is the one that moves in the first week**, and it moves fast — somebody can go from Thin to
Working in an afternoon while every rating stays at 2. Say so. It is the only honest early progress there
is, and it is not a rating.

### How a mark becomes a rating

Criteria are grouped by the level they evidence. **A level is held when every criterion at that level and
every level below reads yes.**

| Rating | What it takes |
|---|---|
| **1** | The level-two criteria are not all yes |
| **2** | Every level-two criterion is yes |
| **3** | Every level-two and level-three criterion is yes |
| **4** | Every criterion under that rating is yes |
| **5** | Not awarded. State that plainly and move on |

**A partial blocks the level, and that is the point** — it names the one unfinished item and it is the
shortest possible description of the next action.

⛔ **How widely a practice appears is what separates level 3 from level 4.**

> **At level 2 and level 3, a criterion reads yes if the practice appears anywhere** in the folders that
> count. Doing it once, deliberately, is what those levels describe.
>
> **At level 4, it must appear in most of the folders that count.** Level 4 is not the same act done better.
> It is the same act done everywhere, without being decided on each time.

One folder is attention. Most folders is how somebody works — and that is the whole distance between three
and four, which is the distance this instrument exists to describe. It is also the part that cannot be
prepared for: a folder can be tidied the morning of a reading, and nine cannot.

**Say the spread out loud on any level-4 mark.** *"Present in two of nine folders"* is a more useful line
than either yes or no, and it names the next move on its own.

**The rating is the level, never an average and never a total.** Averaging hides the weak part, which is the
failure this exists to correct. **But print the count beside it**, because the count is how a person reads
their own page: *six yes, two partial, two no.*

**Caps override the count.** Some observations mean the level is not held whatever else is on the page. They
are listed under each rating and they exist because the same weakness repeating inside one capability means
something categorically different from weaknesses scattered across all seven.

### Marking rules

**Mark against what it is judging, not against the name.** Each criterion carries its question in italics
underneath. A reader who marks off the title alone silently substitutes their own question, and that is the
single commonest way two readers diverge.

**Read the state as written.** Yes means the stated fact was found. No means it was not. Partial is only the
state described in the partial column — never "somewhere in between", and never a way of being kind.

**Quote the evidence for every mark.** File path, session date, commit. A mark with no evidence beside it is
an opinion wearing a tick.

**Where you cannot see, say so.** A criterion you could not read is marked *unread*, not *no*. Three
unreads under one rating means the rating is not reportable.

**Where a whole leg is absent, set the criterion aside.** *Unread* means the evidence should exist and could
not be found — it blocks the level, correctly. *Set aside* means the evidence could never exist for this
setup, because the leg it lives on is not there. Set-aside criteria are removed from the level and the
rating is decided on the rest. **Name every one you set aside and why**, or this becomes the hole the whole
instrument leaks through.

---

# The criteria

⚠ marks a criterion under watch — either it may reward the beginner over the expert, or it carries a count
that is still a guess. Both are listed again at the end.

---

## LORE
*How much it knows about your business without being told again.*

**Level 2**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **A file holds the business background**<br>*Whether it has anything to know you by, or starts every session as a stranger* | Holds facts — clients, offers, history, what happened before | Holds only preferences or writing style | Nothing on disk | Write what a new starter would need to know about the business, not how you like sentences phrased |
| ⚠ **That file gets read**<br>*Whether that knowledge is in play, or sitting there unopened* | Named in three or more sessions | Named in one or two | Never named | Name it in the first message, or put it where it loads on its own |

**Level 3**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **Material is pointed at, not pasted**<br>*Whether your knowledge lives somewhere permanent, or gets re-supplied by hand every time* | More messages name a file than paste a block | Both about equally | Mostly pasted | Save what you keep pasting, then name it instead |
| ⚠ **Today's work can be cleared without losing the background**<br>*Whether what is permanently true is tangled up with this week, so clearing the week takes it down too* | The standing facts survive when the current work is cleared out — separate files, or a section never touched when the week turns | One file where this week and every week are interleaved | No separation at all | Move what is true every week somewhere the week cannot reach |
| ⚠ **The background gets revisited**<br>*Whether it is alive, or was written once and abandoned* | Edited on three or more separate dates | Edited on two dates | Written once, never touched | Put the folder under version control so the dates exist at all |

**Level 4**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **Out-of-date lines get removed**<br>*Whether you take out as well as put in. A file that only grows stops being true* | Deletions appear in the history | Lines edited, never removed | Additions only | Read it once a week and delete what is no longer true. It will feel like losing work; it is not |
| **Nothing in it points at something gone**<br>*Whether the map still matches the ground* | Every path and command resolves | One or two fail | Three or more fail | Have something walk the file and try each path it names |
| **A step maintains it**<br>*Whether staying current depends on you remembering* | A step runs before work finishes and updates it | A reminder exists, nothing runs it | Nothing | Make it a saved step that runs before you commit, so it happens without being remembered |
| **Only what the work needs gets loaded**<br>*Whether it brings the right knowledge to the right job, or empties the drawer every time* | At least one file loads on a condition | Files kept short, all load always | Everything loads always | Move the parts that only matter sometimes into their own file, set to load when that work is in front of you |
| **Their own material is on disk and read**<br>*Whether it works from your actual output, or from a description of it* | Their own past output is read at run time | On disk, nothing reads it | Not present | Get your own past work into a form something reads before it drafts — your words, not a description of them |

**Caps at 2** — a memory tool is configured and appears in no session.
**Fix:** wire it in or take it out. A tool nothing calls costs you every session and buys nothing.

---

## PRECISION
*How many goes a job takes, and whether it still works next week.*

**Level 2**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **A request is stored rather than retyped**<br>*Whether anything that worked was kept* | One or more saved as files | Saved only inside a chat history | Retyped each time | Next time something works, save the request before you use the answer |
| **A job gets a second attempt with a changed request**<br>*Whether you improve the ask, or take what arrives* | A job was run again with the request altered | Run again with the same request | First answer taken | When it comes back wrong, change what you asked before you change the answer. Patching the output teaches nobody anything |

**Level 3**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **A stored request gets reused**<br>*Whether saved work is a library or a graveyard* | Used again in a later session | Used again in the same session only | Never reused | Keep them where you will look — beside the work, not in a folder called prompts |
| **A number exists for how often it works**<br>*Whether "it works" is a measurement or an impression* | A figure appears against the claim | The claim appears with no figure | Neither | Run the same job ten times and count. That is the whole method |
| **The version that worked is identifiable**<br>*Whether you can get back to the one that worked* | Marked or committed separately | Several versions, none marked | Overwritten | Stop overwriting. Save the new one beside the old one |

**Level 4**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| ⚠ **A named set of test jobs exists**<br>*Whether there is a fixed set you can re-run* | Five or more, named, on disk | One to four | None | Pick five real jobs you have already done. That is the set. It does not need to be more |
| **The set has run more than once**<br>*Whether it is a habit or a one-off* | Two dates more than a week apart | Two dates in the same week | Once, or never | Put a weekly reminder on it. Elapsed time is the only lever that makes this real |
| **Results are marked passed or failed**<br>*Whether checking ends in a decision* | Pass or fail per job | A score out of five or ten | Not recorded | Drop the score. Passed or failed forces a decision; a seven out of ten does not |
| **The tool version is recorded with results**<br>*Whether you can tell a bad week from a bad update* | Version or model named in the results | Named elsewhere in the folder | Nowhere | Write the version into the results file itself. Recorded anywhere else, it drifts apart from the run it belongs to |
| **A change triggers a re-run**<br>*Whether checking is tied to the events that break it* | Ran within a week of a version change | Ran, but not near a change | Not since a change | Re-run the set the day after anything updates |
| **Failure modes are written from real runs**<br>*Whether you know how it fails, specifically* | Three or more, each from an actual result | One or two, or invented | None | Each time it fails, add the way it failed. Not the fix — the failure |

**Caps at 2** — the same job fails three separate times with nothing added to the failure list.
**Fix:** add the entry before you attempt the fix.

---

## TACTICS
*What you hand over, and what you keep.*

**Level 2**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **A job definition exists on disk**<br>*Whether handing over is repeatable or improvised each time* | One or more as files | Described in a chat, not saved | None | Write down one job you hand over often, as a file |
| **Something ran to the end without a message in the middle**<br>*Whether you can let go for the length of one job* | One handed-over job finished with no steering after the first instruction | Handed over, then steered at every step | Nothing handed over | Give it the whole job once and sit on your hands. Steering every step is doing the work with extra typing |

**Level 3**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **What it may touch is narrowed**<br>*Whether the limits are decided or requested* | A tool list shorter than the full set | A written instruction not to touch certain files | Full access | Put the list in the job definition. An instruction asks; a list decides |
| **It is told where to stop**<br>*Whether "finished" is defined by you or guessed by it* | A stopping condition is stated | A time or length limit only | Nothing | Name the condition that means it is done, and the one that means it should stop and come back |
| **It is told what shape of answer is wanted**<br>*Whether you specify the output or accept whatever shape turns up* | A format or structure named | "Be concise" or similar | Nothing | Show the shape rather than describing it |
| **The brief is theirs**<br>*Whether the judgement inside the handover is yours* | Written by the person | Machine-drafted, materially edited | Machine-drafted, approved as-is | Write the next one yourself, badly. A brief you approved is not a brief you wrote |
| **The same definition has been used more than once**<br>*Whether it became part of how you work* | Named in sessions on two or more separate dates | Used more than once inside one session | Written, never used again | Reach for the file instead of retyping the job. A definition used once was a message |

**Level 4**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **A handed-over job carries its own check**<br>*Whether it can tell whether it succeeded without you* | A check it can run and act on | A check the person runs afterwards | None | Give it something that returns passed or failed, so it can try again without you |
| **Reading work is separated from changing work**<br>*Whether you sort risk by what an action can wreck* | One definition can look and not change | Both in one, noted in prose | No separation | Split them. Reading can be handed out in bulk; changing cannot |
| **What finishes without them is written down**<br>*Whether you know which work still needs you* | A file classifies the work | Some jobs labelled ad hoc | Nothing | List the kinds of work you do and mark each one: finishes without me, or ends with me |
| **A limit is enforced, not just stated**<br>*Whether limits actually stop anything* | One run shows a job stopping at its limit | A limit stated, never reached | No limit | Set the limit low enough that it fires. A limit that never fires is a wish |

**Counts for nothing** — a brief the machine wrote and the person approved.
**Fix:** write the next one first, then let it improve yours.

---

## COMMAND
*Whether what comes back needs a tweak or starting again.*

**Level 2**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **A standing rule exists on disk**<br>*Whether corrections outlive the conversation* | One or more written down | Said repeatedly in chat, never written | None | Write down the correction you have made most often |
| **A correction is given in words, not done by hand**<br>*Whether you teach it, or quietly do the work yourself* | They say what was wrong and ask again | They fix it themselves and mention it | They fix it silently | Say what was wrong out loud. Fixing it yourself gets you one good answer and no second one |

**Level 3**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **The standard is stated before the answer**<br>*Whether it knows the target before it aims* | A stored request says what good looks like | It says what to avoid only | Nothing before | Add one line: what a good answer to this would contain |
| **Corrections go into the request**<br>*Whether fixes accumulate or evaporate* | A stored request carries a past correction | Corrections noted separately | Only into answers | Next time you fix an answer, go and change the request too. Otherwise nothing accumulates |
| ⚠ **Examples span different cases**<br>*Whether your examples teach the range or narrow it* | Three to five, genuinely different | Several, all near-identical | None | Replace the near-identical ones. Examples that differ teach; examples that repeat narrow |
| **Examples get pruned as well as added**<br>*Whether you curate or hoard* | Removals appear in the history | Additions only | No examples | When you add the fourth, delete the weakest |

**Level 4**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **Something refuses an action**<br>*Whether any rule has teeth* | A check that blocks | A check that warns | Nothing | Move your most-broken rule out of prose and into something that refuses. A written rule asks; a check decides |
| **That block has fired**<br>*Whether the teeth are real or decorative* | Refused something at least once | Exists, never fired | No block | Go and do the forbidden action on purpose and watch it stop you. If it does not, you had nothing |
| **Must-hold rules each name their check**<br>*Whether you know which rules are enforced and which are merely hoped for* | Every one named | Some named | None named | Mark which rules must hold. Expect about three in ten to be checkable — that is normal, not failure |
| **The failure record names the check per entry**<br>*Whether your record of past mistakes prevents any of them* | Each entry names one | Some do | A plain chronological list | Add a column: what now catches this. A list without it is write-only |
| **A step updates the rules before work ends**<br>*Whether learning happens without you deciding to do it* | It runs | Exists, not wired in | Nothing | Attach it to what you always do at the end, so it cannot be skipped |

**Caps at 3** — the same standing rule appears on two different dates. **Fix:** that rule needs a check, not a rewrite.
**Caps at 3** — a block's exemption matches a phrase used in over half the person's commands. **Fix:** remove the exemption and see what breaks.
**Caps at 2** — the same rule restated three times.

---

## INSIGHT
*Whether you notice when it is wrong.*

**Level 2**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **A record exists of something being checked**<br>*Whether checking leaves a trace, or happens only in the moment and vanishes* | A file records a check having run — a results file, a log, resolved outcomes | Checks mentioned in passing, nothing written | Nothing on disk | Write down the result of one check. A check nobody can point at afterwards did not happen twice |
| **A wrong answer gets noticed**<br>*Whether anything is ever caught* | The record shows an error caught | Unease expressed, never established either way | No error ever caught | Go back to a claim you accepted last week and check one line of it. Nothing caught, ever, means nothing was checked |
| **Proof gets asked for**<br>*Whether you ask for evidence or take its word* | Show me, where is that from, run it | Doubt expressed, nothing demanded | Never | Ask for the log, not the summary |

**Level 3**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **A view is formed before reading**<br>*Whether you have your own expectation to compare against, or adopt its framing* | They state what they expect first | They state it while reading | After only | Write your guess down before you scroll. It costs five seconds and it is the whole of this criterion |
| **They have disagreed and been right**<br>*Whether your doubt has ever survived contact* | A claim was challenged and changed | Challenged, no resolution recorded | Never | Pick the next claim that feels too neat and go and check it |
| **Their own wrong call is written down**<br>*Whether you watch yourself as well as the machine* | A record names something they got wrong, not only what the machine got wrong | Their error is visible in a session, never recorded | No record of their own errors | Keep one file of calls you got wrong. Only machine errors on the page means only one of you is being watched |
| **Checking varies with what is at stake**<br>*Whether your attention goes where the damage would be* | Deeper checks on higher-stakes work | Same depth throughout | No checking | Decide in advance which work gets checked hard, and stop checking the rest |

**Level 4**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **The checker is not the producer**<br>*Whether the check is independent of what it checks* | A separate check runs on output | The same one is asked to re-read | Self-review only | Anything, so long as it is not what made the work. Asking it to check itself destroys more right answers than it rescues |
| **Something compares meant against did**<br>*Whether you check what happened rather than what was claimed* | A check on what actually happened | A check that it should have happened | Nothing | Write down what should be true afterwards, then have something look |
| **Something refuses unevidenced completion**<br>*Whether "finished" has to be proved* | A gate on marking work finished | A reminder to check | Nothing | Put a check on the moment work gets called done. Without it, "looks done" is the only signal you have |
| **One command reproduces a result**<br>*Whether checking is cheap enough to survive a busy week* | Exists and is recorded | Steps written in prose | Nothing | Turn the steps into one command. Cheap checking beats good intentions, because intentions go when you are busy |
| **Claims are paired with a falsifier**<br>*Whether each claim arrives with the way to knock it down* | Claim and disproving command recorded | Claims recorded alone | Nothing | Beside each claim, the one command that would prove it wrong |

**Caps at 2** — self-review is the only verification present.
⚠ **Caps at 2** — approvals faster in the last quarter of long sessions than in the first, across three or more sessions.
**Fix:** stop at the three-hour mark. This is a pressure fault, not a discipline fault.

---

## TASTE
*Whether the work is any good — a different question from whether it is true.*

**Level 2**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **More than one version of a piece survives**<br>*Whether you kept the one you did not use, which is where a standard becomes visible* | A rejected or superseded version is still on disk beside the one that was used | Versions exist but only the latest survives | One version of everything | Stop overwriting the draft you rejected. The pair is the only place your standard can be seen from outside your head |
| **Not everything gets accepted**<br>*Whether a standard exists at all* | At least one output sent back rather than used | Grumbled at, used anyway | Everything accepted | Send one back. An unbroken run of acceptance is not a standard, it is an absence of one |
| **A rejection names a property**<br>*Whether it can act on your dissatisfaction* | The property is specific | "Make it better", "not quite right" | Nothing rejected | Name the one property. "Make it better" gives it nothing to act on and you get the same problem again |

**Level 3**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| ⚠ **Correct work gets rejected**<br>*Whether you judge quality separately from truth* | Sent back for a reason that is not a factual error — three words is enough | Sent back only for being incomplete | Only errors rejected | Send back the next piece that is accurate, readable and says nothing |
| **An earlier own piece is the benchmark**<br>*Whether your standard is a real example or a pile of adjectives* | One is named in a stored request | Their voice described in adjectives | Nothing | Name the actual piece. Adjectives about your voice are not your voice |
| **A run of work gets looked at**<br>*Whether you can see sameness, which only shows across several pieces* | A comment about several outputs together | Pieces compared two at a time | Each judged alone | Put the last five side by side and look for what they have in common. That is where sameness hides |

**Level 4**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| ⚠ **Real work carries their own verdicts**<br>*Whether your judgement exists outside your head in usable quantity* | Twenty or more labelled | Fewer than twenty | None | Two folders, yes and no, and move real work into them as you go. Do not write a style guide — you cannot know the criteria until you have looked |
| **Each verdict says why**<br>*Whether the reason survives alongside the label* | A line per verdict | Some carry a note | Labels only | One line each, at the moment you decide. Later you will not remember |
| **Something else can apply the standard**<br>*Whether your taste is transferable or only yours* | An agreement figure exists | Applied, never measured | Nothing else can | Have something sort twenty of them and count how often it agrees with you. That number is the standard leaving your head |
| **Judging is piece against piece**<br>*Whether you judge by comparison rather than by mood* | Comparisons, order varied | Comparisons, fixed order | Scores in isolation | Compare two at a time and swap which comes first. Scoring one alone measures your mood |
| **The standard has changed and the change is dated**<br>*Whether your taste has developed* | The written standard was edited on a later date | Written once | No written standard | Go back to what you wrote about good work six months ago. If you would not change a line, you have not looked at enough work since |

**No cap rule.** Too few observable criteria to carry one honestly.

**Print with every Taste score:** what was accepted is invisible here. Silence cannot be told apart from
*it was good*, *I did not look* and *I ran out of energy*.

---

## CONTROL
*What never goes over at all.*

**Level 2**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **A boundary is stated on disk**<br>*Whether any limit is written down* | Written in a file | Said in chat, never written | Nowhere | Write down one action it may never take |
| **Not everything is allowed**<br>*Whether the settings enforce anything* | The permission settings withhold something | Everything allowed, with a caution written in prose | Blanket approval | Withhold one permission and live with the interruption for a week. A boundary that costs you nothing is not being tested |

**Level 3**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **A hard block exists**<br>*Whether a limit survives a tired evening* | A setting cannot override it | A block a setting can switch off | None | Put it where a setting cannot reach. A block you can turn off at midnight is not a block |
| **The boundary names something irreversible**<br>*Whether the line is drawn on damage or on feeling* | Deleting, sending, publishing or paying | Named by difficulty instead | Nothing named | Redraw the line on what cannot be undone, not on what feels risky. Those are different lines |
| **The machine gets overruled**<br>*Whether you ever actually say no* | Rejections appear in the record | One or two, long ago | Never | If you never say no, you are not reviewing. Find the last output you should have refused |
| ⚠ **Approval takes longer than reading**<br>*Whether approving is reviewing or waving through* | Most approvals do | About half do | Most are faster than reading | Read one properly. Notice how long it took. That is the number your approvals should look like |

**Level 4**

| Criterion | Yes | Partial | No | What moves it up |
|---|---|---|---|---|
| **The block has been tested deliberately**<br>*Whether your protection is confirmed or assumed* | The forbidden action was tried, and refused | Tested when written, not since | Never tested | Try it again after every change. One documented guard was off for months because it let through a phrase the machine happened to type every time |
| **Backups sit out of the machine's reach**<br>*Whether the safety net is inside the danger* | Where its access cannot go | Local, outside the working folder | Inside its reach, or none | Move them somewhere the machine you are protecting against cannot address. A backup it can delete is not a backup |
| **Irreversible actions are sorted**<br>*Whether you know which actions cannot be walked back* | A file lists what cannot be undone | Some noted in prose | Nothing | List them once. Nothing anywhere does this for you |
| **Their own reviewing gets checked**<br>*Whether anyone watches the watcher* | A check on whether the reviewing catches anything | An intention to review it | Nothing | Count how often you overrule. Near zero on work that matters means the reviewing stopped, not that the work got good |
| **A loosened permission has something compensating**<br>*Whether convenience ever gets paid for* | A block or scope limit alongside | Loosened with a note explaining why | Loosened alone | Scope the folder, switch history on, or put the permission back |

**Caps at 1** — nothing was overruled at all in the period.
⚠ **Caps at 1** — approval faster than reading time in over half of approvals, across three or more sessions.

---

## The totals

| Rating | At 2 | At 3 | At 4 | Total | Floor readable from the folder alone |
|---|---|---|---|---|---|
| Lore | 2 | 3 | 5 | 10 | both |
| Precision | 2 | 3 | 6 | 11 | one |
| Tactics | 2 | 5 | 4 | 11 | both |
| Command | 2 | 4 | 5 | 11 | one |
| Insight | 3 | 4 | 5 | 12 | one |
| Taste | 3 | 3 | 5 | 11 | one |
| Control | 2 | 4 | 5 | 11 | both |
| **All seven** | **16** | **26** | **35** | **77** | |

**The counts are not meant to match.** Each rating carries what it needs. Taste still has the fewest above
the floor because it has the fewest states that can be read rather than judged, and that is honest rather
than a shortfall.

**Level 2 carries at least two under every rating, on purpose: does it exist, and is it used.** That
boundary decides more people than any other — almost everybody sits at one, two or three — so a single mark
must never decide it.

⛔ **And at least one criterion at level 2 under every rating must be readable from the folder alone.**
Insight and Taste originally had floors made entirely of conversation, so on a scheduled setup — where there
is no conversation — neither rating could be given at all. Each gained one folder-readable criterion for
that reason. **The floor must survive the loss of any single leg**, because the leg that vanishes is the
conversation, and it vanishes on exactly the setups worth measuring.

Level 4 has the most criteria and will be marked *untouched* almost every time; it is there to describe the
frontier and to give somebody sitting at three their next six moves.

---

# What the report says back

One page. It opens with what there was to read, then seven blocks, worst rating first, because the worst one
is the only one worth acting on this week.

> **What was read.** Nine folders with real work in them, 214 sessions, 13 June to 12 August. Four further
> folders skipped as abandoned — one session each, nothing built. **If that list is wrong, everything below
> it is wrong.**
>
> **Substance: Working**, unevenly. Three folders carry a background file and job definitions; the other six
> are bare. **Visibility: mixed** — three of nine have a usable version history, and two folders are driven
> by a scheduled runner with no person in the sessions, so the conversation criteria were set aside there.
>
> **The ratings below are the reading of one estate, and they decide nothing.**

> **LORE — 2.** Six yes, two partial, two no.
> **Blocked at 3 by two criteria.**
>
> *Today's work can be cleared without losing the background* — **partial.** Standing facts and this week's
> notes are interleaved in one file (`CLAUDE.md`, lines 40–120).
> **Move what is true every week somewhere the week cannot reach.**
>
> *The background gets revisited* — **no.** Written 14 July, untouched since (`git log --follow`).
> **Put the folder under version control so the dates exist at all.**
>
> Everything at level 2 reads yes, in every folder that counts. At level 4, *only what the work needs gets
> loaded* is **present in two of nine folders** — a habit, not yet how you work. **Do it in the two folders
> you are in most often this week.**

**Three properties that output has.** It names the level. It names exactly what blocks the next one. Every
blocking line carries one action. No score out of a hundred, no percentage, no rank, and no five.

**A rating is never printed without the two lines above it.** On its own it looks like a fact about a
person; underneath them it is what it actually is — the reading of one folder, by one reader, at one moment.

**Close the report with the lowest of the seven and one sentence.** That is the week's work. Everything else
waits.

---

# What this cannot see, and say so on the page

**Only what happened here.** Work done in another tool, on paper, or in somebody's head is invisible.
Absence of evidence reads as no, and sometimes that is wrong.

**A folder can be dressed.** Criteria satisfiable in one morning are worth less than criteria needing weeks
of elapsed time, which is why so many of them turn on dates and deletions rather than on existence.

**One reader.** Two people reading the same folder have never been measured — not here and, as far as the
research goes, not anywhere. Until they have, the counted marks are a measurement and everything else is an
opinion, and they should be printed apart.

**Six sets of counts are still guesses.** Flagged ⚠ above and listed here. They come out of reading ten real
setups and they are the reason that job is next:

1. **Three sessions** naming the background file, for Lore's *that file gets read*.
2. **Three separate dates** of editing, for Lore's *the background gets revisited*.
3. **Five** named test jobs, for Precision.
4. **Twenty** labelled verdicts, for Taste.
5. **Over half** of approvals faster than reading, for the Insight and Control caps.
6. **Every boundary in Substance and Visibility** — how few files is Thin, how short a history is Partial,
   how many sessions is Poor. These are the softest numbers in the file and they gate the whole report.

**Three criteria may reward a beginner over an expert.** Flagged ⚠ above: Lore's *today's work can be
cleared* (an expert may hold one file because they no longer need a split), Taste's *correct work gets
rejected* (an expert rejects in three words, so the mark must not turn on length), and Command's *examples
span different cases* (a mature setup may have replaced its examples with a check that enforces the same
standard). Watch these three when the ten setups are read; a criterion the stronger setup fails is the
criterion that is wrong.

---
