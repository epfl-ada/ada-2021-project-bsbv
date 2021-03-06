# Climate Change related quotes from “Quotebank" database between 2015 and early 2020. 
---

## Note:
We use four different notebooks in our analysis. Since the embedding creation required more compute power the colab allowed, Venia used his desktop computer to build the embedding and conduct the textual analysis. The files are structured as follows
* embedding keeps the embedding files.
* main.ipynb has the rest. 

## Abstract
In the last decades we observe a general increase in average temperatures of the Earth, which modifies the weather balances and ecosystems. At the pace of current CO2 emissions, scientists expect an increase of between 1.5° and 5.3°C in average temperature by 2100. If no action is taken, it would have harmful consequences to humanity and the biosphere.

We thus want to create a productive awareness campaign about Climate Change. Thanks to “Quotebank‘’ database and open accessible data, our goal is to understand how the Climate Change topic has been appropriated by society in the last 5 years.

In other words, when do we talk about it, who and in which platform? This article should serve as a head start for people searching how to target a Climate Change awareness campaign.

All the DataStory can be found in the following link: [DataStory](https://blancheberneron.github.io/GreenPeace.github.io/)

#### Table of Contents
- [Organization of the Github repository](#organization-of-the-GitHub-repository)  
- [Research Questions](#research-questions)  
- [Proposed datasets](#proposed-additional-datasets)
- [Methods](#methods)
- [Organization within the team](#organization-within-the-team)

## Organization of the GitHub repository
The GitHub repository contains the following documents:

* A folder entitled "Figures" which contains the images inserted inside of our notebook. 
* A folder entitled "html" which contains the html code used in our data story. 
* The notebook "main.ipynb " is the notebook used for this project extension, which contains all the code used to draw our plots and produce our results.
* A file entitled "climate_vecs.tsv"
* A file entitled "climate_metadata.tsv"
    
External libraries were used in order to make interactive plots.



## Research Questions
During this article we will answer to the following questions:
* What were the topics and events that triggered conversation about climate change?
* Who are the main personalities driving the climate change topic?
* Which news sites focus most on climate change?
       * Which news sites focus on what issues?
* How are the issues politicized?
* Is climate change getting more polarzied? 

## Proposed  datasets
For the project we will use the following additional data sets from Wikidata: 

- Glossary of climate change. 

    **Why?** To determine which quotes are related to climate change topics. 

    **How?** Export expressions from Wikipedia climate change glossary.

- Main features of speakers quoting climate change:  sex, occupation, nationality, political party (if any), religion, ethnic group. 

    **Why?** We aim to understand relationships (if it exists) between quotes, speakers and domains. 

    **How?** We load the most important features of all the speakers from Wikidata. 

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

We use the whole dataset and use word2vecf. A neural embedding that is better able to capture semantic relationships between the entities. 

## Organization within the team

* Venia: 
	* Loading and cleaning the data set
	* Preprocessing the data set
	* Latent Dirichlet Allocation (LDA) Analysis 
	* Media analysis
	* Embedding 
	
* Sandra: 
	* Loading and cleaning the data set
	* Time Series Analysis
* Belén:
	* Loading and cleaning the data set
	* Speakers Analysis
	* Other features Analysis
	* Media Analisys
* Blanche: 
	* Figuring out how to make the template for the data story
	* Writte the DataStory 
	* Adding the plots
