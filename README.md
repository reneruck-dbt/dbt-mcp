# dbt MCP Minimal Server

A minimal MCP (Metrics Control Plane) server for interacting with the dbt Semantic Layer.

## Setup

1. Clone the repository:
```bash
git clone https://github.com/dbt-labs/dbt-mcp-prototype.git
cd dbt-mcp-prototype
```

2. Set up your Python environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt
```

3. Configure environment variables:
```bash
cp .env.example .env
```
Then edit `.env` with your dbt Semantic Layer credentials:
- `DBT_HOST`: Your dbt Semantic Layer host
- `DBT_ENV_ID`: Your dbt environment ID
- `DBT_TOKEN`: Your service token

## Configure for Claude Desktop

Assuming `EDITOR` enviornment variable is configured and standard install location of Claude Desktop for macOS:
```shell
$EDITOR ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

Add the following configuration (where `YOUR_INSTALL_PATH` is the working directory of this virtual environment (hint: use output of `pwd`)):

```json
{
  "mcpServers": {
    "dbt Minimal": {
      "command": "/YOUR_INSTALL_PATH/dbt-mcp-prototype/venv/bin/python",
      "args": ["/YOUR_INSTALL_PATH/dbt-mcp-prototype/minimal_server.py"]
    },
  }
}
```

## Usage

Available commands:
- `list_metrics()`: List all available metrics
- `get_dimensions(metrics)`: Get available dimensions for specified metrics
- `get_granularities(metrics)`: Get available time granularities for metrics
- `query_metrics(metrics, group_by=None, time_grain=None, limit=None)`: Query metrics with optional grouping and filtering

## Requirements

- Python 3.7+
- dbt Semantic Layer access
