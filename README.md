# SCT LLM

A Python script that loads the `vikhyatk/moondream2` vision-language model, analyzes frames from an RTSP camera stream, and can send alerts to a webhook when the model's response contains "yes".

## Requirements

- Python 3.10 or newer
- A network connection to download the model and, if needed, the fallback demo image
- Optional: an NVIDIA GPU for faster inference

The script loads the model with Hugging Face `trust_remote_code=True`, which executes model code downloaded from the model repository.

## Setup (Windows PowerShell)

From the project directory, create and activate a virtual environment:

```powershell
py -3.10 -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install the dependencies:

```powershell
python -m pip install --upgrade pip
python -m pip install torch torchvision accelerate opencv-python pillow requests einops "transformers<5"
```

## Configuration and run

Set the RTSP stream URL before starting the script. Set the webhook URL if alerts should be delivered; otherwise, the script uses a mock webhook and only prints the alert.

```powershell
$env:SCT_RTSP_URL = "rtsp://camera-host/path"
$env:SCT_ALERT_WEBHOOK_URL = "https://your-webhook-url"
python sct_llm.py
```

Keep camera and webhook credentials out of source control. The script requires `SCT_RTSP_URL`; if it cannot connect to that stream, it tries one sample image as a fallback. Press `Ctrl+C` to stop stream analysis.
