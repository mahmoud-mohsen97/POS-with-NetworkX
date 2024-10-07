# POS with NetworkX in articles

# Introduction
The task involves performing Part of Speech (POS) tagging on an Arabic article and representing the results in a network graph. POS tagging is essential for identifying the grammatical categories of words, while network graphs provide a visual and structured way to represent relationships between words. The aim is to create a pipeline that performs POS tagging and optimizes it for representing the structure of the article.

# Data Description
The dataset is an article written in Arabic, containing a mix of Arabic text and English names like `"CyShield"` The challenge lies in processing Arabic text for POS tagging, where proper handling of **multilingual** text (Arabic-English) is essential for accurate tagging.

  - Text: One article taken from Cyshield LinkedIn about and then translated to Arabic with a mix of English names.
  - Processing: Each word is tagged with its part of speech using different methods, including rule-based methods and deep learning techniques.


# POS Experiments
## Rule-Based POS Tagging (spaCy and Stanza)

**Goal**: Implement a baseline POS tagging using pre-trained rule-based models (spaCy with UDPipe and Stanza).

**Approach**:

  - **spaCy-UDPipe**: A bridge to use pre-trained `UDPipe` models for Arabic POS tagging. However, spaCy struggled with tokenizing English names and some Arabic words.
  - **Stanza**: A robust NLP library with pre-trained models for Arabic, which improved the accuracy of POS tagging but still had issues with English names within the Arabic text.

**Conclusion**: Rule-based methods provide fast POS tagging but struggle with mixed-language text and nuanced contexts. This led to exploring more advanced models using deep learning.

## Deep Learning-Based POS Tagging with Transformers

**Goal**: Improve POS tagging accuracy by using a transformer-based model, specifically fine-tuned for Arabic `BERT`.

**Approach**:

  - I used the `CAMeL-Lab/bert-base-arabic-camelbert-mix-pos-msa` model to perform POS tagging. This model handles Modern Standard Arabic (MSA) and provides better accuracy for mixed-language text.
  - The pipeline was set up using `Hugging Face's` transformers library and the model performed better than rule-based approaches in classifying both Arabic text and English names.

**Results**: The BERT-based model accurately tagged the mixed-language text, solving the issues with **tokenization** and **classification** that the rule-based methods faced.

**Conclusion**: Deep learning models, particularly fine-tuned transformers, provide superior accuracy for Arabic POS tagging, especially in handling **multilingual** text.

## Comparison
|      Method       | Implementation Speed | Execution Speed | Accuracy | Resource Utilization | Robustness|
|-------------------|----------------------|-----------------|----------|----------------------|-----------|
| SpaCy POS Tagger  | High                 | High            | low | Low | low|
| Stanza POS Tagger | High                 | High            | Moderate  | Low | Moderate|
| Transformer-Based | Moderate             | low             | High | High | High|

# Network Graph Construction with NetworkX
**Goal**: Visualize the relationships between words and their POS tags using a network graph.

**Approach**:

  - Nodes: Each word and its POS tag were represented as nodes in the graph.
  - Edges: Connections between words were created based on `sequential` relationships (word order) and `syntactic dependencies` (subject-verb-object).
  - Tools: NetworkX was used to build the graph, and additional libraries like `arabic-reshaper` and `bidi` were employed for correctly displaying *Arabic* text in the graph.

**Conclusion**: NetworkX provided an effective visual representation of the POS relationships in the article, showing the structure of the sentences and the syntactic dependencies between words.


# Overall Conclusion
This project demonstrated that deep learning-based POS tagging models, such as `BERT`, outperform rule-based methods in handling the complexities of Arabic and mixed-language texts. The use of NetworkX allowed us to represent the grammatical relationships between words in a visual and structured format. The pipeline provided a clear and **optimized** solution for tagging large articles efficiently.


# Tools and Resources
- Tools Used:
  - [spaCy-UDPipe](https://spacy.io/universe/project/spacy-udpipe/) and [Stanza](https://github.com/stanfordnlp/stanza) for rule-based POS tagging.
  - Hugging Face transformers library for deep learning-based POS tagging [Bert].
  - [NetworkX](https://pypi.org/project/networkx/#:~:text=NetworkX%20is%20a%20Python%20package%20for%20the) for graph construction.
  - arabic-reshaper and bidi for Arabic text handling in graphs.
- External Resources:
  - Pre-trained models for Arabic POS tagging from StanfordNLP (Stanza) and [CAMeL-Lab](https://huggingface.co/CAMeL-Lab/bert-base-arabic-camelbert-mix-pos-msa) (BERT).
  - Documentation from spaCy, Stanza, and Hugging Face for implementation details.
 

# Project Reflections
- Biggest Challenge: Handling **multilingual** text (Arabic and English) within a single document for accurate POS tagging. Pre-trained models like `spaCy` struggled with this, necessitating the use of more advanced models like `BERT`.
- Key Learning: Deep learning-based models like `BERT` provide more accurate and context-aware POS tagging in mixed-language texts, and `NetworkX` offers a clear and efficient way to represent linguistic structures.
