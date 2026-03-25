Loading large model weights into VRAM during a serverless cold start introduces significant initialization latency. Modal mitigates this using Checkpoint/Restore in userspace (Memory Snapshots) coupled with class-based lifecycle decorators.

You need to design a Modal class named `ModelRunner` configured to use an `H100` GPU. Implement an initialization method that simulates loading a large model weight by pausing for 2 seconds, and a generation method that returns the string "Model Ready". You must configure the class so that the initialization state is frozen at build time, completely bypassing the 2-second delay during live container boots.

**Constraints:**
- You MUST set `enable_memory_snapshot=True` in the `@app.cls(...)` decorator.
- You MUST use the `@modal.enter` decorator for the initialization method.
- The hardware must be explicitly defined as `gpu="H100"`.