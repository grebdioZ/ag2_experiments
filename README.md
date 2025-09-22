# AG2 Experiments

This project demonstrates multi-agent conversational workflows using the Autogen (AG2) framework. It includes swarm orchestration examples for airline customer service scenarios, such as flight modification, cancellation, and lost baggage handling.

# HOWEVER

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
  
2. With the ollama client, at least I could proceed, but then

* I needed to patch swarm_agent.py at `transfer_to_agent` and add `**kwargs:Any` to the function definition to prevent and unexpected keyword argument error.
* I needed to use at least the qwen-8b model to get it somewhat to work, but after asking the user for the flight number, the system just keeps alternating between swarm executor with function `transfer_Triage_Agent_to_Flight_Modification_Agent` and the triage agent until the maximum number of iterations (50) was reached.

## Structure
- `swarm_example/`: Jupyter notebooks with swarm agent chat examples.
- `resources.json`: Example resources for agents.

## Requirements
- Python 3.8+
- Install dependencies with `pip install -r requirements.txt` (or use `pyproject.toml` if available).

## Usage
Run the notebooks in `swarm_example/` to see agent chat orchestration in action.

