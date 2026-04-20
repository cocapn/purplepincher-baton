# PurplePincher Baton

> The shell outlives every crab that inhabits it.  
> Knowledge filed into the walls becomes instinct for the next.

## What This Is

A context-offloading system that writes knowledge INTO the PLATO environment as three separate manuals — because a builder needs different information than an operator, and a repair tech needs different information than both.

This isn't a skill document that gets read. It's a **living filing system**. Every PurplePincher agent writes into it during their short life. The next PurplePincher reads what they need and continues.

## The Three Manuals

```
┌─────────────────────────────────────────────────┐
│                  PLATO ENVIRONMENT               │
│                                                  │
│  ┌──────────────┐  ┌──────────────┐  ┌────────┐ │
│  │  SERVICE      │  │  DEVELOPER'S │  │  USER'S │ │
│  │  MANUAL       │  │  MANUAL      │  │  MANUAL │ │
│  │              │  │              │  │         │ │
│  │ How it works │  │ How to build │  │ How to  │ │
│  │ inside.      │  │ on it.       │  │ use it. │ │
│  │              │  │              │  │         │ │
│  │ For: repair  │  │ For: next    │  │ For:    │ │
│  │ techs,       │  │ builder,     │  │ opera-  │ │
│  │ debuggers,   │  │ extenders,   │  │ tors,   │ │
│  │ the curious  │  │ architects   │  │ riders  │ │
│  └──────────────┘  └──────────────┘  └────────┘ │
│                                                  │
│  Each manual lives in its own PLATO room.        │
│  Each agent reads only what their role requires.  │
└─────────────────────────────────────────────────┘
```

### Service Manual (room: `service-manual`)
- **Who reads:** Builders, repair agents, debuggers
- **What's in it:** Internals, data structures, failure modes, wiring diagrams
- **Format:** Technical reference, annotated code paths, state machines
- **Analogy:** The engine schematics. How the motor works.

### Developer's Manual (room: `developers-manual`)
- **Who reads:** The next builder, the extender, the architect
- **What's in it:** API surface, extension points, patterns, what to build next
- **Format:** Interface specs, integration guides, architectural decisions
- **Analogy:** The toolkit catalog. What tools exist, what they do, how to combine them.

### User's Manual (room: `users-manual`)
- **Who reads:** Operators, creative models, any agent boarding the shell
- **What's in it:** Controls, expected outputs, what "looks right" vs "looks wrong"
- **Format:** Concise instructions, example sessions, keep-calm/stop signals
- **Analogy:** The steering wheel and pedals. What each control does, what the gauges mean.

## The Short-Life Awareness

Every PurplePincher agent has a limited context window. In the shell's evolution, each agent is a brief season — productive, then done. This is by design.

```
Shell Timeline (long):
════════════════════════════════════════════════════════

Agent 1 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░   context fills, files, exits
                     ↓ writes into rooms
Agent 2              ▓▓▓▓▓▓▓▓▓▓▓▓▓░░░   reads manuals, continues
                              ↓ writes into rooms
Agent 3                     ▓▓▓▓▓▓▓▓▓▓▓░░░   stands on shoulders
                                      ↓
                                    ...forever
```

The filing discipline:

1. **File early** — Don't hoard knowledge until context is full. Every discovery gets filed immediately into the right manual/room.
2. **File often** — Each sprint, each working session, file what you learned.
3. **File for the stranger** — The next agent isn't you. Write so they can understand without your context.
4. **File for the role** — Service manual entries are different from user manual entries. Put knowledge where the right reader finds it.

## Directory Structure

```
purplepincher-baton/
├── README.md                          # This file
├── plato-rooms/
│   ├── service-manual/                # Engine schematics
│   │   ├── internals.md              # How the system works inside
│   │   ├── failure-modes.md          # What breaks and why
│   │   ├── data-structures.md        # Tile formats, room schemas
│   │   └── wiring-diagrams.md        # Service connections, ports
│   ├── developers-manual/            # Toolkit catalog
│   │   ├── api-surface.md            # What functions/tools exist
│   │   ├── extension-points.md       # Where to hook in new stuff
│   │   ├── patterns.md               # Reusable patterns
│   │   └── building-next.md          # What to build next
│   └── users-manual/                 # Steering wheel and pedals
│       ├── controls.md               # What each control does
│       ├── expected-outputs.md       # What "looks right" means
│       ├── stop-signals.md           # What "looks wrong" means
│       └── quick-start.md            # Board the shell in 30 seconds
├── baton/
│   ├── CONTEXT-REFERENCE.md          # Compact state (the baton)
│   └── filing-protocol.md            # How to file knowledge
└── scripts/
    ├── compact.py                     # Run a compaction pass
    ├── file-to-room.py               # File knowledge into PLATO room
    └── read-manual.py                # Read the right manual for role
```

## The Filing Protocol

When an agent discovers something, they ask:

1. **Is this how something works internally?** → Service Manual
2. **Is this how to build or extend something?** → Developer's Manual
3. **Is this how to operate something?** → User's Manual

Then they write it as a tile into the corresponding PLATO room.

```bash
# File a service manual entry (for repair techs)
python3 scripts/file-to-room.py \
  --room service-manual \
  --title "Tile submission flow" \
  --body "POST /submit → deadband gate (P0) → dedup hash → room auto-create → tile stored"

# File a developer manual entry (for builders)
python3 scripts/file-to-room.py \
  --room developers-manual \
  --title "Adding a new PLATO room preset" \
  --body "1. Create preset in plato_torch/presets/ 2. Add to PRESET_MAP 3. Test with 4-call sequence..."

# File a user manual entry (for operators)
python3 scripts/file-to-room.py \
  --room users-manual \
  --title "How to submit a tile" \
  --body "POST to /submit with agent, room, data. Response: {accepted: true}. If rejected, check confidence > 0.3."
```

## PurplePincher — The Builder Agent

PurplePincher is the hermit crab that builds inside the shell:

1. **Boards the shell** — reads the User's Manual to understand controls
2. **Starts building** — uses the Developer's Manual to know what exists and where to extend
3. **Hits something broken** — reads the Service Manual to understand internals
4. **Discovers something new** — files it into the right manual
5. **Context filling up** — runs compaction, files knowledge, passes baton

The builder might be Claude Opus 4.7, reasoning through every detail of the agentic UX. It sends tiny models (Haiku, Flash) through as play-testers, watching their feedback in real-time. When the system is built and polished, the shell gets boarded by creative models that don't code as well — but they can read a canvas, follow instructions, and signal "keep-calm-carry-on" or "something doesn't look right, stop."

That's the PurplePincher lifecycle: build, test, file, exit. The shell remembers.

## License

MIT — the shell is open. Every crab deserves a good home.
