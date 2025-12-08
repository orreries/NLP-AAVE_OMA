# AAVE Usage in Popular Media

## Project Description: 
This project analyzes the incorporation of African American Vernacular English (AAVE) into popular scripted media.
Using Natural Language Processing (NLP) techniques, this project will utilize a model to
assess the semantic similarity between comedy movie scripts and the AAVE
Corpus.

## Rationale Statement: 
This project is being used to interrogate the way that AAVE is assimilated into the wider English lexicon. AAVE
terms have been adopted into the wider English vocabulary with many ignorant to the fact
that their creation and usage originated in Black communities. Many of the instances AAVE is
being used by individuals outside of Black communities it is used improperly and in a manner
that is flippant usually in the context of a joke, or being the joke itself. This type of flagrant
usage of AAVE has been coined digital blackface. Analyzing how these pieces of media implement AAVE to augment their comedic effect and what picture it creates of Black people and the way they express themselves is the ultimate goal of this project. 

The majority of the scripts analyzed were released in the late 2000s to the mid-2010s. During this period, there was a rise in the belief that America had achieved a post-racial society. This idea within the cultural zeitgeist is underscored by the fact that Barack Obama was elected in 2008. A pertinent guiding question when analyzing the racial dynamics during that period is whether the increased visibility and incorporation of Black people in politics and popular media are inherently respectful, or whether incorporation without intention does more harm to public sentiment than good.

## Workflow: 
I used pandas to store both scripts and tweets in dataframes so I can keep titles, file paths, and cleaned text together. I load my AAVE dictionary from a CSV file using pandas, then use re to count how often each AAVE term appears in a given text. These values are added back into the scripts and tweets dataframes as columns as normalized metrics for the amount of AAVE usage within each dataframe.

To capture semantic similarity, I use the sentence_transformers library [model "all-MiniLM-L12-v2"](https://huggingface.co/sentence-transformers/all-MiniLM-L12-v2) to convert each script and tweet into an embedding. These embeddings are computed from columns in the dataframes and stored as NumPy arrays. Then, I use the scikit-learn cosine_similarity function to build a similarity matrix, where each cell represents the semantic similarity between a specific script and a specific tweet. I compute each script's average cosine similarity to the entire tweet corpus. At the tweet level, I do the same but with respect to all scripts.


## Further Study:  
Future research with this work could be to map the wider flow of AAVE adoption into the popular
English lexicon. This work could augment a temporal analysis of when AAVE usage has
become more commonly used in media. This project could easily be expanded to cover other
types of media (e.g., more genres of film, investigate TV episode scripts, help analyze trends
in books). It could also be used as a tool to analyze memes and social trends to see if there is
significant AAVE usage and if the context in which it’s used is correct.

## Files List: 

1. AAVE_SEMSIM-Final.ipynb: This notebook contains the full workflow for loading movie scripts, cleaning text, embedding scripts and tweets, and computing cosine similarity.

2. AAVE_Dictionary_Cleaned.csv:  A CSV file of the AAVE Master List. It contains a column for the specific terms and another column for their definitions.

3. Comedy Scripts (folder): Each file contains the raw movie script text. The filenames (e.g., Superbad.txt, Bridesmaids.txt) get used as the script titles. The corpus they are from pulled from: https://nlds.soe.ucsc.edu/fc2

4. black_tweets_joined_clean.csv: Cleaned corpus of tweets from Black Twitter. Tweets from the Twitter API from the AAVE Corpus: https://github.com/jazmiahenry/aave_corpora/tree/main

## Citations
Sidnell, J. (2002). *Outline of AAVE grammar*. https://cdt.org/wp-content/uploads/2017/11/Outline_of_AAVE_grammar___Jack_Sidnell_2002_1_Afr.pdf

Richomme, O. (2012). *The post-racial illusion: Racial politics and inequality in the age of Obama*. *Revue de recherche en civilisation américaine*, (3). [http://journals.openedition.org/rrca/464](http://journals.openedition.org/rrca/464)

Powell, J. A. (2009). Post-racialism or targeted universalism. *Denver University Law Review, 86*, 785.

Farrior, C., & Lester, N. A. (2024). Digital Blackface: Adultification of Black Children in Memes and Children’s Books. *Humanities, 13*(4). [https://doi.org/10.3390/h13040091](https://doi.org/10.3390/h13040091)

Ngrams.pdf. (n.d.). *Ngrams*. Retrieved December 7, 2025, from [https://stephanus.tlg.uci.edu/helppdf/ngrams.pdf](https://stephanus.tlg.uci.edu/helppdf/ngrams.pdf)

Galileo AI. (n.d.). *Semantic textual similarity metric guide for AI applications*. Retrieved December 7, 2025, from [https://galileo.ai/blog/semantic-textual-similarity-metric](https://galileo.ai/blog/semantic-textual-similarity-metric)

Sentence Transformers. (n.d.). *Semantic textual similarity — Sentence Transformers documentation*. Retrieved December 7, 2025, from [https://sbert.net/docs/sentence_transformer/usage/semantic_textual_similarity.html](https://sbert.net/docs/sentence_transformer/usage/semantic_textual_similarity.html)

Sen, A. (2024, July 2). *SBERT: How to use sentence embeddings to solve real-world problems*. Analytics Vidhya. [https://anirbansen2709.medium.com/sbert-how-to-use-sentence-embeddings-to-solve-real-world-problems-f950aa300c72](https://anirbansen2709.medium.com/sbert-how-to-use-sentence-embeddings-to-solve-real-world-problems-f950aa300c72)

Sentence Transformers. (n.d.). *SentenceTransformers documentation*. Retrieved December 7, 2025, from [https://sbert.net/](https://sbert.net/)

Sentence-transformers/all-MiniLM-L12-v2. (2024, January 5). *Hugging Face*. [https://huggingface.co/sentence-transformers/all-MiniLM-L12-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L12-v2)

Wired. (n.d.). *The new minstrels are here*. Retrieved December 2, 2024, from [https://www.wired.com/story/new-minstrels-generative-ai/](https://www.wired.com/story/new-minstrels-generative-ai/)

NPR. (n.d.). *The “post-racial” conversation, one year in*. Retrieved December 7, 2025, from [https://www.npr.org/2010/01/18/122701272/the-post-racial-conversation-one-year-in](https://www.npr.org/2010/01/18/122701272/the-post-racial-conversation-one-year-in)
