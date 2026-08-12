# Agent Skills

Reusable Agent Skills for Codex and other clients that support the `SKILL.md`
format. Each skill is self-contained under [`skills/`](./skills).

## Catalog

| Skill | Description |
| --- | --- |
| [`build-project-harness`](./skills/build-project-harness) | Audit repository and task history, confirm project decisions one topic at a time, and create or update a minimal project Harness. |

## Install with Codex

Ask Codex to install the skill from its GitHub directory:

```text
$skill-installer install https://github.com/NIKOPACK/skills/tree/main/skills/build-project-harness
```

Restart Codex after installation so the new skill is discovered.

## Manual installation

Clone the repository and copy the selected skill into your Codex skills
directory:

```bash
git clone https://github.com/NIKOPACK/skills.git nikopack-skills
cp -R nikopack-skills/skills/build-project-harness ~/.codex/skills/build-project-harness
```

## Repository structure

```text
skills/
└── build-project-harness/
    ├── SKILL.md
    ├── LICENSE.txt
    ├── agents/
    │   └── openai.yaml
    └── references/
        ├── evidence-and-decisions.md
        └── harness-components.md
```

## License

Unless a skill states otherwise, this repository is licensed under the MIT
License. Each published skill includes its applicable license in its own
directory.
