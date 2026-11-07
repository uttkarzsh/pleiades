# Pleiades

pleiades is my journey into inference engineering. i will start from the very basics and do things week by week.
the goal is to build a small llm inference engine by hand around **qwen3-0.6b**, on a macbook air m2 (16 gb). every op is written from scratch and checked against hugging face transformers, which is used only as a reference.

## ground rules

- correctness first: every piece is verified against the reference before moving on
- measure everything: prefill and decode tok/s, compared against the theoretical ceiling
- one change at a time, one entry in the benchmark log per change

## week 1 plan

| day | focus | what i'll do | done when |
| --- | --- | --- | --- |
| 1 | setup and hand math | set up the environment, download the model, work out parameter count, kv cache size and the decode ceiling on paper, do attention by hand, load the weights and verify rmsnorm | param count matches my math, rmsnorm matches the reference |
| 2 | attention block | q/k/v projections, qwen3 q/k norms, rope, grouped-query attention, causal mask, output projection for layer 0 | layer 0 attention matches the reference |
| 3 | full forward pass | swiglu mlp, residuals, all 28 layers, final norm, tied lm head | full logits match on several prompts |
| 4 | generation | greedy decoding, then temperature, top-k and top-p sampling | greedy output is identical to the reference |
| 5 | kv cache | split into prefill and decode, cache k and v per layer, attend over the cache | cached and uncached outputs are identical |
| 6 | measurement | time prefill and decode separately, compare with the ~80 tok/s ceiling, move to mps in fp16, baseline against mlx-lm or llama.cpp | i can explain the gap between my engine, the baseline and the ceiling |
| 7 | first quantization | per-row int8 weight-only quantization, perplexity and speed comparison against fp32, short retro, skim nano-vllm | int8 quality and speed numbers recorded and explained |


## week 2 overview: finishing the single-request engine

- int4 weight-only quantization with group-wise scales, compared against int8 and fp16 on perplexity and speed
- per-layer profiling to find where the time actually goes
- port the decode loop to a systems language (c or rust) with my own cpu matmul
- optimize that matmul with cache blocking, neon simd and threads, logging each step

## week 3 overview: serving

- batched decode with per-sequence kv caches
- a simple continuous batching scheduler (waiting queue, running batch, admit and retire each step)
- a paged kv cache with a block table, in the style of pagedattention
- prefix caching if time allows
- throughput vs latency measurements as batch size grows, read alongside the nano-vllm source

## benchmark log

| date | change | prefill tok/s | decode tok/s | % of ceiling | notes |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |
