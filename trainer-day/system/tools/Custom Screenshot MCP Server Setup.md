---
title: Custom Screenshot MCP Server Setup
type: note
permalink: trainer-day/system/tools/custom-screenshot-mcp-server-setup
---

# Custom Screenshot MCP Server Setup

## Overview
Complete end-to-end setup for a custom screenshot MCP server using Playwright and Python that works globally across all Claude Code sessions.

## Prerequisites
- Python with pip
- Node.js and npm
- Claude Desktop

## Installation Steps

### 1. Install Playwright Python Package
```bash
pip install playwright
playwright install firefox
```

### 2. Create Global Screenshot Command
Create `/Users/alex/.local/bin/screenshot`:
```python
#!/usr/bin/env python3
import sys
from playwright.sync_api import sync_playwright

def take_screenshot(url="https://google.com", output="screenshot.png"):
    with sync_playwright() as p:
        browser = p.firefox.launch()
        page = browser.new_page()
        page.goto(url)
        page.screenshot(path=output)
        browser.close()
        print(f"Screenshot saved as {output}")

if __name__ == "__main__":
    url = sys.argv[1] if len(sys.argv) > 1 else "https://google.com"
    output = sys.argv[2] if len(sys.argv) > 2 else "screenshot.png"
    take_screenshot(url, output)
```

Make executable:
```bash
chmod +x ~/.local/bin/screenshot
```

### 3. Create MCP Server
Create `/Users/alex/.local/bin/screenshot-mcp`:
```python
#!/usr/bin/env python3
import json
import sys
import subprocess
import os

def handle_list_tools():
    return {
        "tools": [
            {
                "name": "screenshot",
                "description": "Take a screenshot of a webpage using Playwright Firefox",
                "inputSchema": {
                    "type": "object",
                    "properties": {
                        "url": {
                            "type": "string",
                            "description": "URL to screenshot (default: https://google.com)"
                        },
                        "filename": {
                            "type": "string", 
                            "description": "Output filename with optional relative path (default: screenshot.png)"
                        }
                    }
                }
            }
        ]
    }

def handle_call_tool(name, arguments):
    if name == "screenshot":
        url = arguments.get("url", "https://google.com")
        filename = arguments.get("filename", "screenshot.png")
        
        try:
            # Handle relative paths by ensuring the directory exists
            import os
            if '/' in filename:
                dirname = os.path.dirname(filename)
                if dirname and not os.path.exists(dirname):
                    os.makedirs(dirname, exist_ok=True)
                    
            result = subprocess.run([
                "/Users/alex/.local/bin/screenshot", 
                url, 
                filename
            ], capture_output=True, text=True, cwd=os.getcwd())
            
            if result.returncode == 0:
                return {
                    "content": [
                        {
                            "type": "text",
                            "text": f"Screenshot saved as {filename}\n{result.stdout}"
                        }
                    ]
                }
            else:
                return {
                    "content": [
                        {
                            "type": "text", 
                            "text": f"Error taking screenshot: {result.stderr}"
                        }
                    ],
                    "isError": True
                }
        except Exception as e:
            return {
                "content": [
                    {
                        "type": "text",
                        "text": f"Error: {str(e)}"
                    }
                ],
                "isError": True
            }
    
    return {
        "content": [
            {
                "type": "text",
                "text": f"Unknown tool: {name}"
            }
        ],
        "isError": True
    }

def main():
    for line in sys.stdin:
        try:
            request = json.loads(line)
            
            if request.get("method") == "tools/list":
                response = handle_list_tools()
            elif request.get("method") == "tools/call":
                params = request.get("params", {})
                response = handle_call_tool(
                    params.get("name"),
                    params.get("arguments", {})
                )
            else:
                response = {"error": "Unknown method"}
            
            print(json.dumps(response))
            sys.stdout.flush()
            
        except json.JSONDecodeError:
            print(json.dumps({"error": "Invalid JSON"}))
            sys.stdout.flush()
        except Exception as e:
            print(json.dumps({"error": str(e)}))
            sys.stdout.flush()

if __name__ == "__main__":
    main()
```

Make executable:
```bash
chmod +x ~/.local/bin/screenshot-mcp
```

### 4. Add to PATH
Add to `~/.zshrc`:
```bash
export PATH="$HOME/.local/bin:$PATH"
```

Reload:
```bash
source ~/.zshrc
```

### 5. Configure Claude Desktop
Edit `/Users/alex/Library/Application Support/Claude/claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "basic-memory": {
      "command": "uvx",
      "args": [
        "basic-memory",
        "mcp"
      ]
    },
    "screenshot": {
      "command": "screenshot-mcp",
      "args": []
    }
  }
}
```

### 6. Restart Claude Desktop
Restart Claude Desktop for changes to take effect.

## Usage
In any Claude Code session, use the screenshot tool:
- `screenshot` with URL parameter: `https://example.com`
- `filename` parameter: `temp/test.png` (creates directories automatically)

## Features
- ✅ No Chrome dependency (uses Firefox)
- ✅ Headless by default
- ✅ Global command-line usage
- ✅ Relative path support with auto-directory creation
- ✅ Works across all Claude Code sessions
- ✅ Simple MCP server integration

## Test Command
```bash
python -c "
import json
import subprocess
import sys

request = {
    'method': 'tools/call',
    'params': {
        'name': 'screenshot',
        'arguments': {
            'url': 'https://google.com',
            'filename': 'temp/test.png'
        }
    }
}

proc = subprocess.run([
    'screenshot-mcp'
], input=json.dumps(request), text=True, capture_output=True)

print('STDOUT:', proc.stdout)
"
```