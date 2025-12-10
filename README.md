# AAVE Usage in Popular Media
#### [Link to Colab notebook](https://colab.research.google.com/drive/1vRxxkNJ3ThOfpQjWfyNcjhG9yLoB99qF?usp=sharing)

## Project Description:
This project analyzes the incorporation of African American Vernacular English (AAVE) into popular scripted media. Using Natural Language Processing (NLP) techniques, this project will utilize a model to assess the semantic similarity between comedy movie scripts and the AAVE Corpus.

_[Project Site](https://orreries.github.io/NLP-AAVE_OMA/)_

## Rationale Statement:
This project is being used to interrogate the way that AAVE is assimilated into the wider English lexicon. AAVE terms have been adopted into the wider English vocabulary with many ignorant to the fact that their creation and usage originated in Black communities. Many of the instances AAVE is being used by individuals outside of Black communities it is used improperly and in a manner that is flippant usually in the context of a joke, or being the joke itself. This type of flagrant usage of AAVE has been coined digital blackface. Analyzing how these pieces of media implement AAVE to augment their comedic effect and what picture it creates of Black people and the way they express themselves is the ultimate goal of this project.

The majority of the scripts analyzed were released in the late 2000s to the mid-2010s. During this period, there was a rise in the belief that America had achieved a post-racial society. This idea within the cultural zeitgeist is underscored by the fact that Barack Obama was elected in 2008. A pertinent guiding question when analyzing the racial dynamics during that period is whether the increased visibility and incorporation of Black people in politics and popular media are inherently respectful, or whether incorporation without intention does more harm to public sentiment than good.

## Workflow:
This project explores how comedy movie scripts relate semantically to social media usage of the Black community and whether AAVE terms appear in mainstream screenwriting. The workflow centers on an embedding-based semantic similarity analysis using cosine similarity.

#### _1. Collecting and Preparing the Data_
I started by gathering my two main corpora: A folder of ~300 comedy screenplays (IMSDB) and a JSON collection of tweets grouped by hashtag/topic. To make the tweet data workable, I loaded each JSON file into pandas and converted them into clean DataFrames. Once I verified they displayed correctly in .head(), I exported each DataFrame to CSV for easier use later.

#### _2. Cleaning and Normalizing Script Text_
Each script went through a preprocessing stage:
- Lowercase conversion
- Removing character names, scene headers, and all-caps formatting
- Filtering out non-alphabetic tokens
- Tokenizing the text

This produced a clean text file for every movie, ready for embedding analysis.

#### _3. Scraping and Structuring the AAVE Dictionary_
Next, I scraped the AAVE Master List by looping through its div blocks that contain `<strong>` (terms) and `<mark>` (definitions). I extracted both terms and definitions, stored them in lists, then combined them into a DataFrame, which I saved as a CSV. This AAVE lexicon would later be used for exploratory lexical analysis.

#### _4. Embedding Model + Semantic Similarity_
For the semantic analysis, I embedded both:
- the entire cleaned script
- all tweets in the corpus

To capture semantic similarity, I use the sentence_transformers library model "all-MiniLM-L12-v2" to convert each script and tweet into an embedding:
- the average tweet embedding
- the cosine similarity between the script and average tweet
- the cosine similarity between the script and each individual tweet

The three key numpy steps were:

1. `.reshape(1, -1):` turns a 1D array into a 2D row vector so cosine similarity can run
2. `[0][0]:` pulls out the single scalar similarity value
3. `[0]` for the per-tweet similarities

This produced an overall script-to-Twitter similarity score, a distribution of how close individual tweets are, and max/min/mean similarities to interpret semantic alignment.

#### _5. Interpretation_
Finally, I interpreted the results by comparing the comedy scripts to tweets tagged with culturally specific discourse. The semantic similarity scores revealed how closely each script's language patterns aligned with authentic AAVE usage from Black Twitter, providing insight into whether these films were drawing meaningfully from AAVE linguistic features or simply appropriating surface-level vocabulary.

#### _6. Additional Analysis: Lexical Density (Exploratory)_
In addition to the semantic similarity analysis, I attempted a lexical matching approach to quantify AAVE presence more directly. This process involved searching each film script for both single-word and multi-word AAVE expressions from the AAVE glossary, creating a record of every matching term found. For each script, I calculated the total number of tokens (all words), the total count of AAVE terms including repetitions, and the count of unique AAVE terms without repetition.

From these values, I computed two complementary metrics. Token-based density measures the intensity of AAVE usage by dividing total AAVE term occurrences by the total tokens in the script—revealing how frequently AAVE appears throughout the dialogue. Type-based density measures the diversity of AAVE vocabulary by dividing the number of unique AAVE terms by total tokens, showing how richly the AAVE lexicon is represented. I also calculated AAVE coverage by comparing unique terms found against the full glossary size, indicating what percentage of available AAVE vocabulary each film employs.

However, this lexical approach proved limited due to how the AAVE terms were tokenized and matched. Many AAVE expressions depend heavily on context, syntax, and pragmatic usage that simple dictionary matching cannot capture. A term like "been" or "if" may appear frequently in any English text without necessarily reflecting authentic AAVE usage. The tokenization process also struggled with multi-word expressions and contextual variants that are central to AAVE's linguistic richness. While the lexical density metrics provide a rough quantitative baseline, they require significant refinement to accurately assess the nuanced ways AAVE functions within these scripts. This remains a valuable direction for future research but was not the primary analytical lens for this project.

## Further Study:
Future research with this work could be to map the wider flow of AAVE adoption into the popular English lexicon. This work could augment a temporal analysis of when AAVE usage has become more commonly used in media. This project could easily be expanded to cover other types of media (e.g., more genres of film, investigate TV episode scripts, help analyze trends in books). It could also be used as a tool to analyze memes and social trends to see if there is significant AAVE usage and if the context in which it's used is correct. It was also suggested that one could use transcripts of spoken AAVE (like podcasts) to build a comprehensive authentic usage AAVE corpus and that would be very compelling further research.

Refining the lexical density approach would also benefit from more sophisticated NLP techniques, such as dependency parsing to identify AAVE syntactic structures, leveraging pre-trained models fine-tuned on AAVE data, or developing context-aware matching algorithms that distinguish authentic AAVE usage from coincidental lexical overlap.

## Files List:
1. AAVE_SEMSIM-Final.ipynb: This notebook contains the full workflow for loading movie scripts, cleaning text, embedding scripts and tweets, and computing cosine similarity.
2. AAVE_Dictionary_Cleaned.csv: A CSV file of the AAVE Master List. It contains a column for the specific terms and another column for their definitions.
3. Comedy Scripts (folder): Each file contains the raw movie script text. The filenames (e.g., Superbad.txt, Bridesmaids.txt) get used as the script titles. The corpus they are from pulled from: https://nlds.soe.ucsc.edu/fc2
4. black_tweets_joined_clean.csv: Cleaned corpus of tweets from Black Twitter. Tweets from the Twitter API from the AAVE Corpus: https://github.com/jazmiahenry/aave_corpora/tree/main
5. AAVE_Term_Scraping (1).ipynb: This code was used to scrape the AAVE terms and accompanying definitions from the AAVE glossary website.
6. AAVE_json_convert: This snippet of code converts the tweet JSONs to tabular form.
7. AAVE-A-Collection-of-AAVE.pdf: AAVE Corpus Dataset Information

## Citations
Sidnell, J. (2002). Outline of AAVE grammar. https://cdt.org/wp-content/uploads/2017/11/Outline_of_AAVE_grammar___Jack_Sidnell_2002_1_Afr.pdf

Richomme, O. (2012). The post-racial illusion: Racial politics and inequality in the age of Obama. Revue de recherche en civilisation américaine, (3). http://journals.openedition.org/rrca/464

Powell, J. A. (2009). Post-racialism or targeted universalism. Denver University Law Review, 86, 785.

Farrior, C., & Lester, N. A. (2024). Digital Blackface: Adultification of Black Children in Memes and Children's Books. Humanities, 13(4). https://doi.org/10.3390/h13040091

Ngrams.pdf. (n.d.). (n.d.). Ngrams. Retrieved December 7, 2025, from https://stephanus.tlg.uci.edu/helppdf/ngrams.pdf

Galileo AI. (n.d.). Semantic textual similarity metric guide for AI applications. Retrieved December 7, 2025, from https://galileo.ai/blog/semantic-textual-similarity-metric

Sentence Transformers. (n.d.). Semantic textual similarity — Sentence Transformers documentation. Retrieved December 7, 2025, from https://sbert.net/docs/sentence_transformer/usage/semantic_textual_similarity.html

Sen, A. (2024, July 2). SBERT: How to use sentence embeddings to solve real-world problems. Analytics Vidhya. https://anirbansen2709.medium.com/sbert-how-to-use-sentence-embeddings-to-solve-real-world-problems-f950aa300c72

Sentence Transformers. (n.d.). SentenceTransformers documentation. Retrieved December 7, 2025, from https://sbert.net/

Sentence-transformers/all-MiniLM-L12-v2. (2024, January 5). Hugging Face. https://huggingface.co/sentence-transformers/all-MiniLM-L12-v2

Wired. (n.d.). The new minstrels are here. Retrieved December 2, 2024, from https://www.wired.com/story/new-minstrels-generative-ai/

NPR. (n.d.). The "post-racial" conversation, one year in. Retrieved December 7, 2025, from https://www.npr.org/2010/01/18/122701272/the-post-racial-conversation-one-year-in

## Theme
Made by [bitboody](https://github.com/bitboody/bitboody.github.io)
```

I've moved the lexical analysis to step 6 as "Additional Analysis: Lexical Density (Exploratory)" and framed it as an attempted supplementary approach that revealed limitations. The narrative acknowledges what you tried to measure, explains the methodology, and then discusses why the tokenization and matching approach needs refinement. I also added a sentence to "Further Study" about how this could be improved with more sophisticated NLP techniques.
