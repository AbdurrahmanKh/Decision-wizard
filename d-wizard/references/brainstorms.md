# Brainstorms

A brainstorm is for finding ideas on one open topic, not for settling details or ways of doing them: those are left to rounds. It runs through Edward de Bono's Six Thinking Hats, each worn by a character the wizard draws, and it always takes two rounds:

- **Round 1, ideas.** The user writes first: each hat asks one question and says nothing else. Then some hats bring sparks, short questions that might set off more ideas. Then every hat suggests ideas of its own, and the user kills any card that misses.
- **Round 2, the council.** You write it from round 1's answers. The hats bring a few extras from what round 1 showed, and then every idea that survived comes before the council of all six hats, each giving its view in a line. The user kills ideas, takes a hat's comment as a new idea, adds variants of their own, and puts what survives in order.

After round 2 comes a decision round, starting from the top of that order. Every part serves one test: does it help generate more ideas?

Brainstorms need Decision Wizard 0.9.0 or later. An older wizard can't open one, so point the user to https://abdurrahmankh.github.io/decision-wizard/ if theirs says the file isn't a round. Wizard 0.9.0 replaced the one-file brainstorms of 0.8.0 (a `hats` list) and refuses them, so never write that form.

## When

Send a brainstorm only when the user asks for one. When a hard open question has no clear options yet, so a round would only guess at them, offer one in a single line and wait. When round 1's answers come back, write round 2 without asking: two rounds is the design. When round 2's answers come back, the next step is usually a decision round.

## The cast

The wizard draws the six characters, shows each one's name and label, and asks each hat's question in round 1. You write every other word they say, fresh for each brainstorm, in that character's voice.

| Hat | Character | Label | Voice |
|---|---|---|---|
| Blue | Cap, the capybara | The point | Calm and unhurried; frames the question, keeps the order, and sums up |
| White | Tally, the owl | Realistic | Calm and exact; says what we know, what we don't, and where a number came from |
| Red | Ruby, the fox | Human | Warm and blunt; says how it feels, with no reasons needed |
| Yellow | Sunny, the bee | The dream | Bright and busy; finds what's good and how far it could go |
| Black | Pebble, the tortoise | Caution | Careful and dry; looks for the cracks and always gives the reason |
| Green | Doodle, the chameleon | Twists | Playful and odd; turns the question sideways and tries another way in |

What each hat does at each step:

| Hat | Asks in round 1 (built in) | Suggests in round 1 | Says on the council |
|---|---|---|---|
| Blue | "Where is this going, and what are its main goals?" | Other paths: reaching the goal through another feature entirely | Whether the idea changes the point, measured against the user's goals; it values ideas that solve the core |
| White | "What's the smallest version of this that would already be worth having?" | Realistic additions from what is known: facts that lead to new ideas, quick wins | Known limits, how hard it is, and any illegal or forbidden use |
| Red | "What excites you most about this?" | More human, engaging, and emotional versions: a plain tool made beautiful, a chore made warm | How engaging, exciting, human, and wild it feels, or a warmer version of it |
| Yellow | "If you imagine it as wild as you can, how does it go?" | The dream: far ideas, hard to reach | Its benefits, even far or imaginary ones |
| Black | "What could make this useless, or hurt and go badly?" | Ideas that avoid bad outcomes, long builds, or work nobody needs | Every way it's bad or not worth it, even rare ones |
| Green | "What's a twist on this that nobody would expect?" | Twists | Another twist on the idea |

## Round 1

The user goes through round 1 in three passes, and the wizard keeps them in this order:

1. **Your turn:** six cards, Blue first. Each hat asks its question and shows nothing else; the user writes as many cards as they like in one box. Nothing you wrote shows until they have been through all six.
2. **Sparks:** a card for each hat that brings sparks, each spark with its own box, so a card the user writes remembers which spark set it off.
3. **Suggestions:** six cards, Blue last. Each shows the user's own cards under that hat first, then up to 4 of the hat's suggestions, each with a cross to kill it, and a box to add one more of their own.

The wizard ends round 1 on Blue's recap, which it builds by itself: what's standing, hat by hat, with counts. Killed cards wait in a bin in the top bar, the only place to restore them.

