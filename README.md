# Chord Atlas

Chord Atlas is a responsive guitar chord finder for exploring different voicings across the fretboard. Choose a root note and chord quality to compare open shapes, barre chords, and positions higher up the neck.

The application is distributed as a self-contained HTML page. It runs directly in a modern browser and does not require a server, package installation, framework, or internet connection.

## Features

- Browse chord voicings for all 12 chromatic root notes
- Explore major, minor, seventh, extended, suspended, altered, and other chord qualities
- Compare every available position for the selected chord
- View open, muted, and fretted strings using standard chord-diagram notation
- Show finger numbers below the diagram, inside the dots, or hide them
- See where each voicing begins on the fretboard
- Review the chord tones contained in each voicing
- Use the built-in diagram-reading guide
- Responsive layout for desktop, tablet, and mobile screens
- Works offline as a single HTML file

## Getting started

Clone or download the repository, then open the HTML file in a browser:

```text
chords-db-chord-shape-demo.html
```

No build command is required to use the finished page.

You can also serve the repository with any static file server. For example:

```bash
npx serve .
```

## How to use it

1. Select a root note.
2. Select a chord quality.
3. Compare the displayed voicings.
4. Use the finger-label controls to change how fingering information appears.
5. Check the position label to distinguish open chords from shapes higher up the neck.

The diagrams show strings from the lowest-pitched string on the left to the highest-pitched string on the right.

| Symbol | Meaning |
| --- | --- |
| `●` | Fret and play the string |
| `○` | Play the string open |
| `×` | Mute or skip the string |

## Technology

Chord Atlas is built with plain HTML, CSS, and JavaScript. The page embeds its dependencies and chord data so it can run without external network requests.

### Chord Shape JS

[Chord Shape JS](https://github.com/craigdanj/chord-shape-js) renders the guitar chord diagrams as scalable SVG graphics. It supports open strings, muted strings, finger numbers, barre chords, and shapes that begin above the first fret.

### Chords DB

[Chords DB](https://github.com/tombatossals/chords-db) provides the guitar chord and voicing data. Its compiled guitar database contains the fret positions, fingerings, barre information, base fret, and MIDI notes used by the application.

### Chords DB Adapter

The included Chords DB adapter converts compiled Chords DB positions into the option format expected by Chord Shape JS. In particular, it:

- converts base-fret-relative positions into absolute fret numbers;
- normalizes finger values;
- converts barre fret values into string-to-string spans;
- calculates a suitable diagram height for each voicing; and
- carries the MIDI note data through for displaying chord tones.

## How the page works

The application follows a small data-rendering pipeline:

1. The user selects a root note and chord quality.
2. The matching chord entry is read from the embedded guitar database.
3. The adapter converts each available position into rendering options.
4. Chord Shape JS creates an SVG diagram for every voicing.
5. The interface displays the diagrams with their position and chord-tone information.

## Project structure

The repository may contain the following files during development:

```text
.
├── chords-db-chord-shape-demo.html   # Finished self-contained application
├── chords-db-demo.template.html      # Editable HTML template
├── chords-db-adapter.js              # Data-format adapter
└── build-demo.js                     # Produces the self-contained HTML file
```

If only the finished HTML file is being published, the template and build files are not required at runtime.

## Rebuilding the single-file page

The build script combines the page template, Chord Shape JS, the adapter, and the compiled Chords DB guitar data into the finished HTML file.

With the expected source files available, run:

```bash
node build-demo.js
```

This creates or updates `chords-db-chord-shape-demo.html`.

## Customization

Visual styles are defined with CSS custom properties near the beginning of the page template. These variables control the main colors, surfaces, borders, and shadows:

```css
:root {
  --ink: #191814;
  --muted: #747168;
  --paper: #f4f0e8;
  --card: #fffdf8;
  --line: #d9d2c4;
  --accent: #e75032;
}
```

The chord cards are generated in the page's JavaScript. Rendering dimensions and diagram colors can be adjusted in the options passed through the adapter to Chord Shape JS.

## Browser support

Chord Atlas is intended for current versions of Chrome, Edge, Firefox, and Safari. It uses modern JavaScript, CSS Grid, custom properties, and inline SVG.

## Data and notation notes

- The page currently uses the six-string guitar dataset.
- Strings are ordered from low E to high E.
- A voicing's displayed fret number indicates where its diagram begins.
- Chord-tone labels are derived from the MIDI notes supplied with each Chords DB position.
- The available shapes and fingerings reflect the source dataset and may include several valid alternatives for the same chord.

## Credits

- Guitar chord data: [tombatossals/chords-db](https://github.com/tombatossals/chords-db)
- Chord diagram rendering: [craigdanj/chord-shape-js](https://github.com/craigdanj/chord-shape-js)
- Chords DB integration: Chords DB Adapter

## License

Chord Shape JS and Chords DB are published under the MIT License. Retain the relevant copyright and license notices when redistributing their source code or data.

Add the repository's own license file alongside this README so the licensing terms for Chord Atlas and the adapter are explicit.
