

# Syed MCP Registry

This is a simple, local MCP registry for development and testing. It loads MCP servers from `data/seed.json` and runs on your machine only.

## How to Compile and Run Locally

### Prerequisites
- Docker
- Go 1.24.x

### Steps
1. Clone this repository:
     ```bash
     git clone https://github.com/syedmajidraza/test_mcp.git
     cd test_mcp
     ```
2. Start the registry server:
     ```bash
     docker-compose up --build -d
     ```
     The registry will be available at [http://localhost:8080](http://localhost:8080).

## How to Add MCP Servers

1. Open `data/seed.json` in your editor.
2. Add a new MCP server entry using the following format:
     ```json
     {
         "$schema": "https://static.modelcontextprotocol.io/schemas/2025-10-17/server.schema.json",
         "name": "your-namespace/your-mcp-server",
         "description": "Description of your MCP server.",
         "repository": {
             "url": "https://github.com/syedmajidraza/test_mcp.git",
             "source": "github"
         },
         "version": "1.0.0",
         "packages": [
             {
                 "registryType": "npm",
                 "identifier": "your-npm-package",
                 "version": "1.0.0",
                 "runtimeHint": "npx",
                 "transport": { "type": "stdio" }
             }
         ]
     }
     ```
3. Save the file.
4. Restart the registry to load the new server:
     ```bash
     docker-compose down
     docker-compose up --build -d
     ```
5. Visit [http://localhost:8080](http://localhost:8080) to see your MCP server listed.

## Useful Commands

- Run tests and lint:
    ```bash
    make check
    ```
- Build the publisher CLI:
    ```bash
    make publisher
    ./bin/mcp-publisher --help
    ```

## Documentation

See the [docs](./docs) folder for more details.
