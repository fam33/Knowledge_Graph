# Knowledge_Graph

🧠 Project Overview

This repository contains the complete workflow for Knowledge Graph Construction with Personality Modeling, developed as part of an LLM-driven data science assessment.
The pipeline demonstrates:
Text preprocessing and normalization
Entity and relation extraction using spaCy
Entity alias normalization
Personality trait extraction via a hybrid lexicon approach
Knowledge graph creation and validation with NetworkX

📘 Dataset
1. Source
The dataset is a synthetic two-page narrative generated specifically for this project.
It describes professional collaborations among experts in healthcare, data science, and academia (e.g., Dr. Maya Thompson, Dr. Omar Khalid, Prof. Aisha Mwangi), including contextual details like organizations, events, and regions.

2. Why Synthetic Data?

No real data was available due to privacy and ethical restrictions.
Synthetic text was designed to mimic real-world communication while preserving narrative coherence and diversity.
It ensures reproducibility, semantic richness, and safe experimentation for entity, relation, and personality extraction.

3. Data Characteristics
Feature	Description
Entities	PERSON, ORG, LOC, DATE, EVENT
Relationships	collaboration, recognition, management, advocacy
Traits	analytical, empathetic, pragmatic, resilient, etc.
Format	.txt file with natural paragraphs and dialogue-like structure

⚙️ Environment Setup
1. Prerequisites
Ensure Python ≥ 3.10 and install dependencies:

pip install spacy coreferee nltk networkx matplotlib fuzzywuzzy python-Levenshtein
python -m spacy download en_core_web_lg
python -m coreferee install en


Optional (for richer lexicon matching):

pip install textblob liwc


🚀 Execution
Step 1 – Preprocessing
python src/preprocessing.py


Cleans text (lowercasing, punctuation removal).
Segments into sentences and applies tokenization + lemmatization.

Step 2 – Entity & Relation Extraction
python src/extraction.py


Extracts entities (PERSON, ORG, LOC, etc.) and dependency-based relations.

Step 3 – Entity Normalization
python src/normalization.py

Merges aliases (e.g., “Dr. Maya Thompson” ≈ “Maya”).
Uses Levenshtein string similarity for consistency.


Step 4 – Personality Extraction
python src/personality.py

Identifies adjectives linked to people.
Cross-matches with custom NRC/LIWC-style lexicons.


Step 5 – Knowledge Graph Construction
python src/graph_construction.py

Builds directed graph using NetworkX.
Adds has_trait edges and relation edges between entities.
Exports to KnowledgeGraph_Final.graphml.


Step 6 – Validation
python src/validation.py
Checks schema consistency, connectivity, duplicates.
Prints node counts, edge counts, and type distribution.


📊 Results
1. Extracted Entities
Maya Thompson → PERSON  
Omar Khalid → PERSON  
Aisha Mwangi → PERSON  
Global Health Institute → ORG  
World Health Organization → ORG  
Gates Foundation → ORG  

2. Personality Traits
Maya Thompson: analytical, empathetic, calm, logical  
Omar Khalid: curious, impatient, innovative, perfectionist  
Aisha Mwangi: optimistic, pragmatic, resilient, collaborative

3. Graph Summary
Metric	Value
Total Nodes	32
Total Edges	10
Node Types	PERSON, ORG, TRAIT, LOC, DATE, EVENT
Validation	✅ Schema consistent, no duplicates

4. Visual Output
Blue nodes → entities
Red nodes → traits
Edges → semantic relations (collaborate, recognize, has_trait)

A sample visualization is saved as:
outputs/graph_visualization.png

🧩 Key Insights
The workflow demonstrates a modular LLM pipeline integrating NLP, graph theory, and psychological modeling.
The hybrid rule-based + lexicon approach successfully attributes personality traits.
The resulting graph can support downstream reasoning tasks, such as empathy analysis or team-dynamics modeling.

🧾 Citation / Acknowledgements
spaCy: for NLP and dependency parsing
coreferee: for coreference resolution

NetworkX: for graph construction

NRC / LIWC Lexicons
 for trait mapping

Generated synthetic dataset and workflow authored via LLM-assisted design (GPT-5)
