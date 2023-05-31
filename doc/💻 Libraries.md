
# [HELM](https://github.com/stanford-crfm/helm)

- Stanford group

- Collection of datasets in a standard format (e.g., NaturalQuestions)
- Collection of models accessible via a unified API (e.g., GPT-3, MT-NLG, OPT, BLOOM)
- Collection of metrics beyond accuracy (efficiency, bias, toxicity, etc.)
- Collection of perturbations for evaluating robustness and fairness (e.g., typos, dialect)
- Modular framework for constructing prompts from datasets
- Proxy server for managing accounts and providing unified interface to access models

# [Eleuther AI Harness](https://github.com/EleutherAI/lm-evaluation-harness/tree/master/scripts)

- Tutorial: [This one is very complete](https://wandb.ai/wandb_gen/llm-evaluation/reports/Evaluating-Large-Language-Models-LLMs-with-Eleuther-AI--VmlldzoyOTI0MDQ3)


# For prompting:
### [Promptsource](https://github.com/bigscience-workshop/promptsource)
- Provides a few prompt templates, in the form of: `{{premise}} \n Question: Does this imply that "{{hypothesis}}"? Yes, no, or maybe? ||| {{answer_choices[label]}}`.
- 


# Eliminated possibilities

### Build on Tree of thought repos
- Official repo: https://github.com/ysymyth/tree-of-thought-llm is very small, has a very specific implementation, which makes it efficient but does not help us to generalize
- [Alternative repo putaclic](https://github.com/kyegomez/tree-of-thoughts): Not versatile enough

### [Huggingface Eval](https://huggingface.co/docs/evaluate/index)
- Seems to have
	- Metrics
	- Methods for training
	- Pipelines to wrap models
- But not
	- Specific tasks
	- Libraries to call models

# [CoT Hub](https://github.com/FranxYao/chain-of-thought-hub/tree/main/MATH/lib_prompt/algebra)

Repo avec les datasets suivant : 
- [MMLU](https://arxiv.org/abs/2210.11416): high school and college knowledge
- [GSM8K](https://arxiv.org/abs/2201.11903): elementary school math. -- Performance improvements on this dataset directly translate to daily math abilities when interacting with LLMs
- [MATH](https://arxiv.org/abs/2206.14858) (Hard!): very hard math and natural science. All current models struggle.
- [Big-Bench Hard](https://arxiv.org/abs/2210.09261): a collection of 27 hard reasoning problems
- [HumanEval](https://github.com/openai/human-eval): a classical dataset for evaluating coding capability.
- [C-Eval](https://cevalbenchmark.com/): a collection of 52 disciplines of knowledge test in Chinese
- [TheoremQA](https://github.com/wenhuchen/TheoremQA) (Hard!): a question-answering dataset driven by STEM theorems
