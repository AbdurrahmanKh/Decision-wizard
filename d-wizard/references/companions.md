# Making a companion

Read this only when the user asks you to make a companion for the Decision Wizard: a character who sits beside the cards, changes pose, and says short lines. Companions need wizard 0.7.0 or later, in Chrome or Edge on a computer.

## What a companion is

A folder. The user keeps one companions folder on their computer, and each companion is a folder inside it:

```
Inky/
  idle.svg
  greet.svg
  ...
  companion.json
```

- **Pictures** are named after the pose they fill: `idle.svg`, `greet.png`, and so on. SVG, PNG, WebP, or GIF. Only `idle` is required.
- **`companion.json`** gives the name and the lines. It's optional: without it, the folder's name is the companion's name and it never talks.
- **The whole folder** must stay under 5 MB.

## The 14 poses

| Pose | What it shows | When it's missing, it uses |
|---|---|---|
| idle | standing, at rest | (required) |
| blink | idle with eyes shut, shown for a moment now and then | no blink |
| greet | a wave or hello | idle |
| pick | pleased, an answer was given | greet |
| skip | a shrug, a question was skipped | idle |
| milestone | proud, halfway or a batch done | pick |
| warn | worried, something is about to be cleared | idle |
| error | puzzled, a file didn't load | warn |
| finish | celebrating, the round is done | milestone |
| yawn | sleepy | idle |
| sleep | asleep | idle, with a Zzz drawn over it |
| wake | wide awake again | greet |
| dance1 | first dance step | finish |
| dance2 | second dance step | dance1 |

The dance steps through dance1, dance2, and finish while the whole figure sways. Make every pose, unless the user asks for fewer: borrowed poses work, but a companion with all 14 feels alive.

## Drawing

- **One frame for every pose:** 200 wide by 262 tall. For SVG, use `viewBox="0 -12 200 262"`, with the feet near the bottom and a soft shadow under them. Keep the character in the same place from pose to pose, so it doesn't jump.
- **The frame is small:** about 145 by 190 pixels on a wide screen and 49 by 64 on a narrow one. Use bold shapes and a clear silhouette, and avoid fine detail and text.
- **Both themes:** the wizard has a dark and a light theme, so give the character its own outline (the built-in companions use flat colors with a `#1B1810` outline) and no background.
- **Pixel art:** draw it small (under 100 pixels wide, in about the same 200 by 262 shape) as PNG, WebP, or GIF. The wizard keeps its edges crisp when it scales up.
- **SVG** must be plain drawing: no scripts, no links to other files, no embedded fonts. The wizard shows it as an image.

## companion.json

```json
{
  "name": "Inky",
  "about": "the octopus",
  "lines": {
    "greet": ["{Decisions}. Good thing I brought eight arms."],
    "pick": ["Inked.", "Noted in my best handwriting."],
    "opt_hello": "Inky here. Pens ready."
  }
}
```

- **`name`:** up to 30 characters, never Quill, Swoop, or None. The name is the companion's identity: adding another companion with the same name replaces it, after asking.
- **`about`:** a few words shown after the name, as in "Inky, the octopus". Optional.
- **`lines`:** each moment below names a list of lines, or one line. One line is enough for a moment; up to five keeps it fresh. A moment with no lines stays quiet. A moment name the wizard doesn't know, a line that isn't text, or a placeholder the moment can't fill keeps the whole companion out, with a notice saying why.

## Lines

Lines are short (a sentence, two at most), light-hearted, in the companion's own voice, and in any language. They show in a speech bubble for a few seconds.

- Don't mention Claude.
- A `suggest` line must work whoever `{other}` names, since the user may have many companions.
- Use only the placeholders each moment lists. `{Decisions}` and `{Picked}` start a sentence ("Seven decisions"); `{cname}` is ", Name" or nothing, so it goes right before punctuation ("Morning{cname}!").

| Moment | When it plays | Placeholders |
|---|---|---|
| greet | a round opens | `{Decisions}` |
| estimate | after greet, how long the round may take | `{minutes}` |
| morning | first round of a morning | `{cname}` |
| late | a round opened late at night | `{cname}` |
| back | the user, who gave a name, opens a round | `{cname}` |
| suggest | the day's second round, offering another companion | `{other}` |
| pick | an answer after some thought | |
| skip | a question skipped | |
| speed | an answer given the moment the question appeared | |
| second | the same answer changed a third time | |
| nudge | a question sitting a while with no answer | |
| batch | a card of rows to answer one by one | `{Decisions}` |
| half | half the round answered | |
| last | the last question | |
| finish | every question answered | |
| recap_done | the summary, nothing open | `{Picked}`, `{typedPart}`, `{timePart}` |
| recap_open | the summary, some still open | `{Picked}`, `{typedPart}`, `{ids}` |
| recap_none | the summary, nothing answered | `{ids}` |
| remind | finished, answers not copied yet | |
| copied | answers copied | |
| open_go | jumping to a question still open | `{id}` |
| stat_r | a remark on rounds finished | `{r}` |
| stat_t | a remark on answers the user wrote | `{t}` |
| stat_today | a remark on decisions today | `{td}` |
| wake | woken from a nap | |
| poke | five quick taps on the companion | |
| word | the user typed "wizard" | |
| warn | before answers are cleared | `{answers}` |
| error | a file didn't load | |
| opt_hello | chosen in Options | |
| opt_name | the user typed their name in Options | `{name}` |
| opt_light, opt_dark, opt_system | the theme changed | |
| opt_large, opt_compact, opt_normal | the text size changed | |
| opt_soundon, opt_soundoff | sounds turned on or off | |
| opt_quipson, opt_quipsoff | remarks turned on or off | |
| opt_talkon | speech bubbles turned back on | |
| opt_timereset | the round timer reset | |

## Handing it over

- **In Claude:** zip the companion's folder (the zip holds the folder itself, named after the companion) and give it to the user as a file in the conversation. They unzip it, then drop the folder on the wizard or use Add in the Companion card of Options; the wizard shows the companion and asks before adding it.
- **In Claude Code:** if the user gives you the path of their companions folder, write the companion's folder straight into it; the wizard picks it up by itself within seconds. If a folder with that name is already there, ask before writing over it. Without the path, write the folder where the user asks. Never write a companion into a project's `wizard-rounds/` folder or into a repository.
- Say in one or two sentences what you made: its name, how many poses it has, and which moments it talks in.
