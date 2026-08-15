# AshifForm Pro 🌾🔬
> **Professional Desktop Application for Livestock Feed Formulation & Least-Cost Optimization**

Built with **Electron**, **React 19**, **TypeScript**, **Vite**, **Tailwind CSS**, **Prisma ORM**, and **SQLite 3**.

---

## 📋 Architecture & Foundation Overview

AshifForm Pro is an offline-first desktop platform engineered for animal nutritionists, feed mill operators, and livestock farm managers. It delivers least-cost feed formulation using linear programming, comprehensive raw material ingredient matrixes, species nutritional requirements, and inventory control.

```
┌─────────────────────────────────────────────────────────────┐
│                      AshifForm Pro                          │
│                   Desktop Application                       │
└──────────────────────────────┬──────────────────────────────┘
                               │
       ┌───────────────────────┴───────────────────────┐
       ▼                                               ▼
┌──────────────────────────────┐        ┌──────────────────────────────┐
│       Electron Main          │        │      Chromium Renderer       │
│  (Node.js / SQLite / IPC)    │        │    (React 19 + TypeScript)   │
│  • Window management         │◄──────►│  • TitleBar & Windows Frame  │
│  • Prisma ORM Bridge         │ (Safe  │  • Collapsible Sidebar       │
│  • Context Isolation         │  IPC)  │  • Interactive Dashboard     │
│  • Sandboxed Native API      │        │  • Dark / Light Theme Engine │
└──────────────┬───────────────┘        └──────────────────────────────┘
               │
               ▼
┌──────────────────────────────┐
│       SQLite 3 Database      │
│  (17 Normalized Models)      │
│  • Formulas & Ingredients    │
│  • LP Optimization Logs      │
│  • Animal Growth Stages      │
│  • Offline Sync Queue        │
└──────────────────────────────┘
```

---

## 🚀 Getting Started

### 1. Prerequisites
- **Node.js**: v18.0+ or v20.0+ (LTS recommended)
- **npm**: v9.0+ or **pnpm** / **yarn**

### 2. Installation

Clone the repository and install dependencies:
```bash
git clone https://github.com/your-org/ashifform-pro.git
cd ashifform-pro
npm install
```

### 3. Database Initialization (Prisma + SQLite)

Initialize the SQLite database and generate the Prisma Client:
```bash
# Generate the strongly typed Prisma client
npm run prisma:generate

# Apply migrations to create the local SQLite database
npm run prisma:migrate
```

---

## 💻 Development Commands

| Command | Description |
| :--- | :--- |
| `npm run dev` | Starts the Vite development server with HMR on port 3000 |
| `npm run dev:electron` | Boots the Vite development server and launches the native Electron window |
| `npm run typecheck` | Runs strict TypeScript type checking (`tsc --noEmit`) |
| `npm run lint` | Lints the codebase for syntax, imports, and style consistency |
| `npm run build` | Compiles the React web application and bundles Electron main/preload scripts |
| `npm run build:win` | Packages the application into a Windows `.exe` installer (NSIS & Portable) |
| `npm run prisma:generate` | Generates TypeScript types from `prisma/schema.prisma` |
| `npm run prisma:migrate` | Runs database migrations on the local SQLite database |

---

## 📦 Packaging for Windows (.exe)

The packaging pipeline is configured with **electron-builder**:

```bash
# Build the production bundle and generate Windows binaries
npm run build:win
```

### Output Artifacts (located in `./release`):
1. **NSIS Installer**: `AshifForm Pro-Setup-1.0.0-x64.exe` (with customizable install directory and desktop shortcuts)
2. **Portable Executable**: `AshifForm Pro-1.0.0-x64.exe` (single standalone binary requiring no installation)

Configuration is managed in `electron-builder.json5`.

---

## 🛡️ Security Architecture

AshifForm Pro strictly adheres to Electron security best practices:

- **Context Isolation**: `contextIsolation: true` separates the renderer context from preload scripts.
- **Node Integration Disabled**: `nodeIntegration: false` prevents malicious script injection from accessing native Node.js APIs.
- **Sandboxing**: `sandbox: true` runs the Chromium renderer in an OS-level sandbox.
- **Strict Preload Bridge**: Native APIs (window controls, SQLite database actions, system metrics) are selectively exposed via `contextBridge.exposeInMainWorld('electronAPI', {...})`.
- **Navigation Guard**: Outbound URLs are automatically routed to the user's default OS browser.

---

## 🗄️ Relational Database Schema (Prisma)

The foundation includes 17 database models tailored for livestock feed formulation:

1. `User` & `Role` — Granular Role-Based Access Control (RBAC).
2. `NutrientCategory` & `Nutrient` — Energy, Amino Acids, Minerals, and Vitamins.
3. `IngredientCategory` & `Ingredient` — Raw material feedstuffs catalog with Dry Matter % and costs.
4. `IngredientNutrient` — Chemical nutrient matrix per ingredient.
5. `Species` & `ProductionStage` — Poultry, Swine, Dairy, Beef & Aqua growth profiles.
6. `NutrientRequirement` — Min/Max/Optimal bounds for formulation constraints.
7. `FeedFormula` & `FormulaIngredient` — Multi-species recipes and batch weights.
8. `OptimizationLog` — Linear programming iterations, shadow prices, and slack tolerances.
9. `Warehouse` & `InventoryItem` — Batch tracking, stock balances, and reorder points.
10. `Supplier` & `PurchaseOrder` — Procurement orders and goods receipt.
11. `SyncLog` & `AuditLog` — Offline transaction log and audit trail.
12. `AppSetting` — User preferences and unit system configurations.

---

## 🗺️ Modular Extension Roadmap

The architecture is structured for sequential development of the remaining modules:

- [ ] **1. Authentication & User Roles (RBAC)**
- [ ] **2. Live Milling Dashboard & KPIs**
- [ ] **3. Nutrient Matrix & Chemical Library**
- [ ] **4. Ingredient Catalog & Cost Manager**
- [ ] **5. Animal Requirements & Phase Feeding**
- [ ] **6. Feed Formulation Studio & Mix Sheets**
- [ ] **7. Least-Cost Linear Programming (Simplex Solver)**
- [ ] **8. Warehouse & FIFO Inventory Tracking**
- [ ] **9. Purchasing & Supplier PO Management**
- [ ] **10. Reports, Certificates & Delta Sync Engine**

---

## 📄 License
Commercial proprietary license. All rights reserved.
