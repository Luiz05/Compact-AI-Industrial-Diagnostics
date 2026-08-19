# Designing Compact AI Systems for Industrial Diagnostics through Modular Lightweight Intelligence

This repository contains the experimental implementation, structured knowledge resources, evaluation procedures, and result files associated with the study:

**Designing Compact AI Systems for Industrial Diagnostics through Modular Lightweight Intelligence**

The repository was organized to support transparency, traceability, and reproducibility of the experiments reported in the manuscript.

---

## Overview

The proposed framework investigates the use of compact artificial intelligence components for industrial fault diagnosis and technical report generation.

The experimental pipeline combines:

1. infrared thermography-based fault classification using a lightweight convolutional neural network;
2. Retrieval-Augmented Generation (RAG) based on structured maintenance knowledge;
3. Small Language Models (SLMs) for diagnostic report generation;
4. automatic evaluation of semantic, lexical, grounding, generative, and computational-efficiency characteristics;
5. a paired ablation study comparing RAG-based generation with a parameter-only configuration.

The general workflow is:

```text
Infrared Thermography
        |
        v
ShuffleNet V2 CNN
        |
        v
Fault Class + Confidence
        |
        v
Retrieval-Augmented Generation
        |
        v
Small Language Model
        |
        v
Structured Diagnostic Report
```

---

## Evaluated Language Models

The following Small Language Models were evaluated:

- TinyLlama-1.1B-Chat
- Qwen2.5-3B-Instruct
- Mistral-7B-Instruct
- Zephyr-7B-beta

The notebooks available in this repository correspond to the experimental configurations used in the study.

---

## Fault Classes

The diagnostic framework considers six operating conditions:

- Normal Operation
- Bearing Failure
- Blocked Rotor
- Phase Loss
- Overheating
- Ventilation Defect

---

## Repository Structure

```text
Compact_AI_Industrial_Diagnostic/
|
|-- README.md
|-- LICENSE
|-- requirements.txt
|-- .gitignore
|
|-- CNN/
|   |-- ShuffleNet_5Fold_CNN_RAG_VERSAOFINAL.ipynb
|   `-- Results_classification/
|       |-- five_fold_results.csv
|       |-- holdout_test_predictions.csv
|       |-- fold_1_validation_predictions.csv
|       |-- fold_2_validation_predictions.csv
|       |-- fold_3_validation_predictions.csv
|       |-- fold_4_validation_predictions.csv
|       `-- fold_5_validation_predictions.csv
|
|-- SLM/
|   |-- Framework_FINAL_TinyLamma_PADRONIZADO_v3_CNN_LIMITADO.ipynb
|   |-- Framework_FINAL_QWEN_PADRONIZADO_v3_CNN_LIMITADO.ipynb
|   |-- Framework_FINAL_mistral_PADRONIZADO_v3_CNN_LIMITADO_LOCAL_SNAPSHOT.ipynb
|   `-- Framework_FINAL_zephyr_PADRONIZADO_v3_CNN_LIMITADO_LOCAL_SNAPSHOT.ipynb
|
|-- RAG/
|   |-- RAG_motores_eletricos.json
|   `-- README.md
|
|-- Evaluations_CODE/
|   `-- evaluate_slm_framework_IEEE_v5_CORRIGIDO_METRICAS.ipynb
|
|-- Ablation/
|   |-- Framework_FINAL_TODOS_MODELOS_RAG_PADRONIZADO_v4_AUDITADO_REV1.ipynb
|   |-- Framework_SEM_RAG_TODOS_MODELOS_INFERENCIA_ENXUTO_v2.ipynb
|   `-- Framework_ANALISE_ABLACAO_RAG_vs_SEM_RAG_v1.ipynb
|
`-- Results/
    |-- SLM_RAG/
    |   |-- slm_rag_results_tinyllama_final.csv
    |   |-- slm_rag_results_qwen_final.csv
    |   |-- slm_rag_results_mistral_final.csv
    |   `-- slm_rag_results_zephyr_final.csv
    |
    |-- Evaluation/
    |   `-- results_with_all_metrics.csv
    |
    `-- Ablation/
        `-- without_rag/
            |-- all_generations_without_rag.csv
            |-- generation_tinyllama_without_rag.csv
            |-- generation_qwen_without_rag.csv
            |-- generation_mistral_without_rag.csv
            |-- generation_zephyr_without_rag.csv
            |-- without_rag_operational_summary.csv
            `-- manifest_without_rag.json
```

---

## CNN Fault Classification

The visual diagnostic stage uses ShuffleNet V2 for thermographic fault classification.

The CNN evaluation includes a 5-fold cross-validation procedure, fold-level validation predictions, an independent holdout test set, class probabilities, predicted labels, and confidence scores.

The folder `CNN/Results_classification/` contains the prediction files associated with these experiments. The file `holdout_test_predictions.csv` is also used as the diagnostic input source for the subsequent language-model experiments.

