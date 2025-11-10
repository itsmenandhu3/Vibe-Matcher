Vibe Matcher — Lightweight Fashion Recommendation Prototype

This project implements a compact recommendation system that matches natural-language 
"vibe" queries to fashion products using text embeddings and cosine similarity. 
The workflow demonstrates the complete pipeline from dataset creation to similarity 
ranking, evaluation, and latency analysis.


Project Overview:

The Vibe Matcher system takes a user’s text-based vibe description (e.g., 
"energetic urban chic") and identifies the top-matching fashion items using 
vector embeddings. The prototype uses TF-IDF embeddings for local execution and 
cosine similarity for ranking.

The system is designed to be modular, readable, and easily extendable to more 
advanced embedding models or large-scale vector databases.


Workflow & Architecture:

1. Data Preparation
A curated dataset of 8 fashion products is constructed with:
- `name`
- `description`
- `vibes` (tag list)

This dataset is stored in a Pandas DataFrame and serves as the base catalog for retrieval.

2. Embedding Generation (Fallback Mode)
Product descriptions are converted into vector embeddings using a 
TF-IDF vectorizer. A shared, fitted vectorizer ensures consistent dimensions 
between product embeddings and query embeddings.

Key steps:
- Fit TF-IDF on the product corpus  
- Transform both products and user queries  
- Produce numerical vectors suitable for cosine similarity

3. Vector Search & Ranking
Each user query is:
- Embedded using the same vectorizer  
- Compared to all product vectors via cosine similarity  
- Sorted by descending similarity  
- Returned as the top-3 ranked matches  

Output includes product name, description, vibes, and similarity score.

4. Evaluation & Dynamic Thresholding
Three sample queries are tested to:
- Validate ranking behavior  
- Measure query-wise latency  
- Compute a dynamic "good_match" threshold based on distribution of scores  
- Display grouped, readable result tables  

Dynamic thresholding is calculated as:
threshold = mean_score + 0.5 * std_score
This makes evaluation adaptive and robust to varying embedding strengths.

5. Latency Measurement
Each query records execution time (in milliseconds). A simple latency plot shows 
system responsiveness and comparative performance across queries.


Features:
- Lightweight TF-IDF embedding pipeline
- Cosine similarity–based ranking
- Dynamic threshold evaluation
- Clean, grouped result visualisation
- Fully notebook-driven implementation
- Zero external API requirement


How to Run:
1. Open the notebook (`vibe_matcher.ipynb`)
2. Run all cells sequentially:
   - Data preparation  
   - Embedding generation  
   - Vector search  
   - Evaluation  
3. Optional: Modify or extend product catalog  
4. Optional: Replace TF-IDF with a transformer-based embedding model 

License:
This project is open for educational and prototyping use. 




