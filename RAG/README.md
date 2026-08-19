# RAG Knowledge Base

This directory contains the structured technical knowledge base used by the Retrieval-Augmented Generation (RAG) component of the diagnostic framework.

The knowledge base was developed to provide domain-specific grounding for the generation of technical maintenance reports related to induction-motor operating conditions and faults.

## File

The knowledge base used in the experiments is provided as `RAG_motores_eletricos.json`.

The original structure of the experimental knowledge base has been preserved to maintain consistency with the RAG implementation reported in the study.

## Covered Operating Conditions

The knowledge base contains structured technical information for six operating conditions:

- Normal Operation
- Bearing Failure
- Blocked Rotor
- Phase Loss
- Overheating
- Ventilation Defect

## Knowledge Structure

Fault-specific entries contain structured information that may include fault descriptions, physical mechanisms, probable root causes, observable evidence, system effects, maintenance actions, diagnostic checks, qualitative risk levels, standards and technical guidelines, semantic retrieval terms, and reasoning cues.

This organization was designed to provide the language models with technical context relevant to the fault condition identified by the CNN.

## Retrieval

The RAG framework performs semantic retrieval over the structured technical knowledge base.

The experimental implementation uses MPNet-based sentence embeddings to represent the diagnostic query and available knowledge entries in a shared semantic space. For each diagnostic case, the retrieval procedure selects the most relevant technical information according to semantic similarity. The retrieved context is then incorporated into the prompt supplied to the corresponding Small Language Model.

The experimental configuration uses `top_k = 3`.

The exact retrieval implementation, prompt construction, and model-specific execution procedures are preserved in the notebooks available in the repository.

## Diagnostic Input

The retrieval process is conditioned by diagnostic information originating from the CNN stage, including the predicted fault class and associated confidence information.

```text
CNN Prediction
      |
      v
Fault Class + Confidence
      |
      v
Semantic Retrieval
      |
      v
Top-k Technical Context
      |
      v
Prompt Construction
      |
      v
Small Language Model
      |
      v
Diagnostic Report
```

## Technical Grounding

The knowledge base was constructed from domain-specific technical information related to induction-motor operation, fault diagnosis, inspection, and maintenance.

The structured entries reference relevant technical sources, including manufacturer documentation and internationally recognized standards where applicable. These references are used to provide technical grounding and contextual guidance for the diagnostic reports.

## Standards and Manufacturer Documentation

The knowledge base contains references to technical standards and manufacturer documentation relevant to induction-motor operation and maintenance.

These documents are referenced for grounding purposes. The repository does not distribute the original standards or manufacturer documents. The knowledge base contains structured and summarized technical information rather than full reproductions of the referenced documents.

Users requiring the complete original standards or manuals should obtain them directly from the corresponding publishers, standards organizations, or manufacturers.

## Use of Standards in Generated Reports

The RAG configuration was designed to treat standards as technical references and guidelines rather than as sources for unrestricted verbatim reproduction.

The knowledge-base configuration therefore instructs the generation framework to mention standards as references or guidelines and not to reproduce protected content as direct quotations unless authorized.

## Semantic Retrieval Information

The JSON knowledge base also includes retrieval-oriented information such as semantic keywords and reasoning cues. These fields support the identification of technically relevant entries for each diagnostic condition and help associate CNN-derived diagnostic information with appropriate maintenance knowledge.

## Reproducibility

`RAG_motores_eletricos.json` is the knowledge-base file used by the experimental notebooks included in this repository.

The file is provided in its experimental form to preserve methodological traceability. Users may modify, extend, or replace the knowledge base for other machines, fault classes, maintenance environments, or industrial applications. Such modifications represent adaptations beyond the experimental configuration reported in the associated study.

## Related Repository Components

The individual SLM experiments using this knowledge base are available in `../SLM/`.

The controlled RAG condition used in the ablation study is available in `../Ablation/Framework_FINAL_TODOS_MODELOS_RAG_PADRONIZADO_v4_AUDITADO_REV1.ipynb`.

The parameter-only condition used for comparison is available in `../Ablation/Framework_SEM_RAG_TODOS_MODELOS_INFERENCIA_ENXUTO_v2.ipynb`.

The final RAG generation records are available in `../Results/SLM_RAG/`.

## Citation

If this knowledge base or its associated RAG methodology is used in academic work, please cite the corresponding article.

Citation information will be added after publication.
