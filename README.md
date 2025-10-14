hab mich eingeschissen
# **Political Language Processing**


### **Political Language Processing**
In our project “Political Language Processing”, we analyze political speeches in the German Bundestag using Natural Language Processing. The aim is to gain insights into the dynamics and structure of political communication. Our motivation is to reveal and critically question hidden patterns and relationships in political discourse.

The scenario focuses on a comprehensive analysis of the plenary protocols of the German Bundestag. As a hypothetical client, we consider, for example, political research institutes, media houses, or parties that are interested in detailed analyses and comprehensible visualizations of political communication.

Specifically, we aim to answer the following questions:
* Which party speaks how much, and how fair is the allocation of speaking time?
* Is it possible to automatically identify the party affiliation or even the identity of a speaker based solely on the speech transcript?
* Which main topics dominate the political discourse, and how do the parties differ in this regard?







## **Motivation / Szenario**
* Worum geht es in Ihrem Projekt?
* Was ist Ihre Motivation?
* Welches Szenario wollen Sie betrachten?
* Gibt es vielleicht sogar einen hypothetischen Kunden, für den Ihr Anwendungsfall relevant wäre?
* Welche Fragestellungen würden Sie gern beantworten?

### **Political Language Processing**
In unserem Projekt „Political Language Processing“ untersuchen wir politische Reden im Deutschen Bundestag mittels Natural Language Processing. Ziel ist es, Einblicke in die Dynamik und Struktur der politischen Kommunikation zu gewinnen. Unsere Motivation besteht darin, verborgene Muster und Zusammenhänge im politischen Diskurs sichtbar zu machen und kritisch zu hinterfragen.
Das Szenario konzentriert sich auf eine umfassende Analyse der Plenarprotokolle des Deutschen Bundestages. Als hypothetischen Kunden betrachten wir beispielsweise politische Forschungsinstitute, Medienhäuser oder Parteien, die an detaillierten Analysen und verständlichen Visualisierungen politischer Kommunikation interessiert sind.
Konkret möchten wir folgende Fragestellungen beantworten:
* Welche Partei spricht wie viel und wie gerecht ist die Redezeit verteilt?
* Lässt sich die Parteizugehörigkeit oder sogar die Identität einer Rednerin oder eines Redners automatisch anhand des Rede-Transkripts erkennen?
* Welche Hauptthemen dominieren im politischen Diskurs und wie unterscheiden sich die Parteien darin?



## **Daten**
* Welche Daten wollen Sie für Ihr Projekt verwenden?
* Bitte angeben, ob Sie frei verfügbare Daten verwenden (wenn ja, Link(s) angeben) oder selbst crawlen wollen (dann URL(s) angeben). Falls selber crawlen, vorher checken, ob robots.txt und "Terms of Use" das erlauben.


### **Als Datengrundlage nutzen wir die frei verfügbaren Plenarprotokolle der 19. und 20. Legislaturperiode des Deutschen Bundestags:**
- Zunächst alle Plenarprotokolle in JSON Form über die API des Deutschen Bundestags Crawlen: https://www.bundestag.de/services/opendata
- Vor dem Crawlen prüfen wir die Nutzungsbedingungen sowie die robots.txt der Website auf Zulässigkeit des Datenabrufs
- Dann die gecrawlten Protokolle von ihrer Rohform in ein verarbeitbares Format transformieren

### **Als Fallback-Option, falls das Crawlen nicht klappt, planen wir einen bereits vorverarbeiteten Datensatz der Bundestags-Mine zu verwenden:**
- Grundlage dieses Datensatzes sind Plenarprotokolle von Sitzungen des 19. Bundestages
- Daten sind hier in JSON-Dateien gekapselt und beinhalten neben den Reden auch die Ergebnisse einer Named-Entity-Recognition und einer Sentiment-Analyse (diese verwenden wir nicht)
- Bundestags-Mine Datensatz: https://bundestag-mine.de/



## **Vorgehen**
- Sofern Sie schon Ideen dazu haben:
  * Wie wollen Sie vorgehen?
  * Welche statistischen Analysen können Sie sich vorstellen durchführen, um erste interessante Informationen und Zusammenhänge zu finden?
  * Was für ML-Modelle wollen Sie trainieren?


### **Datenbeschaffung und Vorbereitung:**
- Crawling der Plenarprotokolle über die API
- Transformation der Daten in ein geeignetes Analyseformat (JSON → tabellarische Form)

