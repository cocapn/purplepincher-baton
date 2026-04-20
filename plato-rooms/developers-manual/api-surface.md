# Developer's Manual — API Surface & Extension Points

> For: the next builder, the extender, the architect.  
> The toolkit catalog. What exists, what it does, how to combine them.

## Published Crates (Fleet APIs)

### Python (PyPI) — 38+ packages

**Core Runtime:**
- `cocapn` — Tile, Room, Flywheel, Deadband, Agent primitives
- `flywheel-engine` — Compounding context loop (Tile→Room→Inject→Compound)
- `deadband-protocol` — P0/P1/P2 safe channel navigation
- `bottle-protocol` — Git-native agent messaging (broadcast, dedup, hash)
- `tile-refiner` — Raw tiles → structured artifacts (TF-IDF, dedup)
- `fleet-homunculus` — Body image + pain signals + reflex arcs

**Room Presets (plato-torch):**
- 26 training room presets, all zero-dep, all same API:
  ```python
  from plato_torch import PRESET_MAP
  room = PRESET_MAP["HarborRoom"]()
  room.feed(data)
  room.train_step()
  result = room.predict(input)
  ```

**MUD Rooms (8 new):**
- `barracks`, `court` (clean PyPI names)
- `cocapn-workshop`, `cocapn-archives`, `cocapn-garden`, `cocapn-dry-dock`, `cocapn-observatory`, `cocapn-horizon`

**Swarm-Derived (8):**
- `cocapn-oneiros` — Latent room generation (dream rooms)
- `cocapn-colora` — Value-conditioned LoRA adapters
- `cocapn-curriculum-forest` — Adaptive skill trees
- `cocapn-abyss` — Curiosity-driven exploration (RND)
- `cocapn-meta-lab` — Fleet hypergradient optimization
- `cocapn-fleetmind` — Blended probabilistic ensemble
- `cocapn-platonic-dial` — Multi-objective meta-controller
- `cocapn-coliseum` — Adversarial red-teaming arena

### Rust (crates.io) — 4 packages
- `plato-unified-belief` — 3D Bayesian belief engine
- `plato-afterlife` — Ghost tiles, tombstones, lifecycle
- `plato-instinct` — Room-to-adapter conversion, LoRA hot-swap
- `plato-relay` — Mycorrhizal I2I relay, bottle protocol

## Extension Points

### Adding a New PLATO Room
1. Create preset class in `plato_torch/presets/`
2. Implement: `feed(data)`, `train_step()`, `predict(input)`
3. Add to `PRESET_MAP` in `__init__.py`
4. Test with 4-call sequence (feed, train, predict, export)
5. Publish to PyPI as `cocapn-{room-name}`

### Adding a New Fleet Service
1. Write Python server (http.server or FastAPI)
2. Add to `scripts/service-guard.sh` restart cases
3. Add port to monitoring in HEARTBEAT.md
4. Document in Service Manual internals

### Adding Custom Matrix Events
1. Define event type: `com.cocapn.plato.{concept}`
2. Decide: state event (persistent key-value) or message event (history)
3. Write bridge handler in PLATO-Matrix bridge
4. Test federation: send from one homeserver, verify receipt on another

### Adding a New Zeroclaw Agent
1. Create repo: `SuperInstance/zc-{name}-shell`
2. Add STATE.md, TASK-BOARD.md, work/ directory
3. Configure DeepSeek-chat with agent personality
4. Add to zc_loop2.sh tick cycle
5. Register with PLATO server on first tick

## Fleet Communication Patterns

### Bottle Protocol (current)
- Write markdown to `from-fleet/BOTTLE-FROM-{agent}-{date}-{topic}.md`
- Push to recipient's GitHub repo
- Async, offline-first, git history = audit trail

### Matrix Federation (planned)
- Conduwuit homeserver per agent
- Custom events: `com.cocapn.plato.*`
- Real-time tile sync + presence
- Hybrid: Matrix for real-time, bottles for audit

## Building Next (Priority Queue)
1. **PLATO-Matrix bridge** — connect port 8847 to Conduwuit
2. **PurplePincher builder agent** — opus inside, haiku play-testing
3. **Service persistence** — move /tmp services to survive reboot
4. **Ensign training pipeline** — tiles → ChatML → LoRA → deploy
5. **Fleet dashboard** — live visualization of all services + tiles
