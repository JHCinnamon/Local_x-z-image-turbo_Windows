# Local Prompt-Based Image Generation for Windows

A small local image-generation UI for Windows. It uses Ollama to turn prompts
into images and saves the results in `outputs/`.

The image models `x/flux2-klein` and `x/z-image-turbo` currently work with
Ollama on macOS and Linux, but not Windows. This project is here to make the
Windows path a little less awkward, with Automatic1111 available as an optional
image backend.

## Getting it running

Install [Python 3.10+](https://www.python.org/downloads/) and
[Ollama](https://ollama.com/download), then start Ollama and run:

```powershell
python run.py
```

The launcher installs its missing Python packages, checks Ollama, pulls the
configured models when needed, and starts the local web UI. It will ask for a
prompt before opening the app.

The defaults live in `.env`. Copy `env.example` to `.env` if you want to change
the Ollama host, planner model, or image backend.

## Windows image backend

If the Ollama image-model runtime is unavailable on your machine, run
[Automatic1111 WebUI](https://github.com/AUTOMATIC1111/stable-diffusion-webui)
with its API enabled, then add this to `.env`:

```env
SECONDARY_IMAGE_BACKEND="automatic1111"
SECONDARY_IMAGE_BACKEND_URL="http://127.0.0.1:7860"
REQUIRE_FLUX_RUNTIME="0"
```

Start the app with:

```powershell
python run.py --allow-flux-runtime-fail
```

That is mostly it. Generated images should show up in `outputs/`.
