# ROS 2 Methodology documentation

This directory contains an MkDocs site for documenting ROS 2 engineering patterns.

## Preview locally

```bash
cd ros2_methodology
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
mkdocs serve
```

Open <http://127.0.0.1:8000> in a browser. MkDocs reloads the page as files in
`docs/` change.

## Build the static site

```bash
mkdocs build
```

The generated site is written to `site/`, which is intentionally ignored by Git.
Navigation and site settings live in `mkdocs.yml`.