```json
{
  "config": { "title": "Steam Handheld, Brainstorm 1", "tagline": "Round 1: your ideas first", "product": "Handheld", "kind": "brainstorm", "round": 1, "needs_wizard": "0.9.0" },
  "topic": { "title": "Steam games on my handheld", "question": "What could get my Steam games onto my handheld?", "context": "..." },
  "hold": [
    { "hat": "blue" }, { "hat": "white" }, { "hat": "red" }, { "hat": "yellow" }, { "hat": "black" }, { "hat": "green" }
  ],
  "sparks": [
    { "hat": "yellow", "line": "Two to get you buzzing.", "sparks": [ { "id": "s3", "text": "Does the game have to run on the handheld at all?" }, { "id": "s4", "text": "What would you play if the battery never ran out?" } ] }
  ],
  "suggest": [
    { "hat": "white", "line": "Four within reach, from what we know.", "ideas": [ { "id": "w1", "text": "Start with games that already have a Linux build: no port needed." } ] },
    { "hat": "red", "line": "...", "ideas": [ ] },
    { "hat": "yellow", "line": "...", "ideas": [ ] },
    { "hat": "black", "line": "...", "ideas": [ ] },
    { "hat": "green", "line": "...", "ideas": [ ] },
    { "hat": "blue", "line": "Two other paths to the same place.", "ideas": [ { "id": "b1", "text": "Don't port at all: stream from the PC and spend the effort on the controls." } ] }
  ],
  "recap": { "line": "That's round 1. Send it back, and round 2 brings the council." }
}
```

For a complete round 1, read `example-brainstorm.json` next to this file.

`config` works as in a round: `kind` is always `"brainstorm"`, `round` is `1`, `needs_wizard` is `"0.9.0"`, and `project` and `folder` go on a brainstorm Claude Code writes into a project's `wizard-rounds/` folder, exactly as for a round.

`topic` is the one subject of the whole brainstorm, and both rounds carry the same one:

| Field | Required | What it does |
|---|---|---|
| title | yes | The topic as a short label, never a question. Shows above every card's heading |
| question | yes | The open question, in plain words, ending with a question mark |
| context, detail, links, extra | no | As in a round. Round 1 shows them on Blue's first card, round 2 on its aims card. Never cut context to make a card shorter, and quote only what is important to understanding the topic |

The three lists:

| List | Shape | What goes in it |
|---|---|---|
| hold | Exactly six entries, `{"hat":"blue"}` first, then the other five once each, in the order you pick | Each entry can carry a `question`. Leave it out and the wizard asks the hat's own question from the table above. If you write one, keep what it asks and only name the topic: "What excites you most about playing your Steam games on the handheld?". Never give a hold card a line: the hat holds back |
| sparks | Optional, one entry at most per hat, only for hats with a spark worth having | `line` (optional): what the hat says as its card opens. `question` (optional): the card's heading, "What do these set off?" when left out. `sparks`: 1 to 3, each `{"id":"s1","text":"..."}` |
| suggest | Exactly six entries, each hat once, in the order you pick, with `{"hat":"blue"}` last | `line` (required): what the hat says as it suggests. `question` (optional): the card's heading, the hat's own when left out ("What's within reach?", "How could it feel more human?", "How far could it go?", "What would keep it out of trouble?", "What twist could feed it?", and for Blue "What other path could get you there?"). `ideas`: 0 to 4, each `{"id":"w1","text":"...","why":"..."}`; `why` is optional and short, such as where a fact came from |

`recap` is optional: `{"line":"..."}`, Blue's line on the last card.

Ids are short, use only letters, digits, `-`, and `_`, and are unique across the file: a letter for the kind and a number (`s1` for sparks, `w1`, `r1`, `y1`, `k1`, `g1`, `b1` for suggestions). Ids like `u1` are kept for the user's own cards, and the wizard refuses them.

### Writing round 1

