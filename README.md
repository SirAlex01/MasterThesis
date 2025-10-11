# Linear B → Ancient Greek and English: translation with LLMs

> Code and data for my thesis on translating Linear B administrative tablets into Ancient Greek (and English) using a hybrid pipeline that combines cognate matching, auxiliary classifiers, logogram handling, and an LLMs (Gemini 2.5 Flash) through prompt engineering.

## 📄 Abstract

This project investigates whether large language models can reliably translate Linear B. I build a pipeline with: (i) vocabulary extraction and brute-force cognate mining from, (ii) a generative *NeuroDecipher*-style cognate framework from Jiaming Luo, (iii) auxiliary SVM classifiers for grammatical signals (part of speech, noun type, inflection), (iv) logogram disambiguation, and (v) an LLM prompt that synthesizes all signals to produce parallel Ancient Greek + English translations. On 12 curated tablets, English translations are strong and Ancient Greek reconstructions are close (though often retaining Mycenaean features). I report BLEU/METEOR/ROUGE/TER/CHRF/WER and analyze common error modes (cognate drift, case/number misreadings, misclassified locatives, logograms). The approach already yields dependable first-pass drafts and clear paths for normalization and scaling.

---

---

## 🔗 Linked index of key files (click to open)

| Artifact | Path | Notes |
|---|---|---|
| Thesis (PDF) | [`thesis.pdf`](./thesis.pdf) | Full write-up of the project |
| Translation outputs | [`code/translation_answers.csv`](./code/translation_answers.csv) | LLM + pipeline translations (Greek/English) |
| Cognate dataset (final) | [`code/cognates_final.cog`](./code/cognates_final.cog) | Aggregated cognate matches used by the pipeline |
| Luo original cognates | [`code/transliterated_linear_b-greek_original.cog`](./code/transliterated_linear_b-greek_original.cog) | Original resource from Luo (baseline) |
| Brute-force cognates (script) | [`code/brute_cognates_dataset.py`](./code/brute_cognates_dataset.py) | Exhaustive search procedure |
| Aux classifier dataset (CSV) | [`code/classifiers_dataset.csv`](./code/classifiers_dataset.csv) | Labels for part of speech / noun type / inflection |
| Aux classifier dataset (script) | [`code/classifiers_dataset.py`](./code/classifiers_dataset.py) | Generates the auxiliary dataset |
| Linear B lexicon (Ventris–Chadwick notes) | [`code/Linear B Lexicon.csv`](<./code/Linear%20B%20Lexicon.csv>) | Reference lexicon |
| LB signs standardizer | [`code/LB_signs_standardizer.py`](./code/LB_signs_standardizer.py) | Normalizes Linear B signs |
| LB web-scraper (docs) | [`code/LB-webscrape-documents.py`](./code/LB-webscrape-documents.py) | Collects Linear B texts |
| LA web-scraper (docs) | [`code/LA-webscrape-documents.py`](./code/LA-webscrape-documents.py) | Collects Linear A texts |
| LA web-scraper (sites) | [`code/LA_webscrape_sites.py`](./code/LA_webscrape_sites.py) | Collects site-level info |
| LIBER documents (LB) | [`code/LIBER_documents.csv`](./code/LIBER_documents.csv) | LB document metadata |
| Sequences — Linear B | [`code/sequences_LB.csv`](./code/sequences_LB.csv) | Sequence-level LB data |
| Sequences — Linear A | [`code/sequences.csv`](./code/sequences.csv) | Sequence-level LA data |
| Signs — Linear B | [`code/signs_LB.csv`](./code/signs_LB.csv) | Sign-level LB data |
| Signs — Linear A | [`code/signs.csv`](./code/signs.csv) | Sign-level LA data |
| Sites — Linear A | [`code/sites_data.csv`](./code/sites_data.csv) | LA document-level info |
| Notebook (end-to-end) | [`code/LALB_notebook.ipynb`](./code/LALB_notebook.ipynb) | Cognate model, classifiers, pipeline, MT metrics |
| Luo metrics extractor | [`code/luo_metrics_extractor`](./code/luo_metrics_extractor) | Tools to parse Luo logs/plots |
| Odyssey text (scraped) | [`code/gr_eng_text.csv`](./code/gr_eng_text.csv) | Odyssey text |
| Iliad text (scraped) | [`code/ILIADKEY.csv`](./code/ILIADKEY.csv) | Iliad text |
| Latinized Homeric lexicon | [`code/latinized_homeric_greek_words.tsv`](./code/latinized_homeric_greek_words.tsv) | Preprocessed Homer data for cognates extraction |
| Additional lexicon scripts | [`code/additional_lexicon`](./code/additional_lexicon) | Tselentis' lexicon extraction helpers |

---

## ✅ Results

- **Thesis PDF:** [`thesis.pdf`](./thesis.pdf)  
- **Translation outputs (CSV):** [`code/translation_answers.csv`](./code/translation_answers.csv)  

[comment]: <> (- **Presentation**: [`presentation.pdf`] etc.)


For qualitative analysis, see the Results and Error Analysis chapters in the PDF.
The following table presents the results of the translations compared with my corrected versions of the 12 evaluated Linear B documents.

| Metric     | Ancient Greek | English |
| ---------- | ------------: | ------: |
| BLEU       |         0.641 |   0.768 |
| METEOR     |         0.813 |   0.880 |
| ROUGE-1 F1 |         0.818 |   0.903 |
| ROUGE-2 F1 |         0.698 |   0.837 |
| ROUGE-L F1 |         0.815 |   0.899 |
| TER        |         0.187 |   0.158 |
| CHRF       |         0.836 |   0.848 |
| WER        |         0.189 |   0.161 |
