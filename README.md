# Crunchbase API Data Project: Using T5 LLM Model and OpenAI API Fine-Tuning
## Overview
This project aimed to build a T5 model knowledgeable about startups by training it on Crunchbase basic API data. After training the model on Crunchbase data, we fine-tuned it with custom prompt-completion pairs to improve its language generation capabilities. We then compared this with fine-tuning a GPT-3.5 model using OpenAI's API.

## Data Extraction
Crunchbase Basic API was used to extract the following data:
- Company Name
- Description
- Year Founded
- Location

## Data Preparation:
The Crunchbase data was converted into a dataframe, which was then transformed into a Hugging Face Dataset object. 
- *Input Text*: The company name 
- *Target Text*: the description, year, and location
#### Tokenization and Model Training
- *Tokenization*: The data was tokenized for training using the T5Tokenizer.
- *Training*: A T5 model was trained using Seq2Seq training arguments on the Crunchbase dataset. The training process aimed to improve the model’s understanding of startup data.

## Fine-Tuning Process
**Generating Prompt-Completion Pairs**: 
Using the Crunchbase data, 2000 prompt-completion pairs were generated. These pairs were exported into a JSONL file in OpenAI fine-tuning format. These prompts were used for fine-tuning the T5 model and a GPT-3.5 model via OpenAI.

**Splitting the Data**: We then split the prompt-completion data, originally formatted for OpenAI fine-tuning as {"role": "user", "content": prompt} and {"role": "assistant", "content": completion}. The JSONL file was adjusted to match Hugging Face's format, separating data into prompt and completion columns. Once formatted correctly, the data was split into training and testing sets for further fine-tuning.

### Fine-Tuning the T5 Model
We then fine-tuned the T5 model using the Seq2SeqTrainer and DataCollatorForSeq2Seq, resulting in improvements to training loss and perplexity metrics compared to the T5 model only trained on crunchbase data.

### Fine-Tuning GPT-3.5 Model
In the final stage, we fine-tuned the GPT-3.5 model using OpenAI's API. After converting the split prompt-completion data into JSONL format, we uploaded the files to OpenAI and submitted them for a fine-tuning job. The process took approximately 35 minutes, after which I received a completion email. Upon reviewing the results, I plotted the training loss and accuracy, both of which showed significant improvements compared to T5 models.

## Results
| Model Name              | Training Loss | Perplexity |
|-------------------------|---------------|------------|
| CB Data Trained T5       | 1.3792        | 3.9718     |
| CB Fine-Tuned T5         | 0.7204        | 2.0552     |
| CB Fine-Tuned OpenAI     | 0.6773        | 1.9685     |


### Interaction Testing
**Gradio App**: The Gradio app was used to interact with the fine tuned T5 model, which worked well but required exact matches to trained prompts for correct responses. 

**OpenAI Chat Completions Endpoint**: The GPT-3.5 model performed the best, handling variations in prompt language while still delivering accurate and coherent answers.

## Conclusion
This project demonstrated skills in fine-tuning large language models on specific datasets to significantly enhance their performance in answering domain-specific questions. Fine-tuning the GPT-3.5 model through OpenAI’s API provided the best results in terms of both accuracy and flexibility in handling varied input prompts.






