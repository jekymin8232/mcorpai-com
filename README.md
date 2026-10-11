## 1. Architectural Philosophy: Why This Design?

Modern game development heavily relies on commercial engines such as Unity or Unreal. However, this project was architected to demonstrate **full engineering control over a zero-dependency system and deterministic numerical state management**

* **Zero External Dependencies**: The engine, rules, state machine, rendering pipeline, and narrative assets are fully encapsulated within a single HTML file. It requires no build tools, web servers, or external libraries, running instantaneously on any modern browser
* **Deterministic State Control**: The engine replaces non-deterministic random functions (`Math.random`) with seed-based PRNG algorithms (`sfc32`), ensuring 100% reproducible state simulation.
* **System as Narrative**: Instead of forcing narrative through visual cutscenes, player choices are dynamically constrained by a 'Tunneling' algorithm based on physical and psychological stats (`hun`, `hp`, `se`, `ho`)

---

## 2. Core Architecture

The engine is written in pure Vanilla JavaScript and follows a strict separation of concerns across core modules.

### `HS_Core` (Engine Foundation & Storage)
* Encapsulates `localStorage` access with defensive fail-closed error handling against browser quota limits or blocked access.
* Parses and loads modular JSON data packs embedded in `<script type="application/json" data-hs-pack>` elements.
* Manages independent PRNG streams generated via FNV-1a hash functions and `sfc32` algorithms.

### `HS_Rules` (Pure Rule Simulation)
* Implemented entirely as pure functions without side effects, accepting state and inputs to return updated state objects.
* Evaluates resource decay, weather/luck plans, chain losses, and critical threshold conditions for state transitions.
* Guarantees testability and state rollback capabilities through immutable state evaluation.

### `HS_Flow` (Session & Scene Management)
* Orchestrates execution flow between `HS_Rules` and the rendering layer.
* Tracks scene transition histories, handles branching narrative logic, and manages multi-language string interpolation.

---

## 3. Technical Systems

### Cognitive Tunneling Mechanism
* As player stats drop, high-tier choices become unreachable (`dim`), simulating real-world cognitive narrowing under extreme scarcity.

### Data-Driven Modular Design
* World configurations, calendars, weather tables, and narrative units are serialized into declarative JSON packs (`data-hs-pack`).
* Systems and narrative content remain decoupled, allowing logic modifications without altering core engine scripts.

### SVG Vector Graphics Pipeline
* Visuals are generated dynamically using XML-based Scalable Vector Graphics (SVG), eliminating raster image assets.
* Renders crisp silhouettes across all screen resolutions while maintaining a minimal memory footprint.

---

## 4. Execution

* **Zero Installation**: Open the single `.html` file directly in any modern web browser.
