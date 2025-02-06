---
title: "Understanding Rapid Automatic Keyword Extraction (RAKE) Algorithm."
datePublished: Wed Feb 24 2021 15:06:41 GMT+0000 (Coordinated Universal Time)
cuid: ckljkmbmz024t3es1gaqm4hl5
slug: understanding-rapid-automatic-keyword-extraction-rake-algorithm
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1614176918401/YERKIsSDp.jpeg
tags: python, algorithm, package, nlp

---

#### In the world of Natural Language Processing a.k.a NLP, the first and foremost thing is keyword extraction without which there won't be any further step. Ever questioned how does it happen and are there any alternative algorithms? 🤔

![Mathfun](https://media.giphy.com/media/McPHZWaKkFImC6ODE5/giphy.gif)

### Short answer 📖
Words are ranked based on their meaning defined in the text from which redundant words also called stop words are eliminated. Yes, there are a variety of algorithms in use from RAKE to TF - IDF to TextRank.

### Preferring a rather long one? 📚

This article will cover how the Rapid Automatic Keyword Extraction algorithm functions and its simple application.


#### I don't know what NLP is? 🤷‍♂️ 

The field of study that focuses on the interactions between human language and computers is called Natural Language Processing, or NLP for short. It sits at the intersection of computer science, artificial intelligence, and computational linguistics is what Wikipedia says.

In simple terms, you train your machine to learn the **pattern of words** presented to it so that it can predict the next set of words itself which can have a literal meaning as if your computer is talking to you. It is a huge topic in itself which we will cover some other day.


#### Back to RAKE 🔙

RAKE is based on the observations that texts often contain multiple words with standard punctuation or stop words like ‘and’, ‘of’, ‘the’, etc with minimum meaning for understanding. **Stop words 🛑** in the individual form are meaningless hence we **remove 🗑** them. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1614177002044/LFnUrfJnE.png)


Words that are considered to carry a meaning related to the text are described as the **content bearing** 🐻 and are called **content words** 🗣. This extraction algorithm is extremely efficient and operates on individual text pieces which allows it to be used on unseen text data as well or for dynamic collection purposes. Especially for the type of text which follows specific grammar conventions.

The **input parameters** consist of a list of *stop words* and a *set of phrase and word delimiters*. It uses them to partition the document into **candidate keywords**, these keywords are mainly those words that help a developer in extracting the necessary keyword to get information from the document.

#### Installing Rake in python

```
pip install rake-nltk
```

> Note: This version only works up from python 3.4 to 3.6 and with python 2.7. In case of any issues, you can read [this](https://github.com/csurfer/rake-nltk).

#### Importing Rake

```
from rake_nltk import Rake
```

Creating an object and passing a sample text.

```
rake_test = Rake()
sample_text = """
Roderick’s father is a Scottish gentleman, but his mother is a common woman. His father’s high-class family is ashamed of the son’s marriage to a woman from low society and subsequently shuns Roderick’s parents. 
Roderick’s mother dies soon after giving birth to him, which leaves his father overwhelmed by grief. Lost and with no family left to financially support him, Roderick’s father flees and abandons his only son.
Roderick has very little guidance growing up, but his paternal grandfather offers him the minimal amount of support necessary. The grandfather secures Roderick a free education at a local school in Scotland in an attempt to uphold the family’s nobility.
"""
```

The text is parsed by following steps, firstly the document text is **split** into an **array of words** by the specific word delimiters, and secondly, the array is again split into a **sequence of contiguous words** at phrase delimiters and stop word positions. Finally, the words that lie in the same sequence are assigned the same position in the text and together are considered as a candidate key.

```
rake_test.extract_keywords_from_text(sample_text)
print(rake_test.get_ranked_phrases())
```

The following output is displayed:
```
['subsequently shuns roderick ’', 'paternal grandfather offers', 'little guidance growing', 'grandfather secures roderick', 'mother dies soon', 'roderick ’', 'family ’', 'father ’', 'support necessary', 'scottish gentleman', 'minimal amount', 'low society', 'local school', 'giving birth', 'free education', 'financially support', 'family left', 'class family', 'son ’', 'father overwhelmed', 'father flees', 'common woman', 'roderick', 'mother', 'father', 'woman', 'son', 'uphold', 'scotland', 'parents', 'nobility', 'marriage', 'lost', 'leaves', 'high', 'grief', 'attempt', 'ashamed', 'abandons']
```

After identifying all the candidate keywords from the text data, a graph 📈 of word co-occurrence is generated which calculates the score for each candidate keyword and defined as the member word score. With the help of this graph, we evaluate several metrics for calculating word scores, based on the degree and frequency of the vertices in the graph.

```
print(rake_test.get_ranked_phrases_with_scores())
```

*Scored Output*- 
```
[(12.9, 'subsequently shuns roderick ’'), (9.0, 'paternal grandfather offers'), (9.0, 'little guidance growing'), (8.5, 'grandfather secures roderick'), (8.0, 'mother dies soon'), (4.9, 'roderick ’'), (4.4, 'family ’'), (4.15, 'father ’'), (4.0, 'support necessary'), (4.0, 'scottish gentleman'), (4.0, 'minimal amount'), (4.0, 'low society'), (4.0, 'local school'), (4.0, 'giving birth'), (4.0, 'free education'), (4.0, 'financially support'), (4.0, 'family left'), (4.0, 'class family'), (3.9, 'son ’'), (3.75, 'father overwhelmed'), (3.75, 'father flees'), (3.5, 'common woman'), (2.5, 'roderick'), (2.0, 'mother'), (1.75, 'father'), (1.5, 'woman'), (1.5, 'son'), (1.0, 'uphold'), (1.0, 'scotland'), (1.0, 'parents'), (1.0, 'nobility'), (1.0, 'marriage'), (1.0, 'lost'), (1.0, 'leaves'), (1.0, 'high'), (1.0, 'grief'), (1.0, 'attempt'), (1.0, 'ashamed'), (1.0, 'abandons')]
```

As we know that Rake splits candidate keywords by stop words, so the extracted keywords do not contain interior stop words, therefore an interest was expressed in identifying keywords that contain those words. To find keywords that adjoin one another at least twice in the same document and same order. For this purpose, a new candidate keyword is created as a combination of those keywords and the interior stop words. 

After the **candidate keyword score** 💯 is calculated, the top T candidate keywords are selected from the document as the output displayed. The T value is one-third the number of words in the graph.

![Thank You for reading it](https://media.giphy.com/media/xUPOqo6E1XvWXwlCyQ/giphy.gif)






