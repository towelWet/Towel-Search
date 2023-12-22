Towel Search is a self-hosted metasearch engine. This README provides instructions on how to package the application using Platypus for macOS.

Packaging with Platypus

Prerequisites
Before you start, ensure you have Platypus installed on your macOS. If not, download and install it from Platypus official website.

Steps to Package
Prepare Your Application:
Ensure that your Searx instance is ready and tested. The application should include the searx directory and a Python virtual environment (venv).
Open Platypus:
Launch the Platypus application.
Configure Application Details:
Fill in the necessary details about your application:
App Name: Towel Search
Script Type: Choose 'Shell' from the dropdown menu.
Interface: Select 'None' for a background application.
Add Script and Files:
In the "Script Path" field, browse and select your startup script.
Under "Bundled Files", include the searx directory and the venv folder.
Create the Startup Script:
Use the following Bash script, ensuring it’s in the same directory as your searx folder and the virtual environment:
bash
Copy code
#!/bin/bash

# Find the path to the script itself
SCRIPT_DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"

# The path to the Searx directory
SEARX_DIR="$SCRIPT_DIR/searx"

# Check if the Searx directory exists
if [ ! -d "$SEARX_DIR" ]; then
    echo "Searx directory not found at $SEARX_DIR"
    exit 1
fi

# The path to the virtual environment
VENV_DIR="$SCRIPT_DIR/venv"

# Check if the virtual environment exists
if [ ! -d "$VENV_DIR" ]; then
    echo "Virtual environment not found in $VENV_DIR"
    exit 1
fi

# Activate the virtual environment and start Searx
source "$VENV_DIR/bin/activate"
python "$SEARX_DIR/webapp.py" &

# Wait for the server to start
sleep 2

# Open the browser
open http://127.0.0.1:8888
Generate the App:
Click "Create" in Platypus to generate your .app file.
Run Your Application:
Double-click the .app file to start Towel Search. Your default browser should open to the Searx interface.
