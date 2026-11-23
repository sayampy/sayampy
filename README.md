<div align="center">

# Hey, I'm Sayam 👋

### Math student who builds things, breaks benchmarks, and tries to make them faster.

I like making useful things under real constraints: offline audio cleanup, local LLM inference, and simulations that show how small decisions can change an entire system.

<p>
  <a href="https://github.com/sayampy/deepdenoiser"><img src="https://img.shields.io/github/stars/sayampy/deepdenoiser?style=for-the-badge&logo=github&label=DeepDenoiser" alt="DeepDenoiser stars" /></a>
  <a href="https://github.com/sayampy/deepdenoiser/releases"><img src="https://img.shields.io/github/downloads/sayampy/deepdenoiser/v1.4.4/DeepDenoiser-Arm64-v8.apk?style=for-the-badge&label=APK%20downloads" alt="APK downloads" /></a>
  <a href="https://github.com/sayampy?tab=followers"><img src="https://img.shields.io/github/followers/sayampy?style=for-the-badge&logo=github&label=Followers" alt="GitHub followers" /></a>
</p>

</div>

---

## What I’m about

- 🎧 **Audio that stays private:** building tools that process media locally instead of sending it to a server.
- ⚡ **Making local LLMs faster:** working on expert execution, KV caches, speculative decoding, and calibration.
- 🧮 **Math with moving parts:** game theory, traffic behaviour, and reinforcement-learning experiments.

I enjoy profiling the awkward parts, finding the actual bottleneck, and testing whether a change really helped.

## Recent upstream work · RustingStrata

