---
layout: base.njk
title: Recommended Open Models
description: Research and recommendations for the best open models to use as alternatives to proprietary AI services, plus tooling to run them locally.
---

# Recommended Open Models

Running an AI model on your own computer is one way to avoid sending your data to a commercial service. There are free tools for this, and once set up, you can use the model without an account or subscription.

There are two practical decisions: which model to use, and which software to run it with.

---

## Start Here

If you have never run a model locally before, LM Studio is a straightforward place to start:

1. Install [LM Studio][lm-studio]. It is a desktop app for Mac, Windows, and Linux.
2. Work out how much memory your computer has (see below).
3. Search in the app for one of the models in our table, download it, and start typing.

You do not need to write code or use a terminal. If you are not sure which model to try, **OLMo 3.1 7B** runs on 8 GB and is a reasonable starting point.

The rest of this page explains the recommendations and the alternatives for different hardware and uses.

---

## Will It Run on My Computer?

The first thing to check is available memory. This determines which models you can fit; processor speed affects how quickly they run.

The relevant memory figure depends on your computer:

- **Mac (M1 or newer):** the memory figure on the spec sheet, e.g. "16 GB". The chip shares it with the graphics and the system, so budget about three-quarters of it for the model.
- **Windows or Linux with a dedicated graphics card:** the memory on the card itself, not the computer's main RAM. A machine with 32 GB of RAM and an 8 GB graphics card counts as 8 GB here.
- **No dedicated graphics card:** models still run using main RAM. Expect words to appear at reading speed rather than instantly.

| Memory | What you can run | Typical use |
| --- | --- | --- |
| 4 GB | Small models (3B) | Quick questions, short text, phones |
| 8 GB | Mid-size models (7-9B) | A capable everyday assistant |
| 16 GB | The same, with longer documents | More room for documents and conversation history |
| 24-32 GB | Large models (27-32B) | Close to a commercial service |
| 96 GB or more | Very large mixture-of-experts models | More demanding tasks, mostly on high-memory Macs |

For many everyday tasks, **8 GB is enough**. A 7B model compressed to Q4 is about 4.5 GB, so it fits on a modest laptop, an older graphics card, or a second-hand machine. It is worth trying what you already have before buying hardware.

A few terms you will see when choosing a model:

- **7B, 27B, 32B** count the model's parameters in billions. Bigger means more capable and more memory.
- **Quantization** is compression. Models are published at several sizes, labelled Q3, Q4, Q8 and so on. **Q4 is the standard choice** and roughly halves the memory needed for a small quality cost. LM Studio picks a sensible one for you. Some models also come as **QAT** (quantization-aware trained) files, trained to run at Q4, which lose noticeably less quality.
- **Active parameters** apply to "mixture of experts" models, written like 26B-A4B. Only the active part (4B) does the work for each word, so it runs at the speed of a small model, but the whole 26B still has to fit in memory.

---

## What "Open Model" Means

Most models called open are only **open-weight**. You can download and run them, but the training data and code stay private.

A fully open model releases three things:

- **Weights**, so you can run and fine-tune it yourself.
- **Training data**, so provenance, consent, and copyright can be audited.
- **Training code and documentation**, so it can be reproduced and studied.

Very few capable models release all three. Calling an open-weight release open source is common enough that researchers have a name for it: [open-washing][open-washing].

