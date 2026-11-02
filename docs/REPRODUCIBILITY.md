# Reproducibility and visual sources

## Scope

This guide describes what is available in the committed project and what is required to reproduce it. The documentation update inspected source and saved outputs; it did not rerun model training or hardware/simulation experiments.

## Required inputs

The topology is defined in code and needs no external dataset. The sample `192.168.5.10` address belongs to RouterD's `/24` network; an adjacent comment incorrectly labels it as RouterE. The implementation does not record a `/0` default route as an initial match, so treat it as a limited demonstration rather than a complete router.

## Entry point

Install Python, Jupyter, and the visualization packages:

```bash
python -m pip install jupyter networkx matplotlib graphviz
```

Trie-image rendering also needs the Graphviz system executable `dot` on PATH; the Python `graphviz` package alone does not provide it.

Open `Project.ipynb` and run its code cell. The notebook defines the topology, computes tables, renders diagrams, and forwards a sample packet.

## Evidence and interpretation

The topology figure below is an original saved notebook output. The simulation illustrates data structures and routing decisions; it is not a measured throughput or real-network deployment benchmark. Running the notebook also generates per-router trie PNGs.

## Visual provenance

All screenshots and experiment figures are tied to repository material. Workflow SVGs are explanatory illustrations. The full image inventory is in [assets/sources.json](assets/sources.json).

| Visual | Source |
| --- | --- |
| [overview.svg](assets/overview.svg) | New explanatory project-workflow diagram based on the committed source and documentation; not a screenshot or measured result. |
| [notebook-1.png](assets/notebook-1.png) | Project.ipynb, cell 1 (1-based), committed image/png output; not rerun |

## Validation

```bash
python tools/check_docs.py
```

The standard-library checker validates README/docs local link destinations and SVG/PNG/JPEG headers. It makes no external requests and installs no project runtime dependencies. External web links, model accuracy, image semantics, and full application execution need separate review.

## Refresh notebook visuals

The exporter reads saved `image/png` outputs without executing notebook code:

```bash
python tools/export_notebook_images.py "Project.ipynb"
```

Review the exported images, remove any unsuitable or private content, choose the figures that explain the project, and update the README links and `docs/assets/sources.json`. It does not manufacture results when a notebook has no saved PNG output.

## Reproduction record

For a new experiment or demo, record the source commit, environment versions, data provenance and split, configuration, command/notebook order, and resulting artifacts. Only label a measurement as reproduced after completing that run. Keep credentials and restricted datasets outside version control.
