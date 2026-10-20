# Penguin VR build progress

A static progress page for the Penguin VR study build (Waddle and Hatched). It reads three JSON files and draws the timeline, owner progress, task table and done-when checklist.

## Publish on GitHub Pages

1. Put these files at the root of a repository (or in a `docs/` folder).
2. In the repository, open **Settings → Pages**, set **Source** to "Deploy from a branch", and pick the branch and folder.
3. The page appears at `https://<your-username>.github.io/<repo-name>/` after a minute or two.

The page loads its data with `fetch`, so opening `index.html` straight from disk won't work. To preview locally, run `python3 -m http.server` in this folder and open http://localhost:8000.

## Update progress

Edit the files in `data/` (the GitHub web editor is fine) and commit. The page picks up the change on the next load.

- **`data/tasks.json`**: one entry per task. Change `status` to one of `not_started`, `in_progress`, `blocked` or `done`. Use `note` for a short reason, such as why a task is blocked; it shows when you hover over the task's bar.
- **`data/checks.json`**: one entry per done-when check. Set `done` to `true` when the check passes.
- **`data/meta.json`**: set `updated` to today's date and `by` to your name. This shows under the title.

Example:

```json
{ "id": "T2", "status": "blocked", "note": "Waiting on LSL test results" }
```

Keep the other fields (`id`, `order`, `title`, `owner`, `start`, `end`, `priority`, `area`) as they are unless the plan changes. Dates use the `YYYY-MM-DD` format.

## Files

- `index.html`: the page. It loads d3 from cdnjs and fonts from Google Fonts.
- `data/`: the progress data.
- `.nojekyll`: tells GitHub Pages to serve the files as they are.
