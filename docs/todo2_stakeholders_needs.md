# TODO 2: Stakeholders and needs

Status: **draft, waiting for the developer's review**

Input: `docs/todo1_problem_context.md` (decisions D1-D7, open points O1-O6, assumptions H1-H8).

A **stakeholder** is anyone, or anything, that is affected by the game or places a limit on it.
A **need** is what a stakeholder wants, in their own words. Needs are not yet requirements:
they may be vague ("responds quickly") and are made precise in TODO 3 and TODO 4.

## 1. Stakeholders

| ID | Stakeholder | Who or what it is | Interests | Expectations | Constraints they bring |
|----|-------------|-------------------|-----------|--------------|------------------------|
| S1 | Player | A person playing a casual puzzle game on their PC | A short, enjoyable game they can pick up at once | Works like other match-3 games they know; clear feedback; a fair chance to win | Mouse only; no patience for setup or instructions; may not tell some colours apart |
| S2 | Developer | The student, working with an AI coding agent | Finish a working prototype and understand how it was built | A specification clear enough to build from and to check the result against | One person; limited time; the scope fixed in TODO 1 |
| S3 | Maintainer | Whoever changes the game later (may be the developer, months on) | Change or extend the game without breaking it | Readable code; settings in one place; rules that can be tested | Did not write the original code, or no longer remembers it |
| S4 | Platform | The desktop browser and the PC it runs on | Not a person, so no interests; it sets limits | The page uses only what a browser provides | A page opened from a local file has no server, no network, and stricter browser rules than a hosted page |
| S5 | Course | The exercise sheet and its authors | The requirements workflow is followed in order | Specification before code; nothing built beyond the documented scope; prompts and results recorded | The seven tasks and their order; the write-up format |

S5 was added by the agent. The sheet lists S1-S4 as "possible stakeholders"; S5 is included
because several rules of this project come from the sheet and from nowhere else.

## 2. Needs

**Kind:** *explicit* means it was stated in the brief or decided in TODO 1. *Implicit* means
nobody said it, but a player of casual puzzle games, or a person in that role, would expect it.

### Player (S1)

| ID | Need | Kind | Traces to |
|----|------|------|-----------|
| N1 | I can start playing without installing or setting up anything | Explicit | D1 |
| N2 | I can work out how to play without reading instructions | Implicit | |
| N3 | I can swap two neighbouring tiles with the mouse | Explicit | D4 |
| N4 | I can see which tile I have selected, and I can change my mind | Implicit | D4 |
| N5 | When I make a match, the tiles are removed and the board refills by itself | Explicit | Problem statement |
| N6 | After a move I can tell what happened on the board | Implicit | O6, D7 |
| N7 | A swap that makes no match costs me nothing | Explicit | D5 |
| N8 | I can always see my score, the target, and how many moves I have left | Explicit | D2, problem statement |
| N9 | I am told clearly when I have won or lost | Explicit | D2 |
| N10 | I never get stuck with no possible move | Explicit | D6 |
| N11 | I can play again when a game ends | Implicit | O4 |
| N12 | The game reacts to my clicks without a noticeable delay | Implicit | |
| N13 | I can tell the tile types apart easily, even if I cannot tell some colours apart | Implicit | D3 |
| N14 | The game is fair: the target can be reached, and the same action always follows the same rules | Implicit | O1, O2 |
| N15 | The game starts with a board I can act on, with no matches already sitting there | Implicit | O3 |

### Developer (S2)

| ID | Need | Kind | Traces to |
|----|------|------|-----------|
| N16 | The specification is precise enough that I, or the agent, can build from it and check the result against it | Explicit | Exercise sheet |
| N17 | The scope is small enough to finish as a first prototype | Explicit | D7 |
| N18 | I can test the game rules without clicking through the game by hand, including the random parts | Implicit | H5 |
| N19 | I can run the game with no build step and no tools beyond a browser and an editor | Implicit | D1 |

### Maintainer (S3)

| ID | Need | Kind | Traces to |
|----|------|------|-----------|
| N20 | I can read the code and find where a rule lives; the rules are kept apart from the drawing | Implicit | |
| N21 | Board size, number of tile types, move limit and target score are set in one place | Implicit | D2, D3, O1 |
| N22 | Features left out now (animation, special tiles) can be added later without rewriting the game | Implicit | D7 |

### Platform (S4)

| ID | Need | Kind | Traces to |
|----|------|------|-----------|
| N23 | The game runs from a local file in a current desktop browser with no network connection | Explicit | D1, O5 |
| N24 | The whole game fits on an ordinary laptop screen without scrolling | Implicit | O5 |
| N25 | The game loads nothing from outside its own folder | Implicit | D1, H1 |

### Course (S5)

| ID | Need | Kind | Traces to |
|----|------|------|-----------|
| N26 | The specification exists before any code, and the prototype contains only what the specification documents | Explicit | Exercise sheet |
| N27 | The prompts used and the location of each result are recorded | Explicit | Write-up template |
| N28 | The game has its own name and look | Explicit | H8 |

## 3. Usability and quality concerns for a casual puzzle prototype

The sheet asks which usability and quality concerns are relevant. Each is tied to the needs it
comes from. They become non-functional requirements in TODO 3.

| Concern | What it means here | Needs |
|---------|--------------------|-------|
| Learnability | A new player makes their first match without instructions | N2 |
| Feedback | Every click has a visible result; the state of the game is always on screen | N4, N6, N8, N9 |
| Error tolerance | Mistakes are cheap and can be undone | N4, N7 |
| Accessibility | Tile types differ by more than colour | N13 |
| Responsiveness | No noticeable delay after a click | N12 |
| Fairness | Winnable target; consistent rules; no dead ends | N10, N14, N15 |
| Portability | Runs in common desktop browsers with nothing installed | N1, N23, N24, N25 |
| Testability | Rules can be checked automatically | N18 |
| Maintainability | Readable, configurable, extendable | N20, N21, N22 |

## 4. Tensions noticed

TODO 3 asks for overlaps, dependencies and conflicts to be checked. These three are already
visible and are noted here so they are not lost.

| ID | Tension | Between |
|----|---------|---------|
| T1 | The player needs to see what a move did, but animation is out of scope. With an instant redraw, a cascade or a swap that is reversed may be invisible | N6 against D7 |
| T2 | The maintainer wants rules kept apart from drawing, which usually means several script files. Browsers block some ways of loading scripts for a page opened from a local file, so the way the files are split is limited | N20, N22 against N19, N23 |
| T3 | The player wants a fair, winnable game, but new tiles are random, so no fixed target is winnable every time | N14 against H5 |
