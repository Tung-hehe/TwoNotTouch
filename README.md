# Logic puzzles solver

## Install libraries

```
pip install -r requirements.txt
```

## Run
- Change directory to this folder and run
    ```
    python main.py -p [P] -d [D]
    ```
- `[P]` is a puzzle sorted name

    | Sorted name | Puzzle name         |
    | :---------: | :------------------ |
    |     `B`     | Binox               |
    |     `G`     | Galaxies            |
    |     `S`     | Sudoku              |
    |     `SB`    | StarBattle          |
    |     `T`     | Troix               |
    |     `SL`    | Slitherlink         |
    |     `HMM`   | Haunted Mirror Maze |

- `[D]` is path to problem data
- Example running
    ```
    python main.py -p SB -d ./data/star_battle/puzzle_1.json
    ```
- Help `-h` for more details:
    ```
    python main.py -h
    ```
- Example data in `./data/`

**Note**: *If you want to solve a new puzzle, you need to model this puzzle follow belowed data structure.*

## Binox
Rules:
1. The finished puzzle should be filled with Xs and Os.
2. Horizontally and vertically, there should never be a continuous run of the same symbol longer than 2.
3. There are an equal number of Xs and Os in each row and column.
4. All rows are unique. All columns are unique, too.

Data structure:
```json
    {
        "shape": [6, 6], // size of puzzle [number of rows, number of columns]
        "symbol_number": 2, // max number of the same symbol touching in each row, col
        "fixed": [ // fixed cells
            {"row": 0, "col": 0, "val": "X"}, // a fixed cell
            {"row": 1, "col": 2, "val": "O"},
            {"row": 2, "col": 1, "val": "O"},
            {"row": 2, "col": 2, "val": "O"},
            {"row": 3, "col": 0, "val": "X"},
            {"row": 3, "col": 5, "val": "X"},
            {"row": 4, "col": 2, "val": "O"},
            {"row": 4, "col": 5, "val": "X"}
        ]
    }
```

