# Load-local-LLMs
Choose a model you like from: https://ollama.com/search

deepseek-r1 as an example: 

download command: 
<pre> ollama pull deepseek-r1 </pre>

run command: 
<pre> ollama run deepseek-r1  </pre>

Then you can ask questions and get responses. 

<img width="1113" height="628" alt="image" src="https://github.com/user-attachments/assets/1053f315-0bc3-4118-b3d5-66b33583833f" />



# Call the model with "requests" in Python

After you download a model, you can call it in your code in the following way. Then, we can apply LLMs in our local/offline project. An interesting example in my repository [LLMcooker](https://github.com/zsdbn0901/LLMcooker) shows the convenience. Take a picture of your refrigerator， and a visual LLM will detect what you have. Then, with the detected supplies, it will provide how to cook and their estimated time. 

Python: 
<pre> import requests  </pre>

define a request: 
<pre> def ask_ollama(prompt_text: str, model_name='deepseek-r1') -> str:
    try:
        response = requests.post(
            'http://localhost:11434/api/generate',
            json={
                "model": model_name,
                "prompt": prompt_text,  #<span style="color:green">enter here or define where you need to use</span> 
                "stream": False
            }
        )
        res_json = response.json()
        return res_json.get('response', 'no model or no responses')
    except Exception as e:
        return f"error: {str(e)}"    </pre>

If it is an image input: 

qwen2.5 as an example
<pre>import base64
def ask_vision_model(image_path, vision_prompt=" "):  # enter prompt about the image here or define where you need to use
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
    return res.get("response", "error: no model")</pre>


