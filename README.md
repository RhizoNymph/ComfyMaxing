# ComfyMaxing
Scripts, guides, and files for installing and using ComfyUI.

I have run everything here on both Ubuntu and Windows 11 unless explicitly stated.
For installing, I /highly/ recommend you use https://lykos.ai/ and download StabilityMatrix. It's an open source cross platform stable diffusion package manager that I think is incredibly good and now support on Patreon. You should too. I'm going to make a markdown document in the repo root that goes over installing ComfyUI it, with screenshots. 

After that, navigate to the interface in your browser and go to Manager on the side and Install Custom Nodes in the menu that pops up. You very much need:
- pythongosssss/ComfyUI-Custom-Scripts (math expression, string functions, saving and loading workflows, exporting workflow svgs, reroute primitive, I could go on)
- adieyal/comfyui-dynamicprompts (helping to explore prompt spaces)
- Fannovel16/comfyui_controlnet_aux (depth estimation + line extraction + more)
- cubiq/ComfyUI_IPAdapter_plus (face-id for consistent characters)
- https://github.com/jags111/efficiency-nodes-comfyui (XY plots of parameters)

NOTE: I actually haven't gotten insightface working on windows yet.
For the face-id you need to run ". venv/bin/activate" to activate the virtual environment and "pip install onnxruntime onnxruntime-gpu insightface" to install dependencies. You also need to go to https://github.com/cubiq/ComfyUI_IPAdapter_plus?tab=readme-ov-file#installation and download the checkpoints and loras and put them into ComfyUI/models/ipadater and ComfyUI/models/loras (tbh I havent used the loras yet and everything is fine). 

I mostly use SDXL these days, I get a lot better results with it. My favorite checkpoints are:
- animagine-xl (https://civitai.com/models/260267)
- anything xl (https://civitai.com/models/9409)
- blue_pencil-xl (https://civitai.com/models/119012)
- counterfeitxl (https://civitai.com/models/118406)
- unstable diffusers (https://civitai.com/models/84040)

Some last tips: 
- If you select multiple nodes and right click you get "Convert to Group Node". Make liberal use of this, I like to group parts of workflows that are related like Face and Pose to make everything neater to look at. You have to right click->Convert to Nodes if you want to add anything else or remove it. Make sure you tie up connections of things that are getting grouped before grouping them too. 
- Speaking of easier to look at, the Reroute node is crucial for controlling the path of a nodes line and making things look neat too.
- You can click the little circle in the middle of a line and add a node in between the two nodes that line is connecting. This is useful for Reroute, and so much more.
- If you see something that's an input on a node, you can right click the node and go to "Convert <input> to widget" which will allow you to have that input come from another node. This is useful, but it's necessary for prompting with combinations to convert text on a CLIP Encode node into a widget so you can use Primitives, StringFunctions, and Combinatorial Prompts. (I'm working on a good example workflow for this)
