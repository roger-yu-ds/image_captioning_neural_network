Image Captioning Neural Network
==============================

Producing captions for Flickr images

Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io


--------

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>


# The Data
M. Hodosh, P. Young and J. Hockenmaier (2013) "Framing Image Description as a Ranking Task: Data, Models and Evaluation Metrics", Journal of Artifical Intellegence Research, Volume 47, pages 853-899
http://www.jair.org/papers/paper3994.html

## Folder Structure

	└── data
		└── raw
			├── Flicker8k_Dataset
			│
			├── CrowdFlowerAnnotations.txt  <- the expert judgments
			├── ExpertAnnotations.txt       <- the CrowdFlower judgments
			├── Flickr_8k.devImages.txt     <- the validation set
			├── Flickr_8k.testImages.txt    <- the test set
			├── Flickr_8k.trainImages.txt   <- the training set
			├── Flickr8k.lemma.token.txt    <- a lemmatised version of Flickr8k.token.txt
			├── Flickr8k.token.txt          <- raw caption data
			└── readme.txt                  <- the original readme file
						
## `/Flicker8k_Dataset`
The folder that contains all the 8091 images
						
## `Flickr8k.token.txt` 
The raw captions of the Flickr8k Dataset . The first column is the ID of the caption which is "image address # caption number". 40460 rows

|caption_id|caption|
|----------|-------|
|1000268201_693b08cb0e.jpg#0|	A child in a pink dress is climbing up a set of stairs in an entry way .|
|1000268201_693b08cb0e.jpg#1|	A girl going into a wooden building .|
|1000268201_693b08cb0e.jpg#2|	A little girl climbing into a wooden playhouse .|
|1000268201_693b08cb0e.jpg#3|	A little girl climbing the stairs to her playhouse .|
|1000268201_693b08cb0e.jpg#4|	A little girl in a pink dress going into a wooden cabin .|
|1001773457_577c3a7d70.jpg#0|	A black dog and a spotted dog are fighting|
|1001773457_577c3a7d70.jpg#1|	A black dog and a tri-colored dog playing with each other on the road .|
|1001773457_577c3a7d70.jpg#2|	A black dog and a white dog with brown spots are staring at each other in the street .|
|1001773457_577c3a7d70.jpg#3|	Two dogs of different breeds looking at each other on the road .|
|1001773457_577c3a7d70.jpg#4|	Two dogs on pavement moving toward each other .|

## `Flickr8k.lemma.token.txt`
The lemmatized version of the above captions. 40460 rows

|caption_id|caption|
|----------|-------|
|1000268201_693b08cb0e.jpg#0|	A child in a pink dress be climb up a set of stair in an entry way .|
|1000268201_693b08cb0e.jpg#1|	A girl go into a wooden building .|
|1000268201_693b08cb0e.jpg#2|	A little girl climb into a wooden playhouse .|
|1000268201_693b08cb0e.jpg#3|	A little girl climb the stair to her playhouse .|
|1000268201_693b08cb0e.jpg#4|	A little girl in a pink dress go into a wooden cabin .|
|1001773457_577c3a7d70.jpg#0|	A black dog and a spotted dog be fight|
|1001773457_577c3a7d70.jpg#1|	A black dog and a tri-colored dog play with each other on a road .|
|1001773457_577c3a7d70.jpg#2|	A black dog and a white dog with brown spot be stare at each other in a street .|
|1001773457_577c3a7d70.jpg#3|	Two dog of different breed look at each other on a road .|
|1001773457_577c3a7d70.jpg#4|	Two dog on pavement move toward each other .|


## `Flickr_8k.trainImages.txt`
The training set: 6000 images

|image_id|
|----------|
|2513260012_03d33305cf.jpg|
|2903617548_d3e38d7f88.jpg|
|3338291921_fe7ae0c8f8.jpg|
|488416045_1c6d903fe0.jpg|
|2644326817_8f45080b87.jpg|

## `Flickr_8k.devImages.txt`
The validation set. 1000 rows

