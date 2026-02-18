# Writing an LLM-Engineering Improvement Paper

[TEXT — no multimodal needed]

## Key Structure: The Engineering Recipe

An LLM engineering paper (e.g., optimizations, systems, scaling) typically follows this flow:

1.  **Metric-Driven Problem Statement**: Clearly define the limitation or bottleneck in current systems.
    *   *Bad:* "Training is slow."
    *   *Good:* "Training 175B models requires 3 months on 1024 GPUs, limiting iteration speed."

2.  **The Proposed System/Method**: Often structured as improvements in multiple aspects.
    *   Explain the *design space* and why you chose this specific point.
    *   Visuals are critical: Show the pipeline, data flow, or memory layout.

3.  **Demonstrating Improvements**:
    *   **Scale**: Show it works at the target scale (not just MNIST).
    *   **Efficiency**: Report wall-clock time, memory usage, and throughput (tokens/sec).
    *   **Quality**: Prove that efficiency didn't hurt performance (perplexity, downstream tasks).

## Common Pitfalls

-   **Unfair Baselines**: Comparing optimized code against unoptimized baselines. Ensure baselines use similar constraints (e.g., same batch size, hardware).
-   **Lack of Ablation**: "Our system is 5x faster." *Why?* Is it the custom kernel, the better data loader, or the hardware upgrade? Break down the gains.
-   **Data Contamination**: For engineering papers that also claim model quality improvements, ensure evaluation data wasn't seen during training.

## Example of High-Quality Engineering Analysis

**FlashAttention (Dao et al., 2022)**
-   **Problem**: Attention is quadratic in sequence length and memory bandwidth bound.
-   **Insight**: IO-aware tiling to reduce memory access.
-   **Evaluation**: Shows speedup *and* memory reduction, allowing longer context lengths.

## Improvement Prompting Template

```
Your task is to critique and improve the following LLM Engineering paper section:
<<section_content>>

Here is the guidance for LLM Engineering papers:
- **Measurable Problem**: Is the bottleneck quantified?
- **Ablation**: Are the sources of improvement isolated?
- **Scale**: Is the evaluation realistic for the claimed contribution?
- **Baselines**: Are comparisons fair?

Critique the section based on these criteria.
Suggest improvements, specifically asking for missing metrics or ablations if applicable.
```
