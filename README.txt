BIT PLANES — PHYSICS DEMO
=========================

WHAT'S HERE
  index.html           Self-contained game (sprites embedded). Just open it.
  index-external.html  Same game, loads PNGs from sprites/ (cleaner to edit).
  sprites/             PNG assets, backgrounds already made transparent.
  CLAUDE.md            Full project context for Claude Code — read this first.
  README.txt           This file.

QUICK START IN CLAUDE CODE
  1. Put this whole folder somewhere on your machine.
  2. Open a terminal in this folder and run:  claude
  3. Claude Code auto-reads CLAUDE.md, so it already knows the physics + history.
  4. Try: "open index.html in my browser and help me tune the flight feel"

RUN WITHOUT CLAUDE CODE
  - index.html: just double-click it.
  - index-external.html: needs a local server (browsers block file:// image loads):
        python3 -m http.server 8000
    then open http://localhost:8000/index-external.html

PHYSICS NOTE
  The flight model is ported verbatim from the original medv.io Bit Planes
  source. CLAUDE.md explains every constant and the bugs already fixed.
