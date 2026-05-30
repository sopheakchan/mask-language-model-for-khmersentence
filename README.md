# Masked Language Model for Khmer

This mock up notebook fine-tunes **XLM-RoBERTa**, a multilingual masked language model. It learns from Khmer sentences to understand context and grammar, then predicts missing words. The goal is **contextual structure of a sentence** and word suggestion in Khmer.

## Why XLM-RoBERTa
XLM-RoBERTa is trained on many languages and supports Khmer. With a `<mask>` token, it can predict the most likely word for the missing position based on sentence context.

## Low-Rank Adaptation (LoRA)
Since training a full model is too expensive for me, so this mock up code uses **LoRA** with **rank = 16**. That means:
- Only a small set of parameters are trained.
- Memory and compute usage stay low.
- We still get good domain adaptation for Khmer sentences.

In the notebook, LoRA is configured with small trainable parameters and applied to the attention `query` and `value` layers.

## What the notebook covers
- Install dependencies
- Load Khmer sentence data from Hugging Face
- Tokenize and split data
- Fine-tune XLM-RoBERTa with LoRA
- Evaluate and save the adapter
- Inference and prediction on masked sentences

## Example usage
Here is a simple example of a masked sentence and the model predictions:

Sentence:
```
អ្នកចេះនិយាយភាសា<mask>ទេ
```

Top predictions:
```
1. 'ខ្មែរ' | 42.91%
2. 'អង់គ្លេស' | 11.86%
3. 'ចិន' | 11.50%
4. 'បរទេស' | 7.85%
```

This shows how the model fills in the missing word based on context.
