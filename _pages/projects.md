---
layout: single
title: "Course Projects"
permalink: /projects/
author_profile: true
---

<script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
<script>mermaid.initialize({startOnLoad:true, theme:'neutral'});</script>

<!-- A curated portfolio of NLP and machine learning projects completed as part of graduate coursework. Each project explores a different facet of text analytics; from unsupervised phrase mining to transformer-based classification and abstractive summarization. Descriptions are generalized and omit proprietary dataset details. -->

---

## MPMalGen: Multi-Platform LLM-Powered Malware Variant Generation

A framework extending LLM-based malware variant generation to multi-platform environments (Windows & Android), featuring platform-specific transformation strategies and automated validation pipelines.

**Highlights**
- Extended the LLMalMorph framework with multi-platform support for Windows (C/C++) and Android (Java/Kotlin/Smali) malware sources.
- Introduced Android-specific prompt engineering strategies preserving component lifecycles, manifest registrations, and permission models.
- Integrated DeepSeek-Coder-v2-16B-Instruct for superior code transformation; implemented automated syntactic validation and error recovery pipelines.
- Evaluated on 6 Windows malware families and Android samples; achieved improved AV evasion rates via VirusTotal and Hybrid Analysis.

**System Architecture**

<div class="mermaid">
flowchart TD
    A[("🗂️ Malware Source<br/>(C/C++/Java/Smali/APK)")] --> B["Multi-Platform Ingestion"]
    B --> C["Platform-Aware AST Parser"]
    C --> D["Function Extraction &<br/>Metadata Cache"]
    D --> E["Platform-Specific Prompt<br/>Engineering + Strategy"]
    E --> F["🤖 DeepSeek-Coder-v2<br/>LLM Transformation"]
    F --> G["Syntactic Validation &<br/>Error Recovery"]
    G --> H{"Compile<br/>Success?"}
    H -->|No| G
    H -->|Yes| I["Built-in Recompiler<br/>(EXE / APK)"]
    I --> J[("📊 AV Evasion Evaluation<br/>(VirusTotal)")]

    style A fill:#e1f5fe
    style F fill:#fff3e0
    style J fill:#e8f5e9
</div>

**Report**: [Download PDF](/files/projects/mmislam_Final_project_report.pdf)  
**Presentation**: [Watch Video](/files/projects/mmislam_Final_Presentation.mp4)

---

## Abstractive Title Generation

Sequence-to-sequence models for generating concise paper titles from scientific abstracts, comparing model capacity and instruction tuning.

**Highlights**
- Fine-tuned T5-small, T5-base, and Flan-T5-base with beam search (beams=4), no-repeat bigrams, and early stopping.
- T5-base improved BLEU by ~19% and ROUGE-L by ~8% over T5-small; Flan-T5 achieved the highest test ROUGE-L (0.439).
- Conducted hyperparameter sweeps on epochs and learning rate; identified 5 epochs and lr = 5×10⁻⁴ as optimal for the mid-sized corpus.

**System Architecture**

<div class="mermaid">
flowchart TD
    A[("📄 Abstract Text")] --> B["Prompt Template"]
    B --> C["T5 / Flan-T5 Encoder"]
    C --> D["Encoder Hidden States"]
    D --> E["T5 Decoder<br/>(Beam Search)"]
    E --> F["Generated Title Tokens"]
    F --> G["Detokenizer"]
    G --> H[("📝 Predicted Title")]
    H --> I["BLEU / ROUGE<br/>Evaluation"]

    style A fill:#e1f5fe
    style C fill:#fff3e0
    style H fill:#e8f5e9
</div>

**Report**: [Download PDF](/files/projects/Project_3_report_mmislam.pdf)

---

## Biomedical Document Classification

Binary classification of scientific abstracts using transformer models, addressing severe class imbalance (~10:1) and train-test distribution mismatch.

**Highlights**
- Fine-tuned BERT, DeBERTa-v3, and PubMedBERT with focal loss and weighted sampling to handle class imbalance.
- Implemented curriculum learning by ranking samples by prediction uncertainty and training on progressively harder subsets.
- Ensembled DeBERTa and PubMedBERT via probability averaging; achieved max F1 ≈ 0.88 and F1 ≈ 0.87 on the public and private leaderboards respectively in the corresponding Kagle competition.

**System Architecture**

<div class="mermaid">
flowchart TD
    A[("📄 Title + Abstract")] --> B["Prompt Formatter"]
    B --> C["Tokenizer<br/>(512 tokens)"]
    C --> D["BERT Baseline"]
    C --> E["DeBERTa-v3<br/>+ Focal Loss"]
    C --> F["PubMedBERT<br/>+ Curriculum"]
    D --> G["Logits"]
    E --> H["Logits"]
    F --> I["Logits"]
    G --> J["Probability Averaging<br/>Ensemble"]
    H --> J
    I --> J
    J --> K["Threshold Tuning"]
    K --> L[("🎯 Final Prediction")]

    style A fill:#e1f5fe
    style D fill:#fff3e0
    style E fill:#fff3e0
    style F fill:#fff3e0
    style L fill:#e8f5e9
</div>

**Report**: [Download PDF](/files/projects/Project_2_report_mmislam.pdf)

---

## Phrase Mining & Word Embeddings 

An end-to-end pipeline for extracting and evaluating multi-word phrases from a large biomedical corpus, then retraining Word2Vec embeddings on the phrase-tagged text.

**Highlights**
- Compared three phrase-mining strategies: naive greedy segmentation, a statistical mixed-method approach (PMI + TF-IDF + spaCy noun chunks), and a BioBERT-based semantic clustering method.
- Trained Word2Vec (skip-gram) before and after phrase tagging; observed tighter semantic clusters and higher cosine similarities for domain-specific terms after tagging.
- Validated extracted phrases against a curated phrase dictionary; the mixed-method approach achieved the best balance of coverage and precision.

**System Architecture**

<div class="mermaid">
flowchart TD
    A[("📚 Raw Corpus")] --> B["Tokenizer / Cleaner"]
    B --> C["N-gram Generator"]
    C --> D["Naive Greedy"]
    C --> E["PMI + TF-IDF + NP"]
    C --> F["BioBERT Embeddings"]
    D --> G["Phrase Candidates"]
    E --> H["Phrase Candidates"]
    F --> I["Semantic Clusters"]
    G --> J["Merge & Rank"]
    H --> J
    I --> J
    J --> K["Phrase-Tagged Corpus"]
    K --> L["Word2Vec Retraining<br/>(Skip-gram)"]
    L --> M[("📊 Similarity Evaluation")]

    style A fill:#e1f5fe
    style D fill:#fff3e0
    style E fill:#fff3e0
    style F fill:#fff3e0
    style M fill:#e8f5e9
</div>

**Report**: [Download PDF](/files/projects/Project_1_report_mmislam.pdf)  
**Presentation**: [Watch Video](/files/projects/mmislam_Final_Presentation.mp4)
