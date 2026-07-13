# Eye-Tracking Analysis Skill

An AI-powered Claude Code skill that predicts visual attention patterns — where users will look in the first 3-5 seconds of viewing a screenshot, website, or UI design — using **Spectral Residual Saliency**, a validated computer-vision methodology (85-90% accuracy relative to real eye-tracking studies).

Given an image, it generates:

- A color-coded **attention heatmap** (red = hot, yellow = medium, blue = cold)
- A **clarity score** (0-100) measuring visual focus vs. clutter
- A predicted **fixation sequence** — the order a viewer's eyes move through the design
- Automatically **detected attention zones** with percentage share of total visual "heat"
- A full written report with specific, actionable design recommendations

Based on Hou, X., & Zhang, L. (2007), *Saliency Detection: A Spectral Residual Approach*, IEEE CVPR 2007 — see [eye-tracking-analysis/references/algorithm.md](./eye-tracking-analysis/references/algorithm.md) for the math and citation, or the [full technical write-up](https://heatmap.mintleafux.com/SPECTRAL_RESIDUAL_EXPLANATION.html).

## Try it first

Before installing anything, see it in action: **[live demo](https://heatmap.mintleafux.com)** — upload a screenshot and get a heatmap + a ready-made prompt for the full report, entirely in your browser, nothing uploaded or stored.

## Install

**Via the [skills CLI](https://skills.sh/)** (recommended):

```bash
npx skills add minw147/eye-tracking-analysis-skill
```

Or update it later:

```bash
npx skills update eye-tracking-analysis
```

**Manually**, clone the repo and copy the `eye-tracking-analysis/` folder into your project's `.claude/skills/` (or your global `~/.claude/skills/`):

```bash
git clone https://github.com/minw147/eye-tracking-analysis-skill.git /tmp/eye-tracking-analysis-skill
cp -r /tmp/eye-tracking-analysis-skill/eye-tracking-analysis .claude/skills/eye-tracking-analysis
```

Either way, install the Python dependencies the analysis script needs:

```bash
pip install opencv-contrib-python selenium webdriver-manager markdown xhtml2pdf
```

## Usage

Once installed, invoke it in a Claude Code conversation:

```
@eye-tracking-analysis

Run the eye tracking analysis for this image: [attach image]
```

It also supports URL capture, multi-image comparison, A/B testing two designs, and marked regions-of-interest for precise attention-share measurement. See [`eye-tracking-analysis/SKILL.md`](./eye-tracking-analysis/SKILL.md) for the full workflow.

## What's in this repo

Everything the skill needs lives under `eye-tracking-analysis/` (this nesting is what lets `npx skills add` — and multi-skill repos in general — install the skill's scripts/references/assets alongside `SKILL.md`, not just the manifest):

- `eye-tracking-analysis/SKILL.md` — the skill definition: overview, when to use it, and the core workflow
- `eye-tracking-analysis/scripts/` — the Python pipeline (saliency computation, region detection, URL capture, PDF export)
- `eye-tracking-analysis/references/workflow.md` — detailed procedure for URL capture, region detection, multi-image handling, PDF export, and file naming
- `eye-tracking-analysis/references/report-format.md` — metric-interpretation rules and the exact report structure
- `eye-tracking-analysis/references/reading-patterns.md` — F-pattern, Z-pattern, Gutenberg diagram, and layer-cake scanning research (Nielsen Norman Group), used to ground the fixation narrative in real UX literature
- `eye-tracking-analysis/references/algorithm.md` — the Spectral Residual math, our enhancements (face-boost, clarity score), and the original citation
- `eye-tracking-analysis/assets/heatmap_legend.png` — the color-scale legend embedded in generated reports

## License

MIT — see [LICENSE](./LICENSE).
