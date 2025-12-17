# Noa Playground - Build and Run Guide

## Overview

Noa Playground is a **static web application** that allows users to interact with the Noa AI assistant without requiring Brilliant hardware (Frame or Monocle). The application is a Progressive Web App (PWA) that runs entirely in the browser.

## Architecture

- **Type**: Static Web Application (PWA)
- **Frontend**: Vanilla JavaScript (ES6 modules), HTML5, CSS3
- **No Build Process Required**: The application uses native ES6 modules
- **No Package Manager Required**: No npm, yarn, or other package managers needed
- **No Compilation/Transpilation**: Pure JavaScript - runs directly in the browser

## System Requirements

### Minimum Requirements

1. **Web Browser** (with ES6 module support):
   - Chrome 61+
   - Firefox 60+
   - Safari 11+
   - Edge 16+

2. **HTTP Server** (for local development):
   - Python 3.x (built-in `http.server` module), OR
   - Node.js with `http-server` or similar, OR
   - Any other static file server

3. **API Keys** (runtime requirement):
   - Noa API key from Brilliant Labs (required for functionality)

### External Dependencies

The application loads these dependencies from CDN at runtime:
- **Ionicons 7.1.0**: UI icons (loaded from unpkg.com)

## File Structure

```
noa-playground/
├── index.html              # Main HTML file
├── manifest.json           # PWA manifest
├── noa_config.json         # API configuration
├── CNAME                   # Domain configuration (playground.brilliant.xyz)
├── css/
│   └── style.css          # Application styles
├── js/
│   ├── main.js            # Main application logic
│   ├── persona.js         # Persona creation and management
│   ├── history.js         # Conversation history
│   ├── photo.js           # Image processing
│   └── utils.js           # Utility functions
└── img/                   # Application images/icons
```

## How to Run Locally

### Option 1: Python HTTP Server (Recommended for Quick Testing)

```bash
# Navigate to the project directory
cd /path/to/noa-playground

# Start a local web server on port 8000
python3 -m http.server 8000

# Open in browser
# Navigate to: http://localhost:8000
```

### Option 2: Node.js HTTP Server

```bash
# Install http-server globally (one-time)
npm install -g http-server

# Navigate to the project directory
cd /path/to/noa-playground

# Start the server
http-server -p 8000

# Open in browser
# Navigate to: http://localhost:8000
```

### Option 3: PHP Built-in Server

```bash
# Navigate to the project directory
cd /path/to/noa-playground

# Start PHP server
php -S localhost:8000

# Open in browser
# Navigate to: http://localhost:8000
```

### Option 4: VS Code Live Server Extension

1. Install the "Live Server" extension in VS Code
2. Open the project folder in VS Code
3. Right-click on `index.html`
4. Select "Open with Live Server"

## Configuration

### API Configuration (`noa_config.json`)

The application is pre-configured to connect to:
- **Noa API**: `https://api.brilliant.xyz/dev/noa`
- **Scenario API**: `https://api.cloud.scenario.com/v1` (for image generation)

No changes to this file are typically needed unless you're using a different API endpoint.

### Runtime Configuration

On first run, the application will prompt for:
1. **Noa API Key**: Required to interact with the Noa AI assistant

API keys are stored in the browser's `localStorage` and persist across sessions.

## Features and Capabilities

### Core Features
- Text-based chat with Noa AI assistant
- Image upload and vision analysis
- Conversation history management
- Custom system messages
- Location-aware responses
- Multiple vision model support (GPT-4o, Claude-3 variants)

### PWA Features
- Installable as a standalone app
- Offline-capable manifest
- Mobile-responsive design
- Touch-optimized interface

### Advanced Features
- Web search integration (SerpAPI, DataForSEO, Perplexity)
- Image generation capabilities
- Google Lens and Reverse Image Search
- Customizable AI personality ("Create your Noa")

## Browser Requirements

