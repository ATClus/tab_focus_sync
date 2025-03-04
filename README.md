# Firefox Extension - Tab Focus Sync

## Overview
Tab Focus Sync is a Firefox extension that tracks active tab changes using a SignalR Hub. It monitors tab activations, updates, closures, and window focus events in real time, ensuring seamless synchronization between the browser and your backend.

> Requires the ClusterFocus.

## Features
- **Real-time Tracking:** Utilizes SignalR for live tab status updates.
- **Auto-Reconnect:** Automatically attempts to reconnect if the connection drops.
- **Inactivity Detection:** Stops tracking after 60 minutes of inactivity.
- **Event Handling:** Supports tab activation, updates, removals, and window focus changes.

## Installation
### Prerequisites
- **Firefox Browser:** Ensure you have the latest version with WebExtension support.
- **ClusterFocus Hub:** A running backend at the endpoint (default: `https://localhost:7131/tabfocused`).

### Steps
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/ATClus/tab-focus-sync.git
   ```

2. **Navigate to the Directory:**
    ```bash
    cd tab-focus-sync
    ```

3. **Load the Extension in Firefox:**
    - Open Firefox and go to **about:debugging**.
    - Click on This Firefox > **Load Temporary Add-on**...
    - Select the **manifest.json** file from the repository.

## Usage
Once installed, the extension automatically begins tracking, if the hub is running:

- Start Tracking: Invokes StartTabTracking when a tab is activated or updated.
- Stop Tracking: Calls StopTabTracking when a tab is removed or after a period of inactivity.

> Check the browser console for log messages regarding connection status and tracking events.

## How It Works
### Establishing Connection:
The extension connects to the ClusterFocus using a WebSocket connection at the specified hubUrl.

### Tab Tracking:
- Activation & Updates: On tab activation or update, the extension calls StartTabTracking with the tab's title and URL.
- Removal: When a tab is closed, StopTabTracking is invoked to end tracking.
- Window Focus: If the browser loses window focus, tracking stops; when focus is regained, the active tab is queried and tracked again.
- Inactivity Management: An inactivity timer is set to 60 minutes. If no tab activity occurs within this interval, tracking is automatically stopped.

## Contributing
Contributions are welcome. If you encounter any issues or have suggestions, please open an issue or submit a pull request.

## License
This project is licensed under the MIT License.

## Acknowledgements
- Built with **@microsoft/signalr**.
