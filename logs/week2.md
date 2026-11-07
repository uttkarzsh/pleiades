# week 2: finishing the single-request engine

- [ ] int4 weight-only quantization with group-wise scales
- [ ] compare int4 vs int8 vs fp16 on perplexity and speed
- [ ] per-layer profiling to find where the time actually goes
- [ ] port the decode loop to c or rust with my own cpu matmul
- [ ] optimize the matmul: cache blocking
- [ ] optimize the matmul: neon simd
- [ ] optimize the matmul: threads
