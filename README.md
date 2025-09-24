# AG2 Experiments

This project demonstrates multi-agent conversational workflows using the [AG2 framework](github.com/ag2ai/ag2). It includes swarm orchestration examples for airline customer service scenarios, such as flight modification, cancellation, and lost baggage handling.

This was taken and adapted from the AG2 examples.

Note that at least **I** could not get this to work with the OpenAI Azure backend and had to use native OpenAI or a local Ollama server, see the Important Notes / Issues section below.

## Structure

- `swarm_example/`: Jupyter notebooks with swarm agent chat examples.
- `resources.json`: Example resources for agents.

## Requirements

- Python 3.8+
- Install dependencies with `uv sync`.

## Usage

- Run one of the notebooks in `swarm_example/` to see agent chat orchestration in action.

## Important Notes / Issues

1. I could not get this to work with the OpenAI Azure backend. When executing I get

    ```
        Next speaker: Triage_Agent
  
        >>>>>>>> USING AUTO REPLY...
    ```

      and then a really long traceback ending with

      ```python
        [...]
        File C:\dev\git\ag2_experiments\.venv\Lib\site-packages\openai\_base_client.py:1259, in SyncAPIClient.post(self, path, cast_to, body, options, files, stream, stream_cls)
           1245 def post(
           1246     self,
           1247     path: str,
           (...)   1254     stream_cls: type[_StreamT] | None = None,
           1255 ) -> ResponseT | _StreamT:
           1256     opts = FinalRequestOptions.construct(
           1257         method="post", url=path, json_data=body, files=to_httpx_files(files), **options
           1258     )
        -> 1259     return cast(ResponseT, self.request(cast_to, opts, stream=stream, stream_cls=stream_cls))
        
        File C:\dev\git\ag2_experiments\.venv\Lib\site-packages\openai\_base_client.py:1047, in SyncAPIClient.request(self, cast_to, options, stream, stream_cls)
           1044             err.response.read()
           1046         log.debug("Re-raising status error")
        -> 1047         raise self._make_status_error_from_response(err.response) from None
           1049     break
           1051 assert response is not None, "could not resolve response (should never happen)"
        
            NotFoundError: Error code: 404 - {'error': {'code': '404', 'message': 'Resource not found'}}
      ```

      Apparently, at the first call to OpenAI's API, a 404 error is returned. I have not been able to figure out why.
  
2. With the **OpenAI** (without Azure) or **Ollama** backends, at least I could get it to work, but I had to fix couple of stuff. Most importantly, you also need to **Patch swarm_agent.py at `transfer_to_agent` and add `**kwargs:Any` to the function definition to prevent and unexpected keyword argument error.**

Also, the output is somewhat messy; it is hard to see what input is requested of the user.
