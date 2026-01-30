# Copilot Workspace Instructions

## Development Checklist

Before committing any changes, ensure:

- [ ] `dotnet build` passes with no errors
- [ ] `dotnet test` passes (when tests exist)
- [ ] Code follows C# conventions (PascalCase for public members)
- [ ] No unused variables or imports

## Project Overview

**Soc Ops** is a Social Bingo game built with Blazor WebAssembly (.NET 10). Players find people who match questions to mark squares and get 5 in a row.

## Architecture

```
SocOps/
├── Components/     # Reusable Blazor components
│   ├── BingoBoard.razor
│   ├── BingoSquare.razor
│   ├── BingoModal.razor
│   ├── GameScreen.razor
│   └── StartScreen.razor
├── Models/         # Data models (BingoSquareData, GameState)
├── Services/       # Business logic
│   ├── BingoGameService.cs    # State management
│   └── BingoLogicService.cs   # Game logic
├── Data/           # Static data (Questions.cs)
├── Pages/          # Routable pages (Home.razor)
└── wwwroot/        # Static assets & CSS
```

## Key Commands

```bash
dotnet build SocOps/SocOps.csproj  # Build
dotnet run --project SocOps       # Run dev server (port 5166)
dotnet test                        # Run tests
```

## State Management

- `BingoGameService` manages game state with event-driven updates
- State persisted to localStorage via JSInterop
- Components subscribe to `OnStateChanged` event

---

## 🪔 Design Guide: Tamil Heritage Theme

This application features a rich visual design inspired by Tamil Nadu's cultural heritage, including temple architecture, kolam art, silk sarees, and traditional motifs.

### Color Palette (CSS Variables)

All colors are defined in `wwwroot/css/app.css` under `:root`:

| Variable | Value | Description |
|----------|-------|-------------|
| `--tamil-maroon` | `#800020` | Primary color — Temple pillars, auspicious |
| `--tamil-maroon-dark` | `#5c0017` | Button shadows, depth |
| `--tamil-maroon-light` | `#a3324d` | Hover states |
| `--tamil-gold` | `#d4a72c` | Accents — Prosperity, jewelry, silk |
| `--tamil-gold-bright` | `#f5c842` | Winning highlights |
| `--tamil-gold-dark` | `#b8860b` | Gold shadows |
| `--tamil-green` | `#0b6623` | Marked squares — Mango leaves |
| `--tamil-green-light` | `#2d8f4e` | Success states |
| `--tamil-teal` | `#006d6f` | Peacock accents |
| `--tamil-cream` | `#fef9e7` | Background — Raw silk |
| `--tamil-cream-dark` | `#f5e6c8` | Card surfaces |
| `--tamil-terracotta` | `#c35831` | Warm accents |
| `--tamil-vermillion` | `#e34234` | Kumkum red |
| `--tamil-saffron` | `#ff6600` | Festival orange |

### Typography

Import via Google Fonts in `index.html`:

```html
<link href="https://fonts.googleapis.com/css2?family=Catamaran:wght@400;500;600;700;800&family=Yatra+One&display=swap" rel="stylesheet">
```

| Font | Usage | CSS Class |
|------|-------|-----------|
| **Yatra One** | Titles, headings, "BINGO!" text | `.font-display` |
| **Catamaran** | Body text, UI elements | `.font-body` (default) |

### Cultural Motifs & Patterns

#### Kolam (கோலம்) — Floor Art Patterns
```css
.bg-kolam        /* Full kolam dot pattern background */
.bg-kolam-subtle /* Subtle single-dot pattern */
```

#### Temple & Saree Borders
```css
.border-temple   /* Repeating maroon-gold temple pattern */
.border-saree    /* Double-line gold border with inset */
.rangoli-border  /* Triple-line decorative border */
```

#### Decorative Elements
- `❈` — Kolam corner decorations
- `🪔` — Diya (oil lamp) for marked squares
- `🪷` — Lotus flower accents
- `🔔` — Temple bell for buttons
- `✦` — Star accent separators

### Component Styling Classes

#### Bingo Squares
```css
.bingo-square         /* Default unmarked state */
.bingo-square-marked  /* Green gradient when marked */
.bingo-square-winning /* Gold shimmer with diya glow */
.bingo-square-free    /* Free space styling */
```

#### Buttons
```css
.btn-primary    /* Temple bell style — maroon gradient with gold border */
.btn-secondary  /* Cream background with maroon border */
```

#### Cards
```css
.card-temple    /* White-to-cream gradient with gold border and top pattern */
```

### Animations

| Class | Effect | Usage |
|-------|--------|-------|
| `.animate-diya` | Warm glowing pulse | Winning squares, celebration |
| `.animate-bell` | Gentle swing | Button interactions |
| `.animate-lotus` | Bloom entrance | Modal appearance |
| `.animate-float` | Gentle vertical float | Decorative elements |
| `.animate-pulse-gold` | Opacity pulse | Header lamp |
| `.animate-bounce-in` | Scale + rotate entrance | Modal |

### Tamil Text References

Use bilingual text for cultural authenticity:

| English | Tamil | Usage |
|---------|-------|-------|
| Soc Ops | சோக் ஓப்ஸ் | App title |
| BINGO! | பிங்கோ! | Win celebration |
| Start Game | தொடங்கு | CTA button |
| Keep Playing | தொடரவும் | Continue button |
| Back | திரும்பு | Navigation |
| Welcome | வணக்கம் | Footer greeting |
| Best Wishes | வாழ்த்துக்கள் | Footer message |
| How to Play | விளையாட்டு விதிகள் | Instructions heading |

### Design Principles

1. **Warmth over coolness** — Use warm shadows (`rgba(128, 0, 32, x)`) instead of gray
2. **Gold as celebration** — Reserve bright gold for winning/success states
3. **Layered borders** — Multiple borders mimic silk saree edges (கரை)
4. **Subtle patterns** — Kolam backgrounds should be low-opacity (0.4-0.6)
5. **Diya glow effect** — Winning elements should have animated warm glow
6. **Bilingual UI** — Include Tamil script for key text elements
7. **Temple proportions** — Use generous padding and spacing

### Adding New Components

When creating new UI elements, follow this pattern:

```razor
<div class="card-temple p-6 relative">
    <!-- Optional corner decorations -->
    <div class="absolute top-2 left-2 text-gold opacity-60">❈</div>
    
    <!-- Content with Tamil-themed colors -->
    <h2 class="font-display text-maroon mb-4">Title</h2>
    <p class="text-secondary">Content text</p>
    
    <!-- Primary action -->
    <button class="btn-primary rounded-xl py-3 px-6">
        <span>தமிழ் · English</span>
    </button>
</div>
```
