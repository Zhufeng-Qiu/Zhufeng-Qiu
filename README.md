<h1 align="center">Zhufeng (Zephyr) Qiu</h1>

<p align="center">
  <b>Full-stack development</b> → <b>GPU systems</b> · <b>collective communication</b> · <b>high-performance LLM inference</b>
</p>

<p align="center">
  <a href="https://zhufqiu.com">zhufqiu.com</a> ·
  <a href="mailto:zhufqiu@gmail.com">zhufqiu@gmail.com</a> ·
  Seattle, WA
</p>

---

👋 Hi, I'm Zhufeng (Zephyr) Qiu — a developer who pair-programs with AI most of the
time, and cleans up after it on the others.

Currently deep in AI agents, multi-agent collaboration and AI
infra. I have a habit of taking ideas that sound like they *"shouldn't
be that hard,"* and turning them into real-world systems. They’re usually harder than I expected, but thankfully, most of them eventually run.

This is where I keep my code, my experiments, and the occasional piece of work
that successfully escaped localhost.

I'm applying to PhD programs in **HPC, ML systems, AI infrastructure, and
parallel computing**, and I'd like to start contributing to the AI-infra
open-source community (current progress: joined the developer chat group. And that's it so far).

<br>

## Research projects
Take one computation, implement it across every execution model I can reach — serial, threaded, distributed, single-GPU, multi-GPU — hold the numerics exactly constant, and find out what the hardware actually charges for each choice.

The interesting results are usually the ones that came out the wrong way round.

### [Multi-GPU Similarity Engine](https://github.com/Zhufeng-Qiu/restaurant_recomendation_engine_study) &nbsp;·&nbsp; lossless collective compression

`C++` `CUDA` `NCCL` `MPI` `OpenMP` `Nsight Systems`

One Pearson-similarity kernel, five backends, one frozen numerical contract —
every backend reproduces the reference similarities **bit-exactly**
(`max |diff| = 0.0`), at every thread, rank, GPU and chunk count.

- **1.17M candidate pairs in 4.21 ms** on two A100s — 312× serial, ~20× over 16-thread OpenMP.
- Cut the NCCL AllReduce payload **3× losslessly** (56.2 → 18.8 MB) by packing six
  integer statistics into two `uint64` words with carry-free fields — so NCCL
  **sums them in compressed form, without ever decompressing**.
- Ran the identical binary on **NVLink and PCIe**: communication is 11% of the
  iteration on one and 91% on the other, so the same compression buys **4% vs 55%**.
  Same code, opposite verdicts — the regime decides, not the interconnect's name.

### [Quantized LLM Inference Study](https://github.com/Zhufeng-Qiu/product_price_alerter_lora_model_study) &nbsp;·&nbsp; what 4-bit actually costs

`PyTorch` `CUDA` `PEFT/LoRA` `bitsandbytes` `Modal`

A LoRA-fine-tuned Llama 3.1 8B served on a 16 GB T4, benchmarked with CUDA
events across four quantization configurations on Turing and Ampere.

- Found the deployed configuration was **2.50× slower than it needed to be** — a
  `bf16` compute dtype copied from the training notebook onto a GPU with no bf16
  tensor cores. Nothing errors; it just silently leaves the fast path.
- **4-bit buys capacity, not speed.** NF4 decode is 1.69× *slower* than fp16
  while moving 3.9× fewer bytes: dequantization-bound, not bandwidth-bound.
- 97% of the tokens are prefill, but only 39% of the time is — decode costs
  **54× more per token**.

<br>

## Also here

| Project                                                                 | Description                                                                                                  |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| [**Zephyr Manus**](http://zephyr-manus.zhufqiu.com)                     | Planner–ReAct agent runtime with Docker-isolated tool execution, Redis Streams, and human-in-the-loop resume |
| [**Train Flash-Sale**](https://github.com/Zhufeng-Qiu/train_flash_sale) | High-concurrency ticketing on Spring Cloud — Redis inventory control, RocketMQ, distributed locks            |
| [**Distributed Apriori**](https://github.com/Zhufeng-Qiu/cs6240)        | Frequent-itemset mining over Yelp on Hadoop MapReduce, with interchangeable HBase and S3 backends            |

<br>

## Besides code

🥾 **Hiking** — weekends are spent either in the mountains or on the way to them.<br>
🏊 **Swimming** — breaststroke only. In Chinese, it's literally "frog stroke," which feels about right.<br>
🍳 **Cooking** — an essential survival skill for every international student.<br>
🪈 **Dízi (笛子)** — the Chinese bamboo flute. Once a certified Grade 5 player; now I need a long time just to find the embouchure hole.<br>
🎮 **Dota** — more spectator than player. I don’t even have the client installed.<br>

---

<p align="center">
  <sub>M.S. Northeastern (CS) · M.S. USC (Applied Data Science) · B.S. Wuhan University (GIS)</sub>
</p>