The application uses modern web APIs:
- **ES6 Modules**: For code organization
- **Fetch API**: For HTTP requests
- **Canvas API**: For image processing
- **File API**: For image uploads
- **LocalStorage API**: For persistence
- **FormData API**: For multipart uploads

### CORS Considerations

When running locally, ensure your HTTP server supports:
- Proper MIME types for JavaScript modules (`text/javascript` or `application/javascript`)
- CORS headers if accessing from a different origin

## Deployment

### GitHub Pages (Current Deployment)

The application is deployed at: `https://playground.brilliant.xyz`

To deploy to GitHub Pages:
1. Push code to the `main` or `gh-pages` branch
2. Enable GitHub Pages in repository settings
3. The CNAME file ensures custom domain routing

### Other Static Hosting

The application can be deployed to any static hosting service:
- **Netlify**: Drop the folder or connect to Git
- **Vercel**: Import project and deploy
- **AWS S3 + CloudFront**: Upload files to S3 bucket
- **Firebase Hosting**: `firebase deploy`
- **Cloudflare Pages**: Connect Git repository

**No build step is required** - simply upload all files maintaining the directory structure.

## Development

### No Build Tools Required

This is a traditional web application without a build pipeline:
- ✅ No webpack, rollup, or vite configuration
- ✅ No babel transpilation
- ✅ No package.json or node_modules
- ✅ No TypeScript compilation
- ✅ Direct browser execution

### Making Changes

1. Edit files directly in any text editor
2. Refresh the browser to see changes
3. Use browser DevTools for debugging
4. No compilation or watch mode needed

### Testing Changes

```bash
# Start local server
python3 -m http.server 8000

# Make changes to files
# Refresh browser (Ctrl+R or Cmd+R)
# Changes are immediately visible
```

## Troubleshooting

### Issue: "Failed to load module script"

**Cause**: Server not serving JavaScript files with correct MIME type, or CORS issues

**Solution**: 
- Ensure you're using an HTTP server (not file:// protocol)
- Python's `http.server` handles MIME types correctly
- Check browser console for specific errors

### Issue: "API key required" prompt appears immediately

**Cause**: No API key stored in localStorage

**Solution**: 
- Enter a valid Noa API key when prompted
- Keys are stored locally and persist

### Issue: Images not loading

**Cause**: Relative path issues or server configuration

**Solution**:
- Ensure all files are in the correct directory structure
- Check browser DevTools Network tab for 404 errors

## API Requirements

### Noa API (Required)

- **Endpoint**: `https://api.brilliant.xyz/dev/noa`
- **Authentication**: Bearer token (API key)
- **Purpose**: AI chat, vision analysis, web search

**How to obtain**: Contact Brilliant Labs for preview access

### Scenario API (Optional)

- **Endpoint**: `https://api.cloud.scenario.com/v1`
- **Purpose**: Generate custom AI persona images
- **Note**: Currently commented out in the code

## Security Considerations

1. **API Keys**: Stored in browser localStorage (client-side only)
2. **HTTPS**: Recommended for production deployment
3. **No Server-Side Code**: All processing happens client-side or via external APIs
4. **CORS**: API calls are made directly from browser to Brilliant APIs

## Performance

- **Load Time**: Fast initial load (minimal dependencies)
- **Bundle Size**: Small (~30KB total JavaScript)
- **External Dependencies**: Only Ionicons from CDN
- **Caching**: PWA manifest enables app caching

## Browser Compatibility

| Browser | Minimum Version | Notes |
|---------|----------------|-------|
| Chrome  | 61+ | Full support |
| Firefox | 60+ | Full support |
| Safari  | 11+ | Full support |
| Edge    | 16+ | Full support |
| Mobile Safari | iOS 11+ | PWA installable |
| Chrome Android | 61+ | PWA installable |

## Summary

**To build**: No build process required

**To run locally**:
```bash
python3 -m http.server 8000
# Open http://localhost:8000
```

**To deploy**: Upload files to any static hosting service

**To use**: Obtain a Noa API key and enter it when prompted

This is a **zero-build** static web application that runs entirely in the browser.
