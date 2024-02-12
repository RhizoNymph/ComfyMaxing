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
