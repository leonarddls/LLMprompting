
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