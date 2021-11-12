# Milestone P2: 
## Sensitivity evolution on climate change from English news articles between 2015 and early 2020. 
---



#### Table of Contents
- [Research Questions](#research-questions)  
- [Proposed additional datasets](#proposed-additional-datasets)
- [Methods](#methods)
- [Proposed timeline](#proposed-timeline)
- [Organization within the team](#organization-within-the-team)
- [Questions for TAs](#questions-for-tas)
---

## Abstract
Nowadays Climate Change is a hot topic in many discussions and the concern about the long-term alteration of temperature and typical weather patterns in certain places is increasing through the years. We believe the Quotebank datasets will allow us to analyze how the sensitivity about this topic has evolved through society. Indeed, the media are usually publishing articles that public opinion cares about. Therefore, analyzing how the media appropriate climate change topics and how politics talk about it, could give us insight about American public opinion or even how it is influenced. 

## Research Questions
*Utilizing neural community embeddings to understand the climate discussion in the news.*

Thus the sub questions that will arise through the project:
- How the climate change topic has evolved through the last years. 
- Which are the main events that have raised concern in the media. 
- Are there news channels appropriating more the subject? If yes, what political party do they support? 
- How the climate change topic is used by different political parties.


## Proposed additional datasets
For the project we will use the following additional data sets from Wikidata: 

- Glossary of climate change. 

    **Why?** To determine which quotes are related to climate change topics. 

    **How?** Export the 161 expressions from Wikipedia climate change glossary.

- Main features of speakers quoting climate change: age, sex, occupation, nationality, political party (if any). 

    **Why?** We aim to understand relationships (if it exists) between quotes, speakers and newspapers. 

    **How?** We load the data into PySpark and then join onto the limited climate change dataset from Quotebank. 

- News Papers partisan scores

    **Why?** Integrate information about media sources for newspaper analysis. Is there any relationship between speakers quoting climate change topics and media sources? 
	
    **How?**   
    1. We will rely on Robertson’s partisan scores found here: https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/QAN5VX

    2. Wikidata has a rich collection of metadata for newspaper sites, like ownership, political alignment, country of origin, and many more. 



## Methods
### Connecting to Wikidata
Thankfully for us, the Quotebank dataset offers Wikidata ids for every speaker. This being said, the ids are ambiguous, one speaker can be linked to many qids. Since we are unable to create an entity-linking model taking into account contexts, we will use a naive approach when deciding on who the speaker is. The Wikidata ids seems to be ordered by the recency of the article. Since more famous people are likely to be added earlier than later, we will take the lowest Wikidata ID to represent a speaker. To check this hypothesis we disambiguated ten of the speakers manually, and then found that in 90% of the cases, the lowest qid was correct. 

### Building the embedding
A strong indicator of a news site's alignment on many spectrums is who they quote. People act as sources of expertise, as sources of entertainment, and news. Studying similarity in who news sites quote can reveal clusters of similar news sites based on sources of knowledge and expertise. 

We attempt to put this assumption to the test by developing a neural embedding of news sites. To simplify the exploration process, we decided to limit our analysis to a simpler latent semantic analysis embedding. This was done by first applying tf-idf on the domain-speaker pairs and then applying PCA on the vector space. 

For the final version we will use the whole dataset and use word2vecf. A neural embedding that is better able to capture semantic relationships between the entities. 


## Proposed timeline
The pipeline for the Milestone 3 will be the following:

![Alt text](./pipeline.png?raw=true)

For M2 we decided to not work with the entire dataset but instead work with a sample. This will help effectively build out the pipelines and test our ideas. To do this we first sampled 1.5% of the rows from each year to define our dataset. This totaled to almost 2 million quotes.

Once the sample is obtained, it will pass an initial analysis. This inquiry describes the data,  drops missing values and visualizes the distributions (count of speakers, count of quote’s occurrences) in order to have a homogenized dataset. Also it will search correlations between features, for example between speakers and media sources. 

The first big analysis will rely on the embedding. Using the embedding we calculate the similarity between news sites depending on who they quote (see the methods section). We will then use the following:

- Define cultural dimensions (partisan using left and right leaning news sites)
- Project climate discussion on the dimensions. 

Additionally, the data will be cleaned by extracting the quotes containing words from the glossary and selecting only the ones that are most related to climate change using the c.c score. For M3 we will use a better climate change text extraction method by using climatebert, a recent transformer model that has been shown to successfully extract climate related text. We will get it from https://huggingface.co/climatebert/distilroberta-base-climate-f. 

## Organization within the team
As there are 4 independent (refer to the pipeline scheme) main analysis every member will take one. 
Once those steps realized we will divide between ourself: 
-  Integrate all data sets. 
-  Perform statistical analysis of correlation between speakers' appearance in quotes and types of newspapers.
- Do statistical analysis to answer research questions. 
- Visualize the statistical observations 
- Apply LDA to find topic of discussion


