# **PoLaPro: Political Language Processing**


Our project aims to create a **Retrieval-Augmented Generation (RAG)** system that allows users to access structured and contextualized political knowledge about Germany through a conversational AI interface. The idea is to combine large language models with curated political text data from various sources — such as party programs, parliamentary speeches, and governmental press releases — to make political information transparent, interactive, and easily understandable.

Our **motivation** stems from the observation that political data in Germany is publicly available but highly fragmented and often difficult to navigate. Citizens, students, and journalists frequently need to search through long documents or datasets to find relevant facts or statements. We want to simplify this process by offering a system that can retrieve, interpret, and summarize political content on demand.

A **potential user scenario** could be a civic education organization or a news outlet that integrates our chatbot to enable users to ask questions like “What was the position of the Green Party on nuclear energy in 2023?” or “How did the Bundestag debate evolve on migration policies?” Our system would retrieve relevant sources, cite them, and provide a concise, factual response.


### **The main questions we want to explore include:**

* How can heterogeneous political text data be unified and structured efficiently?
* How can we ensure factual correctness and transparency when using LLMs for political topics?
* What are the best retrieval and ranking strategies for political knowledge bases?


### **Data**

We plan to collect textual political data from freely available public sources, including:
* Bundestag Plenary Protocols (official transcripts of parliamentary sessions): https://www.bundestag.de/protokolle
* Party Programs and Manifestos (e.g., from official party websites or archives like https://www.wahlprogramme.de
* Government Press Releases from https://www.bundesregierung.de
* News and fact databases (e.g., open government datasets or open data portals)
We will first verify compliance with robots.txt and Terms of Use before crawling or downloading any data.
All data will be stored in a structured format and automatically kept up to date to support semantic search and retrieval within the RAG system.


### **Team:**

* Micha Walter: waltermi96328@th-nuernberg.de
* Nico Simon: simonni96318@th-nuernberg.de
* Jan Tischner: tischnerja95752@th-nuernberg.de


---


## **Predecessor project**
In the preceding project, we (different team) analyzed political speeches in the German Bundestag using Natural Language Processing to gain insights into the dynamics and structure of political communication. Our motivation was to reveal and critically question hidden patterns and relationships in political discourse.

The scenario focused on a comprehensive analysis of the plenary protocols of the German Bundestag. As a hypothetical client, we considered, for example, political research institutes, media houses, or parties that are interested in detailed analyses and comprehensible visualizations of political communication.

Specifically, we aimed to answer the following questions:
* Which party speaks how much, and how fair is the allocation of speaking time?
* Is it possible to automatically identify the party affiliation or even the identity of a speaker based solely on the speech transcript?
* Which main topics dominate the political discourse, and how do the parties differ in this regard?

### **Data Acquisition and Preparation:**
- Crawling all publicly available plenary transcripts of the 19th and 20th legislative periods of the German Bundestag in JSON format via the Bundestag’s official API: https://www.bundestag.de/services/opendata
- Before crawling, verify the website’s Terms of Use and robots.txt to ensure the data retrieval is permitted
- Note: For the 20th period, a small number of protocols are missing.
- For downloading, an API client was created and used, it is checked in under the bundestagsapi folder. However since the data only has to be downloaded once, this is not included in any notebook and just kept for reference.
- After crawling, the data was stored in a Pandas dataframe, preprocessed through several stages, and stored in Pickle (*.pkl) files. Below is a OneDrive link, containing the raw data and the preprocessing stages:
[Onedrive Link](https://technischehochschulen-my.sharepoint.com/:f:/g/personal/dreykornju96245_technischehochschulen_onmicrosoft_com/Ej-sEGwae81FhV8L48I0PbEB2m3WW8Pu_nWlVdClo0ceBg?e=QhDzuj)

### **Analysis of Speaking Time Distribution – Who Speaks How Much?**
- Approach: purely statistical evaluation of speaking times using word and character counts in speeches  
- Visualization, e.g., using boxplots, distributions, or heatmaps  
- Idea: identify patterns and differences in speaking time between political parties  
- Idea: evaluate fairness in speaking time distribution between genders  
- Idea: compare interjections and comments (who makes the most, who receives the most, who receives the most applause, who receives the least applause)  
- See the corresponding notebook: [statistics](./ST-Task/statisticTask.ipynb)


### **Automatic Detection of the Speaker’s Party Affiliation in Transcribed Speeches**

- Approach: build a classification model (e.g., SVM or BERT model) to automatically classify party affiliation
- Extra: identify speakers with the largest speaking share using an additional classification model in a pipeline structure
- Evaluation: precision and recall of the classification results (automated evaluation)
- Idea: perform similarity analysis to infer potential speech authorship overlaps
- See the corresponding notebook: [classification](./ML-Task-1_Classification/ML-Task-1_Classification.ipynb)


### **Investigation of the Main Topics Discussed in Bundestag Speeches**

- Approach: use topic modeling algorithms (e.g., LDA or NMF) to identify thematic clusters in the speeches  
- Idea: party-specific comparison — compare topic clusters across parties to reveal differences in communication strategies regarding overarching topics  
- Suggestion from Prof. Albrecht: analyze how parties interpret and use certain terms (e.g., which terms related to migration, environment, or energy are used most frequently by different parties) → implementation still to be defined  
- Evaluation: assess topic coherence and qualitatively evaluate the distinguishability of the identified themes  
- Idea: retrospectively assign speeches to the identified topics  
- Idea: compare party-specific topic clusters with general clusters to illustrate each party’s focus 
- See the corresponding notebook: [topic modeling notebook](./ML-Task-2_Topic-Modeling/TopicModeling_LDA_NMF.ipynb)


### **Predecessor Project Structure Overview:**

```
data/
├── dataGeneration/ … # created by the Data Generation Pipeline
│   │
├── dataFinalStage/ # final result of the Data Generation Pipeline
│   ├── contributionsExtendedFinalStage/
│   │   ├── contributions_extended_19_20.pkl
│   │   ├── contributions_extended_19.pkl
│   │   └── contributions_extended_20.pkl
│   ├── contributionsSimplifiedFinalStage/
│   │   ├── contributions_simplified_19.pkl
│   │   ├── contributions_simplified_20.pkl
│   │   └── contributions_simplified_19_20.pkl
│   ├── speechContentFinalStage/
│   │   ├── speech_content_19_20.pkl
│   │   ├── speech_content_19.pkl
│   │   └── speech_content_20.pkl
│   └── factionsAbbreviations.pkl
├── dataExcel/
│   ├── finalStage/
│   │   ├── contributions_extended_19_20_finalStage.xlsx
│   │   ├── contributions_extended_19_finalStage.xlsx
│   │   ├── contributions_extended_20_finalStage.xlsx
│   │   ├── contributions_simplified_19_20_finalStage.xlsx
│   │   ├── contributions_simplified_19_finalStage.xlsx
│   │   ├── contributions_simplified_20_finalStage.xlsx
│   │   ├── speech_content_19_20_finalStage.xlsx
│   │   ├── speech_content_19_finalStage.xlsx
│   │   ├── speech_content_20_finalStage.xlsx
│   │   └── factionsAbbreviations.xlsx
│   ├── dataGeneration/
│   │   ├── mgs_wiki_rawData.xlsx
│   │   ├── mps_stage02.xlsx
│   │   ├── mpsFactions_stage03.xlsx
│   │   ├── politicians_stage03.xlsx
│   │   ├── speech_content_19_stage04.xlsx
│   │   ├── speech_content_20_stage04.xlsx
│   │   └── factions_stage02.xlsx
├── dataStatistics/…
├── dataClassification/…
├── dataTopicModeling/…
│   ├── lda
│   ├── bertopic
team-16/
├── dataGeneration/
│   ├── dataGeneratorPipeline.ipynb
│   ├── paths.py
│   ├── dataGenerator_Clean_Text.py
│   ├── dataGenerator_Extract_Contributions.py
│   ├── dataGenerator_Match_Names.py
│   └── bundestagsapi/
├── dataPreprocessingHelpers/
│   ├── preprocessing_pipeline.py
│   ├── phrase_patterns.py
│   └── domain_stopwords.py
├── statisticTask/
├── ML-Task-1_Classification/
│   ├── ML-Task-1_Classification.ipynb
│   ├── classification_experiments.ipynb
│   └── preprocessing_ML-Task-1.py
├── ML-Task-2_Topic-Modeling/
├── README.md
├── ProjectSheet.md
├── requirements.txt
├── nlp_project_env_setup.yml
└── pitch_slides.pdf
```


---


## **Codeguidelines**
- Comments, documentation, and filepaths are to be written in english!

- Always comment functions (or larger sections or significant files) according to the following principle:
  ```
  """
  description.
  :dependencies: <filename>: description
  :param: <parameter_name> (<parameter_data_type>): dascription.
  :return: <parameter_name> (<parameter_data_type>): dascription.
  :raises: <error_name>: description.
  """
  ```
  
- If your code reads data from the project directory, always specify the path to this data in the project directory as follows:
  ```
  ### **Input:**
  drectory/
  ├── directory/
  │   └── filename.filetype
  ...
  ```

- If your code writes data to the project directory, always specify the path to this data in the project directory as follows:
  ```
  ### **Output:**
  drectory/
  ├── directory/
  │   └── filename.filetype
  ...
  ```

- If your code creates tabular files such as .pkl, .csv, .xlsx, ects. always include a table in the documentation with a description of the file:
  ```
  **Columns (filename.filetype):**
  | Column name | Description |
  |-------------|-------------|
  | ...         | ...         |
  ```

- To increase usability, always map faction_id columns in any outputs to the abbreviation column of dataStage03/dataFactionsStage03/factionsAbbreviations.pkl:
  ```
  # load faction map:
  faction_map = pd.read_pickle("dataStage03/dataFactionsStage03/factionsAbbreviations.pkl").drop_duplicates(subset="id").set_index("id")["abbreviation"]
  # map factions:
  df["faction_abbreviation"] = df["faction_id"].map(faction_map)
  ```

### **faction_id Map:**
| faction abbreviation | faction id |
|----------------------|------------|
| AFD                  | 0          |
| Grüne / Bündnis 90   | 4          |
| DIE LINKE            | 7          |
| CDU / CSU            | 5          |
| FDP                  | 15         |
| SPD                  | 25         |
| BSW                  | 3          |
| Fraktionslos         | 18         |



