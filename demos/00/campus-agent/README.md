# DigiPen Campus Assistant Demo

This demo showcases an AI-powered campus assistant built with Gradio and OpenAI's agent framework. The assistant helps students with various campus-related queries including building locations, course information, campus policies, and cafe menus.

## Features

The campus assistant includes specialized agents for:
- **Building Agent**: Helps locate buildings and rooms on campus using campus maps
- **Course Agent**: Provides information about DigiPen courses and prerequisites
- **Handbook Agent**: Assists with campus policies and student conduct information
- **Cafe Agent**: Provides current menu information for the Bytes Cafe

## Prerequisites

- Python 3.11 or higher
- OpenAI API key
- Internet connection for API calls

## Setup Options

Choose one of the following setup methods:

### Option 1: Python with uv (Recommended)

1. **Install uv** (if not already installed):
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. **Navigate to the demo directory**:
   ```bash
   cd demos/00/campus-agent
   ```

3. **Set up your OpenAI API key**:
   ```bash
   export OPENAI_API_KEY="your-api-key-here"
   ```
   
   Or create a `.env` file in the project root:
   ```bash
   echo "OPENAI_API_KEY=your-api-key-here" > .env
   ```

4. **Install dependencies**:
   ```bash
   uv pip install -r requirements.txt
   ```

5. **Run the application**:
   ```bash
   uv run python main.py
   ```

6. **Access the application**:
   Open your browser and navigate to `http://localhost:7860`

### Option 2: DevContainer (VS Code)

This option provides a pre-configured development environment with all dependencies.

1. **Prerequisites**:
   - VS Code with the Dev Containers extension
   - Docker Desktop

2. **Set up your OpenAI API key**:
   Create a `.env` file in the `.devcontainer` directory:
   ```bash
   echo "OPENAI_API_KEY=your-api-key-here" > .devcontainer/.env
   ```

3. **Open in DevContainer**:
   - Open VS Code in the project root
   - Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)
   - Type "Dev Containers: Reopen in Container"
   - Select the "Demo: Campus Agent" configuration

4. **Run the application**:
   Once the container is built and running:
   ```bash
   python main.py
   ```

5. **Access the application**:
   The application will be available at `http://localhost:7860`
   (Port 7860 is automatically forwarded by the DevContainer configuration)

## Usage

Once the application is running, you can interact with the campus assistant through the web interface. Try these example queries:

- "I'm trying to find the WANIC classrooms. Can you help?"
- "What's the policy for eating in auditoriums?"
- "What's today's vegetarian dish at the Bytes Cafe?"
- "What are the prerequisites for FLM201?"

The assistant will automatically route your query to the appropriate specialized agent and provide relevant information based on the campus documents and data.

## Architecture

The demo uses a multi-agent architecture where:
- A main **DigiPen Campus Assistant** agent coordinates and routes requests
- Specialized agents handle specific domains (buildings, courses, handbook, cafe)
- Agents use tools like file search and function calls to retrieve information
- The system includes a vector store with campus documents (maps, course catalog, handbook)

## Troubleshooting

### Common Issues

1. **Missing OpenAI API Key**:
   - Ensure your API key is properly set as an environment variable or in the `.env` file
   - Verify the API key is valid and has sufficient credits

2. **Port Already in Use**:
   - If port 7860 is busy, modify the `server_port` parameter in `main.py`
   - Or kill the process using the port: `lsof -ti:7860 | xargs kill -9`

3. **Dependencies Issues**:
   - Ensure you're using Python 3.11 or higher
   - Try reinstalling dependencies: `uv pip install --force-reinstall -r requirements.txt`

4. **DevContainer Issues**:
   - Ensure Docker Desktop is running
   - Rebuild the container: "Dev Containers: Rebuild Container"
   - Check that the `.env` file exists in the `.devcontainer` directory

### Getting Help

If you encounter issues:
1. Check the console output for error messages
2. Verify all prerequisites are installed
3. Ensure your OpenAI API key is valid and properly configured
4. Try the alternative setup method if one doesn't work

## Files Overview

- `main.py`: Main application file with agent definitions and Gradio interface
- `requirements.txt`: Python dependencies
- `vector_store/files/`: Campus documents used by the file search tool
- `agent_graph.png`: Visual representation of the agent architecture
- `.devcontainer/campus-agent/devcontainer.json`: DevContainer configuration
