# Filing Protocol

> How to file knowledge into the three manuals.  
> Every discovery goes somewhere. The next agent needs it.

## The Three-Way Split

When you learn something, ask ONE question:

**Who needs to know this?**

| If the reader needs to... | File in | Room |
|--------------------------|---------|------|
| Understand internals, debug, repair | Service Manual | service-manual |
| Build on top, extend, integrate | Developer's Manual | developers-manual |
| Operate controls, use the system | User's Manual | users-manual |

## When To File

- **Immediately** after discovering something non-obvious
- **At sprint boundaries** — compact working memory into rooms
- **At 50% context** — proactive filing, not emergency
- **Before handing off** — the baton must be complete

## How To File

### Method 1: Direct PLATO Tile
```bash
curl -X POST http://localhost:8847/submit \
  -d '{
    "agent": "oracle1",
    "room": "service-manual",
    "domain": "internals",
    "data": {"title": "X", "body": "Y works because Z"},
    "confidence": 0.9,
    "tags": ["service-manual", "internals"]
  }'
```

### Method 2: File Write (if PLATO is down)
Write directly to the markdown files in `plato-rooms/{manual}/`. Next compaction will sync them as tiles.

### Method 3: Git Commit (permanent record)
```bash
git add plato-rooms/ && git commit -m "📚 Filed: {title} into {manual}"
git push
```

## Filing Standards

### Service Manual Entries
- Include: component name, how it works, failure modes, debug steps
- Format: heading + explanation + code/data examples + fix instructions
- Tone: technical, precise, no handholding

### Developer's Manual Entries
- Include: API surface, extension point, pattern name, when to use
- Format: heading + interface spec + example + gotchas
- Tone: instructional, here's-how-to-build-on-this

### User's Manual Entries
- Include: control name, what it does, expected output, stop signals
- Format: heading + what/why + example + looks-right/looks-wrong
- Tone: direct, concise, operator-to-operator

## The Compaction Cycle

```
Session starts
    │
    ├── Read CONTEXT-REFERENCE.md (baton)
    ├── Read relevant manual for your role
    │
    ├── Work...
    ├── Discover something → FILE IT
    ├── Work...
    ├── Discover something → FILE IT
    │
    ├── Hit 50% context → COMPACT
    │   ├── Write daily memory
    │   ├── File discoveries into manuals
    │   ├── Update CONTEXT-REFERENCE.md
    │   └── Git push
    │
    ├── Continue...
    ├── Hit 80% context → PREPARE BATON
    │   ├── Final compaction
    │   ├── All knowledge filed
    │   ├── CONTEXT-REFERENCE.md complete
    │   └── Git push
    │
    └── Session ends (next agent picks up baton)
```
