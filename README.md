# GPT-Automate-Tests

Built and maintained by [Unnati Nettur](https://github.com/unnati-nettur)

LLM pipelines that generate Behavior-Driven Development (BDD) acceptance tests —
Gherkin scenarios for Cucumber — from natural-language user stories, and compare
four language models under zero-shot and few-shot prompting.

Implementation supporting the study:

> "Comprehensive Evaluation and Insights Into the Use of Large Language Models in
> the Automation of Behavior-Driven Development Acceptance Test Formulation."
> *IEEE Access*, vol. 12, pp. 58715–58721, 2024.
> https://doi.org/10.1109/ACCESS.2024.3391815

## What it does

Each notebook reads user story descriptions from a CSV file, sends them to a model
API together with a prompt and model parameters, and writes the returned BDD
scenarios to `.feature` files. The generated feature files are then validated for
Gherkin syntax, so results can be compared across models and prompt techniques.

## Models compared

| Model | Provider |
| --- | --- |
| GPT-3.5-Turbo | OpenAI |
| GPT-4 | OpenAI |
| PaLM-2 | Google |
| Llama-2-13B | Meta |

Each model runs twice — once with a zero-shot prompt, once with a few-shot prompt
containing worked BDD examples for in-context learning. Both prompts carry the same
six best-practice instructions; only the examples differ.

## Repository contents

| File | Purpose |
| --- | --- |
| `BDD_zero_few_shot_gpt_model.ipynb` | Generation and evaluation for GPT-3.5 and GPT-4 |
| `BDD_zero_few_shot_llama2_13B.ipynb` | Generation and evaluation for Llama-2-13B |
| `BDD_zero_few_shot_palm2_model.ipynb` | Generation and evaluation for PaLM-2 |
| `config.json` | Dataset paths, model parameters and prompt templates |

## Running it

1. Open a notebook in Google Colab or a local Jupyter environment.
2. Set the API key for the relevant provider.
3. Point `config.json` at your user story CSV and adjust model parameters
   (`temperature`, `top_p`, `max_tokens`) as needed.
4. Run the notebook. Generated `.feature` files are written to the configured
   output path, and syntax validation results are collected for analysis.

### Prerequisites

Python 3, `pandas`, and the client library for the provider you are calling
(`openai`, or the relevant Google / Hugging Face client). A Gherkin linter is used
to validate the generated feature files.

## Note on language models

Avoid entering personal or sensitive data into these pipelines. Language models have
known limitations and can produce incorrect or inconsistent output; generated tests
should be reviewed before use.

## License

MIT — see [LICENSE](LICENSE).
