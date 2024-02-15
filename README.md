# ComfyMaxing
Scripts, guides, and files for installing and using ComfyUI.
Right now I assume you're on linux for setup, maybe that won't be true later but I run everything on a local Ubuntu box.

Before I go on I'd like to give a shout out to the resources that helped me learn:
- https://youtube.com/@lizzz260?si=RdzdifKpJQ0vl4IX
- https://github.com/comfyanonymous/ComfyUI_examples
  
I recommend starting with https://github.com/ltdrdata/ComfyUI-Manager which has a script https://github.com/ltdrdata/ComfyUI-Manager/raw/main/scripts/install-comfyui-venv-linux.sh that you can run to clone and install. Do it in a place with plenty of space for storing your models and outputs. Afterwards you can run it with either ./run-gpu.sh or ./run-cpu.sh. Make sure you chmod +x it.

Install tmux so you can keep it running after closing your ssh session. I like to use tmux new-session -d -s ${service} 'cd ${serviceDirectory} && ${serviceCommand}' which creates a new detached session (remove -d to automatically attach) ie tmux new-session -d -s comfy 'cd ~/ComfyUI && ./run-gpu.sh'. If you started it detached you can attach with tmux attach -t ${service}.

After that, navigate to the interface in your browser and go to Manager on the side and Install Custom Nodes in the menu that pops up. You very much need:
- pythongosssss/ComfyUI-Custom-Scripts (math expression, string functions, saving and loading workflows, exporting workflow svgs, reroute primitive, I could go on)
- adieyal/comfyui-dynamicprompts (helping to explore prompt spaces)
- Fannovel16/comfyui_controlnet_aux (depth estimation + line extraction + more)
- cubiq/ComfyUI_IPAdapter_plus (face-id for consistent characters)

For the face-id you need to run ". venv/bin/activate" to activate the virtual environment and "pip install onnxruntime onnxruntime-gpu insightface" to install dependencies. You also need to go to https://github.com/cubiq/ComfyUI_IPAdapter_plus?tab=readme-ov-file#installation and download the checkpoints and loras and put them into ComfyUI/models/ipadater and ComfyUI/models/loras (tbh I havent used the loras yet and everything is fine).

I use the extension https://github.com/miaoshouai/miaoshouai-assistant for https://github.com/AUTOMATIC1111/stable-diffusion-webui to download models from CivitAI for checkpoints then point ComfyUI to the models folder in my webui instance. You CAN install ComfyUI inside of webui but I think it starts to suffer performance wise. You can also just download them yourself and put them in the ComfyUI models folder. I would like to try out some custom nodes for ComfyUI that handle this but I haven't gotten around to it yet. They're out there though (https://github.com/civitai/civitai_comfy_nodes).

My favorites checkpoints are:
- AnythingInkBaseV5: https://civitai.com/models/9409?modelVersionId=30163
- PastelMix[Stylized Anime Model]: https://civitai.com/models/5414?modelVersionId=6297
- RealisticVision: https://civitai.com/models/4201?modelVersionId=130072
- DreamShaper: https://civitai.com/models/4384?modelVersionId=128713
- MeinaMix: https://civitai.com/models/7240?modelVersionId=119057
- EpicRealism: https://civitai.com/models/25694?modelVersionId=143906

There are some more models you need but you can find these in Manager->Install Models. I like:
(upscalers)
- RealESRGAN x4
- ESRGAN x4
- 4x-AnimeSharp
(t2i adapters for controlnet)
- T2I-Adapter (color)
- T2I-Adapter (depth)
- T2I-Adapter (openpose)
- T2I-Adapter (sketch)
- T2I-Adapter (seg)

Okay now you should be good to go on setup and you can start workflows. I'm still learning and have a long way to go, but I will be making all of my workflows that I use public in the workflows folder as jsons and pngs with embedded workflows that you can load by right clicking the ComfyUI canvas and going to Workflow Image->Import. 

Some last tips: 
- If you select multiple nodes and right click you get "Convert to Group Node". Make liberal use of this, I like to group parts of workflows that are related like Face and Pose to make everything neater to look at. You have to right click->Convert to Nodes if you want to add anything else or remove it. Make sure you tie up connections of things that are getting grouped before grouping them too. 
- Speaking of easier to look at, the Reroute node is crucial for controlling the path of a nodes line and making things look neat too.
- You can click the little circle in the middle of a line and add a node in between the two nodes that line is connecting. This is useful for Reroute, and so much more.
- If you see something that's an input on a node, you can right click the node and go to "Convert <input> to widget" which will allow you to have that input come from another node. This is useful, but it's necessary for prompting with combinations to convert text on a CLIP Encode node into a widget so you can use Primitives, StringFunctions, and Combinatorial Prompts. (I'm working on a good example workflow for this)
