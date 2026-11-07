# week 1: the hand-built engine

## day 1: setup and hand math
- [ ] set up the environment
- [ ] download the model
- [ ] work out parameter count, kv cache size and decode ceiling on paper
- [ ] do attention by hand
- [ ] load the weights
- [ ] verify rmsnorm
- [ ] **done when:** param count matches my math, rmsnorm matches the reference

## day 2: attention block
- [ ] q/k/v projections
- [ ] qwen3 q/k norms
- [ ] rope
- [ ] grouped-query attention
- [ ] causal mask
- [ ] output projection for layer 0
- [ ] **done when:** layer 0 attention matches the reference

## day 3: full forward pass
- [ ] swiglu mlp
- [ ] residuals
- [ ] all 28 layers
- [ ] final norm
- [ ] tied lm head
- [ ] **done when:** full logits match on several prompts

## day 4: generation
- [ ] greedy decoding
- [ ] temperature sampling
- [ ] top-k sampling
- [ ] top-p sampling
- [ ] **done when:** greedy output is identical to the reference

## day 5: kv cache
- [ ] split into prefill and decode
- [ ] cache k and v per layer
- [ ] attend over the cache
- [ ] **done when:** cached and uncached outputs are identical

## day 6: measurement
- [ ] time prefill and decode separately
- [ ] compare with the ~80 tok/s ceiling
- [ ] move to mps in fp16
- [ ] baseline against mlx-lm or llama.cpp
- [ ] **done when:** i can explain the gap between my engine, the baseline and the ceiling

## day 7: first quantization
- [ ] per-row int8 weight-only quantization
- [ ] perplexity and speed comparison against fp32
- [ ] short retro
- [ ] skim nano-vllm
- [ ] **done when:** int8 quality and speed numbers recorded and explained
