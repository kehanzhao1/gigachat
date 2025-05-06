# gigachat

------------------------------------------------------------------------------------
Benchmark datasets: 
 
r/Jokes Reddit Dataset (LREC 2020) https://github.com/orionw/rJokesData
Humicroedit (SemEval 2020 Task 7) https://github.com/dora-tang/SemEval-2020-Task-7
HAHA @ IberLEF (2019–2021) https://www.kaggle.com/c/jesterdsub/data
Jester Joke Ratings (Kaggle) – This one could be a good source of ground truth humor scores for simple experiments or validation ()

One million reddit jokes (labelled) : https://huggingface.co/datasets/SocialGrep/one-million-reddit-jokes
unlabelled: https://www.kaggle.com/datasets/abhinavmoudgil95/short-jokes/data

 
One challenge for AL in this domain is how to define uncertainty – One can derive uncertainty for a response for a given prompt. However, active prompt selection/engineering could be a more challenging task. You may want to dig into the literature in active prompt engineering to assess the feasibility of uncertainty sampling (or how to define the uncertain score for prompts).
 
---------------------------------------------------------------------------------



Experiment base tools:
● Base LLM model to finetune : LLaMA
● Potential dataset
○ Unlabelled:
https://www.kaggle.com/datasets/abhinavmoudgil95/short-jokes/code
○ Labelled: https://huggingface.co/datasets/SocialGrep/one-million-reddit-jokes
● Reward model: DistillBERT (pretrained transformer models for text clsasification).
● Reinforcement learning tool: trl library
Experiment steps:
1. Use an initial humour (labelled), make it unfunny with GPT-4 (“summarizing___” )
which would form our prompts “produce a funny version of ____”.
2. Train an initial reward model with multi-class classification (rate this joke from 1-5)
using DistilBERT, based on funniness score from the labelled dataset.
3. Perform active learning loop with batches of prompt, response and sample
responses to be labelled based on uncertainty; label the chosen sample with human
annotators or GPT-4 to speed up, update the reward model; Compare reward model
scores for active selection and random selection
4. Finetune the llm (GPT-2?) with reward model and reinforcement learning (Proximal
Policy Optimization)
5. Evaluate generated quality with human evaluation on base model and fine-tuned
model for same set of prompts, and on reward model scores, diversity metrics
(perplexity); optional: evaluate win rate against GPT-4 or DeepSeek

