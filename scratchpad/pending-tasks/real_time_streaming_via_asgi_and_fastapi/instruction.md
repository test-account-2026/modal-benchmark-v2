Modal's custom `modal-http` proxy allows serverless functions to act as persistent web endpoints without the traditional execution time or bandwidth limits of standard API gateways. 

You need to create a Modal application that exposes a FastAPI web endpoint at the route `/stream`. The endpoint must use FastAPI's `StreamingResponse` to yield 10 sequential string tokens (e.g., "token_1", "token_2") with an asynchronous 0.1-second delay between each, simulating a real-time LLM Server-Sent Events (SSE) stream.

**Constraints:**
- You MUST expose the application using the `@modal.fastapi_endpoint()` decorator.
- The response MUST be a valid asynchronous generator stream utilizing `StreamingResponse`.
- Do NOT use synchronous blocking delays (e.g., `time.sleep`); use `asyncio.sleep`.