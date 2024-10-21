<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#story-beats">About The Project</a>
    </li>
    <li>
        <a href="#built-with">Built With</a>
    </li>
    <li>
        <a href="#data">Data</a>
    </li>
    <li>
        <a href="#data-preprocessing">Data preprocessing</a>
    </li>
    <li>
        <a href="#tested-solutions">Tested solutions</a>
    </li>
    <li>
        <a href="#results">Results</a>
    </li>
  </ol>
</details>

# story-beats
kaggle competition: https://www.kaggle.com/competitions/story-beats

The goal of the competition is to predict the story beat of a scene in a given movie. According to <i>Blake Snyder's Save the Cat! categorization</i>, there are 15 possible story beats:
<ol>
    <li>Opening Image</li>
    <li>Theme Stated</li>
    <li>Setup</li>
    <li>Catalyst</li>
    <li>Debate</li>
    <li>Break Into Two</li>
    <li>B Story</li>
    <li>Fun and Games</li>
    <li>Midpoint</li>
    <li>Bad Guys Close In</li>
    <li>All is Lost</li>
    <li>Dark Night of the Soul</li>
    <li>Break Into Three</li>
    <li>Finale</li>
    <li>Final Image</li>
</ol>

## Built with
[![Python][Python]][Python-url]
[![HuggingFace][HuggingFace]][HuggingFace-url]
[![Kaggle][Kaggle]][Kaggle-url]
[![Pytorch][Pytorch]][Pytorch-url]
[![Sklearn][Sklearn]][Sklearn-url]

## Data
The data is divided into folders. In each folder, a single file corresponds to a single movie.

#### Folders
<ul>
    <li> <b> scene_timestamps </b> - the start and end timestamp for each scene (given in seconds) </li>
    <li> <b> subtitles </b> - subtitle files in SRT/ASS format </li>
    <li> <b> features </b> - CSV files with sts for each scene </li>
    <li> <b> labels </b> - story beat labels for each scene </li>
</ul>

#### Scene stats (features)
<ul>
    <li> <b> s_dur </b> - scene duration (in seconds) </li> 
    <li> <b> n_shots </b> - number of camera shots in the scene </li>
    <li> <b> ava_shot_dur </b> - average shot duration </li>
    <li> <b> rel_id_loc </b> - relative scene location in the movie </li>
    <li> <b> rel_t_loc </b> - relative time location in the movie </li>
    <li> <b> ava_char_score </b> - average total screen time of characters in the scene </li>
    <li> <b> is_prot_appear </b> - determines whether the protagonist appears in the scene </li>
</ul>


## Data preprocessing
The data has been appropriately trasnformed to be suitable as input for machine learning models.

<ul>
    <li> Subtitle files in ASS format were converted to SRT format </li>
    <li> Metadata about subtitles, features and other basic movies info were merged into single dataframe </li>
    <li> Subtitles were appropietly loaded and associated with scenes </li>
    <li> Extra info was extracted and added to every scene within movie </li>
    <li> Subtitles have been cleaned of non-standard characters, lemmetized and stopwords were removed  </li>
</ul>

Depending on the model chosen, data were preprocessed in different ways, not always using all the practices given above

## Tested solutions
The tested solutions, in addition to using a different classifier or model from the Hugging Face portal, also used data prepared differently. In order to analyse the results, the performance of the algorithms on the test data was evaluated in detail. Both the overall performance of the classifiers was tested and a more advanced analysis of metrics such as accuracy, precision, recall and f1-score was performed. In addition, it was examined for which categories the algorithms performed best, using a confusion matrix to identify areas for improvement. As part of the significance analysis of individual features, it was assessed which features had the greatest impact on the final classification decisions. Additionally, grid testing of the hyperparameters was carried out to optimise the model and get the best possible results. 

The following solutions were tested:
<ul>
    <li> Random Forest - top words based on TF-IDF + basic data </li>
    <li> XGBoost - top words based on TF-IDF + basic data </li>
    <li> Bert models (distilbert, bert, bert-large, roberta, roberta-large) - based on prepared subtitles </li>
</ul>

## Results
In the end, the best result was obtained by a solution that took a scene classifier based on several classifiers. Each model had a certain weight with which it classified the scenes. The model had the greater the weight (and therefore the greater the influence on the final classification) the better the results it obtained. The best result had ~48% accuracy which means it classified ~48% scenes correctly out of 15 categories.

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[Python]:https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54
[Python-url]: https://www.python.org/
[HuggingFace]: https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-gray?style=for-the-badge&logoColor=yellow
[HuggingFace-url]: https://huggingface.co/
[Kaggle]:https://img.shields.io/badge/Kaggle-20BEFF?style=for-the-badge&logo=Kaggle&logoColor=white
[Kaggle-url]: https://www.kaggle.com/
[Pytorch]: https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white
[Pytorch-url]: https://pytorch.org/
[Sklearn]: https://img.shields.io/badge/scikit%20learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white
[Sklearn-url]: https://scikit-learn.org/stable/
