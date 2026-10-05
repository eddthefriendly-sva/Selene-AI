# Selene

Selene is a C++ desktop assistant built with Dear ImGui. It talks to a local Ollama model, remembers the last 20 exchanges, includes the current date for your chosen timezone, and searches DuckDuckGo for likely identity or current-information questions.

## First Run

Open the project folder in VS Code and install the recommended C++ and CMake extensions when prompted. Select **Terminal > Run Task > Run Selene in Terminal**. The task checks for and installs missing CMake, Git, Visual Studio 2022 C++ Build Tools, and vcpkg. CMake then installs Selene's C++ libraries and fetches Dear ImGui.

This developer setup needs `winget` and an internet connection. Installing Visual Studio Build Tools may require administrator approval and downloads several gigabytes. The bootstrap checks for existing tools and vcpkg files before installing; vcpkg and CMake reuse downloaded dependencies on later builds.

## Run in VS Code

Use **Terminal > Run Task > Run Selene in Terminal**. The task checks prerequisites, configures and builds Selene, then opens the desktop window. **Terminal > Run Build Task** performs setup and builds without launching the app.

Or build and run from PowerShell:

```powershell
.\build_windows.ps1 -Configuration Debug -Run
```

On first app launch, enter your preferred name and timezone. Selene then checks for Ollama, installs it through `winget` if needed, starts the local service, and pulls the selected model only if it is missing. The app shows setup progress while these downloads run in the background. First launch needs an internet connection and may download several gigabytes. Use **Edit profile** in the window to change your name or timezone later.

## In the App

Choose automatic, always-on, or disabled web search from the search menu. Edit the model field to switch Ollama models. Use **Clear history** to delete saved conversation history.

Set `SELENE_MODEL` to choose a different default model. Selene automatically selects an installed model whose name includes both `qwen` and `coder` if its configured default is missing. Set `OLLAMA_HOST` to use a different Ollama server address.

Profile and conversation data are stored locally in `%LOCALAPPDATA%\Selene\`. Current facts still require web search.

## Build a release executable

To build and package the Windows GUI executable, run:

```powershell
.\build_windows.ps1 -Configuration Release -Package
```

The self-contained GUI executable is written to `dist\Selene.exe`. Ollama and the model remain separate and are installed on first app launch.

Ollama performs model inference, so C++ and ImGui change the app experience and packaging, not the model's generation speed.
