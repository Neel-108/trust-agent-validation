## Trust Agent - Validation Evidence

## Contents

- [What it is](./README.md)
- [Capability Overview](./Capability_Overview.md)
- [Validation Report](./Agentjacking_Validation_Report.md)
- [Known Limitations](./Known_Limitations_Public.md)
- [License](./LICENSE.md)


![Status: Validated](https://img.shields.io/badge/status-validated-success)
![Date: June 2026](https://img.shields.io/badge/date-June%202026-blue)
![Attack Class: Agentjacking](https://img.shields.io/badge/attack%20class-Agentjacking-orange)
![License: All Rights Reserved](https://img.shields.io/badge/license-All%20Rights%20Reserved-red)


Trust Agent is a runtime verification layer for AI agent outputs,
built around one principle: An action is only trustworthy if it
traces back to what the user actually asked for, instead of something a
tool or document handed the agent along the way.

This repository contains validation evidence and a behavioral
description of the system. It does not contain the engine, scoring
logic, or calibration data as those are proprietary. What's published
here is proof the system works and a clear account of where it
currently doesn't, not how it's built.

## Contents

Capability_Overview.md: What the system does, what it catches, and
what it does not claim. Behavioral description only.

Agentjacking_Validation_Report.md: A real-model test against Tenet
Security's disclosed "Agentjacking" attack class (June 2026), including
a deliberately harder adversarial variant and working negative
controls. Full results, methodology, and an honestly reported open
question.

Known_Limitations_Public.md: A plain-language account of where the
system currently declines to auto-confirm rather than guess, and why
that's the correct failure mode for a verification layer.

## Status

Independently built and tested by one person. Validated on a real
local NLI model and a real LLM, it's not a simulation. 
Not yet production-scale or independently audited.

## Contact

Open to demonstration, evaluation, or collaboration discussions. The
engine is not open source; access beyond what's published here is
considered case by case.
email - swapnilpanchal0215@gmail.com



