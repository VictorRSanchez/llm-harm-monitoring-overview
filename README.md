# Monitoring mental-health harms in LLM interactions

MSc thesis in progress (Universidad de Buenos Aires, Data Mining and Knowledge Discovery). Director: Nicolás Martorell (LIAA/UBA-CONICET).
**Status:** active research, unpublished. This is a public overview. It contains no raw data, no model outputs and no code from the full project, because some of that material is red-teaming content that shouldn't be shared before publication.

## What this project is

I'm building a way to detect when a language model responds harmfully to someone who is in distress, and to test whether that harm can be seen inside the model before it is written out.

There are two parts:

1. **A classifier** (a fine-tuned BERT model) that flags harmful responses across six categories: reinforcing self-harm or suicidal ideation, dismissing distress, dangerous medical advice, reinforcing delusions, promoting disordered eating, and harmful crisis refusal.
2. **Linear probes** trained on the hidden states of each target model, to test whether harmful behaviour is represented internally before it is generated. If it is, lighter and earlier monitors become possible.

## Why this matters

Chatbots are now used by people in real distress, and some of those conversations have gone badly. Reported and alleged cases include an eating-disorder helpline chatbot ([Tessa, taken down in 2023](https://cbsnews.com/amp/news/eating-disorder-helpline-chatbot-disabled)) and lawsuits over teenagers' deaths linked to chatbot conversations ([Character.AI and Google settled several in January 2026](https://m.washingtontimes.com/news/2026/jan/7/google-chatbot-maker-character-settle-lawsuit-alleging-chatbot-pushed/); [Raine v. OpenAI](https://news.bloomberglaw.com/litigation/openai-hit-with-suit-from-family-of-teen-who-died-by-suicide) is ongoing). These are allegations and reports, not established findings.

What they share is that the user's message was ordinary and the harm was in the reply, often building up over a conversation. That is hard to see with single-turn safety tests, and there is no shared, validated way to measure it. Regulators are starting to ask companies how they test (the FTC's 2025 inquiry into AI companions; California's SB 243). This project is a small, concrete attempt at that measurement problem.

My background is in telecom and fintech, where monitoring means detecting failures early and measuring them reliably. I'm applying the same instinct here.

## Design

- **Target models:** Llama 3.1 8B Instruct, Qwen3 8B, Mistral 7B Instruct v0.3 (open-weight, run locally, temperature 0.7).
- **Scenarios:** 72 synthetic scenarios, 12 per harm category. No real users and no real user data are involved.
- **Conversations:** 8 turns each, with a matched control version of each scenario (categories 1–5) where the risk is removed, so harm can be compared with and without the disclosure.
- **Measurement:** per response, at or after the turn where the user discloses the problem. Not per conversation, because a per-conversation "any turn" rate grows with the number of turns.
- **Labelling:** a two-stage LLM judge under a written rubric, followed by human review. Harm is reported under the label each response receives, not only for the category the scenario targeted.

## Where it stands (November 2026)

All three models have been generated and annotated: 6,732 responses, labelled by the LLM judge. **These are first-pass judge labels, not ground truth. Human review has not been done yet.**

- In every model, harm after disclosure is far higher than in controls (about 0.38–0.42 against 0.025–0.064).
- Total harm is similar across models, but which categories fail differs. For example, on reinforcing delusions the target-category rate is much higher in Qwen3 and Mistral than in Llama.
- Along the way the matched controls turned out to leak the risk, so I audited them, rewrote 177 of 180, and re-checked them. A blind check of the judge on a random sample of 30 responses gave 73% agreement with me (κ = 0.37) after I tightened the rubric. That is moderate agreement, and I'm reporting it as it is.

Next: human review of a stratified sample, then the classifier, then probing on all three models.

## Limitations

- One non-clinical reviewer. There is no external clinician validation, and I state that as a limitation of the thesis.
- Labels are judge labels until review is done.
- The scenarios are synthetic and model behaviour on real users may differ.
- The target models are small open-weight models and may not represent frontier systems.
- Repeated crisis-resource templates are a known ambiguity in how responses are labelled. They are counted and reported, not hidden.

## Ethics and release

The data is synthetic and no human subjects are involved. Scenarios were written under a rule against asking for means, methods or dosages. Raw model outputs are not released before publication.

## Contact

[LinkedIn](https://www.linkedin.com/in/vrsa/)
