# Theme Color Scheme

## Current Theme: Swedish/Nordic

The theme uses a warm, earthy Swedish/Nordic color palette designed for Höganäs Makerspace.

### Colors

| Color Name | Hex | RGB | Usage |
|---|---|---|---|
| **Mörkbrun** (Dark Brown) | `#4A3B29` | rgb(74, 59, 41) | Background, main surface |
| **Krämvit** (Cream White) | `#F3EFE7` | rgb(243, 239, 231) | Text, foreground |
| **Tegelröd** (Brick Red) | `#9E6C54` | rgb(158, 108, 84) | Highlights, links, accents, buttons |

### Implementation

All colors are defined in `_sass/libs/_vars.scss` using SCSS variables. This means:
- Colors automatically apply to buttons, links, borders, backgrounds, etc.
- Changing one color value updates the entire theme
- The palette is easy to modify and test

### Reverting Colors

To revert to the **original theme colors**, edit `_sass/libs/_vars.scss`:

1. **Find** the Swedish/Nordic palette (starting at line 31)
2. **Comment it out** using `/* ... */`
3. **Uncomment** the original palette block below it (after line 50)
4. Save the file

The Jekyll server will automatically rebuild and apply the change. Reload your browser to see the original colors.

### CSS Classes Affected

The color variables propagate to:
- `background-color` of body and sections
- Text `color` for readability
- `border-color` for dividers and boxes
- Button `:hover` and `:active` states
- Link colors
- Form element focus states
- Navigation menu highlights
- Tile backgrounds and hover effects

No manual CSS updates are needed when switching palettes — all colors follow the variable system.
