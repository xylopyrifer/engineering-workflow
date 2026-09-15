# Engineering Workflow

[中文说明](README.zh-CN.md)

A practical agent skill for taking a project from requirements to a verified handoff. It helps an agent understand the existing system, make proportionate design decisions, establish clear contracts, and deliver maintainable work.

## What it covers

1. Understand the current state and choose the right depth.
2. Clarify requirements and observable acceptance criteria.
3. Design the user journey, technical approach, and module boundaries.
4. Establish code, interface, configuration, and validation conventions.
5. Build a minimal end-to-end path and implement incrementally.
6. Validate, update documentation, and deliver a useful handoff.

Stage exits are self-checks. They do not require user approval at every stage. The skill scales down for small fixes and respects the user's scope and authorization.

## When to use it

- New projects and features that span multiple modules.
- Maintenance, bug fixes, and refactoring in existing projects.
- Automation, data, and content projects intended for continued use.

Ordinary questions, translations, and standalone short writing do not need the full workflow. Domain-specific instructions and existing project conventions still apply.

## Files

| File | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Complete English instructions and discovery metadata. |
| [agents/openai.yaml](agents/openai.yaml) | English display metadata and invocation policy. |
| [README.zh-CN.md](README.zh-CN.md) | Chinese overview and usage notes. |

The skill is text-only and has no runtime dependencies or required external services.

## Use

Download this repository and keep its folder named `engineering-workflow`. Add that folder to the skill location supported by your agent, preserving `SKILL.md` and `agents/openai.yaml`.

You can also provide the agent with `SKILL.md` directly. For an agent that supports named skill invocation, use:

```text
Use $engineering-workflow to add CSV export to this project.
Inspect the existing implementation, define acceptance criteria,
then implement and verify the change.
```

Another example:

```text
Use $engineering-workflow to plan and build a small inventory tool.
Keep the architecture proportionate and deliver a working, verified result.
```

Installation and discovery depend on the host agent. This repository provides the skill files, not an automatic installer. The included metadata permits implicit invocation when supported by the host.
