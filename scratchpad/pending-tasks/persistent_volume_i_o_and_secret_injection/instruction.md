Handling large datasets and model weights requires persistent storage, but improper volume handling in Modal often leads to a "Volume busy" error if file descriptors remain open during unmounts or reloads. 

You need to create a Modal function that mounts a `modal.Volume` at `/data` and injects a Modal Secret named `my-api-keys`. The function must read the environment variable `API_KEY` and write its value to `/data/key_log.txt` in a deterministic, safe manner before explicitly committing the volume changes.

**Constraints:**
- You MUST use a Python context manager (`with open(...) as f:`) for the file write operation to prevent "Volume busy" exceptions.
- You MUST explicitly call `vol.commit()` after the file operation.
- The secret must be injected using the `secrets=[...]` parameter in the function decorator.