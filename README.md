# Election Submissions Text Mining

A natural language processing pipeline over **299 public submissions** to the Australian Parliament's Joint Standing Committee on Electoral Matters inquiry into the 2025 federal election. It extracts text from PDFs, cleans and analyses it, and uses topic modelling to surface the main themes.

## What it does

| Step | Method |
|---|---|
| Text extraction | `pdfplumber` for PDFs, with a **Tesseract OCR fallback** for scanned pages |
| Preprocessing | NLTK tokenisation, stop-word and non-alphabetic token removal, stemming, and removal of repeated document headers |
| Exploration | Document-length distribution, word frequencies, a word cloud, top bigrams and trigrams |
| Term weighting | TF-IDF to rank the most distinctive words across the corpus |
| Topic modelling | **LDA (Gensim, 5 topics)** with an interactive pyLDAvis visualisation |

## Findings

Submissions focus mostly on voter and volunteer experience at polling places. The topic model and word statistics surface themes around **polling logistics, pre-poll voting procedures and campaign volunteer conduct**, alongside more constitutional topics such as Senate and House terms and the electoral commission's role.

## Run

The notebook was written for Google Colab and reads the submission PDFs from a Google Drive folder. To run it, download the submissions from the [inquiry page on aph.gov.au](https://www.aph.gov.au/Parliamentary_Business/Committees/Joint/Electoral_Matters), put them in a folder, and change the `folder` path in the notebook.

```
pip install pdfplumber pytesseract nltk gensim pyLDAvis wordcloud scikit-learn pandas matplotlib
```

Tesseract itself must also be installed for the OCR fallback.

## Data

The submissions are not included in this repository. They are published on the Parliament of Australia website. The notebook output has been cleaned so that no submitter names or submission text appear.

## Limitations

- The number of topics (5) was set by hand; topics were judged by reading their top words, with no coherence score.
- OCR quality varies on scanned pages, and noisy extraction affects word counts.
- Stemming makes some terms hard to read (for example "elector" or "feder").
- LDA is unsupervised, so the topic labels are my interpretation, not ground truth.