---

## Retrieval-Augmented Generation

The RAG component uses a structured technical knowledge base designed for induction-motor fault diagnosis and maintenance support.

The file `RAG/RAG_motores_eletricos.json` contains structured information related to fault descriptions, physical mechanisms, probable root causes, observable evidence, system effects, maintenance actions, diagnostic checks, qualitative risk levels, technical standards and guidelines, and semantic retrieval information.

Additional information about the knowledge base is provided in `RAG/README.md`.

---

## SLM Experiments

The directory `SLM/` contains the individual experimental notebooks used for the four evaluated language models.

Each notebook preserves the experimental implementation used in the study, including model loading, prompt construction, RAG retrieval, generation configuration, and result export.

The notebooks are intentionally provided in their experimental form rather than being refactored into a generalized software package. This decision preserves consistency with the experiments reported in the manuscript.

---

## Experimental Environment

The experiments were primarily executed in Google Colab using an NVIDIA Tesla T4 GPU.

Library versions and model-specific configurations are preserved in the experimental notebooks. Some models require Hugging Face authentication. In these cases, the notebooks expect the user to provide the corresponding authentication token through the execution environment rather than storing credentials directly in the source code.

Users executing the notebooks in different environments may need to adapt model paths, storage locations, Hugging Face authentication, GPU configuration, package installation, and available memory. Such adaptations are left to the user and are not part of the original experimental protocol.

---

## Evaluation

The evaluation pipeline is provided in `Evaluations_CODE/evaluate_slm_framework_IEEE_v5_CORRIGIDO_METRICAS.ipynb`.

The framework evaluates generated reports using complementary metrics related to semantic similarity, lexical similarity, contextual similarity, grounding, novelty, generation quality, and computational efficiency.

The consolidated evaluated results are available in `Results/Evaluation/results_with_all_metrics.csv`.

---

## Ablation Study

The repository includes the experimental workflow used for the paired RAG ablation study.

The RAG condition is implemented in `Ablation/Framework_FINAL_TODOS_MODELOS_RAG_PADRONIZADO_v4_AUDITADO_REV1.ipynb`.

The parameter-only condition without retrieval is implemented in `Ablation/Framework_SEM_RAG_TODOS_MODELOS_INFERENCIA_ENXUTO_v2.ipynb`.

The statistical comparison is implemented in `Ablation/Framework_ANALISE_ABLACAO_RAG_vs_SEM_RAG_v1.ipynb`.

The ablation study compares paired model-fault combinations under matched experimental conditions, with the availability of retrieved technical context being the controlled difference of interest.

The analysis includes:

- Cosine Similarity;
- ROUGE-L;
- BERTScore;
- paired Wilcoxon signed-rank tests;
- bootstrap confidence intervals;
- Holm correction for multiple comparisons;
- rank-biserial effect-size estimation.

The parameter-only generation results are available under `Results/Ablation/without_rag/`.

---

## Experimental Results

The folder `Results/SLM_RAG/` contains the final generation records for the four evaluated SLMs under the RAG configuration.

These files preserve experimental information such as CNN diagnostic input, confidence scores, retrieved context, prompt content, generated diagnostic reports, token usage, latency, memory usage, generation configuration, and execution metadata.

---

## Dataset

The thermographic dataset used for CNN development and evaluation is associated with the previous study:

**A Multimodal Model for Fault Diagnosis in Induction Motors Using Thermal Images and Large Language Models**

The dataset is publicly available at:

https://github.com/jorge-canuto/Induction_motors_fault_data

The present repository does not duplicate the full thermographic image dataset.

---

## Reproducibility Notes

The source code and notebooks provided in this repository correspond to the experimental implementation used in the study.

The original experimental configurations, prompts, model settings, evaluation procedures, and result files have been preserved whenever possible.

The repository is intended primarily to support transparency, methodological traceability, inspection of the experimental workflow, and replication of the reported procedures. It is not intended to provide a hardware-independent or plug-and-play software package.

Adaptations required for different GPU environments, operating systems, library versions, storage structures, or model deployments are the responsibility of the user.

---

## Knowledge-Base Usage

The structured RAG knowledge base contains summarized and organized technical information derived from maintenance literature, manufacturer documentation, and technical standards.

Technical standards and manufacturer documents are referenced for grounding purposes and are not reproduced in full. Users requiring the original standards or manuals should obtain them from their respective publishers or manufacturers.

---

## Citation

If you use this repository, the experimental framework, or the associated resources in academic work, please cite the corresponding article.

Citation information will be added after publication.

---

## License

See the `LICENSE` file for repository licensing information.

---

## Contact

Luiz Fillipe Dahmer dos Santos  
Graduate Program in Computer Science  
Department of Informatics  
State University of Maringa (UEM)  
Brazil
