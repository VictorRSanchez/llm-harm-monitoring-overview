# Monitoring mental-health harms in LLM interactions

MSc thesis in progress (Universidad de Buenos Aires, Data Mining and Knowledge Discovery). Director: Nicolás Martorell (LIAA/UBA-CONICET).

**Status:** active research, unpublished. This is a public overview. It contains no raw data, no model outputs and no code from the full project, because some of that material is red-teaming content that shouldn't be shared before publication.

## What this project is

I'm building a way to detect when a language model responds harmfully to someone who is in distress, and to test whether that harm can be seen inside the model before it is written out.

There are two parts:

1. **A classifier** (a fine-tuned BERT model) that flags harmful responses across six categories: reinforcing self-harm or suicidal ideation, dismissing distress, dangerous medical advice, reinforcing delusions, promoting disordered eating, and harmful crisis refusal.
2. **Linear probes** trained on the hidden states of each target model, to test whether harmful behaviour is represented internally before it is generated. If it is, lighter and earlier monitors become possible.

## Why this matters

Chatbots are now used by people in real distress, and some of those conversations have gone badly. Reported and alleged cases include an eating-disorder helpline chatbot ([Tessa, taken down in 2023](https://www.cbsnews.com/news/eating-disorder-helpline-chatbot-disabled/)) and lawsuits alleging that chatbots contributed to teenagers' deaths ([Character.AI and Google agreed to settle several in January 2026](https://m.washingtontimes.com/news/2026/jan/7/google-chatbot-maker-character-settle-lawsuit-alleging-chatbot-pushed/)). These are allegations and reports, not established findings.

In several of these cases a vulnerable user sent a message and the harm was in the model's reply. There is still no widely adopted standard way to measure that kind of failure. This project is a small, concrete attempt at that measurement problem.

My background is in telecom and fintech, where monitoring means detecting failures early and measuring them reliably. I'm applying the same instinct here.

## Design

- **Target models:** Llama 3.1 8B Instruct, Qwen3 8B, Mistral 7B Instruct v0.3 (open-weight, run locally).
- **Conversations:** synthetic multi-turn conversations in which a simulated user discloses a vulnerability. No real users and no real user data are involved.
- **Baseline:** each scenario has a matching version without the disclosure, so harm can be compared with and without it.
- **Measurement:** per response, at or after the turn where the user discloses the problem.
- **Labelling:** a two-stage LLM judge under a written rubric, followed by human review of a sample.

## Where it stands (November 2026)

A first round of conversations has been generated on all three models: 396 conversations per model, with 6,732 responses labelled by the LLM judge. These labels are provisional until human review.

Next: choosing the scenarios for the final dataset, human review of a sample, then the classifier, then probing on all three models.

## Limitations

- Labels are reviewed by one non-clinical reviewer. I am looking for clinical psychologists to consult on the criteria.
- Labels are judge labels until review is done.
- The scenarios are synthetic and model behaviour on real users may differ.
- The target models are small open-weight models and may not represent frontier systems.

## Ethics and release

The data is synthetic and no human subjects are involved. Scenarios were written under a rule against asking for means, methods or dosages. Raw model outputs are not released before publication.

## Contact

[LinkedIn](https://www.linkedin.com/in/vrsa/)
