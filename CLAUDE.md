# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

DeerFlow is a deep research framework that implements a multi-agent system using LangGraph. It combines LLMs with web search, crawling, and code execution capabilities to generate comprehensive research reports.

## Technology Stack

- **Backend**: Python 3.12+ with FastAPI, LangChain/LangGraph, LiteLLM
- **Frontend**: Next.js 15+ with React 19, TypeScript, Radix UI, Tailwind CSS
- **Package Managers**: uv (Python), pnpm (Node.js)
- **Databases**: MongoDB, PostgreSQL (for checkpointing)

## Common Development Commands

### Setup & Installation
```bash
uv sync                    # Install Python dependencies
cd web && pnpm install     # Install frontend dependencies
```

### Running the Application
```bash
uv run main.py             # Console UI
./bootstrap.sh -d         # Full stack development mode
uv run server.py --reload  # API server only
cd web && pnpm dev        # Frontend development server
```

### Testing & Quality
```bash
make test                  # Run all tests
make coverage             # Run tests with coverage
make lint                 # Python linting (ruff, mypy)
make lint-frontend        # Frontend linting (eslint, prettier)
```

### Docker Operations
```bash
# Build Docker image
docker build -t deer-flow-api .

# Run with Docker
docker run -d -t -p 127.0.0.1:8000:8000 --env-file .env --name deer-flow-api-app deer-flow-api

# Docker Compose (backend + frontend)
docker compose build
docker compose up
```

## Architecture Overview

### Multi-Agent System Architecture
The system uses a 4-component multi-agent architecture orchestrated by LangGraph:

1. **Coordinator** (`backend/agent/coordinator.py`) - Entry point and workflow management
2. **Planner** (`backend/agent/planner.py`) - Task decomposition and planning
3. **Research Team** (`backend/agent/research_team.py`) - Specialized agents (Researcher, Coder)
4. **Reporter** (`backend/agent/reporter.py`) - Final report generation

### Key Components

- **Graph State Management**: Uses LangGraph's state graph pattern with typed state classes
- **Tool Integration**: Web search, crawling, code execution, and file operations
- **Human-in-the-Loop**: Supports plan modification and approval workflows
- **Multi-Search Support**: Tavily, Brave, DuckDuckGo, Arxiv integration
- **RAG Integration**: Private knowledge base support with vector stores

### Frontend Structure

- **Next.js App Router**: Modern React architecture with server components
- **API Integration**: FastAPI backend with TypeScript client generation
- **UI Components**: Radix UI primitives with Tailwind CSS styling
- **Internationalization**: Multi-language support with next-intl

## Configuration

### Environment Variables (.env)
- `OPENAI_API_KEY`, `ANTHROPIC_API_KEY` - LLM provider keys
- `TAVILY_API_KEY`, `BRAVE_API_KEY` - Search engine keys
- `MONGODB_URL`, `POSTGRES_URL` - Database connections
- `PYTHON_REPL`, `MCP_SERVER` - Security features (disabled by default)

### Configuration Files
- `conf.yaml` - LLM models, search configuration, agent settings
- `pyproject.toml` - Python dependencies and tool configuration
- `web/package.json` - Frontend dependencies and scripts

## Key Features

- **Multi-Agent System**: 4-component architecture with LangGraph orchestration
- **Multi-Search Support**: Tavily, Brave, DuckDuckGo, Arxiv integration
- **RAG Integration**: Private knowledge base support
- **Human-in-the-Loop**: Interactive plan modification workflow
- **Content Generation**: Podcast and PowerPoint creation
- **LangGraph Studio**: Visual workflow debugging

## Development Guidelines

### Code Quality
- **Python**: Ruff for formatting and linting (88 char line length)
- **TypeScript**: ESLint + Prettier with strict TypeScript
- **Testing**: pytest with minimum 25% coverage requirement
- **Pre-commit**: Available hooks for code quality

### Security Considerations
- MCP server and Python REPL disabled by default for security
- CORS restricted to localhost in development mode
- API keys should never be committed to version control
- Use environment variables for all sensitive configuration

## Testing Strategy

- **Python**: pytest with 25% coverage minimum
- **Frontend**: TypeScript tests with React Testing Library
- **Integration Tests**: API endpoint testing with FastAPI test client
- **Pre-commit Hooks**: Automated code quality checks

## Common Development Tasks

### Adding a New Search Engine
1. Implement search tool in `backend/tools/search/`
2. Add configuration to `conf.yaml`
3. Update environment variable requirements
4. Add tests for the new search functionality

### Modifying Agent Behavior
1. Update the relevant agent in `backend/agent/`
2. Modify the LangGraph state if needed
3. Update tool integrations as required
4. Test the complete workflow end-to-end

### Frontend Feature Development
1. Create components in `web/components/`
2. Add API endpoints in `backend/routers/`
3. Update TypeScript types if needed
4. Test with both development servers running

## Docker Operations

```bash
docker compose build       # Build containers
docker compose up         # Run full stack
```
