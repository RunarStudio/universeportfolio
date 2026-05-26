---
type: tasks
project: universeportfolio
status: active
updated: 2026-05-26
---

# Universe Portfolio — Task Board

> Tasks for ryuustark/universeportfolio.
> Tagged `<!-- ORCHESTRATOR: ready -->` = picked up by nightly orchestrator (one per run).
> Edit `project/dev/js/data.js` for skill tree changes. Deploy: push to `develop` branch.

---

## Queue

- [x] Add 'Salesforce Architect' as a locked target node to the salesforce skill tree <!-- ORCHESTRATOR: ready -->
  - Context: Skill tree data is in project/dev/js/data.js, inside the `trees.salesforce.nodes` array. The current master node is `{ id: "master", label: "SF Master", ... }`. Add a new node AFTER master representing the career target.
  - Acceptance: A new node `{ id: "sf_architect", label: "SF Architect", size: 16, unlocked: false, desc: "Target: Salesforce Architect certification and role. Requires Admin cert renewal + B2B Commerce + architecture patterns.", rank: "Target · Architect", parents: ["master"] }` is added to the salesforce tree nodes array. Valid JS syntax only.
  - Guardrail: Do not modify any other tree. Do not change existing node ids or labels. Do not touch layout.js, wheel.js, or any file except data.js.

- [ ] Bump salesforce tree level from 90 to 92 to reflect recent interview prep <!-- ORCHESTRATOR: ready -->
  - Context: In data.js, the salesforce tree has `level: 90`. The user has actively prepared for the Architect position and documented experience in an Obsidian prep note.
  - Acceptance: Change `level: 90` to `level: 92` in the salesforce tree object only.
  - Guardrail: One-line change only. Do not touch nodes, other trees, or any other file.

- [ ] Add 'Interview Prep' node to the organization skill tree <!-- ORCHESTRATOR: ready -->
  - Context: trees.organization in data.js. Currently has: root, agile, notion, sprints, po, db_design, tech_debt, and a master node.
  - Acceptance: Add `{ id: "interview", label: "Interview Prep", size: 11, unlocked: true, desc: "Structured Salesforce Architect interview preparation: STAR stories, architecture patterns, common questions.", rank: "Active · Prep", parents: ["po"] }` before the master node. Add "interview" to the master node's parents array alongside existing parents.
  - Guardrail: Only edit data.js. Keep JSON syntax valid. Do not rename or remove existing nodes.

---

## In Progress

_(managed by orchestrator)_

---

## Done

_(none yet)_
