# Decision Wizard

Answer Claude's decision rounds one question at a time, then hand the answers back.

The Decision Wizard is a single web page that works with Claude's **d-wizard** skill. Claude writes your open decisions into a round file. You load it here and answer it. Claude then acts on each answer and reports where it landed.

**Open the wizard: https://AbdurrahmanKh.github.io/decision-wizard/**

## Install it as an app

The hosted wizard installs as an app, with its own window and icon. It opens offline, and whenever you're online it loads the newest version.

- **On a computer,** in Chrome or Edge: open the wizard's Options and press **Install**, or use **Install app** in the browser's menu.
- **On Android,** in Chrome: open the page, then **Install app** from the menu, or the **Install** button in Options. It replaces a shortcut to the page.
- **On an iPhone or iPad,** in Safari: **Share**, then **Add to Home Screen**.

A local copy of `index.html` keeps working as a plain page; installing is for the hosted wizard.

## Install the skill

- **Claude:** d-wizard comes with the team plugin, so most people have nothing to install. For your own copy, download `d-wizard.skill` from the [latest release](https://github.com/AbdurrahmanKh/decision-wizard/releases/latest) and upload it. In Claude, go to Customize > Skills, click **+**, then **Create skill**, then **Upload a skill**, and choose the file. If an older d-wizard is already in your list, delete it first.
- **Claude Code:** copy the [d-wizard](d-wizard) folder into `~/.claude/skills/` (on Windows, `C:\Users\<you>\.claude\skills\`). If you sign in to Claude Code with your Claude account, a skill installed in Claude shows up there too.

## How it works

1. **Ask for a round.** Say "d-wizard this" and name the topic. Claude may also start one on its own when decisions need weighing.
2. **Get the round file.** In Claude it arrives as a file in the chat, even when Claude can reach your folders. In Claude Code it lands in `wizard-rounds/` in your project.
3. **Load and answer.** Open the wizard, press **Load**, and choose the file, drag it in, or paste it. Answer each question, or skip it to leave it open.
4. **Send the answers back.** Choose **Copy answers JSON** in the companion's menu or on the last screen, and paste it to Claude. Or use **Save round JSON file** and give Claude the file. In Chrome or Edge, saving writes the answers into the round file itself, so in Claude Code you just say the answers are ready.

## Brainstorms

When a question is still too open for options, ask Claude for a brainstorm in the wizard. A brainstorm is for finding ideas, not for settling details: those come after, in a round. It looks at one topic through the Six Thinking Hats, each worn by a character: Cap, the capybara (Blue, the point), Tally, the owl (White, realistic), Ruby, the fox (Red, human), Sunny, the bee (Yellow, the dream), Pebble, the tortoise (Black, caution), and Doodle, the chameleon (Green, twists). It always takes two rounds.

**Round 1: your ideas first.**

- **Your turn.** Each hat asks you one question and says nothing else. Write as many cards as you like; Enter adds one.
- **Sparks.** Some hats bring a question or two that might set off more ideas, each with its own box.
- **Suggestions.** Every hat suggests up to four ideas beside yours. Blue's are other paths to the same goal.
- **Kill what misses.** Every card stays unless you kill it, yours too, and you can edit your own. A killed card crumples into the bin at the top, the only place to bring it back from.

**Round 2: the council.** Send round 1 back, and Claude writes round 2 from it.

- **Your aims** open it: your goals, and what you want to avoid.
- **Extras:** a few more ideas from the hats, from what you wrote. Kill any that miss; the rest go to the council.
- **The council:** every idea that survived, one at a time, with the six hats around it at a round table, or in a row if you choose that in Options. A gold mark means a hat has something to say: open it to read. Take a comment as an idea of your own, add a variant, or kill the idea.
- **Your order:** drag what survived into order. The decision round Claude sends next starts from the top.

Send each round back the way you send a round. Brainstorms need wizard 0.9.0 and skill 0.8.0. The one-file brainstorms of wizard 0.8.0 no longer open, but the ones already in your list keep their answers.

## Project folders, for Claude Code

A round Claude Code writes names its project and the `wizard-rounds/` folder it's in. The first time you load a round from a project, the wizard says which project it's from and where it will save, and asks you to pick that folder once, because a web page can't open a folder from a written path. The wizard checks that the folder holds the round, then remembers it for the project. You can also start from the folder: **Open a project folder** in Load connects it and opens its newest round that has no answers yet. From then on:

- **Your answers save themselves.** Each answer is written into the round's file a moment after you give it. When you're done, tell Claude the answers are ready; there's nothing to copy.
- **New rounds open by themselves.** A round that lands in the folder opens right away. If you're partway through another round, it waits in **Load** instead, with a notice and a count on the Load button.
- **Corrected rounds arrive too.** When Claude rewrites a round you've started, the answers to questions that didn't change stay. If an answer would be cleared, the new version waits: **Review** on the round lets you keep yours or replace them.

This works in Chrome and Edge on a computer, while the wizard is open. In a browser tab, the browser asks for your OK again on a later visit: choose **Allow on every visit** there, and it stops asking. The installed app keeps access by itself. **Load** lists the folders the wizard has, each with **Forget**.

## Companions

A companion stands beside the cards and reacts as you answer. On a screen narrower than 1440 px it stands under the question list, or beside the progress bar on a phone, so it never pushes the cards down. Quill, the pocket wizard, and Swoop, the falcon, come with the wizard. Choose one in the Companion card of Options, or None; Quill and Swoop can be hidden there too.

You can add your own, in Chrome and Edge on a computer. Each companion is a folder of pictures, one per pose (`idle.png`, `greet.svg`, and so on; only `idle` is required), with `companion.json` for its name and its lines when it talks. Your companions live in one companions folder on your computer, which you pick once in Options.

- **Add one** with **Add** in the Companion card, or by dropping a companion's folder, or its zip, on the wizard. The wizard shows it and asks first, then copies the folder into your companions folder and switches to it. A folder you put in the companions folder yourself joins by itself.
- **Make one with Claude.** **Create with Claude**, in the builder, writes the prompt for you: describe the companion (its name, title, look, art style, sound, mood, and the language of its lines), copy the prompt, and paste it into Claude, with reference pictures if you like. Claude needs the d-wizard skill, version 0.6.2 or later; it draws the poses, writes the lines, and sends the companion back as a zip. Drop the zip on the wizard as it is. In Claude Code, give Claude your companions folder's path and it writes the companion straight in. You can also just ask Claude for a companion in your own words.
- **Build one yourself** with **Build** in the Companion card. It opens a workshop: a tile for each pose, where you choose or drop a picture; buttons that play the poses the way the wizard will; and a box for each line, moment by moment, with how many lines the moment needs and what it can fill in. **Start from** copies another companion's pictures and lines to begin with. **Save** writes the folder into your companions folder and switches to it.
- **Edit one** with **Edit** beside it in the Companion card, which opens it in the same workshop. Save writes your changes into its folder.
- **Remove one** with **Remove** in the Companion card, which deletes its folder after asking, or delete the folder yourself.
- **Inky, the octopus,** the first companion made this way, is attached to the [wizard 0.7.0 release](https://github.com/AbdurrahmanKh/decision-wizard/releases/tag/wizard-v0.7.0) as `Inky.zip`.

A folder that can't be added, such as one with no idle picture, over 5 MB, or with a line the wizard can't use, gets a red notice saying why. Your companions stay out of the backup, and Clear everything forgets the companions folder without deleting anything in it.

## Your answers stay with you

Rounds and answers are kept in your own browser, and files go only where you save them. With a project folder connected, your answers are also written into that folder's round files, and nowhere else. Nothing you answer is sent anywhere; the page only loads its fonts from Google Fonts.

Each copy of the wizard keeps its own list of rounds, and clearing a browser's site data erases that list. **Back up all rounds**, in the Load panel and next to Clear everything in Options, writes every round and its answers to one file. Load that file in any copy of the wizard to bring the rounds back: it adds what's missing, updates what the backup has a newer copy of, and asks before touching a round that changed after the backup was made.

## What's in this repository

- `index.html`: the wizard, and this site's homepage.
- `manifest.webmanifest`, `sw.js`, and `icons/`: what makes the hosted wizard installable as an app, with its icons. The service worker keeps a copy for offline use and loads the newest version whenever you're online.
- `d-wizard/`: the skill. This folder is its source; `references/example-round.json` is a complete worked round, `references/brainstorms.md` is how Claude writes a brainstorm's two rounds and reads their answers, with `references/example-brainstorm.json` and `references/example-brainstorm-round2.json` as complete ones, and `references/companions.md` is how Claude makes a companion.
- `.nojekyll`: tells GitHub Pages to serve every file exactly as uploaded.

## Versions

- **Wizard: 0.9.1.** It's shown at the bottom of the wizard's Options panel.
- **Skill: 0.8.0.** It's in the skill's `SKILL.md`. It needs wizard 0.3.0 or later, 0.4.0 for rounds with ranking, number, or bracket questions, 0.6.0 for project folders, 0.7.0 for companions, 0.7.3 to drop a companion's zip on the wizard as it is, and 0.9.0 for brainstorms.

A minor update bumps the last number (0.2.2). A major update bumps the middle number (0.3.0). What changed in each version is in [CHANGELOG.md](CHANGELOG.md).
