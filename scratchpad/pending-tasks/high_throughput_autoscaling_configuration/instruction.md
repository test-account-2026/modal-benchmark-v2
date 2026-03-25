Differentiating between queueing latency and initialization latency is critical. To handle sudden bursts of traffic without incurring excessive queueing times, Modal allows fine-grained autoscaler tuning.

You need to configure a Modal function for a mock inference workload that outputs its own configuration dictionary to a local `config.json` file. Configure the Modal function's autoscaler to maintain exactly 2 warm replicas active at all times to avoid cold starts. Furthermore, instruct the autoscaler to only spin up a new container when the active concurrent requests per replica exceed 15.

**Constraints:**
- You MUST explicitly set the parameter `min_containers=2` to maintain warm replicas.
- You MUST explicitly set the parameter `target_inputs=15` to manage the concurrency-based scaling threshold.
- The output JSON must accurately reflect these exact integer values.