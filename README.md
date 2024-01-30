## Auto-tagger

This is a simple prototype for automatically tag generator for programming task on a publicly available datasets. In this repository, it is approached to showcase tag generator with an open-sourced LLM (Mistral-7b) with prompt engineering. The case can be extended with better accuracy by fine-tuning model with given data. 

## Requirements

To run the repository, Python => 3.9 is needed. The required packages needed to run the notebook can be installed with the following command:

```pip install -r requirements.txt```

## Usage

The repository contains a notebook that can be run with Jupyter Notebook or Jupyter Lab. The notebook contains all the steps needed to run the tag generator. The notebook expects the data folder containing the questions and tag dataset. The notebook can be run with the following command from the terminal:

```jupyter notebook```

or

```jupyter lab```  

then run the automatic-tagger.ipynb notebook.

## Approaches & Observations

Here the notebook performs the following steps:
- Data is loaded, preprocessesd (removing html tags, special character etc.) and concatenated (body , title)
- Some data analysis are explored to understand tag, frequency and the nature to how to proceed with the problem
- For the small case scenario, a Large language model type open-sourced model is chosen to generate tags based on the promnpt/few-shot prompt.
    - An LLM model is selected (mistral-7b-instruct-quantized gguf version) for the case of small prototype and fine-tuning with smaller scale
    - The model is loaded and prompt engineering is applied to generate tags for a subset of data
    - Generated tags are then post-processed to remove other characters and compared with the actual tags
- Limitation on this approach is, its truly prototype and not specialized for the task/data. Context window limitated. Model selection and quality of model is important for the case of production/usable case. Fine-tune or better model selection can be done to improve the performance.
- Fine-tuning is not done here but this model and approach can be fine-tuned with the given data to improve the performance

## Results

Results are not great with base prompt and enchanced prompt. It is showed accuracy around 0.2 and 0.33 on small subset of data with zero-shot learning. The results can be improved with fine-tuning the model with the given data.

## Alternate possible approach

1. Fine-tune LLM / Try with GPT4/similar model
- When a case of true prototyping is needed, prompt engineering with GPT-4 can give some glimpse of possible approach quickly setting up
- In case of the availablity of sufficient data and resource, fine-tuning an available LLM model, can boost up performance for task-specific cases. For example, here the model can be fine-tuned with the given data to generate tags for the given task.
- Limitation: Cost of API / hosted model can be high
2. Fine-tune NLP model as supervised multi-label classification problem
- If the tags are fixed or no new tags are expected and minimal frequent tags are negligible, then the problem can be tackled with traditional NLP approach too with a BERT/DistilBERT model where the task will be classifying multiple labels for each text. Data needs to be splitted to train/test/val and the model needs to fine-tune given training data and then can be tested to evaluate
- Limitation: Manual effort for fine-tuning and may only be limited to fixed set of tags
