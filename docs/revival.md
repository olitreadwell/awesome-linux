# What this revival changed

`inputsh/awesome-linux` last took a commit in June 2020 and the upstream
repository is archived. This fork carries the list forward and runs the gate
from <https://github.com/olitreadwell/awesome-list-template>, pinned to engine
revision `0d13482`.

## The readme

- Two tables of contents listed the same headings. The one under
  `## Table of Content` is gone and `make toc` rebuilt the one the engine
  checks.
- The awesome badge pointed at `cdn.rawgit.com`, a dead CDN. It points at
  awesome.re and its own link is https.
- The readme ended with a `## License` section. The linter forbids one, so the
  heading and its sentence are gone. `LICENSE` still carries the WTFPL, and
  GitHub reads the licence from that file.
- 120 bullets used `*` where the engine reads `-`.
- 42 links moved from http to https, each one only after https answered.

## Entries

- Seven entries in the package-management block wrote the target distribution
  before the description, as in `- [pirut](url) (Fedora) - a set of tools`.
  Each one took the same repair: the separator sits after the link now and the
  bracketed marker stays exactly as upstream wrote it, so the line reads
  `- [pirut](url) - (Fedora) a set of tools`.
- Five bracketed markers read as reference links to definitions that do not
  exist, which the linter rejects. They are escaped, so `[4.36]` is `\[4.36\]`
  and `[[FREE](url)]` is `\[[FREE](url)\]`.
- `LXDE` was introduced by a block quote indented three spaces. Two is what the
  linter wants and what the rest of the file uses.
- The `Pantheon` bullet carried the same URL as the `elementary OS` heading
  above it, and the linter reads two links to one page as a duplicate. The
  bullet keeps its words and lost the link markup. A maintainer may want it to
  point at the Pantheon project page instead.
- Three course credits repeated the same user profile that the intro already
  links. The credits keep the name and lost the markup.
- `Etcher` had a trailing space.

## Left alone

- Every description from upstream is the words upstream wrote. The pass changed
  punctuation, the case of a first word, and nothing else.
- Half of this list keeps its entries as headings, one per distribution or
  website, with a paragraph and a screenshot under each one. The engine parses
  bullets, so those sections stay out of `awesome.toml` and out of the gate.
  Reshaping them into bullets would rewrite the list rather than revive it.
- Six entries in the bash section are a bare link with no description. The gate
  warns about them and `tests/test_readme.py` holds that count. Writing those
  descriptions is not a revival.
- Three spell-check warnings stay: `docker`, `debian`, and `git`, each one the
  spelling the project itself uses.

## Links kept on http

`awesome.toml` records eleven entries in `links.allowlist`:

- `lxde.org` answers on http and its https certificate does not validate.
- The other ten are unreachable or return 404 on both schemes:
  `computefreely.org`, `corebird.baedert.org`, the Cinnamon project page,
  `gnome-twitch.vinszent.com`, `manuel-kehl.de/projects/go-for-it`,
  `openbox.org/wiki/Main_Page`, `parnold-x.github.io/nasc`,
  `sawfish.tuxfamily.org`, `vim.org`, and `wereturtle.github.io/ghostwriter`.
  A maintainer should decide whether those entries get a new home or come out
  of the list. `xfce.org` was the one host in that group that answered on
  https, so its entry moved.

## Tooling

- `pyproject.toml` pins the engine, `Makefile` carries the engine targets, and
  `AGENTS.md` describes the layout.
- `github-stats.json` records stars and last push for the 20 GitHub entries,
  and `exports/` holds the list as JSON, NDJSON, and CSV.
- `.githooks/pre-commit` and `.githooks/pre-push` run the gate. Install them
  with `make hooks-install`.
- `make check` covers the list rules, the Contents block, the stats snapshot,
  the exports, and the tests.
