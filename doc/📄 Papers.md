# Self-Notes
- Nye et al (2021): propose a scratchpad allowing to generate reasoning tokens, but only after it has read the full context and questions.
- Here, Self-Notes: allow to deviate from the context on the fly, and generate explicit reasoning tokens.
- Advantage over scratchpad: not forcing the model to re-do the reasoning at the end.
		- This is the difference of forward vs backward reasoning: forward just makes inferences as it goes (ex/ "Frodo went to mount Doom, Sam was accompanying him" => "Sam went to mount Doom"), whereas backwards finds the most relevant facts to answer a question.
- Use five text datasets designed to evaluate multistep reasoning.
	- Amongst others, Create a dataset named Toy Story that introduces a certain number k of relations, and the question at the end implies to go back k "hops" for answering. As a result, Self notes will be more suited to this.
- To generate Self-Notes:
	- either use supervised learning, by training model $M$ on data enriched with "ground truth" self-notes.
	- or use the capability of QA models of also generating questions, to generate itself the question and answer at certain places (which places, it is not specified in the paper).
	- The supervised version is shown to show much better results 
- Interesting idea: check that the inserted Self Notes increase perf by their content, not just the additional compute, by inserting dummies ("\_") at the same location.
# Multi-chain reasoning: https://arxiv.org/pdf/2304.13007.pdf

- GitHub repo: https://github.com/oriyor/reasoning-on-cots
- Focus on multi-hop questions
- Sample different QA chains (ask the model to answer by generating QA chains), then reason over all of these.
	- There is a specific retriever LLM at the end to reason over the multiple QA chains.
		- Firts prompted to "reason step-by-step"
		- Then append the multi-chain context, each line with a (question, andswer) couple.
		- Then append the question, then a step-by-step reasoning chain followed by the final answer.
		- 6-10 of these examples.
	- Different from self-consistency, since self-consistency only takes the answers.
- Test with 15 chains.
- Results seem quite good, but __what is the computational cost__?

# Refiner: https://arxiv.org/pdf/2304.01904.pdf
- Idea: have two models: a generator, and a critic that contradicts it.
- Advantage: can accommodate tasks that do not necessarily have unique closed-form correct answer, such as the Moral Norm task.

From [https://arxiv.org/pdf/2304.05970.pdf](https://arxiv.org/pdf/2304.05970.pdf)
**_Model_** Our primary experiments are carried out with  
the code-davinci-002 (“Codex”) model via the Ope-  
nAI API (Chen et al., 2021). As demonstrated by other  
papers (Wang et al., 2022b; Fu et al., 2022), performance  
trends between methods are consistent across models of  
similar sizes, and Codex is the highest performing model on  
our tested datasets, outperforming the larger PaLM-540B  
(Chowdhery et al., 2022). We thank OpenAI for free access  
to this model as part of their beta program but note that,  
unfortunately, it has been discontinued. We also verify that  
our results generalize to other models (text-davinci  
and gpt-3.5-turbo). We describe our implementation  
details and link to our code in the appendix.

### Good survey of "do they think": https://arxiv.org/pdf/2212.10403.pdf
