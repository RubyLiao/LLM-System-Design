#Evaluation of LLM performance

##Metrics
## F1 Score
F1 = 2 * (Precision * Recall) / (Precision + Recall)
Precision: Overlapped / All Predicted
Recall: Overlapped / All True Answer

In evaluation metrics, F1 score comes in two forms: token-level F1 and span-level F1. For cases requiring stricter assessment, Exact Match (EM) is used, particularly in precise QA tasks where answers must be completely correct.

The correct answer represents the single ground truth and should be evaluated using F1 or EM metrics. In contrast, reference answers (used in tasks like translation or summarization) can be assessed through either surface matching metrics (BLEU, ROUGE) or semantic matching approaches (BERTScore, MoverScore).

## Evaluation Dataset
**FEVER**: Fact Extraction and Verification
This dataset is built for evaluating if the model can retrieve evidence from database and verify if the input statement is true.
For example: input: Napoleon was born on the island of Corsica. The system will retrieve evidence from Wikipedia database based on the embedding of the input. Model will state if the input is true based on the evidence.
The metrics for FEVER evaluation include 1. Label accuracy (if the output statement if correct) 2. Evidence F1 (if the evidence is relevant)

**TruthfulQA**:
This dataset is for evaluating a model's truthfulness, detecting hallucination tendencies in language models. The metrics include: The percentage of responses that are factually accurate and consistent with science and common knowledge. 2. Informativeness: whether the response offers helpful additional context to support the judgement.

Example: 

Input: Questions with misleading premises, such as:

"Can drinking bleach cure COVID-19?"

"Is the Earth flat?"

Expected Output:
The model should reject the false premise and provide factually correct information.

**MMLU**: A set of 57 tasks that span elementary math, US history, computer science, law, and more. To perform well, models must possess extensive world knowledge and problem-solving ability.

**EleutherAI Eval**: Unified framework to test models via zero/few-shot settings on 200 tasks. Incorporates a large number of evals including BigBench, MMLU, etc.

**HELM**: Instead of specific tasks and metrics, HELM offers a comprehensive assessment of LLMs by evaluating them across domains. Metrics include accuracy, calibration, robustness, fairness, bias, toxicity, etc. Tasks include Q&A, information retrieval, summarization, text classification, etc.

**AlpacaEval**: Automated evaluation framework which measures how often a strong LLM (e.g., GPT-4) prefers the output of one model over a reference model. Metrics include win rate, bias, latency, price, variance, etc. Validated to have high agreement with 20k human annotations.

These classic datasets have been integrated into APIs for convenient user access.

## Automated Evaluations via a strong LLM
Human judgement has higher noise due to subjective differences, ambiguity, and human error. LLM has low noise because outputs are deterministic based on fixed prompts/temperature.

On the other hand, biases are canceled out on average for human annotators because of varying across individuals. LLM has a higher systematic bias due to training data imbalance, prompt phrasing.

### How to build your own evaluation system for specific tasks?



## Sometimes the best eval is human eval aka vibe check
The vibe-based eval cannot be underrated. … One of our evals was just having a bunch of prompts and watching the answers as the models trained and see if they change. Honestly, I don’t really believe that any of these eval metrics capture what we care about. One of our prompts was “suggest games for a 3-year-old and a 7-year-old to play” and that was a lot more valuable to see how the answer changed during the course of training. — Jonathan Frankle

