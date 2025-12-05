# AAVE Usage in Popular Media

## Project Description: 
This project analyzes the incorporation of African American Vernacular English (AAVE) into popular scripted media.
Using Natural Language Processing (NLP) techniques, this project will utilize a model to
assess the semantic similarity between around 300 comedy movie scripts and the AAVE
Corpus. An accompanying sentiment analysis to examine the overall positive or negative
usage of AAVE phrases will also be implemented.

## Rationale Statement: 
This project is being used to interrogate the way that AAVE is assimilated into the wider English lexicon. AAVE
terms have been adopted into the wider English vocabulary with many ignorant to the fact
that their creation and usage originated in Black communities. Many of the instances AAVE is
being used by individuals outside of Black communities it is used improperly and in a manner
that is flippant usually in the context of a joke, or being the joke itself. This type of flagrant
usage of AAVE has been coined digital blackface.

## Workflow: 
I used pandas to store both scripts and tweets in dataframes so I can keep titles, file paths, and cleaned text together. I load my AAVE dictionary from a CSV file using pandas, then use re to count how often each AAVE term appears in a given text. These values are added back into the scripts and tweets dataframes as columns as normalized metrics for the amount of AAVE usage within each dataframe.

To capture semantic similarity, I use the sentence_transformers library (model "all-MiniLM-L6-v2") to convert each script and tweet into an embedding. These embeddings are computed from columns in the dataframes and stored as NumPy arrays. Then, I use the scikit-learn cosine_similarity function to build a similarity matrix, where each cell represents the semantic similarity between a specific script and a specific tweet. I compute each script's average cosine similarity to the entire tweet corpus. At the tweet level, I do the same but with respect to all scripts.

## Further Study:  
Future research with this work could be to map the wider flow of AAVE adoption into the popular
English lexicon. This work could augment a temporal analysis of when AAVE usage has
become more commonly used in media. This project could easily be expanded to cover other
types of media (e.g., more genres of film, investigate TV episode scripts, help analyze trends
in books). It could also be used as a tool to analyze memes and social trends to see if there is
significant AAVE usage and if the context in which it’s used is correct.

## Files List: 

1. Semantic_similarity.ipynb: This notebook contains the full workflow for loading movie scripts, cleaning text, embedding scripts and tweets, and computing cosine similarity.

2. Aave_Dictionary.csv:  A CSV file of the AAVE Master List. It contains a column for the specific terms and another column for their definitions.

3. Scripts (folder): Each file contains the raw movie script text. The filenames (e.g., Superbad.txt, Bridesmaids.txt) get used as the script titles. The corpus they are from pulled from: https://nlds.soe.ucsc.edu/fc2

4. Black_Twitter.json: Scraped tweets in json format from the AAVE Corpus: https://github.com/jazmiahenry/aave_corpora/tree/main
