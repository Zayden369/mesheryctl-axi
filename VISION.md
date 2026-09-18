# Vision

`mesheryctl-axi` is an agent-ergonomic interface to Meshery, built on the official Meshery CLI, `mesheryctl`.

Token-efficient reporting in [TOON](https://toonformat.dev/) is a founding reason this wrapper exists: it reshapes the repeated, tabular output agents read most so that output costs a fraction of the tokens, while Meshery documents stay in their canonical form.

## Scope

We aim for full functional parity with `mesheryctl`.
Every capability available through `mesheryctl` should eventually be accessible through an AXI-native interface.

We accept contributions that expose existing `mesheryctl` capabilities more ergonomically.
We do not add Meshery functionality that cannot be provided through `mesheryctl`.

Where `mesheryctl` cannot yet expose a fact an agent needs, the wrapper may read it from Meshery Server directly, as a bridge rather than a second product surface.
The lasting fix for that gap belongs in `mesheryctl`.

## Interface

The interface follows validated AXI principles and optimizes for autonomous agent use.

Output may be structured, but its structure exists for agent comprehension rather than as a stable API for imperative programs.
Human-oriented presentation and compatibility work primarily serving hand-written parsers are not goals.

The wrapper may reshape, combine, or simplify `mesheryctl` operations when doing so improves agent ergonomics without expanding the underlying capability.

## Principles

### Wrap, don't fork

`mesheryctl` remains the source of Meshery capability, authentication, and context.
This project changes how that capability reaches an agent, never what it is.

### Reporting is compact, content is canonical

Reports about Meshery resources, such as lists, statuses, and errors, are shaped so an agent can read them cheaply.
That shape is [**TOON**](https://toonformat.dev/), which carries the repeated, tabular results agents ask for most in far fewer tokens than the equivalent JSON.
Meshery documents themselves, such as designs and models, are returned in their canonical schema form and are never converted into [TOON](https://toonformat.dev/).

### Never block, never guess

An agent cannot answer a prompt, so the wrapper never waits on one.
Ambiguous requests, unknown input, and unsupported paths fail immediately, with an error that says how to proceed.

### Every answer is definitive and points forward

An empty result says so explicitly rather than printing nothing.
A successful answer suggests the next useful command, so an agent can keep working without consulting documentation.

### Humans keep mesheryctl

`mesheryctl` stays the tool for people, and nothing here changes its behavior for human users.
Improvements that help everyone, such as fixes for interactive prompts, belong upstream in `mesheryctl`.

## Non-Goals

- Replacing `mesheryctl` for human users.
- Changing the meaning of `mesheryctl`'s existing output flags.
- Converting designs, models, or other Meshery documents into [TOON](https://toonformat.dev/).
- Providing a stable interface for hand-written parsers or scripts.
