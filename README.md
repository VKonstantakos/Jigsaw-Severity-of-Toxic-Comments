# Jigsaw-Severity-of-Toxic-Comments
Solutions to the Kaggle competition "Jigsaw Rate Severity of Toxic Comments: Rank relative ratings of toxicity between comments".

 ## Table of contents

* [Introduction](#Introduction)
* [Datasets](#Datasets)
* [Methods](#Methods)
* [Resources](#Resources)
* [Support](#Support)

## Introduction

When we ask human judges to look at individual comments, without any context, to decide which ones are toxic and which ones are innocuous, it is rarely an easy task. In addition, each individual may have their own bar for toxicity. A much easier task is to ask individuals which of two comments they find more toxic. But if both comments are non-toxic, people will often select randomly. When one comment is obviously the correct choice, the inter-annotator agreement results are much higher.

In this competition, the task was to score a set of about fourteen thousand comments. Pairs of comments were presented to expert raters, who marked one of two comments more harmful — each according to their own notion of toxicity. In this contest, the comment scores will be compared with several hundred thousand rankings. The average agreement with the raters will determine the final score.

## Datasets

### Data Sources from Older Competitions
- [2017 - Toxic Comment Classification Challenge](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge`)
- [2019 - Jigsaw Unintended Bias in Toxicity Classification](https://www.kaggle.com/c/jigsaw-unintended-bias-in-toxicity-classification)
- [2020 - Jigsaw Multilingual Toxic Comment Classification](https://www.kaggle.com/competitions/jigsaw-multilingual-toxic-comment-classification/)

### Training data:
 
|id|comment_text|toxic|severe_toxic|obscene|threat|insult|identity_hate|
|---|---|---|---|---|---|---|---|
|0000997932d777bf|Explanation\nWhy the edits made under my usern..|    0|1|0|0|0|0|
|000103f0d9cfb60f|D'aww! He matches this background colour I'm s..|    0|0|0|1|1|0|
|000113f07ec002fd|Hey man, I'm really not trying to edit war. It..|    1|0|0|0|1|1|
|0001b41b1c6bb37e|"\nMore\nI can't make any real suggestions on ..|    0|1|1|0|0|0|
|0001d958c54c6e35|You, sir, are my hero. Any chance you remember...|0|0|0|1|0|0|

**id** : unique id of each comment  
**comment_text** : comment text crawled from Wikipedia Talk page  
**toxic**, **severe_toxic**, **obscene**, **obscene**, **threat**, **insult**, **identity_hate** : labels generated from previous competition that match the column description 

### Validation data:  
Pair of comments where experts have marked one to be more toxic than the other.

|worker|less_toxic|more_toxic|
|---|---|---|
|313|This article sucks \n\nwoo woo wooooooo|WHAT!!!!!!!!?!?!!?!?!!?!?!?!?!!!!!!!!!!!!!!!!!...|
|188|"And yes, people should recognize that but the...|Daphne Guinness \n\nTop of the mornin' my fav...|
|82|Western Media?\n\nYup, because every crime in...|"Atom you don't believe actual photos of mastu...|
|347|And you removed it! You numbskull! I don't car...|You seem to have sand in your vagina.\n\nMight...|
|539|smelly vagina \n\nBluerasberry why don't you ...|hey \n\nway to support nazis, you racist|


### Testing data:
Raw text to be predicted the toxicity ranking

|comment_id|text|
|---|---|
|114890|"\n \n\nGjalexei, you asked about whether ther...|
|732895|Looks like be have an abuser , can you please ...|
|1139051|I confess to having complete (and apparently b...|
|1434512|"\n\nFreud's ideas are certainly much discusse...|
|2084821|It is not just you. This is a laundry list of ...|


## Methods
- Data Pre-processing:
  - Calculate weightings
    - In order to generate a singular **y** value to use in a regression model, we give weights to each tag column and sum up their values to create a final field.
    - Weights were chosen after trial and error taking into consideration the relative toxicity between each category.
  - Tokenization
  - Lemmatization
  - Data Cleaning
    - Remove emojis.
    - Remove HTML tags.
    - Remove extra spaces.
    - Remove embedded URL links.
    - Replace repetitive characters.
    - Remove special charecters like &, #, etc.
    - Replace common profanity filter evasion words with their corresponding words.
- Encoding:
    - TF-IDF Vectorizer.
- Models:
  - Linear Regression.
  - Linear Supported Vector Regression (Linear SVR).
  - Ridge Regression.
  - PassiveAggressiveRegressor.
  - HuggingFace PreTrained models:
      - RoBERTa.
      - Toxic BERT.
      - BERT Jigsaw.
      - Toxic detector Distil-RoBERTa.

## Resources
- [Competition page on Kaggle](https://www.kaggle.com/c/jigsaw-toxic-severity-rating)
- [[Reading list] - Papers on Toxic Comment & Machine Learning](https://www.kaggle.com/c/jigsaw-toxic-severity-rating/discussion/286329)
- [[Solutions List] - Every single Jigsaw competition solution write up in history!](https://www.kaggle.com/c/jigsaw-toxic-severity-rating/discussion/286333)

## Support

For questions, email vkonstantakos@iit.demokritos.gr
