## 🎯 Final desired output

| Prompting method | Perf on task group 1 | Perf on task group 2 |  ... | 
| --- | --- | --- | --- |
| Chain of Thought | | | |
| Self-consistency | | | |
| Least-to-most | | | |


# 🗺 How to get there?

### 💾 Load scenarios : Antoine
- Load tasks in a common format
- Format question in each prompt
_Output: JSON with questions in prompt format

### ⚙ Run LLMs: Léo
_Input: JSON with questions in prompted format  
- Run the questions with the correct Adaptation (cf HELM paper for "adaptation")
	- This could have to be done in different ways for each prompting method!
_Output: JSON with predicted answers as text and correct answers

### 📈 Metrics: Aymeric
_Input: Answers as text  
- Extract answers
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