### **Statistik Task: Verteilungsanalyse der Sprechzeiten – Wer redet wie viel?**
- Lösungsansatz: rein statistische Auswertung der Redezeiten mittels Wort- und Zeichen-Anzahlen in den Reden
- Visualisierung bspw. mit Boxplots, Verteilungen oder Heatmaps
- Idee: Muster und Unterschiede in Redezeit zwischen den Parteien erkennen
- Idee: Gerechtigkeit der Verteilung der Redezeit zwischen den Geschlechtern auswerten
- Idee von Prof. Albrecht: Einwürfe und Kommentare vergleichen (wer macht die meisten, wer bekommt die meisten, wer bekommt den meisten Beifall, wer bekommt den wenigsten Beifall)

### **ML-Task 1: Automatische Erkennung der Parteizugehörigkeit der Rednerin oder des Redners in transkribierten Reden**

(Klassifikation, supervised learning)

- Lösungsansatz: Aufbau eines Klassifikationsmodells (bspw. SVM oder BERT-Modell) zur automatischen Klassifikation der Parteizugehörigkeit
- Extra: Identifikation der Redner:innen mit dem größten Redeanteil mittels eines weiteren Klassifikationsmodells im Pipelineprinzip
- Evaluierung: Präzision und Recall der Klassifikationsergebnisse (automatisierte Evaluierung)
- Idee: Similarity Analyse aufbauen, um Vermutungen über selbe Rede-Autor:innen anstellen zu können


### **ML-Task 2: Untersuchung der Hauptthemen, die in den Bundestags-Reden diskutiert werden**

(inhaltliche Analyse, unsupervised learning)

- Lösungsansatz: Verwendung von Topic-Modeling-Algorithmen (z.B. LDA oder NMF) zur Identifizierung von Themenclustern in den Reden
- Idee: parteispezifischer Vergleich: parteilich getrennte Themencluster vergleichen, um Unterschiede in den Kommunikationsstrategien zu den übergeordneten Themen darzustellen
- Vorschlag von Prof. Albrecht: Untersuchung, wie Begriffe bei den Parteien interpretiert werden (bspw. welche Begriffe verschiedene Parteien, für Migration, Umwelt, Energie … häufig verwendet werden) -> Umsetzung hier noch unklar!
- Evaluierung: Bewertung der Kohärenz und qualitative Beurteilung der Unterscheidbarkeit der gefundenen Themen
- Idee: Reden dann rückwirkend den erkannten Themen zuweisen
- Idee: Topic-Cluster der Parteien mit den allgemeinen Clustern vergleichen, um Fokus der Parteien abzubilden



## **Fragen**
Was haben Sie noch für offene Fragen, die Sie mit uns Dozenten klären möchten?







### **Team:**

* Micha Walter: waltermi96328@th-nuernberg.de
* Nico Simon: simonni96318@th-nuernberg.de
* Jan Tischner: tischnerja95752@th-nuernberg.de


---


## **data**

### **For our project, the data was fetched from the open data service provided by the Bundestag:**
- The data from the 19th electural term could simply be downloaded using the API.
- Note: For the 20th period, a small number of protocols were missing.
- For downloading, an API client was created and used, it is checked in under the bundestagsapi folder. However since the data only ahas to be downloaded once, this is not included in any notebook and just kept for reference.
- After crawling, the data was stored in a Pandas dataframe, preprocessed through several stages, and stored in Pickle (*.pkl) files. Below is a OneDrive link, containing the raw data and the preprocessing stages:
[Onedrive Link](https://technischehochschulen-my.sharepoint.com/:f:/g/personal/dreykornju96245_technischehochschulen_onmicrosoft_com/Ej-sEGwae81FhV8L48I0PbEB2m3WW8Pu_nWlVdClo0ceBg?e=QhDzuj)


## **Project Structure Overview:**

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



### **Statistical analysis of German Parliamentary Speeches**
See the [Statistic Task](./ST-Task/statisticTask.ipynb)



### **Text classification and NLP analysis of political party based on German Parliamentary Speeches**
See the corresponding classification notebook:
[classification](./ML-Task-1_Classification/ML-Task-1_Classification.ipynb)



### **Topic Modeling of German Parliamentary Speeches**
See the [topic modeling notebook](./ML-Task-2_Topic-Modeling/TopicModeling_LDA_NMF.ipynb)
The follow-up on BERTopic is also linked from there.

