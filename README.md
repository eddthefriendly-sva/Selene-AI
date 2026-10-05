# Selene

Selene is a C++ terminal assistant that talks to a local Ollama model. It remembers the last 20 exchanges, includes the current date for your chosen timezone, and searches DuckDuckGo for likely identity or current-information questions.

## Requirements

- Windows 10 or later
- Visual Studio 2022 Build Tools with the **Desktop development with C++** workload
- CMake 3.25 or later
- Git
- vcpkg

Install vcpkg from PowerShell:

```powershell
git clone https://github.com/microsoft/vcpkg "$env:USERPROFILE\vcpkg"
& "$env:USERPROFILE\vcpkg\bootstrap-vcpkg.bat"
$env:VCPKG_ROOT = "$env:USERPROFILE\vcpkg"
```

Open the project folder in VS Code and install the recommended C++ and CMake extensions when prompted. The CMake configure step downloads and builds Selene's C++ libraries through vcpkg.

## Run in VS Code

Use **Terminal > Run Task > Run Selene in Terminal**. The task configures and builds Selene, then opens interactive chat in the integrated terminal. **Terminal > Run Build Task** builds without launching it.

Or build and run from PowerShell:

```powershell
cmake --preset windows-msvc
cmake --build --preset windows-msvc
.\out\build\windows-msvc\Debug\Selene.exe --chat
```

The first run asks what Selene should call you and which timezone to use. It then installs Ollama through `winget` if needed, starts the local Ollama service, and pulls the default model. First run needs an internet connection and may download several gigabytes. Use `Selene --setup-profile` to change your name or timezone later.

## Commands

```powershell
Selene
Selene "Explain this PowerShell error"
Selene "Who is Ada Lovelace?"
Selene --no-search "Who is Ada Lovelace?"
Selene --search "Explain this PowerShell error"
Selene --model qwen2.5-coder:14b "Review this design"
Selene --setup-profile
Selene --reset-memory
```

Set `SELENE_MODEL` to choose a different default model. Selene automatically selects an installed model whose name includes both `qwen` and `coder` if its configured default is missing. Set `OLLAMA_HOST` to use a different Ollama server address.

Profile and conversation data are stored locally in `%LOCALAPPDATA%\Selene\`. Use `Selene --reset-memory` to remove the saved conversation history. Current facts still require web search.

## Build a release executable

With the requirements above installed, run:

```powershell
.\build_windows.ps1
```

The self-contained console executable is written to `dist\Selene.exe`. Ollama and the model remain separate and are installed on first use.

Ollama performs model inference, so rewriting the client in C++ mainly changes startup and packaging; it does not make the model itself generate answers faster.
