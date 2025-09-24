# Realtime Chat Application

A real-time chat application built with Go and WebSockets, featuring a modern frontend using HTMX and Tailwind CSS.

## Features

- **Real-time messaging** via WebSockets
- **Multiple concurrent users** support
- **Message history** for new clients
- **Automatic client cleanup** for disconnected users
- **Modern UI** with HTMX (no custom JavaScript required)
- **Responsive design** with Tailwind CSS

## Architecture

### Backend (Go)
- **Hub-and-spoke pattern** for managing client connections
- **Channel-based communication** for thread-safe message passing
- **WebSocket handling** with ping/pong for connection health
- **Template rendering** for server-side HTML generation

### Frontend
- **HTMX** for seamless WebSocket integration
- **Tailwind CSS** for styling
- **No custom JavaScript** required

## Project Structure

```
realtime-chat-go-main/
├── templates/
│   ├── index.html      # Main chat interface
│   └── message.html    # Message template
├── main.go             # Entry point and HTTP server
├── hub.go              # Central message hub
├── client.go           # WebSocket client handling
├── message.go          # Message data structure
├── go.mod              # Go module dependencies
├── go.sum              # Dependency checksums
├── Makefile            # Build automation
└── .gitignore          # Git ignore rules
```

## Prerequisites

- **Go 1.21.5+** installed on your system
- **Web browser** with WebSocket support

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/Boaz-marube/Go-Chat-App.git
cd realtime-chat-go-main
```

### 2. Install Dependencies
```bash
go mod download
```

### 3. Run the Application

**Option A: Using Make (Recommended)**
```bash
make run
```

**Option B: Direct Go Command**
```bash
go run .
```

**Option C: Build and Run Separately**
```bash
make build
./bin/chat
```

### 4. Access the Application
Open your browser and navigate to:
```
http://localhost:8080
```

## Development

### Building
```bash
make build
```

### Running Tests
```bash
make test
```

### Project Configuration
- **Server Port**: 8080 (configurable in `main.go`)
- **WebSocket Endpoint**: `/ws`
- **Static Files**: Served from `templates/` directory

## Usage

1. Open the application in your browser
2. Type your message in the input field
3. Click "Send" or press Enter
4. Messages appear in real-time for all connected users
5. Open multiple browser tabs to test multi-user functionality

## Technical Details

### WebSocket Communication
- **Connection**: Automatic via HTMX WebSocket extension
- **Message Format**: JSON with `clientID` and `text` fields
- **Health Checks**: Ping/pong mechanism every 54 seconds
- **Max Message Size**: 512 bytes

### Client Management
- **UUID-based identification** for each client
- **Automatic registration** on connection
- **Graceful cleanup** on disconnection
- **Non-blocking message delivery** prevents slow clients from affecting others

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes
4. Run tests: `make test`
5. Commit changes: `git commit -am 'Add feature'`
6. Push to branch: `git push origin feature-name`
7. Submit a pull request

## Dependencies

- **[gorilla/websocket](https://github.com/gorilla/websocket)**: WebSocket implementation
- **[google/uuid](https://github.com/google/uuid)**: UUID generation for client IDs

## Railway Deployment

**Prerequisites:**
- GitHub account
- Railway account (free tier available)

**Steps:**
1. **Push to GitHub:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin <your-github-repo-url>
   git push -u origin main
   ```

2. **Deploy on Railway:**
   - Go to [railway.app](https://railway.app)
   - Sign up/Login with GitHub
   - Click "New Project" → "Deploy from GitHub repo"
   - Select your repository
   - Railway will automatically detect Go and deploy

3. **Access your app:**
   - Railway will provide a public URL
   - Your chat app will be live and accessible

**Configuration Files:**
- `railway.toml` - Railway deployment settings
- `nixpacks.toml` - Build configuration
- Port automatically configured via environment variable

## License

This project is open source and available under the [MIT License](LICENSE).

## Troubleshooting

### Port Already in Use
If you get "address already in use" error:
```bash
# Find and kill process using port 8080
lsof -ti:8080 | xargs kill -9
```

### Go Not Found
Ensure Go is installed and in your PATH:
```bash
go version
```

### WebSocket Connection Issues
- Check browser console for errors
- Ensure no firewall blocking WebSocket connections
- Verify server is running on correct port