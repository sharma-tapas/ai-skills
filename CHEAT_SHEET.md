# A collection of steps I need to perform manually

## Setup GRAPHIFY

```bash
uvx graphify@0.14.0 --no-install
export PATH="/Users/tapassharma/go/src/github.com/sharma-tapas/graphify/.venv/bin:$PATH"
mcp-server run "uvx -m graphify"
```

```bash
uv tool install graphifyy && graphify install
# or: pipx install graphifyy && graphify install
# or: pip install graphifyy && graphify install
```

```
/mcp-server run "uvx graphify@0.14.0 --no-install"
```

```
claude skill add safishamsi/graphify
/graphify ~/.claude
```

Change the Skills to **Always** query the knowledge graph first, **before** accessing the codebase. I want to query the code as a last resort.

## Useful commands

```
/graphify .                        # build graph for current folder
/graphify ./docs --update          # re-extract only changed files
/graphify . --cluster-only         # rerun clustering without re-extracting
/graphify . --no-viz               # skip the HTML, just the report + JSON
/graphify . --wiki                 # build a markdown wiki from the graph
graphify export callflow-html      # architecture/call-flow HTML from graphify-out/

/graphify query "what connects auth to the database?"
/graphify path "UserService" "DatabasePool"
/graphify explain "RateLimiter"

/graphify add https://arxiv.org/abs/1706.03762   # fetch a paper and add it
/graphify add <youtube-url>                       # transcribe and add a video

graphify hook install              # auto-rebuild on git commit
graphify merge-graphs a.json b.json              # combine two graphs
```


```
# .graphifyignore
node_modules/
dist/
vendor/
.venv/
*.generated.py

# only index src/, ignore everything else
*
!src/
!src/**
```


## Team setup for graphify

graphify-out/ is meant to be committed to git so everyone on the team starts with a map.

Recommended .gitignore additions:
```
graphify-out/manifest.json    # mtime-based, breaks after git clone
graphify-out/cost.json        # local only
# graphify-out/cache/         # optional: commit for speed, skip to keep repo small
```

Workflow:

    One person runs /graphify . and commits graphify-out/.
    Everyone pulls — their assistant reads the graph immediately.
    Run graphify hook install to auto-rebuild after each commit (AST only, no API cost). This also sets up a git merge driver so graph.json is never left with conflict markers — two devs committing in parallel get their graphs union-merged automatically.
    When docs or papers change, run /graphify --update to refresh those nodes.


##Run tests

/run-tests

##Run tdd tests 