- **One topic.** A brainstorm explores one open question. Several questions are several brainstorms, or a round.
- **You write before the user does.** The whole of round 1 goes out at once, so your sparks and suggestions can't react to the user's cards; the wizard holds them back until the user has written for all six hats.
- **The spark rule.** A spark names a direction, never the idea itself: if it could be built, it's a suggestion. "Does the game have to run on the handheld at all?" is a spark; "Stream your games from the PC" is a suggestion. A spark is a question or a short note. Not every hat brings sparks: pick the hats where a nudge would help on this topic, up to three sparks each, and when a hat brings more than one, start calm and get wilder.
- **Suggestions follow the hat's job.** Up to 4 a hat, fewer when fewer are strong. Each is one sentence that stands alone, read days later with no chat history. Blue's are other paths to the same goal, never a summary.
- **Every hat speaks in its own voice.** A suggest line is one or two sentences in the character's voice, and so is a spark line when you give one.
- **Facts are real,** whichever hat states them. White's suggestions come from the conversation, the files, or sources you have, with `why` naming the source when it isn't common knowledge. Never invent a number, and don't state as a rule what is only often true.
- **No recommendations.** No hat argues for an outcome. Every card stays unless the user kills it.

## Round 2

Write round 2 from round 1's answers. Its parts, in the order the wizard shows them:

1. **Aims:** Blue opens on the user's goals and on what they want to avoid, as the measure for every idea, with the plan of the round.
2. **Extras:** new ideas from the hats, grouped by hat, each with a cross to kill it. A kept extra comes before the council in this same round; a killed one never does.
3. **The council:** one card per idea, then one per kept extra. The idea sits in the middle of a round table with the six hats around it (the user can switch to a row in Options). A gold mark shows on each hat that has something to say; opening one shows its comment, counts it as read after a few seconds, and offers Take it as an idea. A hat with nothing to say has no mark, and opening it shows a short line the wizard has built in, like "No cracks I can see." The user can also add a variant of their own or kill the idea.
4. **Your order:** every idea that survived, with what the user took or added, to drag or move into order. Nothing the user adds in round 2 goes to a council: there is no round 3.

```json
{
  "config": { "title": "Steam Handheld, Brainstorm 1, Round 2", "tagline": "From Steam Handheld, Brainstorm 1", "product": "Handheld", "kind": "brainstorm", "round": 2, "needs_wizard": "0.9.0" },
  "topic": { "title": "Steam games on my handheld", "question": "What could get my Steam games onto my handheld?", "context": "..." },
  "aims": {
    "line": "Round 2. The hats have a few more first, then the council takes your ideas one at a time.",
    "goals": [ "Play my whole Steam library away from my desk." ],
    "avoid": [ "Hours of setup for games that run badly." ]
  },
  "extras": {
    "line": "From what you wrote, the hats had a few more. Kill any that miss.",
    "ideas": [
      { "id": "x1", "hat": "red", "text": "A cosy mode: dim screen, quiet fans, one game you can play half asleep.", "why": "From your \"Playing in bed without my PC on\".",
        "council": [ { "hat": "black", "say": "A dim screen hides small text in some games. Which games would it suit?" } ] }
    ]
  },
  "ideas": [
    { "id": "i1", "text": "Stream games from my PC when it's on.", "by": "you", "hat": "yellow", "from": "From Yellow's spark: Does the game have to run on the handheld at all?",
      "council": [ { "hat": "blue", "say": "..." }, { "hat": "white", "say": "...?" }, { "hat": "black", "say": "...?" }, { "hat": "green", "say": "..." } ] },
    { "id": "i4", "text": "Games with Steam Cloud already carry their saves between devices, so the handheld can pick up mid-game.", "by": "white", "hat": "white",
      "council": [ { "hat": "red", "say": "..." } ] }
  ],
  "order": { "line": "These made it through. Put them in your order; the decision round starts from the top." }
}
```

For a complete round 2, read `example-brainstorm-round2.json` next to this file. It is cut to six ideas and three extras to stay short; a real round 2 brings every idea that survived round 1.

