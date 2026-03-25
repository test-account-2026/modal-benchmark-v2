Modal allows developers to execute Python mapping functions concurrently across remote containers, but enforces a strict hard limit of 1,000 concurrent inputs per `.map()` invocation. 

You need to implement a Modal local entrypoint that processes an array of 5,000 mock image URLs using a remote Modal function called `process_image`. You must implement a batching or chunking mechanism to ensure no more than 800 inputs are submitted to `process_image.map()` at any given time. Aggregate all 5,000 processed results and save them to `results.json`.

**Constraints:**
- You MUST NOT exceed the 1,000 concurrent input limit for any single `.map()` call.
- You MUST use `Function.map()` rather than standard Python multiprocessing or sequential loops for the remote execution.