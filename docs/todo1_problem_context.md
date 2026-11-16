# TODO 1: Clarify the problem context

Status: **complete**

## 1. The brief as given

> You are asked to develop a game inspired by classic match-3 puzzle games such as Candy
> Crush. The intended outcome is a basic playable version that can run locally on a standard
> personal computer.

Two further rules from the exercise sheet apply:

- Implementation begins only after there is a structured requirements specification.
- Anything not explicitly in the documented scope is out of scope for the first prototype.

## 2. Ambiguous or underspecified aspects

Each row quotes or names the part of the brief that is unclear and says why it matters.

| ID | Unclear point | Why it matters |
|----|---------------|----------------|
| A1 | "basic playable version" has no definition of done | Without one, nobody can say when the prototype is finished or test it |
| A2 | "inspired by ... match-3" does not say which mechanics are included | Swap, match, removal, gravity, refill and cascades are the usual core; special tiles, boosters and obstacles are common too. The brief does not draw the line |
| A3 | No goal or end condition | A game needs a way to win, lose or stop: target score, move limit, timer, or endless play |
| A4 | Board is not described | Size, shape and number of tile types drive difficulty and layout |
| A5 | Input method is not stated | Click two tiles, drag a tile, or keyboard all lead to different interface code |
| A6 | Behaviour on an invalid move is not stated | A swap that makes no match can be reverted, refused, or allowed |
| A7 | Starting board rules are not stated | A random board may start with matches already on it, or with no possible move |
| A8 | Behaviour when no valid move remains is not stated | Options: reshuffle, end the game, or leave the player stuck |
| A9 | Scoring is not defined | Points per tile, bonus for longer matches, bonus for cascades |
| A10 | "run locally" is vague | A file opened in a browser, an installed desktop program, or a script that needs a runtime installed first |
| A11 | "standard personal computer" is vague | Operating system, screen size and input devices are not named |
| A12 | Technology is not chosen | Language and libraries decide how the game is run and who can maintain it |
| A13 | Look, animation and sound are not mentioned | Animated falling tiles take far more work than an instant redraw |
| A14 | Saving and high scores are not mentioned | Persistence adds storage and its own failure cases |
| A15 | Restart is not mentioned | Whether the player can start again without reloading |

## 3. Hidden assumptions

Things the brief seems to take for granted without saying so.

| ID | Assumption | Risk if wrong |
|----|------------|---------------|
| H1 | One player, one device, no network | Multiplayer or online play would change the architecture |
| H2 | The player uses a mouse or trackpad | A touch-only or keyboard-only player could not play |
| H3 | The board is a rectangular grid and tiles fall straight down | Other shapes or fall directions change the core algorithm |
| H4 | Matches are straight lines of three or more, horizontal or vertical | L, T or diagonal matches would need different detection |
| H5 | New tiles are random | Fairness and testing both depend on how randomness is handled |
| H6 | One developer working with an AI coding agent, no fixed deadline | Affects how much scope is realistic |
| H7 | No accounts, payments, ads or levels map | These are central to the commercial game the brief names |
| H8 | The game has its own name and look | Copying an existing game's name, art or levels is not acceptable |

## 4. Design choices

Decided by the developer on 2026-11-16. The agent proposed the options; the developer chose.

| ID | Choice | Decision | Reason | Resolves |
|----|--------|----------|--------|----------|
| D1 | How it runs | A web page opened from a local file in a desktop browser | Nothing to install, works on any PC with a browser | A10, A11, A12 |
| D2 | How a game ends | A move limit with a target score. Reaching the target within the limit wins; running out of moves first loses | Gives a clear win and loss that can be tested | A1, A3 |
| D3 | Board | 8 × 8 rectangular grid, 6 tile types | The usual setup for the genre | A4, H3 |
| D4 | Input | The player clicks one tile, then a neighbouring tile, to swap them | Simplest to build and to test | A5, H2 |
| D5 | Swap that makes no match | The two tiles swap back and the move is not counted | The player is not punished for a mistake | A6 |
| D6 | No valid move left | The board is reshuffled | The game never gets stuck | A8 |
| D7 | Left out of the first prototype | Special tiles, sound, saving and high scores, multiple levels, animation | Keeps the first version small. Animation is a candidate for a later "Should" | A2, A13, A14 |

### Still open after this task

These are not decided yet. They are carried into TODO 3 and TODO 4, where each requirement has
to be made measurable.

| ID | Open point | From |
|----|------------|------|
| O1 | The number of moves and the target score | D2 |
| O2 | The scoring rule: points per tile, and whether longer matches or cascades earn more | A9 |
| O3 | Starting board rules: no match already on the board, and at least one valid move | A7 |
| O4 | Whether the player can restart without reloading the page | A15 |
| O5 | Which browsers must be supported, and the smallest window size | A11 |
| O6 | Whether a failed swap that is swapped back must be shown to the player, given there is no animation | D5, D7 |

## 5. Refined problem statement

Build a single-player match-3 puzzle game with its own name and look, as a web page that runs
from a local file in a desktop browser with no installation and no network connection.

The game is played on an 8 × 8 grid filled with tiles of 6 types. The player swaps two
neighbouring tiles by clicking one and then the other. A swap is kept only if it forms a
straight line of three or more tiles of the same type, horizontal or vertical; otherwise the
tiles swap back and no move is used. Matched tiles are removed, the tiles above fall down, new
random tiles fill the empty cells from the top, and any new matches this creates are resolved
in turn until the board is stable. If the board has no valid move, it is reshuffled.

Removed tiles earn points. The player wins by reaching a target score within a fixed number of
moves and loses if the moves run out first.

The first prototype is **playable** when a person can open the page, play one full game from
the first move to a win or a loss using only the mouse, and see their score and remaining
moves at all times.

**Out of scope for the first prototype:** special tiles, boosters and obstacles; sound;
animation; saving and high scores; more than one level; multiplayer; accounts, payments and
ads; touch and keyboard control.