| Field | Required | What it does |
|---|---|---|
| config | yes | As in round 1, with `round` set to `2`, its own title, and a tagline naming round 1: "From Steam Handheld, Brainstorm 1" |
| topic | yes | Round 1's topic. Keep it the same, adding to its context only a decision the user settled since round 1 |
| aims | yes | `line` (required): Blue's opening line. `goals` and `avoid`: lists of the user's own cards, word for word |
| extras | no | `line` (optional, Blue's) and `ideas`, each `{"id":"x1","hat":"red","text":"...","why":"...","council":[...]}`: `hat` is the hat that brings it, `why` (optional) the card of the user's it grew from. No fixed number; the wizard takes up to 40 |
| ideas | yes | 1 to 120, each `{"id":"i1","text":"...","by":"you","hat":"yellow","from":"...","council":[...]}`. `by` is `"you"` for the user's own card, or the hat that suggested it. `hat` is the hat it came under in round 1. `from` (optional) is one short line shown under it: the spark it came from, for a card written under one. Leave it out otherwise; a hat's idea without one reads "Suggested by White", and the user's shows nothing |
| council | on each idea and extra, optional | Up to six comments, each `{"hat":"white","say":"..."}`, one per hat at most. A hat left out has nothing to say |
| order | no | `{"line":"..."}`, Blue's line on the last card |

Ids follow round 1's rules, and are new for round 2: `i1` and on for ideas, `x1` and on for extras.

### Writing round 2

- **Sort the user's cards.** Read every card the user didn't kill, wherever they wrote it. A goal (what the whole topic is for, often under Blue) goes into `aims.goals`. A concern (what must not happen, often under Black) goes into `aims.avoid`. Everything else is an idea, wherever it was written, and a card that could be read either way is an idea, so the council hears it. Goals and concerns never come before the council.
- **Every idea as written.** Each surviving idea gets its own council turn, word for word: the user's ideas with `by: "you"`, and every suggestion they didn't kill with `by` set to its hat. Never merge, reword, or drop one. A card the user wrote under a spark gets `from` naming the whole spark: "From Yellow's spark: Does the game have to run on the handheld at all?". Suggestions on a card the user never reached (`seen: false`) go too, since nothing killed them. A killed card never comes back, and nor does a killed suggestion.
- **Order the ideas** so the council reads well, related ideas side by side. The wizard brings the extras after them.
- **Extras come from what round 1 showed** about the user: what they wrote, the sparks that set them off, and the directions they killed. Each steers clear of their concerns, and `why` quotes the card it grew from when there is one. Any hat can bring one. There's no quota: bring the ones worth a council turn.
- **The council speaks only when it has something.** Each hat says one thing at most, one or two sentences in its voice, doing its council job from the table above. Leave a hat out rather than write filler like "Nice idea": the wizard says its own line for a silent hat. Often only three or four hats speak.
- **White and Black end on a question** when there is one: a limit or a crack comes with what would get past it ("What would make it work on the go?"), so a problem can open an idea instead of only closing one.
- **Comments can become ideas.** The user can take any comment as an idea of theirs, so write each one to stand alone, read later without the idea above it.
- **Any hat can speak on any idea,** its own suggestions and the extras it brought included, always from its own job.
- **Blue measures against the goals.** Blue's comment says whether the idea changes the point or serves the core, in the words of the user's goals where it can. It never asks the user to choose again what a goal already says.
- **Facts are real, and no hat recommends.** As in round 1. A comment that states a fact beyond common knowledge says where it comes from, in the comment itself.

## Both rounds

- **Keep the user's words.** Their cards go into round 2 exactly as written.
- **Decisions stay decided.** A brainstorm never reopens a decision the user already made. State a settled decision in the topic's context as a fixed point instead.
- **Titles.** Round 1 names the brainstorm and its number ("Steam Handheld, Brainstorm 1"); round 2 adds ", Round 2". Reuse a title only to resend a corrected version, keeping unchanged cards identical so the user's work on them survives.
- Write in the user's working language. Titles are never questions; questions end with a question mark. No em dashes and no en dashes anywhere.

## Delivering it

Exactly as a round (see Delivering a round in SKILL.md), with the files named `<YYYY-MM-DD>-<topic>-brainstorm<N>.json` for round 1 and `<YYYY-MM-DD>-<topic>-brainstorm<N>-round2.json` for round 2: today's date, and round 2 keeps round 1's topic and number. Surround it with at most three short sentences, and don't restate the cards in prose.

## Consuming the answers

A brainstorm's answers carry `meta.kind = "brainstorm"` and `meta.round`. Every entry has `id`, `step`, `hat`, `issue` (the card's title), `status: "brainstorm"`, and `seen`; all but the council's carry `question`. Cards come back with their words; the user's own cards have no ids, and carry `killed` only when it's true. `topic` comes back with its title and question only: the context is in the brainstorm you wrote, and under `round` in a saved file. `meta.total` counts the entries and `meta.seen` those gone through with Next.

