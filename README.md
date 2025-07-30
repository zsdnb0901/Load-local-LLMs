# Load-local-LLMs
Choose a model you like from: https://ollama.com/search

deepseek-r1 as an example: 

download command: 
<pre> ollama pull deepseek-r1 </pre>

run command: 
<pre> ollama run deepseek-r1  </pre>

Then you can ask questions and get responses. 

# Call the model with "requests" in Python

Python: 
<pre> import requests  </pre>

define a request: 
<pre> 
def ask_ollama(prompt_text: str, model_name='deepseek-r1') -> str:
    try:
        response = requests.post(
            'http://localhost:11434/api/generate',
            json={
                "model": model_name,
                "prompt": prompt_text, # enter here or define somewhere else
                "stream": False
            }
        )
        res_json = response.json()
        return res_json.get('response', 'no model found or no responses')
    except Exception as e:
        return f"error: {str(e)}"  </pre>
