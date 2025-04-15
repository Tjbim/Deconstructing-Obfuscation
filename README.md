# LLM Assembly Deobfuscation Study

This repository contains the data and dialogues accompanying the paper: "Evaluating Large Language Models for Assembly Code Deobfuscation" (April 2025).

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)

## Overview

We tested seven state-of-the-art Large Language Models (as of April 2025) on their ability to deobfuscate assembly code protected with various obfuscation techniques. This repository contains the original obfuscated assembly code samples and the complete dialogues with each model.

## Repository Structure

```
/
├── original_code/                      # Original disassembled code samples
│   ├── code_unobf.capstone             # Baseline with no obfuscation
│   ├── code_sub.capstone               # Instruction substitution
│   ├── code_fla.capstone               # Control flow flattening
│   ├── code_bcf.capstone               # Bogus control flow
│   ├── code_all.capstone               # All techniques combined                  
│   └── ollvm_flags.md                  # OLLVM compilation flags used
│
├── dialogues/                          # LLM dialogues by obfuscation technique
│   ├── bogus_control_flow/             # BCF obfuscation dialogues
│   │   ├── gpt_4o.md
│   │   ├── gpt_4.5.md
│   │   ├── gpt_o1-pro.md
│   │   ├── gpt_3o_mini.md
│   │   ├── deepseek_r1.md
│   │   └── grok_3.md
│   │
│   ├── instruction_substitution/       # IS obfuscation dialogues
│   │   ├── claude_3.7_sonnet.md
│   │   ├── gpt_4o.md
│   │   ├── gpt_4.5.md
│   │   ├── deepseek_r1.md
│   │   └── grok_3.md
│   │
│   ├── control_flow_flattening/        # CFF obfuscation dialogues
│   │   ├── claude_3.7_sonnet.md
│   │   ├── gpt_4o.md
│   │   ├── deepseek_r1.md
│   │   └── grok_2.md
│   │
│   └── combined_techniques/            # All obfuscation techniques combined
│       ├── claude_3.7_sonnet.md
│       ├── gpt_4.5.md
│       ├── gpt_o1-pro.md
│       ├── deepseek_r1.md
│       └── grok_3.md
│
│
└── paper_reference.md                  # Summary and connection to paper sections
```

## Models Evaluated

- **GPT-4o** (OpenAI)
- **GPT-3o Mini High** (OpenAI)
- **GPT-4.5 Preview** (OpenAI)
- **GPT-o1-pro** (OpenAI)
- **Claude 3.7 Sonnet** (Anthropic)
- **DeepSeek R1** (DeepSeek AI)
- **GROK 3** (xAI)
- **GROK 2** (xAI)

## Dialogue Format

Each dialogue file follows a consistent format:

```markdown
# [Model Name]

## Dialogue Transcript

### Human:
[Prompt text]

### [Model]:
[Model response]

### Human:
[Follow-up prompt]

...
```

## Obfuscation Techniques

1. **Bogus Control Flow (BCF)**: Compiled with flags: `-mllvm -bcf -mllvm -boguscf-prob=100 -mllvm -boguscf-loop=1`
2. **Instruction Substitution (IS)**: Compiled with flags: `-mllvm -sub`
3. **Control Flow Flattening (CFF)**: Compiled with flags: `-mllvm -fla -mllvm -perFLA=100`
4. **Combined Techniques**: Compiled with all flags: `-mllvm -sub -mllvm -fla -mllvm -perFLA=100 -mllvm -bcf -mllvm -boguscf-prob=100 -mllvm -boguscf-loop=1`

## How to Cite This Repository

If you use these materials in your research, please cite:

```bibtex
@misc{llm_deobfuscation_2025,
  author = {[Author Names]},
  title = {Evaluating Large Language Models for Assembly Code Deobfuscation},
  year = {2025},
  publisher = {GitHub/Zenodo},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/[username]/llm-deobfuscation}},
  doi = {10.5281/zenodo.XXXXXXX}
}
```

## License

The dialogue transcripts and analysis are licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The code samples are provided for research purposes only.

## Contact

For questions regarding this data or the accompanying paper, please contact [anton.tkachenko@promon.no].
