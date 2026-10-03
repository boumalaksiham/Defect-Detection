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

## Implementation checklist

- [ ] Add the original implementation if available, or develop the planned prototype.
- [ ] Add dependency and configuration files.
- [ ] Document data provenance and acquisition.
- [ ] Keep training, calibration, and test data separate.
- [ ] Commit evaluation scripts and a reproducible results report.
- [ ] Add a demonstration and meaningful tests.
