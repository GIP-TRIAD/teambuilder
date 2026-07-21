# Team Builder

A single-file, web app for splitting a class roster into teams.

Everything runs in the browser. There's no server and no data ever leaves your
machine.

**[Launch Team Builder](https://gip-triad.github.io/teambuilder/)**

## Features

- **Upload a CSV** of students (`name, university, gender`). A template is one click
  away if you don't have one yet.
- **Configure teams**: choose the number of teams and set each team's size
  individually.
- **Toggle constraints**: university coverage is a hard requirement; gender balance
  is a soft preference the app optimizes for.
- **Click-to-lock board**: click a student's name to lock them into a team. The app
  will:
  - grey out any choice that would make the board unsolvable,
  - automatically lock in a student's team the moment it becomes the *only*
    remaining valid option,
  - star its top 1–2 recommended arrangements for whichever students aren't locked
    yet.
- **Pairing rules**: optionally require two specific students to be on the same
  team, or keep them apart — either as a hard rule or a soft preference.
- **Undo / Reset**: step back through your locks, or clear the board and start over.
- **Export**: download the current team composition as a CSV, ready to paste into a
  spreadsheet or share with co-instructors.
- **Next round, different groups**: once a set of teams is locked in, click **Start
  next round** to save it as a reference and build a fresh set of teams
biased toward
  putting students with *different* teammates than last time. A live badge shows
  both how many repeat pairings are on the board right now and the true minimum
  still reachable from your current locks, so you know whether it's worth
  continuing to click for a better arrangement.
- **Autosaves locally** as you go, so refreshing the page won't lose your progress.

## CSV format

```csv
name,university,gender
Chen,Singapore,M
Lulu,Singapore,F
Marcel,Marseille,M
Dominique,Marseille,F
```

- `gender` accepts `M`/`F` or `Male`/`Female`.
- Basic quoted fields are supported (e.g. `"Doe, Jane"`), though this isn't a full
  RFC4180 parser.

### Exported CSV

`Export CSV` produces one row per student:

```csv
team,name,university,gender
Team Alpha,Chen,Singapore,M
Team Alpha,Marcel,Marseille,M
Team Beta,Dominique,Marseille,F
(unplaced),Cristina,Naples,F
```

Only students you've actually locked into a team are listed under that team.
Anyone not yet locked in appears under `(unplaced)` rather than being guessed into a
team on your behalf — the board's star recommendations are a hint, not a
prediction, so exporting only ever reflects locks you've actually made.

## Known limitations

- CSV parsing supports basic quoted fields but isn't a full RFC4180 implementation.
  clears every lock at once.
- Not tested for rosters larger than ~15 students.
