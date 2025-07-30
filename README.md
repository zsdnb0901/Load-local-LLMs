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
def ask_ollama(prompt_text: str, model_name='llama3:8b') -> str:
    """将 prompt_text 发给本地 Ollama 并返回回答"""
    try:
        response = requests.post(
            'http://localhost:11434/api/generate',
            json={
                "model": model_name,
                "prompt": prompt_text,
                "stream": False
            }
        )
        res_json = response.json()
        return res_json.get('response', '⚠️ 没有返回 response 字段')
    except Exception as e:
        return f"Ollama 请求失败: {str(e)}"  </pre>