There are degrees of openness. The [Model Openness Framework][model-openness-framework] offers a way to assess them. The [OSI's Open Source AI Definition][osi-ai-definition] is another reference point, though its handling of training data is still contested.

Running a model yourself reduces supplier dependence, but testing, monitoring and updates are still your responsibility ([SAFE AI][safe-ai-tools]).

It is also worth checking the licenses of the tools below, rather than assuming they are open source because they run open models.

---

## Choosing a Model (November 2026)

The table starts with smaller models, which are sufficient for many everyday tasks.

| Memory | Model | Openness | Good for |
| --- | --- | --- | --- |
| 4 GB | [SmolLM3-3B][smollm3] | Fully open | Old laptops, no graphics card, phones |
| 8 GB | [OLMo 3.1 7B][olmo3-collection] | Fully open | **Start here.** Everyday use |
| 8 GB | [Gemma 4 E4B (QAT)][gemma4-e4b-qat] | Open-weight | Running on a processor without a graphics card, e.g. a server |
| 8-16 GB | [Qwen3.5-9B][qwen35-9b] | Open-weight | Coding on modest hardware |
| 24 GB | [OLMo 3.1 32B][olmo3-collection] | Fully open | The most capable fully open option |
| 24 GB | [Qwen3.8-27B][qwen38-27b] | Open-weight | Coding, data tasks, reading images |
| 96 GB+ | [Qwen3.8-Flash-Next][qwen38-flash-next] | Open-weight, restrictive license | Near-frontier capability on a high-memory Mac |

You only need to download a model once: about 2 GB for the smallest, or around 4.5 GB for a 7B. After that you can use it offline. This is particularly useful on a metered or intermittent connection.

Why we chose these models:

- **Fully open:** [OLMo 3 / 3.1][olmo3-blog] (Ai2, Apache 2.0) publishes weights, training data, code, and checkpoints. It is our first recommendation for a fully open model, with the 7B version a practical size for most people.
- **Fully open and tiny:** [SmolLM3-3B][smollm3] (Hugging Face, Apache 2.0) publishes its weights, data mixture, and training code. Its smaller size makes it useful on more limited hardware, for summarising, drafting, and translation between its six languages.
- **Trained on openly licensed data:** the [Comma models][comma-models] are trained only on openly licensed and public domain text. They are less capable than newer models, but show that training on a documented, openly licensed corpus is possible.
- **Open-weight, the pragmatic middle:** Qwen, DeepSeek, and similar releases run locally, so you avoid lock-in and data exposure. Their training data is undisclosed, so the provenance concerns are the same as for proprietary models. [Qwen3.5-9B][qwen35-9b] is the practical choice if you want to write code on an 8 GB machine.
- **Small and efficient on servers:** [Gemma 4 E4B][gemma4-e4b-qat] (Google, Apache 2.0) uses about 4B parameters per word and comes as an official QAT Q4 file. In a [like-for-like test][gemma-qwen-low-end] one size down, Gemma's Q4 beat Qwen3.5's Q4 by 15-26 points on every task, while Qwen read prompts 25-50% faster. HOT runs E4B for its docs assistant on a shared 4 CPU / 16 GB server.

A larger model is not always necessary. A 7B model can handle summarising, drafting, translating, and answering questions, usually with less waiting. Try a couple of models on your own tasks before deciding whether you need a larger one; published benchmarks only tell part of the story.

<details>
<summary><strong>More detail on Qwen3.8-27B</strong></summary>

Qwen3.8-27B is from Alibaba Cloud and released under Apache 2.0. It reads images and video as well as text, so you can feed it a flowchart and ask questions about it.

Qwen reports improved coding performance over Qwen3.6-27B, which it replaces here: 61.7 vs 53.5 on SWE-bench Pro, for example. This makes it worth considering for coding on a single consumer graphics card.

Budget 24 GB. At Q4 the weights alone are around 18 GB, so a 16 GB card only manages it with heavier compression or by offloading part of the work to the processor.

It holds about 262,000 tokens at once, its "context window". A token is roughly three-quarters of a word, so that is a long book's worth of text, but not unlimited: a 2 MB text file is about double that and will not fit in one pass.

</details>

<details>
<summary><strong>More detail on Qwen3.8-Flash-Next</strong></summary>

Qwen3.8-Flash-Next is a mixture-of-experts model with 6B active parameters. It is quick once loaded, but the 4-bit download is around 100 GB. In practice that means a Mac with 96-128 GB or more of unified memory. On a Mac, pick an MLX build.

Unlike Qwen3.8-27B, it uses the Qwen Community License, which restricts some commercial uses. If that matters, [Mistral Small 4][mistral-small-4] is a similar size (119B, 6B active) under Apache 2.0, though five months older.

</details>

For evaluating models on your own tasks rather than on published benchmarks, [OpenCompass][opencompass] runs reproducible comparisons. For image generation rather than text, [PD12M][pd12m] is a public domain image dataset, giving the same provenance guarantee the Common Pile gives for text.

---

## What to Run It With

The tools below let you run models on your own hardware, keeping prompts local and avoiding usage fees or reliance on a hosted service.

### Most people: LM Studio

**[LM Studio][lm-studio]** is a desktop app with model search, download, and chat in one window. It is free for personal and internal business use.

The app itself is proprietary and cannot be audited or modified, although its command-line tool and SDKs use the MIT license. If your organization requires open-source software, llama.cpp has a built-in interface you can use instead.

### Developers and servers: llama.cpp

**[llama.cpp][llama-cpp]** (MIT) is the engine nearly everything else is built on, LM Studio included. Give `llama-server` a model file and it serves an OpenAI-compatible API on port 8080 plus a built-in web chat page. It does not require a Python environment or container. Running it directly avoids the overhead a wrapper adds to every request.

On a server without a graphics card:

- **Reading the prompt is the slow part,** not writing the answer. Keep prompts short. With E4B on 4 CPU cores, HOT measured about 25 tokens a second reading and 5 writing, so a long prompt takes most of a minute before the first word.
- **Turn off "thinking"** (`--reasoning-budget 0`). Hidden reasoning adds tens of seconds before anything appears.
- **Set threads to your CPU allowance** (`-t`), not the machine's core count. Oversubscribing made llama.cpp about 2.5x slower in our tests.

### Coding agents

**[OpenCode][opencode]** points a terminal coding agent at any OpenAI-compatible endpoint, including a local `llama-server`. This lets you use a local model to work on code in your project.

### Phones

- **[PocketPal AI][pocketpal]** (MIT) is fully offline chat on Android and iOS. No account, and no connection needed once a model is downloaded. Workable on 4 GB of RAM, with SmolLM3-3B a good fit.
- **[MNN][mnn]** (Apache 2.0, Alibaba) is for developers embedding inference in an app. It is substantially faster than llama.cpp on mobile hardware, with the [MNN-LLM paper][mnn-llm-paper] reporting large speedups on Android CPU and GPU. Its official chat apps are a working reference implementation.

### A whole team

**[Open WebUI][open-webui]** provides a shared chat interface for a team. It connects to a llama.cpp backend, serves it over a web page, and installs like an app on mobile. Two caveats: you need a server and a domain, and [since v0.6.6 its license][open-webui-license] adds branding restrictions that make it no longer OSI-approved open source (v0.6.5 and earlier remain BSD-3-Clause). Check the terms before redistributing or rebranding it.

### A note on Ollama

[Ollama][ollama] is the usual recommendation for an easy start, and we no longer suggest it as a first choice. It has a [history of crediting llama.cpp poorly][ollama-credit] despite being built on it, and now [measurably trails llama.cpp on throughput][ollama-throughput] by anywhere from 10% upwards. For the uses covered here, we recommend LM Studio for a desktop app or llama.cpp for running a server directly.

---

_These recommendations are a starting point. We will update them as we test more models and tools ourselves._

[lm-studio]: https://lmstudio.ai
[open-washing]: https://doi.org/10.1145/3630106.3659005
[model-openness-framework]: https://arxiv.org/abs/2403.13784
[osi-ai-definition]: https://opensource.org/ai/open-source-ai-definition
[safe-ai-tools]: https://doi.org/10.5281/zenodo.22079930
[smollm3]: https://huggingface.co/HuggingFaceTB/SmolLM3-3B
[olmo3-collection]: https://huggingface.co/collections/allenai/olmo-3
[qwen35-9b]: https://huggingface.co/Qwen/Qwen3.5-9B
[qwen38-27b]: https://huggingface.co/Qwen/Qwen3.8-27B
[qwen38-flash-next]: https://huggingface.co/Qwen/Qwen3.8-Flash-Next
[mistral-small-4]: https://huggingface.co/mistralai/Mistral-Small-4-119B-2603
[olmo3-blog]: https://allenai.org/blog/olmo3
[comma-models]: https://github.com/r-three/common-pile
[gemma4-e4b-qat]: https://huggingface.co/google/gemma-4-E4B-it-qat-q4_0-gguf
[gemma-qwen-low-end]: https://dev.to/gde/comparing-qwen-and-gemma-on-the-low-end-qwen-is-faster-without-drafting-gemma-has-better-quality-30bo
[opencompass]: https://github.com/open-compass/opencompass
[pd12m]: https://huggingface.co/datasets/Spawning/PD12M
[llama-cpp]: https://github.com/ggml-org/llama.cpp
[opencode]: https://github.com/sst/opencode
[pocketpal]: https://pocketpal.dev/
[mnn]: https://github.com/alibaba/MNN
[mnn-llm-paper]: https://arxiv.org/abs/2506.10443
[open-webui]: https://openwebui.com
[open-webui-license]: https://docs.openwebui.com/license/
[ollama]: https://ollama.com
[ollama-credit]: https://news.ycombinator.com/item?id=47624999
[ollama-throughput]: https://github.com/ollama/ollama/issues/14861
