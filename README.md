# Truth and Deception: Can Data Reveal When Someone is Lying?
> More detailed explanation of the methodology can be found in the Jupyter notebook

The **aim** of this project was to classify audio stories as either truthful or deceptive. The dataset consists of 2 minute audio stories where the narrator is either telling a story that actually happened to them (truth) or a made-up story (deceptive). An additional constraint is that the model can only take in 30 second segments of these 2 minute audio stories.

## Dataset
-  100 unique, 2 minute audio stories, each labelled as truthful or deceptive
-  30 second sampling was done randomly where a random 30 second snippet from each audio story was extracted, discarding the rest of the story
-  The Librosa library was used to extract audio time series for each of the samples
-  Each 30 second audio sample was transformed and augmented to artificially increase the dataset, resulting in a final sample size of 400 (rather than the initial 100)

## Attributes
The project compared model performance across three sets of attributes, each specialising on slightly different types of audio features.

_Set 1 (Time-Domain)_: Power, Pitch - Mean, Pitch - Standard Deviation, Fraction Voiced\
_Set 2 (Time-Domain)_: Pitch - Mean, Pitch - Standard Deviation, Fraction Voiced, Root Mean Square Energy, Zero-Crossing Rate\
_Set 3 (Frequency-Domain)_: Power, Pitch - Mean, Pitch - Standard Deviation, Fraction Voiced, Spectral Centroid, Spectral Bandwidth

## Quality Metrics
Classification accuracy was used as the main metric of comparing performance across models. This is defined as the _no. correct samples / no. incorrect samples_. Confusion matrices were also used to compare performance across model ensembles for each of the attribute sets.

## Models
The three main models used were:
1. Random Forest
2. Support Vector Machines
3. k-Nearest-Neighbours

Performance for each of these models was also compared across a standardised dataset and a hyperparameter tuned version of the model. For each of the attribute sets, hard-vote ensemble models were created, combining the tuned models to obtain a maximally optimised model.

## Performance
Final ensemble accuracy is as follows:\
_Set 1 (Time-Domain)_: 0.88\
_Set 2 (Time-Domain)_: 0.88\
_Set 3 (Frequency-Domain)_: 0.78

### Confusion Matrices
![image](https://github.com/user-attachments/assets/4168e0ff-a5ef-42dc-be88-5ef46b45d073)

## Reflections
This was an incredible learning experience, allowing me to implement a machine learning pipeline and methodology. I also appreciated being able to compare and contrast the effect of various models and datasets on ultimate model performance. There are a few points of improvement I have noted down, were I to do this project again.

Firstly, I would adjust the feature selection as the two time-domains had very similar performance, despite the second having more attributes (and, thus, complexity). The frequency-domain attributes resulted in a poorer performance overall, perhaps indicating that a different set of frequency attributes would be appropriate. 

Secondly, there are some points to improve on regarding over-fitting. Several of the models appear to be overfitting, with exceptional performance on the training dataset. I would investigate regularisation parameters in a little more depth for the next go around.

Finally, I would explore the impact of having a more focused hyperparameter search. I only used the grid-search for this project which, due to computation constraints, was only able to search across a small number of potential values. I would use a combination of random-search and grid-search next time. 
