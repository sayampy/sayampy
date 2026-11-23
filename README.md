<div align="center">
  <img src="./assets/workbench.svg" alt="Sayam's workbench: sound, inference, and simulation" width="100%" />
  <p>
    <a href="https://github.com/sayampy/deepdenoiser"><img src="https://img.shields.io/github/stars/sayampy/deepdenoiser?style=flat-square&label=DeepDenoiser%20stars" alt="DeepDenoiser stars" /></a>
    <a href="https://github.com/sayampy/deepdenoiser/releases"><img src="https://img.shields.io/github/downloads/sayampy/deepdenoiser/total?style=flat-square&label=downloads" alt="DeepDenoiser downloads" /></a>
    <a href="https://github.com/sayampy?tab=followers"><img src="https://img.shields.io/github/followers/sayampy?style=flat-square&label=followers" alt="GitHub followers" /></a>
  </p>
</div>

Maths student from India. I build apps, poke at inference speed, and write simulations when I can't settle an argument in my head.

Lately I've been splitting time between an offline audio app, patches to a Rust inference engine, and a traffic simulator that suggests "smart" drivers aren't always smart.

## Things I've built

<table>
  <tr>
    <td width="50%" valign="top">
      <a href="https://github.com/sayampy/deepdenoiser">
        <img src="https://raw.githubusercontent.com/sayampy/deepdenoiser/master/fastlane/metadata/android/en-US/images/phoneScreenshots/1.jpg" alt="DeepDenoiser Android app screenshot" width="100%" />
      </a>
      <h3><a href="https://github.com/sayampy/deepdenoiser">DeepDenoiser</a></h3>
      An Android app for cleaning up noisy audio and video. Runs on-device. No account, no upload, no cloud bill.
      <br /><br />
      <sub>React Native · Expo · Kotlin · ONNX Runtime</sub>
      <br />
      <a href="https://play.google.com/store/apps/details?id=com.sayampy.deepdenoiser">Google Play</a> · <a href="https://github.com/sayampy/deepdenoiser/releases">Releases</a>
    </td>
    <td width="50%" valign="top">
      <a href="https://github.com/sayampy/traffic-jam-analyze">
        <img src="https://raw.githubusercontent.com/sayampy/traffic-jam-analyze/master/.github/assets/strategy_performance.png" alt="Traffic simulation strategy performance chart" width="100%" />
      </a>
      <h3><a href="https://github.com/sayampy/traffic-jam-analyze">Traffic Jam Simulator</a></h3>
      A little highway model comparing different driver behaviours. Turns out, constantly trying to get ahead can make everyone slower.
      <br /><br />
      <sub>Python · Pygame · Game theory</sub>
      <br />
      <a href="https://github.com/sayampy/traffic-jam-analyze">See the experiments</a>
    </td>
  </tr>
</table>

**Old side quest:** [Football RL](https://github.com/sayampy/-Buggy-Football-RL), where I played with DQN agents and a game environment. It is very much an experiment, not a finished game.

## RustingStrata patches

Most of my recent open-source work has gone into [RustingStrata](https://github.com/RustingStudio/RustingStrata). I got interested because running MoE models on limited VRAM is full of awkward edge cases. These are the bits I've been working on:

| PR | Status | The change |
|---|---|---|
| [#74](https://github.com/RustingStudio/RustingStrata/pull/74) | <img src="https://img.shields.io/github/pulls/detail/state/RustingStudio/RustingStrata/74?label=merged" alt="Merged" /> | Inkling 2 host fallback when experts don't fit in VRAM, adaptive GPU staging, and suffix drafts by default. In my test runs, decode moved from **8.6 to 16.3 tok/s** on Inkling 2 and **16.1 to 26.7 tok/s** on Tiel Coder. |
| [#80](https://github.com/RustingStudio/RustingStrata/pull/80) | <img src="https://img.shields.io/github/pulls/detail/state/RustingStudio/RustingStrata/80?label=merged" alt="Merged" /> | Batched CPU-side expert matvecs. Around **25-36% faster decode** in the natural-prompt tests, with identical output in the correctness checks. |
| [#84](https://github.com/RustingStudio/RustingStrata/pull/84) | <img src="https://img.shields.io/github/pulls/detail/state/RustingStudio/RustingStrata/84?label=open" alt="Open" /> | TurboQuant KV cache for CUDA, using Walsh-Hadamard transforms and Lloyd-Max quantization. Adds separate K/V formats and a much smaller cache representation. |
| [#89](https://github.com/RustingStudio/RustingStrata/pull/89) | <img src="https://img.shields.io/github/pulls/detail/state/RustingStudio/RustingStrata/89?label=open" alt="Open" /> | Adds speculative draft counts to benchmark JSON, so scripts can see how many drafts were made and accepted. |

I also prototyped a budgeted calibration search balancing prefill, decode, and time-to-first-token in [#87](https://github.com/RustingStudio/RustingStrata/pull/87). That PR was closed without merging.

<sub>Speed figures are from the specific hardware, models, and prompts documented in the PRs. They aren't universal benchmark claims.</sub>

## A few tools on my desk

<p align="center">
  <img src="https://skillicons.dev/icons?i=python,ts,rust,kotlin,react,android,pytorch,linux,git&perline=9" alt="Python, TypeScript, Rust, Kotlin, React, Android, PyTorch, Linux and Git" />
</p>

Python is where most experiments start. Rust has been taking up more of my time lately. TypeScript and Kotlin get the apps out of the door.

## The bench queue

Got a model, quantization method, or weird slowdown you'd like me to test? **Send me a bench request.** Pick a topic and leave a short explanation. I may turn a good one into the next experiment.

<div align="center">
  <a href="https://github.com/sayampy/sayampy/issues/new?template=experiment-request.yml">
    <img src="https://img.shields.io/badge/PUT%20SOMETHING%20ON%20THE%20BENCH-suggest%20an%20experiment-c9f36b?style=for-the-badge&labelColor=202820&logo=github&logoColor=white" alt="Suggest an experiment" />
  </a>
  <br />
  <sub><a href="https://github.com/sayampy/sayampy/issues?q=is%3Aissue">Browse suggestions and join the discussion</a></sub>
</div>

## GitHub, lately

<div align="center">
  <img height="155" src="https://github-readme-stats.vercel.app/api?username=sayampy&show_icons=true&hide_title=true&hide_border=true&theme=github_dark&include_all_commits=true" alt="GitHub stats" />
  <img height="155" src="https://github-readme-stats.vercel.app/api/top-langs/?username=sayampy&layout=compact&langs_count=6&hide_border=true&theme=github_dark" alt="Most used languages" />
  <img src="https://github-readme-activity-graph.vercel.app/graph?username=sayampy&theme=github-compact&hide_border=true&area=true" alt="GitHub contribution graph" width="100%" />
</div>

---

<div align="center">
  <sub>If you found a bug, have a better benchmark, or just want to talk shop, my issues are open.</sub>
  <br />
  <a href="https://github.com/sayampy">GitHub</a> · <a href="https://ko-fi.com/sayampy">Ko-fi</a>
</div>
