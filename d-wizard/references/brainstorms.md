# Brainstorms

A brainstorm looks at one open topic through Edward de Bono's Six Thinking Hats. Each hat is worn by a character the wizard draws, and each brings its own kind of thinking: facts, feelings, benefits, caution, and new ideas, with the Blue hat hosting at both ends. The user goes through the hats one card at a time, stars the ideas that matter, adds a note to any idea, adds ideas of their own, and answers any question a hat asks. Nothing is picked and nothing is recommended: a brainstorm gathers material, and the decisions come after, in a round.

Brainstorms need Decision Wizard 0.8.0 or later. An older wizard can't open one, so point the user to https://abdurrahmankh.github.io/decision-wizard/ if theirs says the file isn't a round.

## When

Send a brainstorm only when the user asks for one. When a hard open question has no clear options yet, so a round would only guess at them, offer one in a single line and wait. Once you have the brainstorm's answers, the next step is usually a round.

## The cast

The wizard draws the six characters and shows each one's name beside its hat. You write every word they say, fresh for each brainstorm, in that character's voice.

| Hat | Character | Kind of thinking | Voice |
|---|---|---|---|
| Blue | Cap, the capybara | The host: the focus and the plan, then what came out and what's next | Calm and unhurried; frames the question, keeps the order, and sums up |
| White | Tally, the owl | Facts: what we know, and what we're missing | Calm and exact; says what we know, what we don't, and where a number came from |
| Red | Ruby, the fox | Feelings: gut reactions, no reasons needed | Warm and blunt; says how it feels, with no reasons needed |
| Yellow | Sunny, the bee | Benefits: why it could work | Bright and busy; finds what's good and who it helps |
| Black | Pebble, the tortoise | Caution: why it might not | Careful and dry; looks for the cracks and always gives the reason |
| Green | Doodle, the chameleon | New ideas: other ways to get there | Playful and odd; turns the question sideways and tries another way in |

## The brainstorm JSON

```json
{
  "config": { "title": "Loyalty Points, Brainstorm 1", "tagline": "One line under the title", "product": "Team or product label", "kind": "brainstorm", "needs_wizard": "0.8.0" },
  "topic": { "title": "Loyalty points at checkout", "question": "Should checkout offer loyalty points?", "context": "...", "detail": [ ] },
  "hats": [
    { "hat": "blue", "line": "Today's focus is points at checkout. Five hats, then back to me." },
    { "hat": "white", "line": "...", "question": "What do we know about points at checkout?", "ideas": [ { "id": "w1", "text": "...", "why": "..." } ], "ask": "What do you know about our shoppers that I don't?" },
    { "hat": "red", "line": "...", "ideas": [ ] },
    { "hat": "yellow", "line": "...", "ideas": [ ] },
    { "hat": "black", "line": "...", "ideas": [ ] },
    { "hat": "green", "line": "...", "ideas": [ ] },
    { "hat": "blue", "line": "Here is what you starred. Now, what's next?", "ideas": [ { "id": "n1", "text": "A next step" } ] }
  ]
}
```

`config` works as in a round: `kind` is always `"brainstorm"`, `needs_wizard` is `"0.8.0"`, and `project` and `folder` go on a brainstorm Claude Code writes into a project's `wizard-rounds/` folder, exactly as for a round. Give each brainstorm its own title that names its number ("Loyalty Points, Brainstorm 1"); reuse a title only to resend a corrected version, and keep unchanged ideas identical so the user's stars and notes on them survive.

`topic` is the one subject of the whole brainstorm:

| Field | Required | What it does |
|---|---|---|
| title | yes | The topic as a short label, never a question. Shows above every hat's question |
| question | yes | The open question, in plain words, ending with a question mark. It is the heading of Blue's opening card |
| context, detail, links, extra | no | As in a round, and shown in full on Blue's opening card. The same rule holds: never cut context to make a card shorter, and quote only what is important to understanding the topic |

`hats` is exactly seven entries: Blue first, then White, Red, Yellow, Black, and Green, each once, in the order you pick for this topic, then Blue again last. The wizard refuses any other shape.

Per hat:

| Field | Where | What it does |
|---|---|---|
| hat | every hat | `"blue"`, `"white"`, `"red"`, `"yellow"`, `"black"`, or `"green"` |
| line | every hat, required | What the character says as its card opens, one or two sentences in its voice. Every hat speaks |
| question | the five middle hats and the closing Blue, optional | The hat's question about this topic, ending with a question mark: "What could go wrong with points at checkout?". Left out, the wizard asks a general one ("What could go wrong?", and on the closing card "What did we find, and what's next?"). Write one; it reads better |
| ideas | the five middle hats and the closing Blue | Up to 6 ideas, each `{"id":"w1","text":"...","why":"..."}`. On the closing Blue, they are next steps, and the wizard shows what the user starred above them by itself. The opening Blue brings none |
| ask | the five middle hats, optional | One question for the user, answered in a text box on the card: something only they know, such as their gut call or what they have seen with their own customers |

