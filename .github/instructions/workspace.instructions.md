---
name: socops-workspace
description: Workspace-level instructions for the SocOps Blazor WebAssembly Bingo Game. Follow these patterns when modifying or extending the codebase.
---

# SocOps Workspace Instructions

## Mandatory Development Checklist

Before committing code, ensure:
- [ ] **Lint**: No warnings/errors in IDE (check Problems panel)
- [ ] **Build**: `dotnet build SocOps/SocOps.csproj` succeeds
- [ ] **Test**: Manual test in browser at http://localhost:5166
- [ ] **Events**: All event subscriptions have matching unsubscriptions in `Dispose()`
- [ ] **State**: Game state changes trigger `OnStateChanged` events
- [ ] **Styling**: Only utility classes from [app.css](SocOps/wwwroot/css/app.css) used

## Architecture Overview

**SocOps** is a Blazor WebAssembly Bingo game with:
- 55 grid with win detection
- State persistence via localStorage
- Service-driven architecture (no component business logic)

### Key Patterns
- **Services** own state, expose `OnStateChanged` events
- **Components** subscribe to services, render UI, emit `EventCallback<T>`
- **Models** are simple POCOs in `Models/`

## Core Coding Conventions

### Services
```csharp
public class BingoGameService
{
    public event Action? OnStateChanged;
    private void NotifyStateChanged() => OnStateChanged?.Invoke();
    
    public void Mutate()
    {
        // ... change state
        _ = SaveGameStateAsync(); // Fire-and-forget non-critical async
        NotifyStateChanged();
    }
}
```

**Rules:**
- Register as `AddScoped` in [Program.cs](SocOps/Program.cs)
- Emit `OnStateChanged` after all mutations
- Use `_ = ...` for fire-and-forget async

### Components
```razor
@inject BingoGameService GameService
@implements IDisposable

@code {
    protected override void OnInitialized()
    {
        GameService.OnStateChanged += HandleStateChanged;
    }
    
    private void HandleStateChanged() => InvokeAsync(StateHasChanged);
    
    public void Dispose()
    {
        GameService.OnStateChanged -= HandleStateChanged; // REQUIRED
    }
}
```

**Rules:**
- Always unsubscribe in `Dispose()` to prevent leaks
- All `[Parameter]` properties need default values
- Use `EventCallback<T>` for child-to-parent communication
- Keep components small and single-purpose

### Parameters & Events
```razor
@code {
    [Parameter]
    public List<BingoSquareData> Board { get; set; } = new();
    
    [Parameter]
    public EventCallback<int> OnClick { get; set; }
}
```

## Quick Reference

### Adding Questions
Edit [Questions.cs](SocOps/Data/Questions.cs):
```csharp
public static readonly List<string> QuestionsList = new() { "new question", /* ... */ };
```

### Adding Components
1. Create in `Components/` directory
2. Inject services via `@inject`
3. Subscribe/unsubscribe to events
4. Use utility CSS classes

### Adding Services
1. Create in `Services/`
2. Add `public event Action? OnStateChanged`
3. Register: `builder.Services.AddScoped<YourService>()`

### JSInterop
```csharp
await _jsRuntime.InvokeVoidAsync("localStorage.setItem", key, value);
var result = await _jsRuntime.InvokeAsync<string>("localStorage.getItem", key);
```

### Styling
Use utilities from [app.css](SocOps/wwwroot/css/app.css):
- Layout: `flex`, `grid`, `grid-cols-5`, `gap-1`
- Spacing: `p-4`, `mb-2`, `mx-auto`
- Colors: `bg-accent`, `bg-marked`, `text-gray-700`
- Typography: `text-xl`, `font-semibold`

For component-specific styles, create `ComponentName.razor.css` (auto-scoped).

## Critical Anti-Patterns

 **Business logic in components**   Put in services  
 **Mutating parameters**   Emit `EventCallback`  
 **Missing `Dispose()`**   Always unsubscribe from events  
 **Inline styles**   Use utility classes  
 **Blocking JSInterop**   Always `await`  

## Project Structure
```
SocOps/
 Components/      # Reusable UI (BingoBoard, BingoSquare, etc.)
 Services/        # State & logic (BingoGameService, BingoLogicService)
 Models/          # POCOs (GameState, BingoSquareData, BingoLine)
 Data/            # Static data (Questions.cs)
 Pages/           # Routable pages
 wwwroot/         # CSS, static assets
```

## Running & Building
```bash
# Dev server (http://localhost:5166)
dotnet run --project SocOps/SocOps.csproj

# Build only
dotnet build SocOps/SocOps.csproj
```

## Key Files
- [Program.cs](SocOps/Program.cs) - DI setup
- [BingoGameService.cs](SocOps/Services/BingoGameService.cs) - Game state
- [BingoLogicService.cs](SocOps/Services/BingoLogicService.cs) - Win detection
- [Questions.cs](SocOps/Data/Questions.cs) - Game content

**Dependencies**: .NET 10 SDK, Blazor WebAssembly, Bootstrap
