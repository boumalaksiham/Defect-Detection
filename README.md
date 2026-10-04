# Manufacturing Defect Detection — Project Plan

**Status: design only.** This repository currently contains this README. Training code, model weights, data loaders, configuration, tests, and a dashboard are not yet committed. It does not currently provide a runnable system or measured performance/business impact.

## Research question

Can a model trained on defect-free product images identify anomalous surfaces in held-out inspection images?

## Proposed approach

- Use an appropriate category from MVTec AD, subject to its dataset terms.
- Train a convolutional autoencoder on normal training images.
- Calibrate the reconstruction-error threshold on a separate validation split.
- Evaluate once on held-out normal and anomalous images.
- Compare with a simple baseline and, if labels permit, a supervised classifier.

## Planned evaluation

Report AUROC, precision, recall, F1, sample counts, threshold-selection procedure, and measured inference time with hardware details. Add visual failure analysis. No results or labor savings have been established by this repository.

## Decisions the first experiment should resolve

The proposed normal-only training setup asks whether reconstruction error is enough to distinguish a defect from harmless variation in texture or lighting. A high reconstruction error could reflect either, so inspecting false positives is part of the planned evaluation.

Threshold choice should follow the intended inspection tradeoff: missed defects and unnecessary rejection of normal products are different errors. Report image-level detection separately from localization if pixel-level masks are later used. Any classifier comparison should state the additional defect labels it receives; it would not have the same training information as the normal-only autoencoder.

This is an experiment specification, not evidence that those choices have already been tested.

## Implementation checklist

- [ ] Add the original implementation if available, or develop the planned prototype.
- [ ] Add dependency and configuration files.
- [ ] Document data provenance and acquisition.
- [ ] Keep training, calibration, and test data separate.
- [ ] Commit evaluation scripts and a reproducible results report.
- [ ] Add a demonstration and meaningful tests.
