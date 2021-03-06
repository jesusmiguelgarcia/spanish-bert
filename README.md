# SpanBERTa: RoBERTa for Spanish

SpanBERTa is a transformer language model for Spanish. SpanBERTa is of the same size as BERT-Base and is trained on 18 GB of [OSCAR’s Spanish corpus](https://oscar-corpus.com/) following the pretraining approach specified in [RoBERTa: A Robustly Optimized BERT Pretraining Approach](https://arxiv.org/pdf/1907.11692.pdf).

## Related Articles
- [Tutorial: Pretraining SpanBERTa from scratch](https://colab.research.google.com/drive/1mXWYYkB9UjRdklPVSDvAcUDralmv3Pgv)
- [Tutorial: Finetuning SpanBERTa for NER on CoNLL-2002](https://colab.research.google.com/drive/1ezuE7wC7Fa21Wu3fvzRffx2m14CAySS1#scrollTo=LhKZ3vItVBzi)

## About the Model
|Module| Download |
|------|----------|
| SpanBERTa | [config.json](https://s3.amazonaws.com/models.huggingface.co/bert/skimai/spanberta-base-cased/config.json), [pytorch_model.bin](https://s3.amazonaws.com/models.huggingface.co/bert/skimai/spanberta-base-cased/pytorch_model.bin) |
| Tokenizer | [merges.txt](https://s3.amazonaws.com/models.huggingface.co/bert/skimai/spanberta-base-cased/merges.txt), [vocab.json](https://s3.amazonaws.com/models.huggingface.co/bert/skimai/spanberta-base-cased/vocab.json) |

The model uses a Byte-level BPE tokenizer with a vocabulary size of 50265 sub-word tokens and is trained for 200K steps in 8 days using 4 Tesla V100 GPUs.

Training loss: [tensorboard](https://tensorboard.dev/experiment/4wOFJBwPRBK9wjKE6F32qQ/#scalars)

## Usage
The model weights can be loaded using `transformers` library by Hugging Face.

```python
from transformers import AutoTokenizer, AutoModelWithLMHead

tokenizer = AutoTokenizer.from_pretrained("skimai/spanberta-base-cased")
model = AutoModelWithLMHead.from_pretrained("skimai/spanberta-base-cased")
```

Example using `pipeline`:

```python
from transformers import pipeline

fill_mask = pipeline(
    "fill-mask",
    model="skimai/spanberta-base-cased",
    tokenizer="skimai/spanberta-base-cased"
)

fill_mask("Lavarse frecuentemente las manos con agua y <mask>.")
```

	[{'score': 0.6469631195068359,
	  'sequence': '<s> Lavarse frecuentemente las manos con agua y jabón.</s>',
	  'token': 18493},
	 {'score': 0.06074320897459984,
	  'sequence': '<s> Lavarse frecuentemente las manos con agua y sal.</s>',
	  'token': 619},
	 {'score': 0.029787985607981682,
	  'sequence': '<s> Lavarse frecuentemente las manos con agua y vapor.</s>',
	  'token': 11079},
	 {'score': 0.026410052552819252,
	  'sequence': '<s> Lavarse frecuentemente las manos con agua y limón.</s>',
	  'token': 12788},
	 {'score': 0.017029203474521637,
	  'sequence': '<s> Lavarse frecuentemente las manos con agua y vinagre.</s>',
	  'token': 18424}]



