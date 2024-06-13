# Eva_Patel_RAG_Chatbot

### How I Construct the Dataset

## 1. PDF Extraction and Summarization:
   - First, a PDF document (`dataset.pdf`) was extracted using PyMuPDF (`fitz` library) to obtain the raw text.
   - The text was then split into chunks of manageable size (`text_chunks`) to facilitate summarization and subsequent processing.

## 2. Summarization:
   - Each chunk of text was summarized using the `facebook/bart-large-cnn` model via the Hugging Face `pipeline` for summarization. The goal was to condense each chunk into a concise summary while maintaining key information.

## 3. Question Generation and QA Pair Generation:
   - Summarized chunks were further processed to generate questions (`generate_questions` function) using the `valhalla/t5-base-qg-hl` model. These questions were then answered using the `deepset/roberta-base-squad2` model (`qa_pipeline`), resulting in QA pairs (`generate_qa_pairs` function).
   - The QA pairs constituted the final dataset used for evaluation and chatbot interaction.

### How dataset is formed
![image](https://github.com/evapatel1654/Eva_Patel_RAG_Chatbot/assets/133888581/f105f5fc-2b95-4816-95e0-fc23114ceb52)



### Output which chatbot gave on the query
![image](https://github.com/evapatel1654/Eva_Patel_RAG_Chatbot/assets/133888581/afa0d114-95f3-456a-8a02-598afe4bc141)


### Choosing Evaluation Metrics

## 1. BLEU (Bilingual Evaluation Understudy):
   # - Why:
  BLEU measures the similarity between a candidate (generated summary) and multiple references (original summaries) based on n-gram overlap. It is commonly used for machine translation and text generation tasks.
   # - Usage:
   Calculated using NLTK's `corpus_bleu` function with smoothing to evaluate the quality of the summarization against the original references.
   # - Obtained:
   Average BLEU Score: 0.08714335918223264

## 2. ROUGE (Recall-Oriented Understudy for Gisting Evaluation)**:
  # - Why:
  ROUGE evaluates the quality of summaries by comparing n-gram overlap, recall, and precision with reference summaries.
  # - Usage:
   Employed the `rouge_score` library to compute ROUGE-1, ROUGE-2, and ROUGE-L scores to assess the generated summaries against the original references.
  # - Obtained:
  Average ROUGE-1: 0.09003837600972746, ROUGE-2: 0.0744632886045723, ROUGE-L: 0.09003837600972746

## 3. QA Accuracy:
  # - Why:
  Evaluates the accuracy of the generated answers to questions compared to expected answers in the dataset.
  # - Usage:
  Implemented using the `deepset/roberta-base-squad2` model via the `qa_pipeline`, checking if the chatbot's responses match the expected answers.
  # - Obtained:
  QA Accuracy: 28.57142857142857%
  
  
### Accuarcy Screenshot:
![image](https://github.com/evapatel1654/Eva_Patel_RAG_Chatbot/assets/133888581/89d9ca46-eaca-4b7a-bda4-2db04d85af3b)


### Attempts to Improve Accuracy

# 1. Model Selection:
   - Chose state-of-the-art pre-trained models (`facebook/bart-large-cnn`, `valhalla/t5-base-qg-hl`, `deepset/roberta-base-squad2`) for summarization, question generation, and question answering to leverage their capabilities in natural language processing tasks.

# 2. Chunking and Processing:
   - Implemented functions (`split_text`, `split_text_for_summarization`) to handle large volumes of text by chunking and processing in manageable sizes, optimizing model performance and accuracy.

# 3. Fine-Tuning and Hyperparameter Tuning:
   - While this specific implementation uses pre-trained models, fine-tuning on domain-specific data or adjusting hyperparameters such as max sequence lengths in summarization or QA generation could further enhance accuracy.

# 4. Evaluation and Iteration:
   - Continuously evaluated the performance using chosen metrics (BLEU, ROUGE, QA Accuracy) to identify areas for improvement. Iterative adjustments could include refining text preprocessing, experimenting with different models, or incorporating ensemble techniques.

### Conclusion

The process involved systematically processing PDF content, summarizing it, generating questions, and evaluating responses using robust NLP models and metrics. By leveraging these steps and metrics, the approach aims to ensure the chatbot provides accurate and relevant information based on the content of the PDF document, enhancing its utility and reliability in providing answers and summaries. To improve more accuary we need to divided data which is extracted in smaller chunks so that we can improve accuarcy.
