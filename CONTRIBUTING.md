# Contributing

Thanks for contributing to the H₂S Dosimeter project.

## Project boundaries

The ML pipeline, FastAPI backend, and dashboard are intentionally separated. Keep that separation intact unless there is a documented reason to change the architecture.

## Development guidelines

- Keep generated models, datasets, plots, databases, and frontend build artifacts out of Git unless they are intentionally versioned.
- Do not add real credentials or private worker data.
- Treat current ML results as prototype results: the repository documents synthetic/physics-based evaluation and real-hardware validation remains a dependency.
- Add or update tests when changing API behavior, color processing, dose estimation, or validation logic.

## Pull requests

Describe the component changed, validation performed, and any hardware/data assumptions. For UI changes, include screenshots when useful.
