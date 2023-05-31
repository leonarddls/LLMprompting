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

# HELM paper
![[Pasted image 20230531161013.png]]
#### Problem: Models in research are never tested in the same settings
__Solution: Create a top-down taxonomy of all evaluation cases to be holistic.__
- This allows testing all possible combinations of scenarios and metrics (see graph above).

They create new useful definitions:
1. Scenario: what we want the model to do (e.g. the task). Each instance has an _input_, and a list of _references_. Each reference is a string, annotated with properties relevant for evaluation (it can be only the correct answer, or a list of possible answers with the correct one annotated).
2. Adaptation: "procedure that transforms a trained language model into a system that can make predictions on new instances". Examples of adaptation: prompting, finetuning.
3. Metrics. "The model outputs a completion (string), along with log probabilities of the prompt and completion". Then compute metrics over these completions and probabilities.
	- Example metrics: Exact match, ECE (Expected Calibration Error), Inference runtime...

### Tasks
- QA
- Information retrieval
- Summarization
- Sentiment analysis
- Toxicity detection
- Text classification

Detail on Information Retrieval tasks:
Problem setting. We address the re-ranking task in a pointwise fashion: we formulate the information retrieval problem using prompting as a binary log-probability problem, similar to Nogueira  and Cho (2019): Given a passage 𝑐𝑖 and a query 𝑞, we ask the model whether the passage contains an answer to the query. If the model’s answer is Yes with a high probability, we rank the corresponding 𝑐𝑖 higher, while the No answer with high probability achieves the opposite. Figure 12 depicts an example instance. The rankings produced are then evaluated using standard information retrieval metrics.

Detail on Summarization tasks: Many different metrics: 
- Compare vs reference (with Rouge-2, or BERTS)
- Faithfulness
- Extractievness
"We compute extractiveness since prior work has shown that current summarization systems tend to be less faithful, on average, whenever they extract less""

> Model selection. As one of the pillars of this work, our aim was common understanding of  language models. To achieve this ambition, we had to navigate the access conditions of different models (Liang et al., 2022). Some models were open (full model weights are available for download)  (e.g. GPT-NeoX (20B), OPT (175B), BLOOM (176B))

> First, for scenarios which require probabilities and not just completions (e.g. HellaSwag, MS  MARCO (regular), The Pile), we currently are not able to evaluate (possibly because the model  itself fundamentally does not yield such probabilities) for T0++ (11B), T5 (11B), UL2 (20B), GLM  (130B), and YaLM (100B).

### Adaptation via prompting

> In-context examples. Since we include 5 in-context examples, two core decisions are why we  use this number of examples and how we select the examples. We follow Brown et al. (2020) in  their choice of the number, testing in §8.2: prompting-analysis how the number of examples  influences performance. To select examples, we sample examples to ensure class coverage (for   classification coverage) in order of class frequency, so the 5 most frequent classes will be represented in-context. Critically, we choose to fix the in-context examples across all evaluation instances, in contrast to prior work (e.g. Brown et al., 2020), to more accurately perform few-shot evaluation (Perez et al., 2021)
![[Pasted image 20230531175916.png]]

##### How to select / evaluate an answer in multiple choice scenarios? 2 options
> Prior work introduces two classes of approaches to address adaptation for multiple choice  scenarios. The first is the separate approach employed by Brown et al. (2020), where each choice is  independently scored by concatenating it with the question and computing its probability according  to the LM. In this approach, the probabilities may be further calibrated by the probability the LM   assigns to the answer choice alone. The second is the joint approach employed by Hendrycks et al. (2021c), where all the choices are concatenated with the question to form a prompt (e.g., “\<question> A. <choice 1> B. <choice 2> Answer:”) and the LM predicts the choice index (e.g., A or B). This resembles how one might see a multiple choice question presented on an exam or test.   In §8.2: prompting-analysis, we vary this adaptation strategy to test the influence on performance:  we find the strategy significantly influences accuracy (among other metrics), and the most accurate strategy depends on the scenario (i.e. no strategy is uniformly more accurate).


>  Most strikingly, we find that across all scenarios, accuracy, robustness, and fairness are extremely strong correlated. Strikingly, we find that the relationship between accuracy and calibration can be quite different for very similar scenarios: for two commonsense-centric QA scenarios, we see accuracy and calibration are highly correlated in OpenBookQA (correlation of greater than 0.8) whereas accuracy and calibration error are highly correlated in HellaSwag (correlation greater than 0.85). Further, while not unsurprising given the strong correlations between accuracy, robustness, and fairness, the finding that more robust and more fair models can be less well-calibrated is counter-intuitive and surprising.

> Head-to-head comparison for accuracy across all the core scenarios:
> 1. InstructGPT davinci v2 (175B*)
> 2. TNLG v2 (530B)
> 3. Anthropic-LM v4-s3 (52B), very close to the previous
> In light of the significant difference in model scale of a factor of more than 10 between TNLG v2 (530B) and Anthropic-LM v4-s3 (52B), given InstructGPT davinci v2 (175B*) and Anthropic-LM v4-s3 (52B) share instruction-tuning in common (which other models, beyond smaller InstructGPT variants, do not), this suggests that instruction-tuning and the use of human feedback is an efficient and effective means for improving model accuracy.


### 🚨 Missing adaptation => That's where we step in!  
> With the advances in language models and foundation models, we have witnessed the rise of a   sprawling class of different adaptation methods (see Bommasani et al., 2021, §4.3). At present,   these include a variety of gradient-free prompting strategies (see Liu et al., 2022c) like chain-of-  thoughts (Wei et al., 2022c), parameter-efficient gradient-based methods (see He et al., 2022) like adapters (Houlsby et al., 2019), and full gradient-based fine-tuning. Beyond exploring any of these  specific methods, we recommend work also explore how interoperable these methods are across  different scenarios, metrics, and models so as to understand how best practices for adaptation should emerge.



