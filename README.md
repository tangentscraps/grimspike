# tangentscraps/grimspike

> A brainfuck interpreter, syntax highlighter, and full-screen terminal debugger
> written in Nim (2013-era "nimrod"), built pair-programming style over one day.
> Repo: https://github.com/tangentscraps/grimspike — 7 files, 15 commits. Last pushed 2015-12-20.

## What it is

**Grimspike** is a complete little brainfuck toolchain in ~260 lines of Nim:
- `bfrun.nim` — an interpreter with a step-through debugger (`-d` flag) and a
  built-in test suite (`-t` flag)
- `bfsyn.nim` — a syntax highlighter that colorizes brainfuck source on stdin
- `hello.bf` — the classic commented hello-world, lifted from Wikipedia

The debugger is the fun part: on every instruction it redraws the terminal with
three panels — a hexdump of the 30,000-byte tape, the source code with each
opcode syntax-highlighted (and the instruction pointer in reverse video), and the
program's output so far with control characters rendered as caret notation.
Pressing Enter steps one instruction.

Per the README, it was "built in collaboration with
[@SirSkidmore](https://github.com/SirSkidmore), who didn't get any credit in the
commits because we were pair programming on my server" — so the single-author
commit history is misleading; Taylor Skidmore is the co-author (also named in
the source-file copyright header).

## Tech stack

Nim (called "nimrod" at the time — the Makefile invokes `nimrod c`), standard
library only: `os`, `unsigned`, `terminal`, `unittest`. The classic 30,000-byte
tape, 8 opcodes, no extensions. Builds via a 20-line Makefile with catch-all
`gen/%` / `run/%` rules.

## Inventory

| Path | Contents |
|------|----------|
| `bfrun.nim` | Interpreter, debugger UI, unit + acceptance tests, CLI (`-t` / `-d` / PATH) |
| `bfsyn.nim` | 40-line stdin→stdout syntax highlighter (raw ANSI escape codes) |
| `hello.bf` | Annotated hello-world from Wikipedia |
| `hello.nim` | Literally `echo("hello world")` — the Nim toolchain smoke test |
| `Makefile` | Catch-all compile/run rules around `nimrod c` |
| `README.md` | One-line description + the SirSkidmore credit note |
| `.gitignore` | `gen`, `nimcache`, emacs junk |

## Surprising / notable

- **Twelve commits in one day:** everything from "create repo" (2013-05-29) to a
  tested, debugged interpreter landed 2013-05-29/30. The commit messages read
  like a live lab notebook: *"work in progress: bfrun (hello world produces
  'jfmmpnypsmeol' :/)"* → *"(broken) added a small debugger"* → *"split ram
  into code and data (still broken though :/)"* → *"got the debugger running
  and fixed the [ and ] opcodes."*
- **Real tests in a toy:** unit tests for five of the eight opcodes plus an
  acceptance test that runs a BF program emitting ASCII `'A'` — remarkably
  disciplined for a weekend toy.
- **Stale by one language rename:** the Makefile still says `nimrod`, the
  language's name before it became "Nim." A modern `nim c` would need small
  porting (old-style `T` type prefixes, `E_base`, etc.).
- No linked streams or videos found in the repo. Verdict at triage: **keep**.

---

## Original README

a brainf**k intepreter, syntax highlighter, and debugger written in nim.

(built in collaboration with [@SirSkidmore](https://github.com/SirSkidmore), who didn't get any credit in the commits because we were pair programming on my server)