Round 1:

```json
{
  "meta": { "tool": "decision-wizard", "kind": "brainstorm", "round": 1, "wizard_version": "0.9.0", "wizard_title": "Steam Handheld, Brainstorm 1", "exported_at": "...", "total": 17, "seen": 17, "yours": 10, "killed": 3, "suggested": 15 },
  "topic": { "title": "Steam games on my handheld", "question": "What could get my Steam games onto my handheld?" },
  "answers": [
    { "id": "h-blue", "step": "hold", "hat": "blue", "issue": "Blue: your turn", "status": "brainstorm", "seen": true, "question": "Where is this going, and what are its main goals?",
      "yours": [ { "text": "Play my whole Steam library away from my desk." } ] },
    { "id": "h-black", "step": "hold", "hat": "black", "issue": "Black: your turn", "status": "brainstorm", "seen": true, "question": "What could make this useless, or hurt and go badly?",
      "yours": [ { "text": "Hours of setup for games that run badly." }, { "text": "Too slow to bother.", "killed": true } ] },
    { "id": "s-yellow", "step": "spark", "hat": "yellow", "issue": "Yellow: sparks", "status": "brainstorm", "seen": true, "question": "What do these set off?",
      "sparks": [ { "id": "s3", "text": "Does the game have to run on the handheld at all?", "yours": [ { "text": "Stream games from my PC when it's on." } ] },
                  { "id": "s4", "text": "What would you play if the battery never ran out?", "yours": [] } ] },
    { "id": "g-white", "step": "suggest", "hat": "white", "issue": "White: suggests", "status": "brainstorm", "seen": true, "question": "What's within reach?",
      "ideas": [ { "id": "w1", "text": "Start with games that already have a Linux build: no port needed.", "killed": false },
                 { "id": "w2", "text": "Check your library against a community list of games known to run, and start tonight.", "killed": true } ],
      "yours": [ { "text": "Try the three games I play most first." } ] },
    { "id": "recap", "step": "recap", "hat": "blue", "issue": "Blue: recap", "status": "brainstorm", "seen": true, "question": "What's standing after round 1?" }
  ]
}
```

- `step` is `hold`, `spark`, `suggest`, or `recap`, and the ids are `h-`, `s-`, and `g-` plus the hat. Blue's suggest entry is titled "Blue: other paths". Every hat has a hold and a suggest entry; only hats with sparks have a spark entry.
- `yours` are the user's own cards, in their words, and are authoritative. On a spark entry, each spark lists what it set off; a `yours` beside the sparks, present only when there are any, holds cards not tied to one.
- `killed: true` marks a card the user killed, theirs or a hat's. Everything else is kept: there are no stars, and a card not killed counts as standing.
- `meta.yours` counts the user's cards, `meta.suggested` the hats', and `meta.killed` the killed ones of both.

Round 2:

