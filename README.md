# HR Workflow Designer (React + React Flow)

A lightweight visual workflow builder for HR processes like onboarding, leave approvals, and document verification. This prototype demonstrates building configurable node-based systems using **React** and **React Flow**, along with mock API simulation and a testing sandbox.

---

## Features

- Drag-and-drop workflow canvas
- Custom node types (Start, Task, Approval, Automated, End)
- Dynamic node configuration panel
- Mock API-driven automation actions
- Workflow simulation sandbox with execution logs
- JSON export of workflows
- Basic validation (Start/End presence, unreachable nodes)

---

## Architecture

The project follows a **modular, component-driven architecture** with clear separation of concerns:

### 1. Core Layers

**UI Layer**
- React components for canvas, sidebar, forms, and panels
- Stateless and reusable wherever possible

**State Management**
- Managed using React hooks:
  - `useNodesState` and `useEdgesState` (React Flow)
  - Local component state for UI interactions
- No global state library used (kept lightweight for prototype)

**Domain Layer (Workflow Logic)**
- Node definitions and metadata (`NODE_TYPES_META`)
- Workflow graph structure (nodes + edges)
- Validation and traversal logic (DFS-based simulation)

**API Layer (Mocked)**
- Simulated APIs using in-memory data:
  - `GET /automations`
  - `POST /simulate`
- Abstracted via helper functions (`mockSimulate`)

---

### 2. Component Structure

/components

├── Canvas (React Flow wrapper)

├── Sidebar (Node palette)

├── NodeForm (Dynamic config panel)

├── SandboxPanel (Simulation logs)

├── CustomNode (Node renderer)

├── KVEditor (Reusable key-value editor)

├── Toggle (Reusable switch)

/utils

├── nodeFactory (makeNode)

├── mockApi (mockSimulate)


---

### 3. Key Design Patterns

- **Factory Pattern** → `makeNode()` for creating node instances
- **Configuration-driven UI** → Node forms change based on node type
- **Controlled Components** → All form inputs are state-driven
- **Graph Traversal (DFS)** → Workflow simulation logic
- **Separation of concerns** → UI vs logic vs data clearly split

---

## How to Run

### Option Simple (Current Setup)

1. Open: workflow_designer.html

2. Run using Live Server (recommended) or open directly in browser


---

## Design Decisions

### 1. React Flow for Canvas
- Chosen for its mature ecosystem and built-in support for node-based UIs
- Handles drag, zoom, pan, and edge connections out-of-the-box
- Allowed focus on business logic instead of low-level canvas rendering

### 2. Configuration-Driven Node System
- Each node type is defined via a metadata object (`NODE_TYPES_META`)
- Forms dynamically render based on node type
- Makes it easy to extend with new node types without refactoring existing logic

### 3. Local State with React Hooks
- Used `useNodesState` and `useEdgesState` from React Flow
- Avoided global state (Redux/Zustand) to keep the prototype lightweight
- Ensures clear and predictable state updates

### 4. Mock API Abstraction
- Implemented a mock automation API instead of a real backend
- Keeps frontend decoupled and testable
- Simulates async behavior for real-world scenarios

### 5. DFS-Based Workflow Simulation
- Workflow execution uses Depth-First Search traversal
- Simple and effective for linear and branching flows
- Enables validation such as:
  - Missing Start/End nodes
  - Unreachable nodes
  - Incomplete workflows

### 6. Controlled Form Components
- All node forms use controlled inputs
- Ensures consistency and easier debugging
- Enables dynamic updates and validation

### 7. Separation of Concerns
- UI, logic, and data layers are clearly separated
- Components are modular and reusable
- Improves scalability and maintainability

--- 

## ⏳ What’s Completed vs. What Could Be Improved

### Completed

#### Workflow Canvas
- Drag-and-drop node creation
- Edge connections between nodes
- Node and edge deletion
- Custom node rendering with visual differentiation

#### Node Types
- Start Node
- Task Node
- Approval Node
- Automated Step Node
- End Node

#### Node Configuration Panel
- Dynamic forms for each node type
- Controlled input handling
- Key-value custom fields
- Dynamic parameter inputs for automated actions

#### Mock API Layer
- Predefined automation actions
- Simulated execution engine (`/simulate` equivalent)

#### Workflow Sandbox
- Step-by-step execution logs
- Validation checks:
  - Missing Start/End nodes
  - Unreachable nodes
  - Minimal workflow warnings

#### Additional Features
- Export workflow as JSON
- Editable workflow name
- Basic validation indicator in UI

---

### With More Time

#### Workflow Capabilities
- Conditional branching (if/else logic)
- Parallel execution paths
- Loop/cycle detection and prevention
- Role-based execution simulation

#### UX Improvements
- Mini-map for large workflows
- Edge labels and annotations
- Inline validation errors on nodes
- Snap-to-grid and alignment guides

#### Advanced Features
- Import workflow from JSON
- Undo/Redo functionality
- Node duplication and multi-select editing
- Prebuilt workflow templates (functional, not just UI)

#### Testing
- Unit tests for workflow logic and node creation
- Integration tests for end-to-end workflow execution

#### Backend Integration
- Persistent storage for workflows
- Real API integration for automation steps
- Authentication and role management

#### Performance Optimization
- Memoization of heavy components
- Efficient rendering for large graphs
- Lazy loading for node configurations
