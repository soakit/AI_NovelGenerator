# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

AI_NovelGenerator (自动小说生成工具) is a Chinese novel generation tool that uses Large Language Models to create coherent, long-form novels with consistent characters and plots. The application features a GUI built with CustomTkinter and supports multiple LLM backends including OpenAI, DeepSeek, Gemini, Azure, and local Ollama models.

## Core Architecture

The application follows a modular architecture with clear separation of concerns:

- **Entry Point**: `main.py` - Launches the CustomTkinter GUI application
- **UI Layer**: `ui/` package - Contains all GUI components organized by functionality
- **Generation Engine**: `novel_generator/` package - Core novel generation logic
- **Adapters**: `llm_adapters.py`, `embedding_adapters.py` - Unified interfaces for different AI services
- **Configuration**: `config_manager.py` - Handles settings persistence and API configuration
- **Utilities**: `utils.py`, `consistency_checker.py` - Support functions and validation

### Key Components

1. **Novel Generation Pipeline** (`novel_generator/`):
   - `architecture.py` - World building and character system generation
   - `blueprint.py` - Chapter outline and story structure planning
   - `chapter.py` - Individual chapter content generation
   - `finalization.py` - Chapter review and state updates
   - `knowledge.py` - Knowledge base and document integration
   - `vectorstore_utils.py` - Vector database operations for context retrieval

2. **UI Modules** (`ui/`):
   - `main_window.py` - Primary application window
   - `config_tab.py` - LLM and embedding model configuration
   - `chapters_tab.py` - Chapter generation and editing interface
   - `character_tab.py` - Character management and development
   - `setting_tab.py` - Novel world-building and settings

3. **AI Integration**:
   - Supports multiple LLM providers through unified adapter pattern
   - Vector embeddings for long-term context consistency
   - ChromaDB for local vector storage
   - Semantic retrieval for maintaining plot coherence

## Common Development Commands

### Running the Application
```bash
python main.py
```

### Installing Dependencies
```bash
pip install -r requirements.txt
```

### Building Executable
```bash
pip install pyinstaller
pyinstaller main.spec
```
The executable will be generated in `dist/AI_NovelGenerator_V1.4.4/`

### Testing LLM Configuration
The application includes built-in configuration testing through the GUI. No separate test commands are defined.

## Configuration Management

The application uses `config.json` for persistent settings including:
- API keys and endpoints for various LLM services
- Model parameters (temperature, max_tokens, timeout)
- Novel generation settings (topic, genre, chapter count, word count)
- Embedding model configuration for vector retrieval
- File output paths

Configuration is managed through `config_manager.py` with thread-safe operations for testing API connectivity.

## Vector Database Integration

The application uses ChromaDB for maintaining long-term story context:
- Stores chapter summaries, character states, and plot points
- Enables semantic retrieval of relevant context during generation
- Supports multiple embedding models (OpenAI, local Ollama models)
- Vector store located in `vectorstore/` directory (created at runtime)

## Multi-Language LLM Support

The adapter system (`llm_adapters.py`) provides unified interfaces for:
- OpenAI/OpenAI-compatible APIs (including DeepSeek)
- Google Gemini
- Azure OpenAI and Azure AI Studio
- Local Ollama models
- Custom base URL handling with automatic `/v1` suffix management

## File Organization Patterns

Generated novels are organized with structured naming:
- `Novel_setting.txt` - World building and character definitions
- `Novel_directory.txt` - Chapter outlines and structure
- `chapter_X.txt` - Individual chapter content
- `outline_X.txt` - Chapter-specific outlines
- `global_summary.txt` - Overall story state
- `character_state.txt` - Character development tracking
- `plot_arcs.txt` - Plot point management

## Important Notes

- The application is primarily designed for Chinese novel generation
- GUI uses CustomTkinter for modern interface styling
- Supports both cloud-based and local LLM deployments
- Vector embeddings are essential for maintaining story consistency across long narratives
- Configuration testing is integrated into the UI workflow