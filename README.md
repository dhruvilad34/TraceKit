# TraceKit

> A structured workflow record, traceability, and state management platform.

[![Live Demo](https://dhruvilad34.github.io/TraceKit/)](https://dhruvilad34.github.io/TraceKit/)

---

## Table of Contents

- [Overview](#overview)
- [Live Demo](#live-demo)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [Sample Output](#sample-output)
- [What I Learned](#what-i-learned)
- [License](#license)

---

## Overview

TraceKit is a browser-based platform for designing and documenting structured multi-step process workflows. It allows users to build step-by-step process records, configure parameters at each stage, auto-generate traceability matrices, visualise resource state transitions, and export everything as structured JSON.

The project was built to demonstrate applied computing skills across workflow design, structured data modelling, state machine implementation, and AI-assisted tooling — all within a single self-contained web application with no dependencies or backend required.

---

## Live Demo

🔗 **[dhruvilad34.github.io/TraceKit](https://dhruvilad34.github.io/TraceKit/)**

> Open in any modern browser — no installation, no login required.

---

## Features

### 📋 Workflow Builder
- Visual operation palette with 12 configurable step types
- Each step type has tailored parameter input fields
- Reorder steps up and down within the workflow
- Free-text notes and remarks field per step
- Visual process flow with step connectors between cards

### 🔗 Traceability Matrix
- Automatically generated as you build your workflow
- Maps every step to a corresponding source document reference
- Status tracking per step — `verified`, `pending`, `requires review`
- Export as structured JSON with a single click

### ⚙️ Resource State Diagrams
- Auto-generated state transition diagrams based on active workflow steps
- Models valid state flows per resource type
- Reflects real-world state machine design patterns
- Example: `Idle → Setup → Running → Complete → Clean`

### 🤖 AI Parameter Assistant
- Powered by the Anthropic Claude API
- Describe any process step in plain language
- Receive structured, context-aware parameter suggestions instantly
- One-click to add AI-generated step directly into the workflow

### 📤 JSON Export
- Full workflow exported as clean structured JSON
- Includes step metadata, parameters, status flags, and verification requirements
- Ready for downstream processing or integration

---

## Tech Stack

| Category | Technology |
|---|---|
| Frontend | HTML5, CSS3, Vanilla JavaScript |
| AI Integration | Anthropic Claude API |
| Styling | CSS custom properties, CSS Grid, Flexbox |
| Theme | Light & dark mode (auto via `prefers-color-scheme`) |
| Deployment | GitHub Pages — single `.html` file, zero dependencies |

---

## Getting Started

### Prerequisites
- Any modern browser (Chrome, Firefox, Safari, Edge)
- No Node.js, no npm, no framework required

### Run Locally

```bash
# Clone the repository
git clone https://github.com/dhruvilad34/TraceKit.git

# Navigate into the folder
cd tracekit

# Option 1 — open the file directly
open index.html

# Option 2 — serve locally
npx serve .
# Then visit http://localhost:3000/index.html
```

### Deploy to GitHub Pages

```bash
git init
git add tracekit.html README.md
git commit -m "Initial release: TraceKit v1.0"
git remote add origin https://github.com/dhruvilad34/TraceKit.git
git push -u origin main
```

Then in your GitHub repository:
1. Go to **Settings → Pages**
2. Under **Source** select **Deploy from a branch**
3. Choose **main** branch, **/ (root)** folder
4. Click **Save**

Live at:
```
https://dhruvilad34.github.io/TraceKit/
```

---

## Project Structure

```
tracekit/
│
├── tracekit.html       # Complete single-file application (HTML + CSS + JS)
└── README.md           # Project documentation
```

> The entire application lives in one self-contained HTML file — no build step, no bundler, no external dependencies.

---

## How It Works

```
User selects operation type from palette
          ↓
Step card added to workflow canvas
          ↓
User fills in parameters and notes
          ↓
Traceability matrix auto-updates  ←─────────────────────┐
          ↓                                              │
Resource state diagrams auto-update                      │
          ↓                                   (live sync on every change)
AI assistant generates parameters (optional)             │
          ↓                                              │
Export full record as JSON ──────────────────────────────┘
```

---

## Sample Output

```json
{
  "document_type": "Workflow Record",
  "title": "Process Record 2024-001",
  "version": "1.0",
  "status": "draft",
  "generated_at": "2024-11-01T10:30:00.000Z",
  "steps": [
    {
      "step_number": 1,
      "step_id": "STEP-001",
      "operation_type": "Dispense",
      "description": "Initial material intake and verification",
      "parameters": {
        "quantity": "55.0 kg",
        "tolerance": "± 2.0%",
        "equipment": "Station A",
        "reference_id": "MAT-001"
      },
      "notes": "Requires second-person verification before proceeding.",
      "critical_step": true,
      "requires_double_check": true,
      "status": "draft"
    },
    {
      "step_number": 2,
      "step_id": "STEP-002",
      "operation_type": "Process",
      "description": "Primary processing stage",
      "parameters": {
        "speed": "250 rpm",
        "duration": "12 min",
        "endpoint": "32 kW",
        "equipment": "Unit 02"
      },
      "notes": "Monitor endpoint by power consumption.",
      "critical_step": true,
      "requires_double_check": false,
      "status": "draft"
    }
  ],
  "traceability_matrix": [
    {
      "step_number": 1,
      "source_reference": "DOC-§001",
      "status": "verified"
    },
    {
      "step_number": 2,
      "source_reference": "DOC-§002",
      "status": "pending"
    }
  ]
}
```

---

## What I Learned

Building TraceKit strengthened my skills across several areas:

- **Frontend architecture** — structuring a complex, stateful single-page application without a framework using vanilla JavaScript and modular render functions
- **State machine design** — modelling resource state transitions and implementing them as visual diagrams driven by user-defined workflow data
- **AI API integration** — working with the Anthropic Claude API to parse structured outputs from natural language prompts and inject them into application state
- **Data modelling** — designing a flexible JSON schema that captures workflow steps, parameters, traceability links, and metadata in a consistent exportable structure
- **UX design** — building an interface that guides users through a complex multi-step process while remaining simple and intuitive

---