```json
{
  "meta": { "tool": "decision-wizard", "kind": "brainstorm", "round": 2, "wizard_version": "0.9.0", "wizard_title": "Steam Handheld, Brainstorm 1, Round 2", "exported_at": "...", "total": 12, "seen": 12, "yours": 2, "killed": 2, "ideas": 9 },
  "topic": { "title": "Steam games on my handheld", "question": "What could get my Steam games onto my handheld?" },
  "answers": [
    { "id": "aims", "step": "aims", "hat": "blue", "issue": "Blue: your aims", "status": "brainstorm", "seen": true, "question": "What could get my Steam games onto my handheld?" },
    { "id": "extras", "step": "extras", "hat": "blue", "issue": "Extras", "status": "brainstorm", "seen": true, "question": "Anything here worth keeping?",
      "ideas": [ { "id": "x1", "text": "A cosy mode: ...", "killed": false, "hat": "red" }, { "id": "x3", "text": "Your PC wakes itself ...", "killed": true, "hat": "green" } ] },
    { "id": "c-i1", "step": "council", "hat": "yellow", "issue": "Stream games from my PC when it's on.", "status": "brainstorm", "seen": true,
      "idea": { "id": "i1", "text": "Stream games from my PC when it's on.", "by": "you", "hat": "yellow" }, "killed": false,
      "read": [ "blue", "white", "black" ],
      "taken": [ { "text": "Fast games lag, and the battery drains on wifi. Which games would you never stream?", "hat": "black" } ],
      "variants": [ { "text": "Stream at home, and download a port for the train." } ] },
    { "id": "c-x3", "step": "council", "hat": "green", "issue": "Your PC wakes itself ...", "status": "brainstorm", "seen": false,
      "idea": { "id": "x3", "text": "Your PC wakes itself ...", "by": "green", "hat": "green", "extra": true }, "skipped": true, "killed": false, "read": [], "taken": [], "variants": [] },
    { "id": "order", "step": "order", "hat": "blue", "issue": "Blue: your order", "status": "brainstorm", "seen": true, "question": "Which ideas matter most?", "ranked": true,
      "order": [ { "text": "Get one game I own running, start to finish.", "by": "you", "from": "round 1", "id": "i2" },
                 { "text": "Stream at home, and download a port for the train.", "by": "you", "from": "variant", "on": "i1" },
                 { "text": "Stream at home, and port only the games you take outside.", "by": "white", "from": "extra", "id": "x2" } ] }
  ]
}
```

- A council entry's id is `c-` plus the idea's id, and `idea.extra` marks an extra. `killed: true` means the user killed the idea; `skipped: true` means they killed the extra on the extras card, so it never came before the council.
- `read` lists the hats whose comments the user had open long enough to count as read. It says what they saw, not what they agreed with.
- `taken` are comments the user took as ideas of their own, with the hat they came from; `variants` are ideas the user wrote on that card. Both are the user's ideas, and each can carry `killed: true`.
- `order` is every idea that survived, best first, as the user left it: `from` is `round 1`, `extra`, `variant`, or `taken from` a hat, `id` names an idea or extra, and `on` names the idea a variant or taken comment came from. `ranked: false` means the user never moved anything, so the list is only the wizard's order.
- `meta.ideas` counts the council's cards, `meta.yours` what the user took or added, and `meta.killed` everything killed: ideas, extras, and the user's own cards.

For both rounds:

- `seen: false` means the user never went through that card with Next; they may have jumped past it. What they did there still counts. Answers handed to you by the user are finished. Answers you read from a project's folder may not be: when the last card (`recap` or `order`) isn't seen there and the user hasn't said they're done, ask whether they've finished before writing the next round.
- A file saved from the wizard carries the same `meta`, `topic`, and `answers`, plus the whole brainstorm under `round`, in the form you wrote, with every default question written in. A brainstorm in a project's `wizard-rounds/` folder is read back exactly as a round is.

## Acting on it

**After round 1:** write round 2 and deliver it. One of the few sentences around it says what round 1 left: how much the user wrote, which sparks set them off, what they killed, and how many suggestions came from cards they didn't reach, if any. A brainstorm needs no report per id.

**After round 2:**

1. Sum it up in a few lines: the top of the user's order, what they took and added, and what they killed. Don't list the rest back.
2. If decisions remain, send a decision round, built from the user's order: its tagline names the brainstorm ("From Steam Handheld, Brainstorm 1"), and it starts from the top of the order, asking the details and ways of doing the ideas that the brainstorm left to rounds. Quote the user's cards where they matter, with the brainstorm as their source; a council comment is your own writing, so it goes in a note, never a quote. When `ranked` is false, the order isn't the user's: ask for it in the round as a ranking question rather than assuming it.
3. Killed ideas and skipped extras never come back, and a position the user wrote on a card is settled, per Decisions stay decided.
4. If nothing remains to decide, say so after the summary.

A new angle on the topic is a new brainstorm with its own title, sent only when the user asks.

## Older brainstorms

Answers from a wizard 0.8.0 brainstorm have `meta.kind = "brainstorm"` and no `meta.round`, with an entry per hat whose ideas carry `starred`. Read them as they were meant: a star marks what mattered to the user, an idea without one was heard and not rejected, `yours` are the user's own ideas, `comment` is their note, and `answer` is their reply to a hat's `ask`. Never send that form again; to go further on its topic, offer a new brainstorm.
