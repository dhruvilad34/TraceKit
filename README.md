# PharmaTrace

**Pharmaceutical Batch Record & Traceability Platform**

A browser-based tool that simulates the core workflow of pharmaceutical Manufacturing Execution Systems (MES) including electronic batch record design, traceability matrix generation, equipment state management, and AI-assisted GMP parameter generation.

## Overview

PharmaTrace was built to demonstrate hands-on understanding of pharmaceutical manufacturing processes, GMP documentation standards, and MES architecture specifically the workflows used in systems like Werum PAS-X. It mirrors real responsibilities in pharmaceutical process engineering and MES recipe design roles.

## Features

### Recipe Builder
- Drag-and-drop style operation palette with 12 pharmaceutical unit operations (Dispense, Mix/Blend, Granulate, Dry, Mill, Lubricate, Compress, Coat, IPC Inspect, Pack/Label, Hold/Wait, Sample/QC)
- GMP-relevant parameter fields specific to each operation type (e.g. impeller speed, LOD target, tablet hardness, inlet temperature)
- Step reordering (move up / move down)
- Free-text GMP remarks and operator instruction fields
- Visual process flow with step connectors

### Traceability Matrix
- Auto-generated traceability matrix mapping electronic MBR steps to Paper Master Formula reference sections (`MF-§001`, `MF-§002`, …)
- Status tracking: `verified`, `requires review`, `pending`
- Highlights critical steps requiring double-person verification
- Exportable as structured JSON

### Equipment State Diagrams (ESP)
- Auto-generated equipment state diagrams based on operations in the active recipe
- State transition flows per equipment type (e.g. Idle → CIP → Ready → Running → Cleaning for granulators)
- Reflects real pharmaceutical shop floor state machine design

### AI Parameter Assistant
- Powered by Claude (Anthropic API)
- Describe a manufacturing step in plain language → receive GMP-compliant parameter suggestions
- Automatically parses AI output and populates a new step card in the recipe
- Supports any unit operation type

### JSON Export
- Exports full Master Batch Record in structured JSON format compatible with Werum PAS-X data models
- Exports Traceability Matrix as a separate JSON document
- Includes product metadata, batch information, critical step flags, and double-check requirements

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript (no framework) |
| AI Integration | Anthropic Claude API (`claude-sonnet-4-20250514`) |
| Styling | CSS custom properties, responsive grid layout, dark mode support |
| Export | JSON (browser `navigator.clipboard`) |
| Deployment | Single `.html` file — runs in any modern browser |

## Getting Started

### Run locally
No installation required. Simply open `pharmatrace.html` in any modern browser:

```bash
# Option 1: double-click the file in your file explorer

# Option 2: serve locally (optional, for API calls)
npx serve .
# then open http://localhost:3000/pharmatrace.html
```

### Deploy to GitHub Pages
```bash
git init
git add pharmatrace.html README.md
git commit -m "Initial release"
git remote add origin https://github.com/dhruvilad34/pharmatrace.git
git push -u origin main
```
Then go to **Settings → Pages → Deploy from branch → main** in your GitHub repo.

Your app will be live at:
```
https://dhruvilad34.github.io/PharmaTrace/
```

## Project Structure

```
pharmatrace/
├── pharmatrace.html      # Complete single-file application
└── README.md             # This file
```

---

## Pharmaceutical Domain Coverage

This project demonstrates practical knowledge of:

| Domain | Coverage |
|---|---|
| MES Architecture | Recipe design, master batch records, parameter value lists |
| GMP Documentation | Electronic batch records, traceability matrices, change control |
| Process Control | Equipment state diagrams, critical process parameters |
| Unit Operations | Wet granulation, fluid bed drying, tablet compression, film coating |
| Data Standards | Structured JSON export compatible with Werum PAS-X data models |
| Quality Systems | IPC (In-Process Control), double-check requirements, CoA verification |

## Sample Workflow

1. Open `pharmatrace.html` in your browser
2. Enter a Master Batch Record title (e.g. `Metformin HCl 500mg Tablets – MBR-2024-001`)
3. Click operations in the left sidebar to build your recipe step by step
4. Fill in GMP parameters for each step (equipment, speeds, temperatures, targets)
5. Switch to the **Traceability** tab to see the auto-generated matrix
6. Switch to **Equipment States** to review state diagrams for your equipment
7. Use the **AI Parameter Assistant** (right panel) to generate parameters from a text description
8. Click **Export MBR JSON** to download the structured batch record

## Example Output (JSON Snippet)

```json
{
  "document_type": "Master Batch Record",
  "system": "PharmaTrace v1.0",
  "mbr_title": "Metformin HCl 500mg Tablets – MBR-2024-001",
  "mbr_version": "1.0",
  "status": "draft",
  "product": {
    "name": "Metformin HCl",
    "strength": "500mg",
    "dosage_form": "Film-coated tablet"
  },
  "steps": [
    {
      "step_number": 1,
      "step_id": "STEP-001",
      "operation_type": "Dispense",
      "description": "Dispense Metformin HCl API",
      "parameters": {
        "mat_id": "MET-001 / SAP-88210",
        "qty": "55.0",
        "tol": "± 2.0",
        "equip": "Dispensing Booth A"
      },
      "critical_step": true,
      "requires_double_check": true
    }
  ]
}
```

---

## License

MIT License — free to use, modify, and distribute.