Example data:
1. [./data/binox/puzzle_1.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/binox/puzzle_1.json): `#1` in [Toughest 6x6 Binox, Volume 1, Book 1](https://files.krazydad.com/binox/sfiles/BINOX_6x6_TF_v1_4pp_b1.pdf)
2. [./data/binox/puzzle_2.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/binox/puzzle_2.json): `#1` in [Toughest 8x8 Binox, Volume 1, Book 1](https://files.krazydad.com/binox/sfiles/BINOX_8x8_TF_v1_4pp_b1.pdf)
3. [./data/binox/puzzle_3.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/binox/puzzle_3.json): `#1` in [Toughest 10x10 Binox, Volume 1, Book 1](https://files.krazydad.com/binox/sfiles/BINOX_10x10_TF_v1_4pp_b1.pdf)
4. [./data/binox/puzzle_4.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/binox/puzzle_4.json): `#1` in [Toughest 12x12 Binox, Volume 1, Book 1](https://files.krazydad.com/binox/sfiles/BINOX_12x12_TF_v1_2pp_b1.pdf)
5. [./data/binox/puzzle_5.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/binox/puzzle_5.json): `#1` in [Toughest 14x14 Binox, Volume 1, Book 1](https://files.krazydad.com/binox/sfiles/BINOX_14x14_TF_v1_2pp_b1.pdf)

Modeling: [./docs/binox.md](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/docs/binox.md)

Detail and puzzles: [Krazydad](https://krazydad.com/binox/)

## Galaxies
Rules:
1. Connect the dots to make edges so that each circle is surrounded by a symmetrical galaxy shape,
2. The puzzle is completely tiled with galaxies.
3. Each galaxy shape must be rotationally symmetric, having an identical appearance when rotated 180 degrees.

Data structure:
```json
    {
        "shape": [21, 11], // size of puzzle [number of rows, number of columns]
        "galaxies": [ // centers of galaxies
            [
                {"row": 0, "col": 4} // center of a galaxy
            ],
            [
                {"row": 0, "col": 0},
                {"row": 1, "col": 0}
            ],
            [
                {"row": 0, "col": 5},
                {"row": 0, "col": 6},
                {"row": 1, "col": 5},
                {"row": 1, "col": 6}
            ],
        ]
    }
```

Example data:
1. [./data/galaxies/puzzle_1.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/galaxies/puzzle_1.json): `#16` in [ 7x7 Galaxy, Book 1](https://files.krazydad.com/galaxies/books/GAL_d7_b1.pdf)
2. [./data/galaxies/puzzle_2.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/galaxies/puzzle_2.json): `#10` in [ 10x10 Galaxy, Book 1](https://files.krazydad.com/galaxies/books/GAL_d10_b1.pdf)
3. [./data/galaxies/puzzle_3.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/galaxies/puzzle_3.json): `#5` in [ 21x11 Galaxy, Book 1](https://files.krazydad.com/galaxies/books/GAL_d11_b1.pdf)
4. [./data/galaxies/puzzle_3.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/galaxies/puzzle_4.json): `#2` in [ 21x21 Galaxy, Book 1](https://files.krazydad.com/galaxies/books/GAL_d21_b1.pdf)

Modeling: [./docs/galaxies.md](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/docs/galaxies.md)

Detail and puzzles: [Krazydad](https://krazydad.com/galaxies/)

## Sudoku
Rules:
1. Each row, column, block not contain duplicate values
2. Value in cell in range [1, $n$]

Data structure:
```json
{
    "shape": 9, // size of puzzle
    "fixed_cells": [ // fix cells
        {"row": 0, "col": 2, "val": 1},
        {"row": 0, "col": 3, "val": 6},
        {"row": 0, "col": 7, "val": 5},
        {"row": 1, "col": 0, "val": 5},
        {"row": 1, "col": 1, "val": 3},
    ]
}
```

Example data:
1. [./data/sudoku/puzzle_1.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/sudoku/puzzle_1.json): `#1` in [ Insane Sudoku Puzzles, Volume 22, Book 1 ](https://files.krazydad.com/sudoku/sfiles/KD_Sudoku_IN22_8_v1.pdf)

Modeling: [./docs/star_battle.md](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/docs/sudoku.md)

Detail and puzzles: [Krazydad](https://krazydad.com/sudoku/)

## Star Battle
Rules:
1. Each puzzle is divided into $s$ different regions.
2. Each cage, row and column contains $n$ (base on $s$) star.
3. The stars may not be adjacent to each other (not even diagonally).

Data structure:
```json
{
    "shape": [10, 10], // size of puzzle [number of rows, number of columns]
    "star_number": 2, // nStar each row, col, cage
    "cages": [
        // a cage includes cells
        [
            {"row": 0, "col": 0}, // a cell in cage
            {"row": 0, "col": 1},
            {"row": 0, "col": 2},
            {"row": 0, "col": 3},
            {"row": 1, "col": 0}
        ],
        // other cage
        [
            {"row": 0, "col": 4},
            {"row": 0, "col": 5},
            {"row": 0, "col": 6},
            {"row": 0, "col": 7},
            {"row": 0, "col": 8}
        ]
        // ...
    ]
}
```

Example data:
1. [./data/star_battle/puzzle_1.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/star_battle/puzzle_1.json): `#1` in [Star Battle 8x8, Volume 1, Book 1](https://files.krazydad.com/starbattle/sfiles/STAR_R2_8x8_v1_b1.pdf)
2. [./data/star_battle/puzzle_2.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/star_battle/puzzle_2.json): `#1` in [Star Battle 10x10, Volume 1, Book 1](https://files.krazydad.com/starbattle/sfiles/STAR_R2_10x10_v1_b1.pdf)
3. [./data/star_battle/puzzle_3.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/star_battle/puzzle_3.json): `#1` in [Star Battle 14x14, Volume 1, Book 1](https://files.krazydad.com/starbattle/sfiles/STAR_14x14_v1_b1.pdf)

Modeling: [./docs/star_battle.md](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/docs/star_battle.md)

Detail and puzzles: [Krazydad](https://krazydad.com/starbattle/)

## Troix
Rules:
1. The puzzle is filled with Xs, Os, and Is.
2. Horizontally and vertically, there can be no more than 2 of the same symbol touching (no three-in-a-row).
3. There is an equal number of each symbol in each row and column.

Data structure:
```json
    {
        "shape": [9, 9], // size of puzzle [number of rows, number of columns]
        "symbol_number": 2, // max number of the same symbol touching in each row, col
        "fixed": [ // fixed cells
            {"row": 0, "col": 0, "val": "X"}, // a fixed cell
            {"row": 3, "col": 0, "val": "I"},
            {"row": 3, "col": 1, "val": "O"},
            {"row": 3, "col": 3, "val": "X"},
        ]
    }
```

Example data:
1. [./data/troix/puzzle_1.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/troix/puzzle_1.json): `#1` in [9x9 TroixPuzzles, Volume 1, Book 1](https://files.krazydad.com/troix/sfiles/TROIX_9x9_regular_v1_4pp_b1.pdf)
2. [./data/troix/puzzle_2.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/troix/puzzle_2.json): `#1` in [12x12 TroixPuzzles, Volume 1, Book 1](https://files.krazydad.com/troix/sfiles/TROIX_12x12_regular_v1_2pp_b1.pdf)
3. [./data/troix/puzzle_3.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/troix/puzzle_3.json): `#1` in [15x15 TroixPuzzles, Volume 1, Book 1](https://files.krazydad.com/troix/sfiles/TROIX_15x15_regular_v1_2pp_b1.pdf)
4. [./data/troix/puzzle_4.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/troix/puzzle_3.json): `#1` in [21x21 TroixPuzzles, Volume 1, Book 1](https://files.krazydad.com/troix/sfiles/TROIX_21x21_regular_v1_1pp_b1.pdf)

Modeling: [./docs/troix.md](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/docs/troix.md)

Detail and puzzles: [Krazydad](https://krazydad.com/troix/)

## Slitherlink
Rules:
1. Connect horizontally or vertically adjacent dots to form a meandering path that forms a single loop, without crossing itself, or branching.
2. The numbers indicate how many lines surround each cell. Empty cells may be surrounded by any number of lines (from 0 to 3).

Data structure:
```json
    {
        "shape": [7, 7], // size of puzzle [number of rows, number of columns]
        "surrounded_line_number": [ // number of lines surround cells
            {"row": 0, "col": 0, "val": 2},
            {"row": 0, "col": 1, "val": 2},
        ]
    }
```

Example data:
1. [./data/slitherlink/puzzle_1.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/slitherlink/puzzle_1.json): `#1` in [ Tough Slitherlink Puzzles, 7 x 7 Format, Volume 1, Book 1](https://files.krazydad.com/slitherlink/sfiles/sl_d2_07x07_b001.pdf)
2. [./data/slitherlink/puzzle_2.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/slitherlink/puzzle_2.json): `#1` in [ Tough Slitherlink Puzzles, 10 x 10 Format, Volume 1, Book 1](https://files.krazydad.com/slitherlink/sfiles/sl_d2_10x10_b001.pdf)
3. [./data/slitherlink/puzzle_3.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/slitherlink/puzzle_3.json): `#1` in [ Tough Slitherlink Puzzles, 20 x 20 Format, Volume 1, Book 1](https://files.krazydad.com/slitherlink/sfiles/sl_d2_20x20_b001.pdf)

Modeling: [./docs/slitherlink.md](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/docs/slitherlink.md)

Detail and puzzles: [Krazydad](https://krazydad.com/slitherlink/)


## Hauted Mirror Maze
Rules:
1. Fill each empty box of the puzzle grid with the right monster: a ghost, vampire, or zombie
2. The clues along the edges tell you how many monsters you can see from that point looking into the grid, and the diagonal lines are mirrors that reflect a line of sight 90 degrees, as with a laser..
3. Vampires (V) are seen only head-on (have no reflection in a mirror).
4. Ghosts (G) are only seen as reflections in mirrors (not head-on).
5. Zmobies (Z) are always seen.
6. Each puzzle also has a handy list of monsters so you know how many of each type are hiding in that mirror maze.
7. Some cells contain the same monsters.
8. Some cells contain fixed monsters.

Data structure:
```json
    {
        "shape": [7, 7], // size of puzzle [number of rows, number of columns]
        "visibility": { // number of monsters you can see from that point looking into the grid
            "top": [0, 1, 3, 12, 1, 1, 1],
            "bot": [1, 1, 3, 1, 1, 1, 1],
            "left": [0, 2, 1, 4, 2, 0, 1],
            "right": [3, 2, 2, 2, 11, 2, 1]
        },
        "mirrors": [ // mirrors position
            {"row": 0, "col": 0, "val": "/"},
            {"row": 0, "col": 1, "val": "/"},
            {"row": 0, "col": 2, "val": "\\"},
            {"row": 0, "col": 3, "val": "\\"},
            {"row": 0, "col": 4, "val": "\\"}
        ],
        "monster_number": [ // number of each type of monsters are hiding in that mirror maze
            {"name": "V", "val": 19},
            {"name": "G", "val": 20},
            {"name": "Z", "val": 10}
        ],
        "fixed_cells": [
            {"row": 5, "col": 3, "val": "Z"} // fixed monster cells
        ],
        "same_cells": [ // cells contain the same monsters
            {"row": 1, "col": 2},
            {"row": 4, "col": 5},
            {"row": 5, "col": 0}
        ]
    }
```

Example data:
1. [./data/haunted_mirror_maze/puzzle_1.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/haunted_mirror_maze/puzzle_1.json): `#1` in [ Haunted Mirror Maze, 6 x 6 Format](https://thegriddle.net/puzzledir/hmm_2013_09_10.pdf)
2. [./data/haunted_mirror_maze/puzzle_1.json](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/data/haunted_mirror_maze/puzzle_2.json): `#2` in [ Haunted Mirror Maze, 7 x 7 Format](https://thegriddle.net/puzzledir/haunted_5.pdf)

Modeling: [./docs/slitherlink.md](https://github.com/Tung-hehe/LogicPuzzlesSolver/blob/main/docs/haunted_mirror_maze.md)

Detail and puzzles: [Krazydad](https://krazydad.com/haunted/)
