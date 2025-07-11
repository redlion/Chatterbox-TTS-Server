# Chatterbox TTS Server: OpenAI-Compatible API with Web UI, Large Text Handling & Built-in Voices

**Self-host the powerful [Chatterbox TTS model](https://github.com/resemble-ai/chatterbox) with this enhanced FastAPI server! Features an intuitive Web UI, a flexible API endpoint, voice cloning, large text processing via intelligent chunking, audiobook generation, and consistent, reproducible voices using built-in ready-to-use voices and a generation seed feature.**

> 🚀 **Try it now!** Test the full TTS server with voice cloning and audiobook generation in Google Colab - no installation required!
> 
> [![Open Live Demo](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/devnen/Chatterbox-TTS-Server/blob/main/Chatterbox_TTS_Colab_Demo.ipynb)

This server is based on the architecture and UI of our [Dia-TTS-Server](https://github.com/devnen/Dia-TTS-Server) project but uses the distinct `chatterbox-tts` engine. Runs accelerated on NVIDIA (CUDA) and AMD (ROCm) GPUs, with a fallback to CPU.

[![Project Link](https://img.shields.io/badge/GitHub-devnen/Chatterbox--TTS--Server-blue?style=for-the-badge&logo=github)](https://github.com/devnen/Chatterbox-TTS-Server)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
[![Python Version](https://img.shields.io/badge/Python-3.10+-blue.svg?style=for-the-badge)](https://www.python.org/downloads/)
[![Framework](https://img.shields.io/badge/Framework-FastAPI-green.svg?style=for-the-badge)](https://fastapi.tiangolo.com/)
[![Model Source](https://img.shields.io/badge/Model-ResembleAI/chatterbox-orange.svg?style=for-the-badge)](https://github.com/resemble-ai/chatterbox)
[![Docker](https://img.shields.io/badge/Docker-Supported-blue.svg?style=for-the-badge)](https://www.docker.com/)
[![Web UI](https://img.shields.io/badge/Web_UI-Included-4285F4?style=for-the-badge&logo=googlechrome&logoColor=white)](#)
[![CUDA Compatible](https://img.shields.io/badge/NVIDIA_CUDA-Compatible-76B900?style=for-the-badge&logo=nvidia&logoColor=white)](https://developer.nvidia.com/cuda-zone)
[![ROCm Compatible](https://img.shields.io/badge/AMD_ROCm-Compatible-ED1C24?style=for-the-badge&logo=amd&logoColor=white)](https://rocm.docs.amd.com/)
[![API](https://img.shields.io/badge/OpenAI_Compatible_API-Ready-000000?style=for-the-badge&logo=openai&logoColor=white)](https://platform.openai.com/docs/api-reference)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/devnen/Chatterbox-TTS-Server/blob/main/Chatterbox_TTS_Colab_Demo.ipynb)

<div align="center">
  <img src="static/screenshot-d.png" alt="Chatterbox TTS Server Web UI - Dark Mode" width="33%" />
  <img src="static/screenshot-l.png" alt="Chatterbox TTS Server Web UI - Light Mode" width="33%" />
</div>

---

## 🗣️ Overview: Enhanced Chatterbox TTS Generation

The [Chatterbox TTS model by Resemble AI](https://github.com/resemble-ai/chatterbox) provides capabilities for generating high-quality speech. This project builds upon that foundation by providing a robust [FastAPI](https://fastapi.tiangolo.com/) server that makes Chatterbox significantly easier to use and integrate.

**🚀 Want to try it instantly?** [Launch the live demo in Google Colab](https://colab.research.google.com/github/devnen/Chatterbox-TTS-Server/blob/main/Chatterbox_TTS_Colab_Demo.ipynb) - no installation needed!

The server expects plain text input for synthesis and we solve the complexity of setting up and running the model by offering:

*   A **modern Web UI** for easy experimentation, preset loading, reference audio management, and generation parameter tuning.
*   **Multi-Platform Acceleration:** Full support for **NVIDIA (CUDA)** and **AMD (ROCm)** GPUs, with an automatic fallback to **CPU**, ensuring you can run on any hardware.
*   **Large Text Handling:** Intelligently splits long plain text inputs into manageable chunks based on sentence structure, processes them sequentially, and seamlessly concatenates the audio.
*   **📚 Audiobook Generation:** Perfect for creating complete audiobooks - simply paste an entire book's text and the server automatically processes it into a single, seamless audio file with consistent voice quality throughout.
*   **Predefined Voices:** Select from curated, ready-to-use synthetic voices for consistent and reliable output without cloning setup.
*   **Voice Cloning:** Generate speech using a voice similar to an uploaded reference audio file.
*   **Consistent Generation:** Achieve consistent voice output across multiple generations or text chunks by using the "Predefined Voices" or "Voice Cloning" modes, optionally combined with a fixed integer **Seed**.
*   **Docker support** for easy, reproducible containerized deployment on any platform.

This server is your gateway to leveraging Chatterbox's TTS capabilities seamlessly, with enhanced stability, voice consistency, and large text support for plain text inputs.

## ✨ Key Features of This Server

**🔥 Live Demo Available:**
*   **🚀 [One-Click Google Colab Demo](https://colab.research.google.com/github/devnen/Chatterbox-TTS-Server/blob/main/Chatterbox_TTS_Colab_Demo.ipynb):** Try the full server with voice cloning and audiobook generation instantly in your browser - no local installation required!

This server application enhances the underlying `chatterbox-tts` engine with the following:

**🚀 Core Functionality:**

*   **Large Text Processing (Chunking):**
    *   Automatically handles long plain text inputs by intelligently splitting them into smaller chunks based on sentence boundaries.
    *   Processes each chunk individually and seamlessly concatenates the resulting audio, overcoming potential generation limits of the TTS engine.
    *   **Ideal for audiobook generation** - paste entire books and get professional-quality audiobooks with consistent narration.
    *   Configurable via UI toggle ("Split text into chunks") and chunk size slider.
*   **Predefined Voices:**
    *   Allows usage of curated, ready-to-use synthetic voices stored in the `./voices` directory.
    *   Selectable via UI dropdown ("Predefined Voices" mode).
    *   Provides reliable voice output without manual cloning setup.
*   **Voice Cloning:**
    *   Supports voice cloning using a reference audio file (`.wav` or `.mp3`).
    *   The server processes the reference audio for the engine.
*   **Generation Seed:** Added `seed` parameter to UI and API for influencing generation results. Using a fixed integer seed *in combination with* Predefined Voices or Voice Cloning helps maintain consistency.
*   **API Endpoint (`/tts`):**
    *   The primary API endpoint, offering fine-grained control over TTS generation.
    *   Supports parameters for text, voice mode (predefined/clone), reference/predefined voice selection, chunking control (`split_text`, `chunk_size`), generation settings (temperature, exaggeration, CFG weight, seed, speed factor, language), and output format.
*   **UI Configuration Management:** Added UI section to view/edit `config.yaml` settings (server, model, paths) and save generation defaults.
*   **Configuration System:** Uses `config.yaml` for all runtime configuration, managed via `config.py` (`YamlConfigManager`). If `config.yaml` is missing, it's created with default values from `config.py`.
*   **Audio Post-Processing (Optional):** Includes utilities for silence trimming, internal silence reduction, and (if `parselmouth` is installed) unvoiced segment removal to improve audio quality. These are configurable.
*   **UI State Persistence:** Web UI now saves/restores text input, voice mode selection, file selections, and generation parameters (seed, chunking, sliders) in `config.yaml` (`ui_state` section).

**🔧 General Enhancements:**

*   **Performance:** Optimized for speed and efficient VRAM usage on GPU.
*   **Web Interface:** Modern, responsive UI for plain text input, parameter adjustment, preset loading, reference/predefined audio management, and audio playback.
*   **Model Loading:** Uses `ChatterboxTTS.from_pretrained()` for robust model loading from Hugging Face Hub, utilizing the standard HF cache.
*   **Dependency Management:** Clear `requirements.txt`.
*   **Utilities:** Comprehensive `utils.py` for audio processing, text handling, and file management.

## ✅ Features Summary

*   **Core Chatterbox Capabilities (via [Resemble AI Chatterbox](https://github.com/resemble-ai/chatterbox)):**
    *   🗣️ High-quality single-speaker voice synthesis from plain text.
    *   🎤 Perform voice cloning using reference audio prompts.
*   **Enhanced Server & API:**
    *   ⚡ Built with the high-performance **[FastAPI](https://fastapi.tiangolo.com/)** framework.
    *   ⚙️ **Custom API Endpoint** (`/tts`) as the primary method for programmatic generation, exposing all key parameters.
    *   📄 Interactive API documentation via Swagger UI (`/docs`).
    *   🩺 Health check endpoint (`/api/ui/initial-data` also serves as a comprehensive status check).
*   **Advanced Generation Features:**
    *   📚 **Large Text Handling:** Intelligently splits long plain text inputs into chunks based on sentences, generates audio for each, and concatenates the results seamlessly. Configurable via `split_text` and `chunk_size`.
    *   📖 **Audiobook Creation:** Perfect for generating complete audiobooks from full-length texts with consistent voice quality and automatic chapter handling.
    *   🎤 **Predefined Voices:** Select from curated synthetic voices in the `./voices` directory.
    *   ✨ **Voice Cloning:** Simple voice cloning using an uploaded reference audio file.
    *   🌱 **Consistent Generation:** Use Predefined Voices or Voice Cloning modes, optionally with a fixed integer **Seed**, for consistent voice output.
    *   🔇 **Audio Post-Processing:** Optional automatic steps to trim silence, fix internal pauses, and remove long unvoiced segments/artifacts (configurable via `config.yaml`).
*   **Intuitive Web User Interface:**
    *   🖱️ Modern, easy-to-use interface.
    *   💡 **Presets:** Load example text and settings dynamically from `ui/presets.yaml`.
    *   🎤 **Reference/Predefined Audio Upload:** Easily upload `.wav`/`.mp3` files.
    *   🗣️ **Voice Mode Selection:** Choose between Predefined Voices or Voice Cloning.
    *   🎛️ **Parameter Control:** Adjust generation settings (Temperature, Exaggeration, CFG Weight, Speed Factor, Seed, etc.) via sliders and inputs.
    *   💾 **Configuration Management:** View and save server settings (`config.yaml`) and default generation parameters directly in the UI.
    *   💾 **Session Persistence:** Remembers your last used settings via `config.yaml`.
    *   ✂️ **Chunking Controls:** Enable/disable text splitting and adjust approximate chunk size.
    *   ⚠️ **Warning Modals:** Optional warnings for chunking voice consistency and general generation quality.
    *   🌓 **Light/Dark Mode:** Toggle between themes with preference saved locally.
    *   🔊 **Audio Player:** Integrated waveform player ([WaveSurfer.js](https://wavesurfer.xyz/)) for generated audio with download option.
    *   ⏳ **Loading Indicator:** Shows status during generation.
*   **Flexible & Efficient Model Handling:**
    *   ☁️ Downloads models automatically from [Hugging Face Hub](https://huggingface.co/) using `ChatterboxTTS.from_pretrained()`.
    *   🔄 Easily specify model repository via `config.yaml`.
    *   📄 Optional `download_model.py` script available to pre-download specific model components to a local directory (this is separate from the main HF cache used at runtime).
*   **Performance & Configuration:**
    *   💻 **GPU Acceleration:** Automatically uses NVIDIA CUDA if available, falls back to CPU.
    *   ⚙️ All configuration via `config.yaml`.
    *   📦 Uses standard Python virtual environments.
*   **Docker Support:**
    *   🐳 Containerized deployment via [Docker](https://www.docker.com/) and Docker Compose.
    *   🔌 NVIDIA GPU acceleration with Container Toolkit integration.
    *   💾 Persistent volumes for models (HF cache), custom voices, outputs, logs, and config.
    *   🚀 One-command setup and deployment (`docker compose up -d`).

## 🔩 System Prerequisites

*   **Operating System:** Windows 10/11 (64-bit) or Linux (Debian/Ubuntu recommended).
*   **Python:** Version 3.10 or later ([Download](https://www.python.org/downloads/)).
*   **Git:** For cloning the repository ([Download](https://git-scm.com/downloads)).
*   **Internet:** For downloading dependencies and models from Hugging Face Hub.
*   **(Optional but HIGHLY Recommended for Performance):**
    *   **NVIDIA GPU:** CUDA-compatible (Maxwell architecture or newer). Check [NVIDIA CUDA GPUs](https://developer.nvidia.com/cuda-gpus).
    *   **NVIDIA Drivers:** Latest version for your GPU/OS ([Download](https://www.nvidia.com/Download/index.aspx)).
    *   **AMD GPU:** ROCm-compatible (e.g., RX 6000/7000 series). Check [AMD ROCm GPUs](https://rocm.docs.amd.com/en/latest/reference/gpu-arch-specs.html).
    *   **AMD Drivers:** Latest ROCm-compatible drivers for your GPU/OS.
*   **(Linux Only):**
    *   `libsndfile1`: Audio library needed by `soundfile`. Install via package manager (e.g., `sudo apt install libsndfile1`).
    *   `ffmpeg`: For robust audio operations (optional but recommended). Install via package manager (e.g., `sudo apt install ffmpeg`).

## 💻 Installation and Setup

This project uses specific dependency files to ensure a smooth, one-command installation for your hardware. Follow the path that matches your system.

**1. Clone the Repository**
```bash
git clone https://github.com/devnen/Chatterbox-TTS-Server.git
cd Chatterbox-TTS-Server
```

**2. Create a Python Virtual Environment**

Using a virtual environment is crucial to avoid conflicts with other projects.

*   **Windows (PowerShell):**
    ```powershell
    python -m venv venv
    .\venv\Scripts\activate
    ```

*   **Linux (Bash):**
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```
    Your command prompt should now start with `(venv)`.

**3. Choose Your Installation Path**

Pick one of the following commands based on your hardware. This single command will install all necessary dependencies with compatible versions.

---

### **Option 1: CPU-Only Installation**

This is the most straightforward option and works on any machine without a compatible GPU.

```bash
# Make sure your (venv) is active
pip install --upgrade pip
pip install -r requirements.txt
```

<details>
<summary><strong>💡 How This Works</strong></summary>
The `requirements.txt` file is specially crafted for CPU users. It tells `pip` to use PyTorch's CPU-specific package repository and pins compatible versions of `torch` and `torchvision`. This prevents `pip` from installing mismatched versions, which is a common source of errors.
</details>

---

### **Option 2: NVIDIA GPU Installation (CUDA)**

For users with NVIDIA GPUs. This provides the best performance.

**Prerequisite:** Ensure you have the latest NVIDIA drivers installed.

```bash
# Make sure your (venv) is active
pip install --upgrade pip
pip install -r requirements-nvidia.txt
```

**After installation, verify that PyTorch can see your GPU:**
```bash
python -c "import torch; print(f'PyTorch version: {torch.__version__}'); print(f'CUDA available: {torch.cuda.is_available()}'); print(f'Device name: {torch.cuda.get_device_name(0) if torch.cuda.is_available() else None}')"
```
If `CUDA available:` shows `True`, your setup is correct!

<details>
<summary><strong>💡 How This Works</strong></summary>
The `requirements-nvidia.txt` file instructs `pip` to use PyTorch's official CUDA 12.1 package repository. It pins specific, compatible versions of `torch`, `torchvision`, and `torchaudio` that are built with CUDA support. This guarantees that the versions required by `chatterbox-tts` are met with the correct GPU-enabled libraries, preventing conflicts.
</details>

---

### **Option 3: AMD GPU Installation (ROCm)**

For users with modern, ROCm-compatible AMD GPUs.

**Prerequisite:** Ensure you have the latest ROCm drivers installed on a Linux system.

```bash
# Make sure your (venv) is active
pip install --upgrade pip
pip install -r requirements-rocm.txt
```

**After installation, verify that PyTorch can see your GPU:**
```bash
python -c "import torch; print(f'PyTorch version: {torch.__version__}'); print(f'ROCm available: {torch.cuda.is_available()}'); print(f'Device name: {torch.cuda.get_device_name(0) if torch.cuda.is_available() else None}')"
```
If `ROCm available:` shows `True`, your setup is correct!

<details>
<summary><strong>💡 How This Works</strong></summary>
The `requirements-rocm.txt` file works just like the NVIDIA one, but it points `pip` to PyTorch's official ROCm 5.7 package repository. This ensures that the correct GPU-enabled libraries for AMD hardware are installed, providing a stable and performant environment.
</details>

---

## 🚀 Live Demo - Try It Now! (Google Colab)

**Want to test Chatterbox TTS Server immediately without any installation?**

[![Open Live Demo](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/devnen/Chatterbox-TTS-Server/blob/main/Chatterbox_TTS_Colab_Demo.ipynb)

### Why Try the Demo?
- ✅ **Full Web UI** with all controls and features
- ✅ **Voice cloning** with uploaded audio files  
- ✅ **Predefined voices** included
- ✅ **Large text processing** with chunking (perfect for audiobooks)
- ✅ **Free GPU acceleration** (T4 GPU)
- ✅ **No installation** or setup required
- ✅ **Works on any device** with a web browser

### Quick Start:
1. **Click the badge above** to open the notebook in Google Colab
2. **Select GPU runtime**: Runtime → Change runtime type → T4 GPU → Save
3. **Run Cell 1**: Click the play button to install dependencies (~1-5 minutes)
4. **Run Cell 2**: Start the server and access the Web UI via the provided links
5. **Wait for "Server ready! Click below" message**: Locate the "localhost:8004" link and click. This starts the Web UI in your browser
6. **Generate speech**: Use the web interface to create high-quality TTS audio

### Notes:
- **First run**: Takes a few minutes to download models (one-time only)
- **Session limits**: Colab free tier has usage limits; sessions may timeout after inactivity
- **For production**: Use the local installation or Docker deployment methods below

---

*Prefer local installation? Continue reading below for full setup instructions.*

## ⚙️ Configuration

The server relies exclusively on `config.yaml` for runtime configuration.

*   **`config.yaml`:** Located in the project root. This file stores all server settings, model paths, generation defaults, and UI state. It is created automatically on the first run (using defaults from `config.py`) if it doesn't exist. **This is the main file to edit for persistent configuration changes.**
*   **UI Configuration:** The "Server Configuration" and "Generation Parameters" sections in the Web UI allow direct editing and saving of values *into* `config.yaml`.

**Key Configuration Areas (in `config.yaml` or UI):**

*   `server`: `host`, `port`, logging settings.
*   `model`: `repo_id` (e.g., "ResembleAI/chatterbox").
*   `tts_engine`: `device` ('auto', 'cuda', 'cpu'), `predefined_voices_path`, `reference_audio_path`, `default_voice_id`.
*   `paths`: `model_cache` (for `download_model.py`), `output`.
*   `generation_defaults`: Default UI values for `temperature`, `exaggeration`, `cfg_weight`, `seed`, `speed_factor`, `language`.
*   `audio_output`: `format`, `sample_rate`, `max_reference_duration_sec`.
*   `ui_state`: Stores the last used text, voice mode, file selections, etc., for UI persistence.
*   `ui`: `title`, `show_language_select`, `max_predefined_voices_in_dropdown`.
*   `debug`: `save_intermediate_audio`.

⭐ **Remember:** Changes made to `server`, `model`, `tts_engine`, or `paths` sections in `config.yaml` (or via the UI's Server Configuration section) **require a server restart** to take effect. Changes to `generation_defaults` or `ui_state` are applied dynamically or on the next page load.

## ▶️ Running the Server

**Important Note on Model Downloads (First Run):**
The very first time you start the server, it needs to download the `chatterbox-tts` model files from Hugging Face Hub. This is an **automatic, one-time process** (per model version, or until your Hugging Face cache is cleared).

*   ⏳ **Please be patient:** This download can take several minutes, depending on your internet speed and the size of the model files (typically a few gigabytes).
*   📝 **Monitor your terminal:** You'll see progress indicators or logs related to the download. The server will only become fully operational and accessible *after* these essential model files are successfully downloaded and loaded.
*   ✔️ **Subsequent starts will be much faster** as the server will use the already downloaded models from your local Hugging Face cache.

You can *optionally* use the `python download_model.py` script to pre-download specific model components to the `./model_cache` directory defined in `config.yaml`. However, please note that the runtime engine (`engine.py`) primarily loads the model from the main Hugging Face Hub cache directly, not this specific local `model_cache` directory.

**Steps to Run:**

1.  **Activate the virtual environment (if not activated):**
    *   Linux/macOS: `source venv/bin/activate`
    *   Windows: `.\venv\Scripts\activate`
2.  **Run the server:**
    ```bash
    python server.py
    ```
3.  **Access the UI:** After the server starts (and completes any initial model downloads), it should automatically attempt to open the Web UI in your default browser. If it doesn't, manually navigate to `http://localhost:PORT` (e.g., `http://localhost:8004` if your configured port is 8004).
4.  **Access API Docs:** Open `http://localhost:PORT/docs` for interactive API documentation.
5.  **Stop the server:** Press `CTRL+C` in the terminal where the server is running.

## 🔄 Updating to the Latest Version

Follow these steps to update your existing installation to the latest version from GitHub while preserving your local configuration.

**1. Navigate to Your Project Directory**
```bash
cd Chatterbox-TTS-Server
```

**2. Activate Your Virtual Environment**

*   **Windows (PowerShell):**
    ```powershell
    .\venv\Scripts\activate
    ```

*   **Linux (Bash):**
    ```bash
    source venv/bin/activate
    ```

**3. Backup Your Configuration**

⚠️ **Important:** Always backup your `config.yaml` before updating to preserve your custom settings.

```bash
# Create a backup of your current configuration
cp config.yaml config.yaml.backup
```

**4. Update the Repository**

Choose one of the following methods based on your needs:

*   **Standard Update (recommended):**
    ```bash
    git pull origin main
    ```
    If you encounter merge conflicts with `config.yaml`, continue to Step 5.

*   **Force Update (if you have conflicts or want to ensure clean update):**
    ```bash
    # Fetch latest changes and reset to match remote exactly
    git fetch origin
    git reset --hard origin/main
    ```

**5. Restore Your Configuration**

```bash
# Restore your backed-up configuration
cp config.yaml.backup config.yaml
```

**6. Check for New Configuration Options**

⭐ **Recommended:** Compare your restored config with the new default config to see if there are new options you might want to adopt.

**7. Update Dependencies**

⭐ **Important:** Always update dependencies after pulling changes. Choose the command that matches your hardware.

*   **For CPU-Only Systems:**
    ```bash
    pip install -r requirements.txt
    ```
*   **For NVIDIA GPU Systems:**
    ```bash
    pip install -r requirements-nvidia.txt
    ```
*   **For AMD GPU Systems:**
    ```bash
    pip install -r requirements-rocm.txt
    ```

**8. Restart the Server**

If the server was running, stop it (`CTRL+C`) and restart:

```bash
python server.py
```

⭐ **Note:** Your custom settings in `config.yaml` are preserved with this method. The server will automatically add any new configuration options with default values if needed. You can safely delete `config.yaml.backup` once you've verified everything works correctly.

⭐ **Docker Users:** If using Docker and you have a local `config.yaml` mounted as a volume, the same backup/restore process applies before running:
```bash
docker compose down
docker compose pull  # if using pre-built images
docker compose up -d --build
```

## 🐳 Docker Installation

Run Chatterbox TTS Server easily using Docker. The recommended method uses Docker Compose, which is pre-configured for different GPU types.

### Prerequisites

*   [Docker](https://docs.docker.com/get-docker/) installed.
*   [Docker Compose](https://docs.docker.com/compose/install/) installed (usually included with Docker Desktop).
*   **(For GPU)**
    *   **NVIDIA:** Up-to-date drivers and the [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html) installed.
    *   **AMD:** Up-to-date ROCm drivers installed on a Linux host.

### Using Docker Compose (Recommended)

This method uses the provided `docker-compose.yml` files to manage the container, volumes, and configuration easily.

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/devnen/Chatterbox-TTS-Server.git
    cd Chatterbox-TTS-Server
    ```

2.  **Start the container based on your hardware:**

    *   **For NVIDIA GPU (or CPU-only):**
        The default `docker-compose.yml` is configured for NVIDIA GPUs and will fall back to CPU if a GPU is not available.
        ```bash
        docker compose up -d --build
        ```

    *   **For AMD ROCm GPU:**
        Use the `docker-compose-rocm.yml` file, which is specifically configured for AMD GPUs.
        ```bash
        docker compose -f docker-compose-rocm.yml up -d --build
        ```

    *   The first time you run this, Docker will build the image, which involves downloading all dependencies. This can take some time. Subsequent starts will be much faster.

3.  **Troubleshooting NVIDIA GPU Errors:**
    *   If you see an error like `CDI device injection failed`, your Docker environment may not support the modern GPU syntax.
    *   **To fix this:** Open `docker-compose.yml`, comment out the `deploy` section, and uncomment the `runtime: nvidia` line as shown in the file's comments. Then run `docker compose up -d --build` again.

4.  **Access the UI:**
    Open your web browser to `http://localhost:PORT` (e.g., `http://localhost:8004` or the host port you configured).

5.  **View logs:**
    ```bash
    # For NVIDIA/CPU
    docker compose logs -f

    # For AMD
    docker compose -f docker-compose-rocm.yml logs -f
    ```

6.  **Stop the container:**
    ```bash
    # For NVIDIA/CPU
    docker compose down

    # For AMD
    docker compose -f docker-compose-rocm.yml down
    ```

### Configuration in Docker

*   The server uses `config.yaml` for its settings. The `docker-compose.yml` should mount your local `config.yaml` to `/app/config.yaml` inside the container.
*   If `config.yaml` does not exist locally when you first start, the application inside the container will create a default one (based on `config.py`), which will then appear in your local directory due to the volume mount.
*   You can then edit this local `config.yaml`. Changes to server/model/path settings typically require a container restart (`docker compose restart chatterbox-tts-server`). UI state changes are often saved live by the app.

### Docker Volumes

Persistent data is stored on your host machine via volume mounts defined in `docker-compose.yml`:

*   `./config.yaml:/app/config.yaml` (Main application configuration)
*   `./voices:/app/voices` (Predefined voice audio files)
*   `./reference_audio:/app/reference_audio` (Your uploaded reference audio files for cloning)
*   `./outputs:/app/outputs` (Generated audio files saved from UI/API)
*   `./logs:/app/logs` (Server log files)
*   `hf_cache:/app/hf_cache` (Named volume for Hugging Face model cache to persist downloads, matching `HF_HOME` in Dockerfile)

## 💡 Usage

### Web UI (`http://localhost:PORT`)

The most intuitive way to use the server:

*   **Text Input:** Enter your plain text script. **For audiobooks:** Simply paste the entire book text - the chunking system will automatically handle long texts and create seamless audio output.   
*   **Voice Mode:** Choose:
    *   `Predefined Voices`: Select a curated voice from the `./voices` directory.
    *   `Voice Cloning`: Select an uploaded reference file from `./reference_audio`.
*   **Presets:** Load examples from `ui/presets.yaml`.
*   **Reference/Predefined Audio Management:** Import new files and refresh lists.
*   **Generation Parameters:** Adjust Temperature, Exaggeration, CFG Weight, Speed Factor, Seed. Save defaults to `config.yaml`.
*   **Chunking Controls:** Toggle "Split text into chunks" and adjust "Chunk Size" for long texts.
*   **Server Configuration:** View/edit parts of `config.yaml` (requires server restart for some changes).
*   **Audio Player:** Play generated audio with waveform visualization.

### API Endpoints (`/docs` for interactive details)

The primary endpoint for TTS generation is `/tts`, which offers detailed control over the synthesis process.

*   **`/tts` (POST):** Main endpoint for speech generation.
    *   **Request Body (`CustomTTSRequest`):**
        *   `text` (string, required): Plain text to synthesize.
        *   `voice_mode` (string, "predefined" or "clone", default "predefined"): Specifies voice source.
        *   `predefined_voice_id` (string, optional): Filename of predefined voice (if `voice_mode` is "predefined").
        *   `reference_audio_filename` (string, optional): Filename of reference audio (if `voice_mode` is "clone").
        *   `output_format` (string, "wav" or "opus", default "wav").
        *   `split_text` (boolean, default True): Whether to chunk long text.
        *   `chunk_size` (integer, default 120): Target characters per chunk.
        *   `temperature`, `exaggeration`, `cfg_weight`, `seed`, `speed_factor`, `language`: Generation parameters overriding defaults.
    *   **Response:** Streaming audio (`audio/wav` or `audio/opus`).
*   **`/v1/audio/speech` (POST):** OpenAI-compatible.
    *   `input`: Text.
    *   `voice`: 'S1', 'S2', 'dialogue', 'predefined_voice_filename.wav', or 'reference_filename.wav'.
    *   `response_format`: 'opus' or 'wav'.
    *   `speed`: Playback speed factor (0.5-2.0).
    *   `seed`: (Optional) Integer seed, -1 for random.    
*   **Helper Endpoints (mostly for UI):**
    *   `GET /api/ui/initial-data`: Fetches all initial configuration, file lists, and presets for the UI.
    *   `POST /save_settings`: Saves partial updates to `config.yaml`.
    *   `POST /reset_settings`: Resets `config.yaml` to defaults.
    *   `GET /get_reference_files`: Lists files in `reference_audio/`.
    *   `GET /get_predefined_voices`: Lists formatted voices from `voices/`.
    *   `POST /upload_reference`: Uploads reference audio files.
    *   `POST /upload_predefined_voice`: Uploads predefined voice files.

## 🔍 Troubleshooting

*   **CUDA Not Available / Slow:** Check NVIDIA drivers (`nvidia-smi`), ensure correct CUDA-enabled PyTorch is installed (Installation Step 4).
*   **VRAM Out of Memory (OOM):**
    *   Ensure your GPU meets minimum requirements for Chatterbox.
    *   Close other GPU-intensive applications.
    *   If processing very long text even with chunking, try reducing `chunk_size` (e.g., 100-150).
*   **Import Errors (e.g., `chatterbox-tts`, `librosa`):** Ensure virtual environment is active and `pip install -r requirements.txt` completed successfully.
*   **`libsndfile` Error (Linux):** Run `sudo apt install libsndfile1`.
*   **Model Download Fails:** Check internet connection. `ChatterboxTTS.from_pretrained()` will attempt to download from Hugging Face Hub. Ensure `model.repo_id` in `config.yaml` is correct.
*   **Voice Cloning/Predefined Voice Issues:**
    *   Ensure files exist in the correct directories (`./reference_audio`, `./voices`).
    *   Check server logs for errors related to file loading or processing.
*   **Permission Errors (Saving Files/Config):** Check write permissions for `./config.yaml`, `./logs`, `./outputs`, `./reference_audio`, `./voices`, and the Hugging Face cache directory if using Docker volumes.
*   **UI Issues / Settings Not Saving:** Clear browser cache/local storage. Check browser developer console (F12) for JavaScript errors. Ensure `config.yaml` is writable by the server process.
*   **Port Conflict (`Address already in use`):** Another process is using the port. Stop it or change `server.port` in `config.yaml` (requires server restart).
*   **Generation Cancel Button:** This is a "UI Cancel" - it stops the *frontend* from waiting but doesn't instantly halt ongoing backend model inference. Clicking Generate again cancels the previous UI wait.

### Selecting GPUs on Multi-GPU Systems

Set the `CUDA_VISIBLE_DEVICES` environment variable **before** running `python server.py` to specify which GPU(s) PyTorch should see. The server uses the first visible one (effectively `cuda:0` from PyTorch's perspective).

*   **Example (Use only physical GPU 1):**
    *   Linux/macOS: `CUDA_VISIBLE_DEVICES="1" python server.py`
    *   Windows CMD: `set CUDA_VISIBLE_DEVICES=1 && python server.py`
    *   Windows PowerShell: `$env:CUDA_VISIBLE_DEVICES="1"; python server.py`

*   **Example (Use physical GPUs 6 and 7 - server uses GPU 6):**
    *   Linux/macOS: `CUDA_VISIBLE_DEVICES="6,7" python server.py`
    *   Windows CMD: `set CUDA_VISIBLE_DEVICES=6,7 && python server.py`
    *   Windows PowerShell: `$env:CUDA_VISIBLE_DEVICES="6,7"; python server.py`

**Note:** `CUDA_VISIBLE_DEVICES` selects GPUs; it does **not** fix OOM errors if the chosen GPU lacks sufficient memory.
## 🤝 Contributing

Contributions are welcome! Please feel free to open an issue to report bugs or suggest features, or submit a Pull Request for improvements.

## 📜 License

This project is licensed under the **MIT License**.

You can find it here: [https://opensource.org/licenses/MIT](https://opensource.org/licenses/MIT)

## 🙏 Acknowledgements

*   **Core Model:** This project utilizes the **[Chatterbox TTS model](https://github.com/resemble-ai/chatterbox)** by **[Resemble AI](https://www.resemble.ai/)**.
*   **UI Inspiration:** Special thanks to **[Lex-au](https://github.com/Lex-au)** whose **[Orpheus-FastAPI](https://github.com/Lex-au/Orpheus-FastAPI)** project served as inspiration for the web interface design.
*   **Similar Project:** This server shares architectural similarities with our [Dia-TTS-Server](https://github.com/devnen/Dia-TTS-Server) project, which uses a different TTS engine.
*   **Containerization Technologies:** [Docker](https://www.docker.com/) and [NVIDIA Container Toolkit](https://github.com/NVIDIA/nvidia-docker).
*   **Core Libraries:**
    *   [FastAPI](https://fastapi.tiangolo.com/)
    *   [Uvicorn](https://www.uvicorn.org/)
    *   [PyTorch](https://pytorch.org/)
    *   [Hugging Face Hub](https://huggingface.co/docs/huggingface_hub/index) & [SafeTensors](https://github.com/huggingface/safetensors)
    *   [Descript Audio Codec (DAC)](https://github.com/descriptinc/descript-audio-codec)
    *   [SoundFile](https://python-soundfile.readthedocs.io/) & [libsndfile](http://www.mega-nerd.com/libsndfile/)
    *   [Jinja2](https://jinja.palletsprojects.com/)
    *   [WaveSurfer.js](https://wavesurfer.xyz/)
    *   [Tailwind CSS](https://tailwindcss.com/) (via CDN)