## `Flickr_8k.testImages.txt`
The test set. 1000 rows

## `ExpertAnnotations.txt`
The expert judgments.  The first two columns are the image and caption IDs.  Caption IDs are <image file name>#<0-4>.  The next three columns are the expert judgments for that image-caption pair.  Scores range from 1 to 4, with a 1 indicating that the caption does not describe the image at all, a 2 indicating the caption describes minor aspects of the image but does not describe the image, a 3 indicating that the caption almost describes the image with minor mistakes, and a 4 indicating that the caption describes the image.

5822 rows

|image_id|caption_id|score_1|score_2|score_3|
|--------|----------|-------|-------|-------|
|1119015538_e8e796281e.jpg|229862312_1a0ba19dab.jpg#2|3|	3|	3|
|1119015538_e8e796281e.jpg|2445283938_ff477c7952.jpg#2|1|	1|	1|
|1119015538_e8e796281e.jpg|2510020918_b2ca0fb2aa.jpg#2|1|	1|	1|
|1119015538_e8e796281e.jpg|2534502836_7a75305655.jpg#2|2|	3|	4|
|1119015538_e8e796281e.jpg|348380010_33bb0599ef.jpg#2|2|	3|	3|
|1119015538_e8e796281e.jpg|387830531_e89c192b92.jpg#2|2|	3|	3|
|1119015538_e8e796281e.jpg|416106657_cab2a107a5.jpg#2|4|	4|	4|

## `ExpertAnnotations.txt`
contains the CrowdFlower judgments.  The first two columns are the image and caption IDs.  The third column is the percent of Yeses, the fourth column is the total number of Yeses, the fifth column is the total number of Noes.  A Yes means that the caption describes the image (possibly with minor mistakes), while a No means that the caption does not describe the image.  Each image-caption pair has a minimum of three judgments, but some may have more.

47830 rows

|image_id|caption_id|pc_yes|total_yes|total_no|
|--------|----------|------|---------|--------|
|1056338697_4f7d7ce270.jpg|	1056338697_4f7d7ce270.jpg#2|	1|	3|	0|
|1056338697_4f7d7ce270.jpg|	114051287_dd85625a04.jpg#2|		0|	0|	3|
|1056338697_4f7d7ce270.jpg|	1427391496_ea512cbe7f.jpg#2|	0|	0|	3|
|1056338697_4f7d7ce270.jpg|	2073964624_52da3a0fc4.jpg#2|	0|	0|	3|
|1056338697_4f7d7ce270.jpg|	2083434441_a93bc6306b.jpg#2|	0|	0|	3|
|1056338697_4f7d7ce270.jpg|	2204550058_2707d92338.jpg#2|	0|	0|	3|
|1056338697_4f7d7ce270.jpg|	2224450291_4c133fabe8.jpg#2|	0|	0|	3|
|1056338697_4f7d7ce270.jpg|	2248487950_c62d0c81a9.jpg#2|	0.333333333333333|	1|	2|

# Metrics
The following are mandatory (see [BLEU](https://en.wikipedia.org/wiki/BLEU)):
- BLEU-1
- BLEU-2
- BLEU-3
- BLEU-4

Other metrics that could be explored are:
- [NIST](https://en.wikipedia.org/wiki/NIST_(metric)), which is an altered BLEU
- [METEOR](https://en.wikipedia.org/wiki/METEOR) (Metric for Evaluation of Translation with Explicit ORdering)
- [ROUGE](https://en.wikipedia.org/wiki/ROUGE_(metric))
- [Word error rate (WER)](https://en.wikipedia.org/wiki/Word_error_rate)

## Calculating BLEU
See the [A Gentle Introduction to Calculating the BLEU Score for Text in Python](https://machinelearningmastery.com/calculate-bleu-score-for-text-python/)

The `nltk` package has a module [nltk.translate.bleu_score](https://www.nltk.org/_modules/nltk/translate/bleu_score.html) that contains a couple of functions that calculate bleu scores:
- `sentence_bleu()`
- `corpus_bleu()`
