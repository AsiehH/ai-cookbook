

- Add these lines in the `project.toml` file.

	```
	[tool.uv]
	add-bounds = "exact"
	exclude-newer = "7 days"
	```
- commit `uv.lock` to git. This is your source of truth. It pins every package and carries SHA-256 hashes 
verified on every install. 

	By default, `uv sync` silently rewrites the lockfile if `pyproject.toml ` changed. With `--locked`, the build fails instead. An AI agent quietly adding a package, a teammate's accidental bump, anything that drifted gets rejected before it merges.
	

**Pin uv itself too. It's part of your supply chain.**

- run `uv sync --locked` 	

- `uv audit --frozen` scans your dependencies for known vulnerabilities and "adverse" project statuses [ref](https://astral.sh/blog/uv-audit).
