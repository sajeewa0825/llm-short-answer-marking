# Data licence

## LLM marks, rationales and prompts (`marks/`, `prompts/`)

Copyright (c) 2026 the authors listed in `CITATION.cff`.
Licensed under the Creative Commons Attribution 4.0 International licence (CC BY 4.0):
https://creativecommons.org/licenses/by/4.0/

You may share and adapt this material for any purpose, provided that you cite the paper and this repository (see `CITATION.cff`).

## Questions, reference answers, student answers and human scores (`data/answers.csv`)

These columns come from two public datasets and remain under the terms set by their original authors. Cite the original papers when you use them.

- **SAF** (`dataset = saf`): Filighera, A., Parihar, S., Steuer, T., Meuser, T., Ochs, S.: Your answer is incorrect... Would you like to know why? Introducing a bilingual short answer feedback dataset. In: Proc. ACL 2022, pp. 8577–8591 (2022). Distributed under CC BY 4.0.
- **Mohler** (`dataset = mohler`): Mohler, M., Bunescu, R., Mihalcea, R.: Learning to grade short answer questions using semantic similarity measures and dependency graph alignments. In: Proc. ACL-HLT 2011, pp. 752–762 (2011). Redistributed for research use with attribution; refer to the original release for its terms.

The derived columns added in this repository (`score_norm`, `score_band`, `answer_words`, `role`, `pilot`) are released under CC BY 4.0.
