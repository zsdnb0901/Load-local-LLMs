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
<pre> import base64
def ask_vision_model(image_path, vision_prompt=" "):
    with open(image_path, "rb") as f:
        img_base64 = base64.b64encode(f.read()).decode("utf-8")

    response = requests.post(
        "http://localhost:11434/api/generate",
        json={
            "model": "qwen2.5vl:7b",
            "prompt": vision_prompt,
            "images": [img_base64],
            "stream": False
        }
    )
    res = response.json()
    return res.get("response", "error: no model") </pre>

If it is an image input: 
qwen2.5 as an example
<pre> 
import base64
def ask_vision_model(image_path, vision_prompt=" "):  # enter prompt about the image here
    with open(image_path, "rb") as f:
        img_base64 = base64.b64encode(f.read()).decode("utf-8")
    response = requests.post(
        "http://localhost:11434/api/generate",
        json={
            "model": "qwen2.5vl:7b",
            "prompt": vision_prompt,
            "images": [img_base64],
            "stream": False
        }
    )
    res = response.json()
    return res.get("response", "error: no model")