I’ve been contributing to [RustingStrata](https://github.com/RustingStudio/RustingStrata), a Rust-based GGUF inference engine. Most of my recent work has been around making MoE and Inkling 2 inference more practical, improving memory use, and making benchmarks more useful.

### Merged

- **[ #74 · Faster Inkling 2 and MoE decoding](https://github.com/RustingStudio/RustingStrata/pull/74)**  
  Added a host fallback when routed experts cannot be staged in GPU memory, adaptive expert staging, and lossless suffix speculative decoding by default. In the tested runs, Inkling 2 decode went from **8.6 to 16.3 tok/s**, while Tiel Coder went from **16.1 to 26.7 tok/s**.  
  <a href="https://img.shields.io/github/pulls/detail/state/RustingStudio/RustingStrata/74"><img src="https://img.shields.io/github/pulls/detail/state/RustingStudio/RustingStrata/74" alt="PR 74 status" /></a>

- **[ #80 · Batched host expert matvecs](https://github.com/RustingStudio/RustingStrata/pull/80)**  
  Reworked CPU-side expert execution to quantize activations once and process expert rows in a shared Rayon pass. Natural-prompt tests showed around **25–36% faster decode** in the measured cases, with identical output in the tested correctness checks.  
  <a href="https://img.shields.io/github/pulls/detail/state/RustingStudio/RustingStrata/80"><img src="https://img.shields.io/github/pulls/detail/state/RustingStudio/RustingStrata/80" alt="PR 80 status" /></a>

### In review

- **[ #84 · TurboQuant KV cache for CUDA](https://github.com/RustingStudio/RustingStrata/pull/84)**  
  Implemented WHT + Lloyd–Max KV quantization for the Inkling 2 and general CUDA attention paths, including independent K/V formats. The 4-bit format stores the cache in about **28% of the FP16 size** in the measured layout.

- **[ #87 · Universal calibration v2](https://github.com/RustingStudio/RustingStrata/pull/87)**  
  Reworked calibration into a budgeted search that balances prefill speed, decode speed, and time-to-first-token. It also expands calibration to architectures that previously had separate or unsupported paths.

- **[ #89 · Draft acceptance in benchmark JSON](https://github.com/RustingStudio/RustingStrata/pull/89)**  
  Adds machine-readable counts for speculative drafts made and accepted, so benchmark tools can inspect more than just the final token speed.

<p>
  <a href="https://github.com/RustingStudio/RustingStrata/pulls?q=is%3Apr+author%3Asayampy"><img src="https://img.shields.io/badge/More%20RustingStrata%20work-View%20PRs-8A63D2?style=for-the-badge&logo=github" alt="View all my RustingStrata pull requests" /></a>
</p>

## Things I’ve built

### 🎧 [DeepDenoiser](https://github.com/sayampy/deepdenoiser)

An offline Android app for removing background noise from audio and video. Processing happens on-device, so recordings stay on the phone.

**Stack:** React Native · Expo · Kotlin · DeepFilterNet3 · ONNX Runtime

[Google Play](https://play.google.com/store/apps/details?id=com.sayampy.deepdenoiser) · [Source](https://github.com/sayampy/deepdenoiser) · [Releases](https://github.com/sayampy/deepdenoiser/releases)

### 🚦 [Traffic Jam Behavioral Analysis](https://github.com/sayampy/traffic-jam-analyze)

A cell-based highway simulator for comparing driver strategies. It explores a fun question: can a driver make things worse for everyone by trying too hard to get ahead?

**Stack:** Python · Pygame · Game theory · Simulation

### ⚽ [Football RL Experiments](https://github.com/sayampy/-Buggy-Football-RL)

A learning project where I experimented with Deep Q-Networks, agents, and training loops in a game environment.

**Stack:** Python · PyTorch · NumPy

## 🎮 Pick a rabbit hole

Curious about a particular corner of my GitHub? Pick one and open it.

<details>
<summary>⚡ I want to see inference optimisation and Rust</summary>

Start with [RustingStrata](https://github.com/RustingStudio/RustingStrata). The PRs above cover expert execution, speculative decoding, KV-cache compression, and automatic calibration.

</details>

<details>
<summary>🎧 I want an actual app I can try</summary>

Try [DeepDenoiser](https://github.com/sayampy/deepdenoiser). It denoises audio and video locally on Android.

</details>

<details>
<summary>🚦 I like maths, strategy, and unexpected outcomes</summary>

Explore [Traffic Jam Behavioral Analysis](https://github.com/sayampy/traffic-jam-analyze). It compares how different driving strategies affect the whole traffic system.

</details>

<details>
<summary>⚽ Show me the learning agent</summary>

Take a look at [Football RL Experiments](https://github.com/sayampy/-Buggy-Football-RL), my early experiments with DQN-based agents.

</details>

### 🧩 A tiny inference puzzle

**Why batch CPU-side experts together instead of running a separate matrix-vector operation for each expert?**

<details>
<summary>Reveal the idea</summary>

The old path repeated parallel work and quantized the same activation for each expert. The batched path quantizes once, then processes the expert rows together in one Rayon pass. Less repeated work, better use of the CPU, and faster decode in the workloads I tested.

That is the core idea behind [PR #80](https://github.com/RustingStudio/RustingStrata/pull/80).

</details>

## Tools I use

<p align="center">
  <img src="https://skillicons.dev/icons?i=ts,js,python,rust,kotlin,react,android,pytorch,linux,git&perline=5" alt="TypeScript, JavaScript, Python, Rust, Kotlin, React, Android, PyTorch, Linux and Git" />
</p>

<p align="center">
  <sub>Also working with Expo, ONNX Runtime, CUDA, Vulkan, GitHub Actions, and a fair amount of profiling.</sub>
</p>

## GitHub activity

<p align="center">
  <img height="170" src="https://github-readme-stats.vercel.app/api?username=sayampy&show_icons=true&include_all_commits=true&rank_icon=github&hide_border=true&theme=transparent" alt="GitHub stats" />
  <img height="170" src="https://github-readme-stats.vercel.app/api/top-langs/?username=sayampy&layout=compact&langs_count=8&hide_border=true&theme=transparent" alt="Most used languages" />
</p>

<p align="center">
  <img src="https://streak-stats.demolab.com?user=sayampy&hide_border=true&theme=transparent" alt="GitHub contribution streak" />
</p>

---

<div align="center">

**Found something interesting?** Open an issue, start a discussion, or just say hi.

<a href="https://ko-fi.com/sayampy"><img src="https://img.shields.io/badge/Support%20my%20work-Ko--fi-FF5E5B?style=for-the-badge&logo=ko-fi&logoColor=white" alt="Support my work on Ko-fi" /></a>

</div>
