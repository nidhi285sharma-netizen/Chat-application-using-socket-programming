# Real-Time WebSocket Chat Application

## Overview
This project is a real-time chat application demonstrating socket programming. 
It uses a Python backend running the `websockets` library and an HTML/JS/CSS frontend dashboard to simulate multiple clients side-by-side in real-time. Everything is run simultaneously through a simple interface.

## Prerequisites
1. **Python 3.7+** must be installed.
2. The Python `websockets` library is required (automatically handled if you use the provided batch script).

## Installation & Execution instructions

To start the project, simply run the PowerShell script provided:

```powershell
.\run.ps1
```

**What happens underneath:**
1. It installs the required `websockets` module into your Python environment if needed.
2. Starts the **Socket Server** (`server.py`) on `ws://127.0.0.1:8765`.
3. Starts a **Local Web Server** to host the UI on `http://127.0.0.1:8000` (This bypasses browser security blocks against raw HTML 'file:///' URLs).
4. Automatically opens the dashboard website locally where you can begin chatting.

### Manual Execution (Without the script)
If you prefer to start things manually:
1. `pip install websockets`
2. Open a terminal and run `python server.py`
3. Open a second terminal and run `python -m http.server 8000 --bind 127.0.0.1`
4. Go to `http://127.0.0.1:8000/index.html` in your web browser.

## Using the Application
1. **Multiple Clients:** On the web dashboard, you will see fields dedicated to "Client 1" and "Client 2". You can click the text field labeled `Username` to customize their names, e.g., "Alice" and "Bob". 
2. **Chatting:** When Alice types and sends a message, it is transmitted to the Python Backend and simultaneously broadcast back to Bob's chat box, functioning exactly like WhatsApp or Discord!
3. **Server Logging:** The Server Summary dashboard tracks connections and relays data so you can see exactly when sockets are opened, what data passes through, and when they are closed.
4. **Summary Feature:** Click the "Generate Chat Summary" button on the Server Panel to visually dump out the exact chronological transcript of all sent messages!

## Suggestions: What to Add Next

To expand on this foundation, you can iteratively add the following features:

*   **Group Chat Rooms:** Allow clients to type in a "Room ID" (e.g., `#general` or `#gaming`) and modify `server.py` so messages are only routed to sockets connected within the same "room".
*   **Timestamping in UI:** Modify `app.js` to attach a JavaScript `new Date().toLocaleTimeString()` to every sent message within the chat bubble UI.
*   **Online Users List:** Send special JSON payloads from `server.py` whenever a socket connects or disconnects, broadcasting a live list of Active Usernames that can render dynamically inside the UI.
*   **Media and Files:** Parse base64 encoded strings within the JSON payloads to allow image and file sharing in real-time through the WebSocket!
*   **Database Integration:** Right now, messages erase when you refresh. Connect SQLite or MongoDB to `server.py` to persist transcripts automatically!
