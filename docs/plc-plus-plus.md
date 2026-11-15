# TwinCAT PLC++ — local research note

> **Status: local observation from TwinCAT 3.1.4026.27.**
> Beckhoff has not exposed a PLC++ language reference in the local installation
> or in the public Information System search used for this note. Treat this as a
> field note, not as a released specification. Do not base production decisions
> on the unverified points below.

## What is confirmed locally

TwinCAT 3.1.4026.27 / XAE Base (`3.1.4026.27`) contains a distinct **PLC++**
project family alongside the classic TwinCAT PLC project:

- project type: `TwinCAT PLC++ Project`
- module type: `TwinCAT PLC++ Module`
- template group: `Default PLC++ Templates`
- project converter: the PLC project context menu has
  `Convert PLC project to PLC++...`
- the command-line helper describes the same operation as
  `convert [<plc-project>] — Convert PLC project to PLC++`
- the XAE shell checks the target platform and reports:
  `PLC++ not supported for platform '%s'. Configuration for PLC++ projects not changed.`
- during build, System Manager has a separate progress step:
  `PLC++ Compiling...`

The conversion UI can treat the result as a **project (YES)** or a
**library (NO)**.

## Practical interpretation

PLC++ is a **separate TwinCAT PLC project/compiler generation**, not simply a
renamed classic PLC project:

| Area | Classic TwinCAT PLC project | PLC++ |
| --- | --- | --- |
| Project type | `TwinCAT PLC Project` | `TwinCAT PLC++ Project` |
| Default templates | PLC templates | separate PLC++ templates |
| Module type | PLC module | `TwinCAT PLC++ Module` |
| Migration | native format | explicit conversion from a PLC project |
| Conversion result | — | PLC++ project or PLC++ library |
| Build | PLC compiler | separate `PLC++ Compiling...` stage |
| Platform support | normal platform rules | explicit platform gate |

Classic PLC projects remain usable. PLC++ is opt-in: a project is not converted
until the user runs the conversion command, and the conversion should be done
on a copy first.

## Not established by this note

The local evidence does **not** establish:

- the PLC++ language grammar or whether it is IEC 61131-3 ST, a C++-based
  language, or a mixed model;
- whether existing ST POUs are translated automatically or only re-hosted;
- runtime scheduling, memory model, performance, or licensing differences;
- whether PLC++ projects and classic PLC projects can share POUs/libraries
  without conversion.

Those points need an official Beckhoff PLC++ manual or release note. Until
then, the safe statement is: **PLC++ is a new, separately compiled TwinCAT PLC
project generation with its own templates, module type and converter; its
language-level differences are not yet documented in the sources available
here.**
