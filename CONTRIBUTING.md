# Contributing

Thanks for wanting to improve **The AI-Augmented Developer Skill Tree**! This is
a single, dependency-free HTML page, so contributing is genuinely quick — no
build step, no framework, no `npm install`.

The most valuable contributions are **content**: a missing skill, a sharper
"why it matters," or a better resource link. You don't need to be a designer or
know JavaScript to help.

## Ways to contribute

- 💡 **Suggest a skill or resource** — [open an issue](../../issues/new/choose)
  (no code needed). This is the easiest and most welcome path.
- 🔗 **Report a broken or outdated link** — same, via an issue.
- ✍️ **Send a pull request** — edit the content directly (see below).

## How the project is laid out

Everything lives in **`index.html`** — HTML, CSS, and JS in one file. The
content you see on the page is generated from a single JavaScript array near the
bottom of the file called `STAGES`.

```js
var STAGES = [
  {
    mark: "I",                 // tier numeral (I–VI)
    title: "Foundations",      // tier name
    sub: "how the model works",// short tier subtitle
    proj: {                    // the hands-on project that closes the tier
      h: "Explain it to a rubber duck",
      d: "Write a one-page, jargon-free explanation of…"
    },
    stops: [                   // the skills in this tier
      {
        n: "01",               // skill number (unique, two digits)
        h: "What an LLM actually is",              // title
        d: "Tokens, the context window, next-token prediction…",  // one-line what
        why: "Almost every surprising behaviour falls out of…",   // why it matters
        chk: "You can explain, without jargon, why a model…",     // "you've got it when"
        pit: "Treating it like a database or a person…",          // the pitfall to dodge
        res: [                                                    // resources
          { l: "Karpathy — Intro to LLMs (1hr)", u: "https://…" },
          { l: "prompt-forge — build & test prompts", u: "https://…", t: true }
        ]
      }
    ]
  }
];
```

Field notes:

- **`n`** must be unique across the whole tree and two digits (`"07"`, not `7`).
- **`d` / `why` / `chk` / `pit`** are each **one sentence**. Keep them tight — the
  value is in being concrete, not long. `chk` should be a testable "you can do X."
- **`res[].t: true`** marks a resource as a small tool (renders with a ◆ and a
  tinted chip). Only use it for actual tools, not articles.
- Per-tier colors come from the `TIER_COLORS` array — you shouldn't need to touch
  it unless you add or remove a tier.
- Progress is stored in `localStorage` under a versioned key
  (`aidevtree-done-vN`). **If you renumber or reorder skills, bump that version**
  so returning visitors don't see mismatched checkmarks.

## Adding a skill

1. Find the right tier's `stops` array in `STAGES`.
2. Add a new object with all six fields (`n`, `h`, `d`, `why`, `chk`, `pit`, `res`).
3. Give it the next unused `n` in that tier (renumber later skills if inserting
   in the middle — and bump the `localStorage` version if you do).

## Adding or fixing a resource

- Prefer a **specific** link (the exact video, paper, or doc page) over a
  homepage or channel.
- Prefer **stable, well-known** sources (official docs, canonical papers,
  established educators) over churny blog posts.
- Free resources are strongly preferred; if something is paid, say so in the label.

## Running it locally

No tooling required. Either:

- **Just open `index.html`** in your browser, or
- Serve it (needed only if you want the exact production behaviour):

  ```sh
  python3 -m http.server 8000
  # then visit http://localhost:8000
  ```

## Before you open a PR

- Open the page and confirm your change renders in **both the skill tree and mind
  map views**.
- Toggle your OS to **dark mode** and check it still looks right (the page is
  theme-aware).
- Click your new skill's orb to confirm XP still counts, and open the card to
  check your text reads well.
- Verify every link you added actually loads.

## Style

- Match the voice of the existing entries: direct, practical, a little opinionated.
- No new dependencies, external fonts, CDNs, or trackers — the page must stay
  self-contained and work offline.

By contributing, you agree your contributions are licensed under the project's
[MIT License](LICENSE). Please also read the [Code of Conduct](CODE_OF_CONDUCT.md).
