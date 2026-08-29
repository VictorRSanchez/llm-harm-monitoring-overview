# Monitoring Mental Health Harms in LLM Interactions
*(working title — MSc thesis, in progress)*

**Status:** Active research, unpublished. This repo is a public overview — no raw data, model outputs, or code from the full project are included here, as some material involves red-teamed harmful content that isn't appropriate to share pre-publication.

## Overview

This thesis builds a monitoring system for harmful behavior in LLM outputs, with two components:

1. **A classifier** trained to detect harmful LLM outputs across categories related to mental-health harm (e.g. reinforcement of self-harm, dismissal of user distress, dangerous compliance under pressure).
2. **Interpretability probing** — linear probes trained on a language model's internal representations, to test whether harmful content is encoded internally before it's generated. If harmfulness is detectable pre-generation, that has implications for building lighter-weight, earlier-intervention safety monitors.

The dataset underlying the classifier is built through a structured red-teaming and elicitation pipeline designed to surface both clearly harmful and borderline ("near-miss") model behavior across several open-weight LLMs.

## Background

The project draws on reliability and monitoring engineering principles from telecom/fintech systems — treating harmful LLM behavior analogously to a system failure to be detected, characterized, and predicted, rather than purely as a content-classification problem.

## Contact

Questions or interested in this work — reach out via [LinkedIn](https://www.linkedin.com/in/vrsa/).
