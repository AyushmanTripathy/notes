# Agentic Development

## Knowledge for AI

LLM can be assisted with knowledge is following ways

| Concept     | Purpose                  |
| ----------- | ------------------------ |
| MCP         | Tool Access              |
| RAG         | Factual Knowledge        |
| Fine Tuning | Baked into Model Weights |
| Skills      | Procedural Knowledge     |

## Memory For AI

Humans have different type of memory, Agents are mirroring this

| Type       | Description       | Maps to            |
| ---------- | ----------------- | ------------------ |
| Semantic   | Facts             | RAG                |
| Episodic   | Past interactions | Logs, chat history |
| Procedural | How to            | Skills             |

### Model Context Protocol

- Consists of client, server & transport layer
- Primitives can be
    - Tool (functions that can be called)
    - Resource (Read-only data)
    - Prompt Templates

```
Primitives <-> Server <-> Client <-> LLM
```

### Skills

- LLM are rich in factual information
- LLMs lack prodecural knowledge (how to do a thing)
- It consists of SKILL.md & a few optional directories
- Its open standard under agentskills.io

#### Progressive Disclosure

- Context is loaded in 3 tiers
    1. Metadata only (front matter)
    2. Body (SKILL.md)
    3. Resources

- At startup every skill's metadata is loaded
- LLM decides if any skill needs to be further loaded

#### SKILL.md format

- Front matter (YAML)
    1. name
    2. description (trigger for when to use the skill)
- Body (MD)
- Optional directories
    1. scripts (execute js or bash)
    2. references (additional docs)
    3. assets (static resource)

## Multimodal AI

Modality refers to data type. Types of multimodal setups are,

1. Feature level fusion

Feature vectors are extracted from image (differrent modality)

```
Image -> Vision Encoder -> LLM
```

2. Native multimodality

Text, Audio, Image get tokenized into same high dimensional space called Shared vector space

### Temporal Reasoning

Deals with Video in LLMs. In the old approach,

- Snapping images from a video, losses information
- 2D pixel patches from frame by frame of video are taken

In temporal reasoning,

- 3D cude of pixels, capturing an area over short period of time
- Motion is baked into the token itself

## References

IBM Technology's AI playlist
