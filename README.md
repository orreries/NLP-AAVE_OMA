# AAVE Usage in Popular Media
#### [Link to Colab notebook](https://colab.research.google.com/drive/16Ilqg3L3DdGvmgkaE_33xcAJ0DF6qI1B?usp=sharing)

## Project Description:
This project aims to systematically analyze how African American Vernacular English (AAVE) is incorporated into popular scripted media. The primary goal is to assess both the frequency and context of AAVE's use by comparing comedy movie scripts to the AAVE Corpus using Natural Language Processing (NLP) techniques. By evaluating the semantic similarity between these scripts and authentic AAVE language as used in social media, the project seeks to determine whether such incorporations reflect meaningful engagement with AAVE or merely surface-level appropriation.

_[Project Site](https://orreries.github.io/NLP-AAVE_OMA/)_

## Rationale Statement:
This project interrogates how AAVE is assimilated into the wider English lexicon. AAVE terms have been adopted into the wider English vocabulary, with many ignorant of the fact that their creation and usage originated in Black communities. Many of the instances in which AAVE is being used by individuals outside of Black communities, it is used improperly and in a manner that is flippant, usually in the context of a joke, or being the joke itself. This type of flagrant usage of AAVE has been coined digital blackface. Analyzing how these pieces of media use AAVE to augment their comedic effect and the picture they create of Black people, and how they express themselves, is the ultimate goal of this project.

The majority of the scripts analyzed were released in the late 2000s to the mid-2010s. During this period, there was a rise in the belief that America had achieved a post-racial society. This idea within the cultural zeitgeist is underscored by Barack Obama's 2008 election. A pertinent guiding question when analyzing the racial dynamics during that period is whether the increased visibility and incorporation of Black people in politics and popular media are inherently respectful, or whether incorporation without intention does more harm to public sentiment than good.

## Workflow:
This project explores how comedy movie scripts relate semantically to social media usage of the Black community and whether AAVE terms appear in mainstream screenwriting. The workflow centers on an embedding-based semantic similarity analysis using cosine similarity.

#### _1. Collecting and Preparing the Data_
I started by gathering my two main corpora: a 10 movie subcorporus of a folder of ~300 comedy screenplays (IMSDB) and a JSON collection of tweets grouped by hashtag/topic. For tweets, I loaded each JSON file into pandas, converted it to a clean DataFrame, checked .head(), and exported each to CSV for later use.

#### _2. Cleaning and Normalizing Script Text_
Each script went through a preprocessing stage:
- Lowercase conversion
- Removing character names, scene headers, and all-caps formatting
- Filtering out non-alphabetic tokens
- Tokenizing the text

This produced a clean text file for every movie, ready for embedding analysis.

#### _3. Scraping and Structuring the AAVE Dictionary_
I scraped the AAVE Master List by looping through its divs containing terms and definitions, extracting both terms and definitions into lists. I then combined them into a DataFrame and saved it as a CSV. This lexicon supported later lexical analysis.

#### _4. Semantic Similarity_
For the semantic analysis, I embedded both:
- The entire cleaned script
- All tweets in the corpus

To capture semantic similarity, I use the sentence-transformers "all-MiniLM-L12-v2" model to embed each script and tweet. The embeddings were formatted as follows:
- The average tweet embedding
- The cosine similarity between the script and the average tweet
- The cosine similarity between the script and each individual tweet

The cosine similarity function produced an overall script-to-Twitter similarity score (0-1), a distribution of how close individual tweets are, and max/min/mean similarities to interpret semantic alignment.

I compared comedy scripts to tweets tagged with cultural discourse. Semantic similarity scores indicated how closely scripts aligned with authentic AAVE on Black Twitter, revealing whether these films meaningfully drew on AAVE or merely used surface vocabulary.

#### _5. Additional Analysis: Lexical Density (Exploratory)_
In addition to semantic similarity analysis, I used lexical matching to quantify AAVE presence. I searched each script for single- and multi-word AAVE expressions from the glossary, recording each match. For each script, I calculated the total tokens, the total AAVE term count (including repetitions), and the count of unique AAVE terms.

From these values, I computed two complementary metrics. Token-based density measures the intensity of AAVE usage by dividing total AAVE term occurrences by the total tokens in the script—revealing how frequently AAVE appears throughout the dialogue. Type-based density measures the diversity of AAVE vocabulary by dividing the number of unique AAVE terms by total tokens, showing how richly the AAVE lexicon is represented. I also calculated AAVE coverage by comparing the number of unique terms found to the full glossary size, indicating the percentage of available AAVE vocabulary each film employs.

However, this lexical approach proved limited because the AAVE terms were tokenized and matched in suboptimal ways. Many AAVE expressions depend heavily on context, syntax, and pragmatic usage that simple dictionary matching cannot capture. A term like "been" or "if" may appear frequently in any English text without necessarily reflecting authentic AAVE usage. The tokenization process also struggled with multi-word expressions and contextual variants that are central to AAVE's linguistic richness. While the lexical density metrics provide a rough quantitative baseline, they require significant refinement to accurately assess the nuanced ways AAVE functions within these scripts. This remains a valuable direction for future research, but was not the primary analytical lens for this project.

## Further Study:
Future research on this work could map the broader flow of AAVE adoption into the popular English lexicon. This work could augment a temporal analysis of when AAVE usage has become more common in media. This project could easily be expanded to cover other media (e.g., more film genres, TV episode scripts, and book trends). It could also be used to analyze memes and social trends to determine whether there is significant AAVE usage and whether the context in which it's used is appropriate. It was also suggested that one could use transcripts of spoken AAVE (e.g., podcasts) to build a comprehensive, authentic AAVE corpus, which would be compelling for further research.

Refining lexical density would benefit from advanced NLP, such as dependency parsing to identify AAVE syntax, using pre-trained models fine-tuned on AAVE, or context-aware algorithms to distinguish true AAVE from overlaps.

## Files List:
1. AAVE_SEMSIM-Final.ipynb: This notebook contains the full workflow for loading movie scripts, cleaning text, embedding scripts and tweets, and computing cosine similarity.
2. AAVE_Dictionary_Cleaned.csv: A CSV file of the AAVE Master List. It contains a column for the specific terms and another column for their definitions.
3. Comedy Scripts (folder): Each file contains the raw movie script text. The filenames (e.g., Superbad.txt, Bridesmaids.txt) get used as the script titles. The corpus they are from pulled from: https://nlds.soe.ucsc.edu/fc2
4. black_tweets_joined_clean.csv: Cleaned corpus of tweets from Black Twitter. Tweets from the Twitter API from the AAVE Corpus: https://github.com/jazmiahenry/aave_corpora/tree/main
5. AAVE_Term_Scraping (1).ipynb: This code was used to scrape the AAVE terms and accompanying definitions from the AAVE glossary website.
6. AAVE_json_convert: This snippet of code converts the tweet JSONs to tabular form.
7. AAVE-A-Collection-of-AAVE.pdf: AAVE Corpus Dataset Information

## Citations
Farrior, C., & Lester, N. A. (2024). Digital Blackface: Adultification of Black Children in Memes and Children's Books. *Humanities, 13*(4). https://doi.org/10.3390/h13040091

Galileo AI. (n.d.). Semantic textual similarity metric guide for AI applications. Retrieved December 7, 2025, from https://galileo.ai/blog/semantic-textual-similarity-metric

Petty, J. (2024). Text analysis without AI: Lexical density, string similarity, readability & other metrics. GreenFlux Blog. https://blog.greenflux.us/text-analysis-without-ai-lexical-density-string-similarity-readability-other-metrics/

Powell, J. A. (2009). Post-racialism or targeted universalism. *Denver University Law Review, 86*, 785.

Richomme, O. (2012). The post-racial illusion: Racial politics and inequality in the age of Obama. *Revue de recherche en civilisation américaine, (3)*. http://journals.openedition.org/rrca/464

Sen, A. (2024, July 2). SBERT: How to use sentence embeddings to solve real-world problems. Analytics Vidhya. https://anirbansen2709.medium.com/sbert-how-to-use-sentence-embeddings-to-solve-real-world-problems-f950aa300c72

Sentence Transformers. (n.d.). SentenceTransformers documentation. Retrieved December 7, 2025, from https://sbert.net/

Sentence Transformers. (n.d.). Semantic textual similarity — Sentence Transformers documentation. Retrieved December 7, 2025, from https://sbert.net/docs/sentence_transformer/usage/semantic_textual_similarity.html

Sentence-transformers/all-MiniLM-L12-v2. (2024, January 5). Hugging Face. https://huggingface.co/sentence-transformers/all-MiniLM-L12-v2

Sidnell, J. (2002). Outline of AAVE grammar. https://cdt.org/wp-content/uploads/2017/11/Outline_of_AAVE_grammar___Jack_Sidnell_2002_1_Afr.pdf

Stephanus. (n.d.). Ngrams. Retrieved December 7, 2025, from https://stephanus.tlg.uci.edu/helppdf/ngrams.pdf

Wired. (n.d.). The new minstrels are here. Retrieved December 2, 2024, from https://www.wired.com/story/new-minstrels-generative-ai/
io)

NPR. (n.d.). The "post-racial" conversation, one year in. Retrieved December 7, 2025, from https://www.npr.org/2010/01/18/122701272/the-post-racial-conversation-one-year-in

## Theme
Made by [bitboody](https://github.com/bitboody/bitboody.github.io)
