

# Load tasks
- Load tasks in a common format

# Run LLMs
- Several different prompts
- Run the right prompts

# Evaluate
- Being able to evaluate the outputs for different tasks


# Future directions
To improve reasoning:
- Force decomposition: Chain-of-Thought
- [Self-consistency](https://www.semanticscholar.org/reader/5f19ae1135a9500940978104ec15a5b8751bc7d2)
- [Least to most prompting](https://www.semanticscholar.org/reader/5437e8adab596d7294124c0e798708e050e25321)is another instance of forcing decomposition, quite impressive perf increase over Chain of Thought
- Self-Contrarian : Ask model to adapt a critical POV !!!
	- By posing as people holding different opinions ? Different personalities ?
	- Have these dialog a slight bit
- Selection of the most prescient personalities in a crowd.
	- This could be dynamic: generate 10 personnalities, ask them for each question "who would you trust on that one given the past record and their personnality?" Then approve the answer.
- Summarize the question
- Bayesian approach: Give the explanations that are most consistent with the data
- Raisonnement par l'absurde