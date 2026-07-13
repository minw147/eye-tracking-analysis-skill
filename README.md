# Eye-Tracking Analysis Skill

An AI-powered Claude Code skill that predicts visual attention patterns — where users will look in the first 3-5 seconds of viewing a screenshot, website, or UI design — using **Spectral Residual Saliency**, a validated computer-vision methodology (85-90% accuracy relative to real eye-tracking studies).

Given an image, it generates:

- A color-coded **attention heatmap** (red = hot, yellow = medium, blue = cold)
- A **clarity score** (0-100) measuring visual focus vs. clutter
- A predicted **fixation sequence** — the order a viewer's eyes move through the design
- Automatically **detected attention zones** with percentage share of total visual "heat"
- A full written report with specific, actionable design recommendations

Based on Hou, X., & Zhang, L. (2007), *Saliency Detection: A Spectral Residual Approach*, IEEE CVPR 2007 — see [references/algorithm.md](./references/algorithm.md) for the math and citation, or the [full technical write-up](https://heatmap.mintleafux.com/SPECTRAL_RESIDUAL_EXPLANATION.html).

## Try it first

Before installing anything, see it in action: **[live demo](https://heatmap.mintleafux.com)** — upload a screenshot and get a heatmap + a ready-made prompt for the full report, entirely in your browser, nothing uploaded or stored.

## Install

Copy this repo's contents into your project's `.claude/skills/eye-tracking-analysis/` (or your global `~/.claude/skills/eye-tracking-analysis/`):

```bash
git clone https://github.com/minw147/eye-tracking-analysis-skill.git .claude/skills/eye-tracking-analysis
```

Install the Python dependencies the analysis script needs:

```bash
pip install opencv-contrib-python selenium webdriver-manager markdown xhtml2pdf
```

## Usage

Once installed, invoke it in a Claude Code conversation:

```
@eye-tracking-analysis

Run the eye tracking analysis for this image: [attach image]
```

It also supports URL capture, multi-image comparison, A/B testing two designs, and marked regions-of-interest for precise attention-share measurement. See [`SKILL.md`](./SKILL.md) for the full workflow.

## What's in this repo

- `SKILL.md` — the skill definition: overview, when to use it, and the core workflow
- `scripts/` — the Python pipeline (saliency computation, region detection, URL capture, PDF export)
- `references/workflow.md` — detailed procedure for URL capture, region detection, multi-image handling, PDF export, and file naming
- `references/report-format.md` — metric-interpretation rules and the exact report structure
- `references/reading-patterns.md` — F-pattern, Z-pattern, Gutenberg diagram, and layer-cake scanning research (Nielsen Norman Group), used to ground the fixation narrative in real UX literature
- `references/algorithm.md` — the Spectral Residual math, our enhancements (face-boost, clarity score), and the original citation
- `assets/heatmap_legend.png` — the color-scale legend embedded in generated reports

## License

MIT — see [LICENSE](./LICENSE).
