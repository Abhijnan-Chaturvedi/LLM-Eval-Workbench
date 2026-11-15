# LLM Evaluation Workbench

**Pick the right LLM with evidence on quality, cost and speed, measured on your own task.**

Live app: https://abhijnan-chaturvedi.github.io/LLM-Eval-Workbench/

Built by [Abhijnan Chaturvedi](https://www.linkedin.com/in/abhijnan-chaturvedi/)

## The problem

Most teams choose a model from a vendor demo and a public leaderboard. That breaks down in three ways:

1. **Benchmarks are not your task.** A model that tops a public ranking can still miss on your data, your prompts and your definition of a good answer.
2. **Spot checks do not repeat.** Reading twenty outputs by hand cannot be rerun when the prompt, the model version or the price changes.
3. **Three decisions are made apart.** Quality sits with engineering, cost with finance and speed with product. Nobody sees the trade-off in one place.

The result is a model choice that is hard to defend and expensive to reverse.

## Who it is for

| User | Question they need answered |
|---|---|
| Product manager | Which model ships, and can I defend the choice? |
| LLM engineer | Did this prompt or model change make answers worse? |
| Business owner | What does it cost at the quality we need? |

## How it works

1. **Golden dataset.** A set of test inputs, each with an expected answer.
2. **Model runs.** Every model answers the same cases. Tokens and response time are recorded.
3. **Stage 1, automated check.** Each answer is scored against the expected one: exact label match for classification, word overlap for free text.
4. **Stage 2, LLM judge.** A judge model scores correctness, completeness and faithfulness from 1 to 5 and gives a reason.
5. **Decision.** Quality, cost and speed are weighted into one recommendation, gated by a minimum quality bar.

Where the two stages disagree on an answer, it goes to a human review queue instead of being averaged away.

## Product decisions and trade-offs

| Decision | Why | Trade-off accepted |
|---|---|---|
| Two stages, not one | A cheap reference check catches clear misses. The judge handles open answers. | Judge calls add cost and need their own calibration. |
| Disagreements go to a human | People review only the cases where the stages disagree. | A small review queue remains by design. |
| The quality bar is a gate, not a weight | A cheap model below the bar must never win on price. | Some low-cost options are ruled out early. |
| The user sets the weights | The best model depends on the business priority. | There is no single universal winner to quote. |
| No server, no stored keys | Anyone can open it. Keys stay in the visitor's browser. | Live runs need the visitor's own API key. |

## Two modes

- **Demo mode** opens with synthetic sample data across three tasks (classification, summarisation, policy Q&A). Model names, prices and response times are illustrative and are not measurements of any real model. The scoring logic is the same one used in live runs.
- **Live mode** runs real models through any OpenAI-compatible endpoint (OpenRouter by default) using your own API key. The key is held in page memory only and is never stored or sent anywhere except the endpoint you enter.

## How success would be measured

- Time from "which model?" to a signed-off decision
- Agreement between the judge and human reviewers
- Share of answers that still need human review
- Cost per 1,000 requests at the target quality

## Roadmap

- Upload human labels to calibrate the judge
- Rerun the same set on every prompt or model change
- Saved runs, to compare this week against last
- Production sampling to catch quality drift

## Background

The method comes from my work as a GenAI product manager, where I defined a two-stage LLM evaluation framework (LLM as a judge plus a golden dataset) to compare 5 models on cost against accuracy. This project is a from-scratch, domain-neutral build. It contains no employer code or data.

## Run it locally

It is a single file with no build step and no dependencies. Download `index.html` and open it in a browser.