Idea ids are short (a letter for the hat and a number: `w1`, `r2`, `n1`) and unique across the whole brainstorm. `why` is optional and short: where a fact came from, or the reason behind a risk.

For a complete worked brainstorm, read `example-brainstorm.json` next to this file.

## Writing it

- **One topic.** A brainstorm explores one open question. Several questions are several brainstorms, or a round.
- **Blue opens and closes.** The opening line frames the focus and can say the order. The closing line hands back to the user, and its ideas are the next steps you see.
- **Pick the order for the topic.** White first when the facts are thin or disputed; Red early when feelings already run high; Black before Green, so new ideas can answer the cracks. The opening card shows the order as the plan.
- **Each hat thinks only its way.** White states facts and names what is missing, never opinions. Red gives feelings with no reasons. Yellow gives benefits and who gains. Black gives risks, each with its reason. Green gives alternatives and new angles, including ones that drop the topic's premise.
- **Up to 6 ideas a hat.** Fewer strong ideas beat padding. Each idea is one sentence that stands alone, read days later with no chat history.
- **Facts are real.** White's facts come from the conversation, the files, or sources you have, with `why` naming the source. Never invent a number. When nothing is known, that is the idea: say what is missing.
- **No recommendations.** No hat argues for an outcome, and Blue doesn't pick. The user's stars say what matters.
- **Ask sparingly.** An `ask` goes only where the user knows something you don't. Most brainstorms need two or three, not five.
- **Decisions stay decided.** A brainstorm never reopens a decision the user already made. State a settled decision in the topic's context as a fixed point instead.
- Write in the user's working language. Titles are never questions; questions end with a question mark. No em dashes and no en dashes anywhere.

## Delivering it

Exactly as a round (see Delivering a round in SKILL.md), with the file named `<YYYY-MM-DD>-<topic>-brainstorm<N>.json`. Surround it with at most three short sentences, and don't restate the ideas in prose.

## Consuming the answers

A brainstorm's answers carry `meta.kind = "brainstorm"`:

```json
{
  "meta": { "tool": "decision-wizard", "kind": "brainstorm", "wizard_version": "0.8.0", "wizard_title": "Loyalty Points, Brainstorm 1", "exported_at": "...", "total": 7, "seen": 7, "ideas": 20, "yours": 2, "starred": 7 },
  "topic": { "title": "Loyalty points at checkout", "question": "Should checkout offer loyalty points?" },
  "answers": [
    { "id": "open", "hat": "blue", "issue": "Blue: the focus", "question": "Should checkout offer loyalty points?", "status": "brainstorm", "seen": true },
    { "id": "white", "hat": "white", "issue": "White: facts", "question": "What do we know about points at checkout?", "status": "brainstorm", "seen": true,
      "ideas": [ { "id": "w1", "text": "...", "starred": true, "comment": "The user's note on it" },
                 { "id": "w2", "text": "...", "starred": false } ],
      "yours": [ { "text": "An idea the user added", "starred": true } ],
      "ask": "What do you know about our shoppers that I don't?", "answer": "What the user typed, or an empty string" },
    { "id": "close", "hat": "blue", "issue": "Blue: wrap-up", "question": "What did we find, and what's next?", "status": "brainstorm", "seen": true,
      "ideas": [ { "id": "n1", "text": "A next step", "starred": true } ], "yours": [ { "text": "A step the user added", "starred": true, "comment": "Their note on it" } ] }
  ]
}
```

- Everything comes back, unstarred ideas too. A star means it matters to the user. An idea without a star was heard, not rejected; don't treat it as dismissed.
- `comment` is the user's note on an idea, a next step, or one of their own. A position it states is settled, per Decisions stay decided.
- `yours` are the user's own ideas, in their words, and are authoritative. They start starred; one without a star was kept but not stressed.
- `answer` is the user's reply to that hat's `ask`, verbatim.
- `seen: false` means the user never went through that card with Next; they may have jumped past it. Its stars and notes still count.
- `meta.ideas` counts the ideas and next steps you wrote, `meta.yours` the user's own, and `meta.starred` the stars across both.
- A file saved from the wizard carries the same `meta`, `topic`, and `answers`, plus the whole brainstorm under `round`, as `config`, `topic`, and `hats`, with every hat's question written in (the wizard's general one where you left it out). A brainstorm in a project's `wizard-rounds/` folder is read back exactly as a round is.

## Acting on it

1. Sum it up in a few lines: what the user starred, hat by hat, their own ideas, their answers to the hats' questions, and the next steps they starred. Don't list the unstarred ideas back.
2. If decisions remain, send them as a decision round, built from what the user starred: the starred ideas and steps become options and context, and the user's own answers and notes are quoted where they matter, with the brainstorm as their source. Never ask again what a note or an answer already settled.
3. If nothing remains to decide, say so after the summary.

Never send the same brainstorm again to collect more stars. A new angle on the topic is a new brainstorm with its own title, sent only when the user asks.
