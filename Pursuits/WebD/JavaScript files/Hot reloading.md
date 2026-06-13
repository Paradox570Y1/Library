**Hot reloading** is a developer convenience feature that lets you **see code changes instantly while an app is running**, _without restarting it_ and (often) _without losing state_.
## What actually happens under the hood

Hot reloading:
- Detects file changes
- Recompiles **only the changed parts**
- Injects the new code into the running app
- Tries to preserve in-memory state (variables, UI state, etc.)