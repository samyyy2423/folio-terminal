# terminal

For [Folio](https://github.com/samyyy2423/folio) programs run in a terminal: colours and styles, tables lined
up in columns, boxes, progress bars that draw over themselves, and spinners. With the ANSI codes that every
Linux and Mac terminal, and Windows Terminal, understand. In Folio alone, so it works everywhere Folio does.

```text
folio add terminal
```

```
use the package "terminal" as terminal

say terminal's red("error:") " the file isn't there"
say terminal's bold(terminal's green("done")) " " terminal's colored("note", "bright cyan")

set people to list of (record with name "Ana", age 31), (record with name "Bo", age 7)
say terminal's table(people)
say terminal's box("Folio 1.11\nready", "round")

say terminal's progress_bar(0, 120, 20)
for each k from 1 to 120
    wait 10 milliseconds
    say terminal's again(terminal's progress_bar(k, 120, 20))   # over the line before
end
```

```text
┌──────┬─────┐
│ name │ age │
├──────┼─────┤
│ Ana  │  31 │
│ Bo   │   7 │
└──────┴─────┘
╭───────────╮
│ Folio 1.11 │
│ ready     │
╰───────────╯
████████████████████ 100%
```

## What it has

| | |
|---|---|
| `red`, `green`, `yellow`, `blue`, `magenta`, `cyan`, `white`, `gray`, `black` | the words in that colour |
| `colored(words, colour)`, `on_color(words, colour)` | the words in a colour, or on one: a name, `"bright red"`, or `"#ff8800"` |
| `rgb(words, r, g, b)`, `on_rgb(words, r, g, b)` | any colour, each part from 0 to 255 |
| `bold`, `dim`, `italic`, `underline`, `inverse`, `strike` | the words in that style |
| `link(words, address)` | words a terminal can open, as a link |
| `table(rows, headers, style)` | rows lined up in columns: a list of records or dictionaries (their fields are the columns), or of lists; headers pick the fields, or `nothing` for all of them; style `"box"`, `"ascii"`, `"plain"` or `"markdown"`. Numbers go on the right, and a cell can have new lines in it |
| `box(words, style)` | lines around the words: `"box"`, `"round"`, `"double"` or `"ascii"` |
| `progress_bar(done, out_of, size)` | `█████░░░░░░░░░░░░░░░  25%` |
| `spinner(n)` | one of ten spinner frames: say a new one each step |
| `again(words)` | the words, said over the line (or lines) said last |
| `clear_screen()` | the codes that clear the terminal |
| `plain(words)` | the words with every code taken out |
| `width(words)` | how many columns they take: codes take none, and Chinese, Japanese, Korean and most emoji take two |
| `aligned(words, size, side)` | padded with spaces to `size` columns: `"left"`, `"right"` or `"center"` |
| `set_colors(no)` | every function here gives back the words as they are, for output to a file or a `--no-color` option |

Styles nest: `terminal's red("a" + terminal's bold("b") + "c")` is red all through, and the colour comes back
after a different one inside it ends.

On Windows, colours show in Windows Terminal (where Windows 11 runs programs) and in VS Code's terminal; the
old console window shows the codes as they are, so a program for it can call `set_colors(no)`.

## Tests

```text
folio test terminal.test.folio
```

## License

Apache License 2.0, as Folio is: see [LICENSE](LICENSE).
