# Life Insurance Needs Analysis + AI Explanations

> 🚧 **Work in progress.** I'm building this project during my Master of AI (target: spring 2027).

## The problem

Before recommending life insurance, an advisor completes a **fact-find** (income, debts, dependants, assets, existing coverage) and a **needs analysis** that estimates how much coverage the family would need. The advisor then explains the recommendation to the client in plain language (a "reasons why" letter). This is careful, repetitive work, and errors or unclear explanations hurt clients.

I've done this work for about 7 years as a licensed advisor (CLU®). This project turns that domain knowledge into software:

1. **A transparent calculation engine:** deterministic, tested Python that computes the coverage need with standard methods (capital needs analysis: income replacement, debt payoff, final expenses, education funding, less existing assets and coverage), with every assumption explicit.
2. **An AI layer on top:** an LLM that (a) pulls structured inputs out of a free-text fact-find and (b) drafts a plain-language explanation of the result. The LLM never does the arithmetic; it reads the engine's output, and every number in its draft is checked back against the engine.

## Design principles

- **Calculations are code, not prompts.** The numbers come from tested functions; the model only handles language.
- **Human in the loop.** Output is a draft for a licensed advisor to review, never advice sent straight to a client.
- **No real client data.** The repository uses synthetic example clients only.

## Plan

- [ ] Data model for a fact-find (`pydantic`): household, income, debts, assets, existing coverage, goals
- [ ] Needs engine: income replacement (present value at a chosen discount rate and term), debts, final expenses, education; unit tests for each component
- [ ] CLI/notebook demo on 3 synthetic households
- [ ] LLM extraction: free-text fact-find → validated JSON, with an evaluation set measuring field-level accuracy
- [ ] LLM explanation: engine output → plain-language summary, with an automatic check that every number matches the engine
- [ ] Small Streamlit UI
- [ ] Write-up: accuracy, failure cases, the limits of automating advice

## Planned structure

```
src/        factfind.py (data model) · needs.py (engine) · llm.py (extraction + explanation)
tests/      unit tests for the engine
examples/   synthetic client fact-finds
```

## Tech

Python · pydantic · pytest · an LLM API · Streamlit

---
*Qianmeng (Laura) Ma, Master of AI student (Seneca Polytechnic), CLU®. Educational project, not financial advice.*
