# 🎯 Soc Ops — Social Bingo

> **Break the ice, spark conversations, and make lasting connections!**

Soc Ops is an interactive social bingo game perfect for in-person mixers, team events, and networking sessions. Find people who match the prompts, mark your card, and race to get 5 in a row! Built with Blazor WebAssembly for a seamless mobile-first experience.

🎮 **[Play the Game](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/)** • 📚 **[View Lab Guide](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/)**

---

## ✨ Features

- 🎲 **Randomized boards** — Every player gets a unique arrangement of prompts
- 💾 **Auto-save progress** — Game state persists in localStorage; pick up where you left off
- 🏆 **Smart win detection** — Automatic bingo detection for rows, columns, and diagonals
- 🎉 **Victory celebrations** — Delightful modal with confetti when you win
- 📱 **Mobile-optimized** — Responsive design that works great on phones at events
- ⚡ **Blazing fast** — Powered by Blazor WebAssembly for instant interactions

---

## 🚀 Quick Start

### Prerequisites
- [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) or higher

### Run Locally
```bash
cd SocOps
dotnet run
# Open http://localhost:5166 in your browser
```

### Build
```bash
cd SocOps
dotnet build
```

---

## 🎨 Customize Your Game

### Change Questions
Personalize the game for your event by editing `SocOps/Data/Questions.cs`:

```csharp
public static readonly List<string> QuestionsList = new()
{
    "has a pet",
    "speaks more than 2 languages",
    "your custom icebreaker question here",
    // ... add 24+ questions for a full board
};
```

### Workshop Experience
This project is part of a hands-on workshop for learning GitHub Copilot agents. Follow the complete [Lab Guide](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/) or explore offline in the [`.lab/`](.lab/) folder.

---

## 🛠️ Tech Stack

- **Framework**: Blazor WebAssembly (.NET 10)
- **Styling**: Custom CSS utilities (Tailwind-inspired)
- **State Management**: Scoped services with localStorage persistence
- **Deployment**: GitHub Pages via GitHub Actions

---

## 📁 Project Structure

```
SocOps/
├── Components/     # Reusable UI components (BingoBoard, BingoSquare, Modals)
├── Models/         # Game state and data models
├── Services/       # Game logic and state management services
├── Data/           # Question bank and static data
├── Pages/          # Blazor pages (Home, etc.)
└── wwwroot/        # Static assets and CSS
```

---

## 🚢 Deployment

The game automatically deploys to GitHub Pages when you push to `main`:
- **Live URL**: `https://{your-username}.github.io/{repo-name}`
- **Setup**: Enable GitHub Pages in repository Settings > Pages > GitHub Actions

---

## 📚 Lab Guide

This repository includes a comprehensive lab for learning GitHub Copilot agents:

| Part | Title |
|------|-------|
| [**00**](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=00-overview) | Overview & Checklist |
| [**01**](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=01-setup) | Setup & Context Engineering |
| [**02**](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=02-design) | Design-First Frontend |
| [**03**](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=03-quiz-master) | Custom Quiz Master |
| [**04**](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=04-multi-agent) | Multi-Agent Development |

---

## 📝 License

MIT License — Feel free to use this for your next event, conference, or team gathering!
