# Front End Development Libraries Certification Projects

Five projects for the freeCodeCamp **Front End Development Libraries** certification
(<https://www.freecodecamp.org/learn/front-end-development-libraries/>).

Each project passes the official freeCodeCamp test suite with **zero failures**.

| Project | Path | Test result |
| --- | --- | --- |
| Build a Random Quote Machine | [`random-quote-machine/`](random-quote-machine/) | 12 / 12 passing |
| Build a Markdown Previewer | [`markdown-previewer/`](markdown-previewer/) | 8 / 8 passing |
| Build a Drum Machine | [`drum-machine/`](drum-machine/) | 8 / 8 passing |
| Build a JavaScript Calculator | [`javascript-calculator/`](javascript-calculator/) | 16 / 16 passing |
| Build a 25 + 5 Clock | [`25-5-clock/`](25-5-clock/) | 29 / 29 passing |

Live site: <https://brutaldesu.github.io/fcc-front-end-libraries/>

## Implementation notes

- Plain HTML + CSS + JavaScript. Each project is a single self-contained `index.html`
  with no build step and no framework runtime, so every page loads straight from
  GitHub Pages.
- The markdown previewer uses [marked.js](https://marked.js.org) from a CDN; the drum
  machine and the clock ship their own audio (see below), so nothing depends on a
  third-party media host.
- The calculator implements immediate execution with "last operator wins" semantics and
  treats a minus sign pressed straight after an operator as the sign of the next
  operand.
- The 25 + 5 clock derives the remaining time from its own counter rather than the wall
  clock, and keeps the paused value so a paused countdown resumes where it stopped.

## Audio assets

The drum pads and the clock alert are generated locally so the repository is
self-contained:

```bash
python generate_audio.py   # drum-machine/audio/{Q..C}.wav
python generate_beep.py    # 25-5-clock/beep.wav (2 s)
```

## Local verification harness

`make-harness.js` generates a `harness.html` next to each project that loads the official
freeCodeCamp test bundle, so the suite can be run locally before submitting:

```bash
node make-harness.js
python -m http.server 8766 --bind 127.0.0.1
```

Then open `http://127.0.0.1:8766/<project>/harness.html`, pick the matching suite and run
the tests.

> Notes for the harness:
> - Navigate with `activateTab: true`. Otherwise the tab stays hidden, Chrome clamps
>   `setTimeout` and the tooltip/timing tests exceed their mocha timeouts.
> - The harness installs a small media-playback shim. Chrome blocks audible autoplay on
>   pages without a user gesture, which makes `audio.paused` assertions fail for reasons
>   unrelated to the implementation.

`bundle.js`, `harness.html`, `make-harness.js` and the generator scripts are local test
tooling and are not part of the published site.
