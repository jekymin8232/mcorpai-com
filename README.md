# Homeless Survivor

> "The more abundance fills everything, the more clearly we come face to face with the loneliness and lack within us."[cite: 1, 2]

In a future where AI architecture and system control take precedence, this project is a simulation engine implemented using web standard technologies as a deterministic state machine with a numerical model operating under complex constraints within a single-file environment[cite: 1, 2].

---

## 1. Architectural Philosophy: Why This Design?

Modern game development heavily relies on commercial engines such as Unity or Unreal. However, this project was architected to demonstrate **full engineering control over a zero-dependency system and deterministic numerical state management**[cite: 1, 2].

* **Zero External Dependencies**: The engine, rules, state machine, rendering pipeline, and narrative assets are fully encapsulated within a single HTML file[cite: 1, 2]. It requires no build tools, web servers, or external libraries, running instantaneously on any modern browser[cite: 1, 2].
* **Deterministic State Control**: The engine replaces non-deterministic random functions (`Math.random`) with seed-based PRNG algorithms (`sfc32`), ensuring 100% reproducible state simulation[cite: 1, 2].
* **System as Narrative**: Instead of forcing narrative through visual cutscenes, player choices are dynamically constrained by a 'Tunneling' algorithm based on physical and psychological stats (`hun`, `hp`, `se`, `ho`)[cite: 1, 2].

---

## 2. Core Architecture

The engine is written in pure Vanilla JavaScript and follows a strict separation of concerns across core modules[cite: 1, 2].

### `HS_Core` (Engine Foundation & Storage)
* Encapsulates `localStorage` access with defensive fail-closed error handling against browser quota limits or blocked access[cite: 1, 2].
* Parses and loads modular JSON data packs embedded in `<script type="application/json" data-hs-pack>` elements[cite: 1, 2].
* Manages independent PRNG streams generated via FNV-1a hash functions and `sfc32` algorithms[cite: 1, 2].

### `HS_Rules` (Pure Rule Simulation)
* Implemented entirely as pure functions without side effects, accepting state and inputs to return updated state objects[cite: 1, 2].
* Evaluates resource decay, weather/luck plans, chain losses, and critical threshold conditions for state transitions[cite: 1, 2].
* Guarantees testability and state rollback capabilities through immutable state evaluation[cite: 1, 2].

### `HS_Flow` (Session & Scene Management)
* Orchestrates execution flow between `HS_Rules` and the rendering layer[cite: 1, 2].
* Tracks scene transition histories, handles branching narrative logic, and manages multi-language string interpolation[cite: 1, 2].

---

## 3. Technical Systems

### Cognitive Tunneling Mechanism
* As player stats drop, high-tier choices become unreachable (`dim`), simulating real-world cognitive narrowing under extreme scarcity[cite: 1, 2].

### Data-Driven Modular Design
* World configurations, calendars, weather tables, and narrative units are serialized into declarative JSON packs (`data-hs-pack`)[cite: 1, 2].
* Systems and narrative content remain decoupled, allowing logic modifications without altering core engine scripts[cite: 1, 2].

### SVG Vector Graphics Pipeline
* Visuals are generated dynamically using XML-based Scalable Vector Graphics (SVG), eliminating raster image assets[cite: 1, 2].
* Renders crisp silhouettes across all screen resolutions while maintaining a minimal memory footprint[cite: 1, 2].

---

## 4. Execution

* **Zero Installation**: Open the single `.html` file directly in any modern web browser[cite: 1, 2].
