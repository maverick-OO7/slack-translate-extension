# Slack Translate Extension - Technical Documentation

## Table of Contents
1. [Overview](#overview)
2. [Architecture](#architecture)
3. [Features](#features)
4. [Installation & Setup](#installation--setup)
5. [Configuration](#configuration)
6. [API Reference](#api-reference)
7. [File Structure](#file-structure)
8. [Development Guide](#development-guide)
9. [Troubleshooting](#troubleshooting)
10. [Contributing](#contributing)

## Overview

The Slack Translate Extension is a Chrome browser extension that provides seamless translation functionality directly within the Slack web application. The extension supports both automatic and manual translation modes, allowing users to translate messages in real-time without leaving their Slack workspace.

### Key Capabilities
- **Real-time translation** of Slack messages
- **100+ language support** via Google Translate API
- **Dual operation modes**: Auto-translate and Manual translate
- **Smart filtering** with regex pattern matching
- **Persistent user preferences**
- **Non-intrusive integration** with Slack's UI

## Architecture

### Extension Components

```
┌─────────────────────────────────────────────────────────────┐
│                    Chrome Extension                         │
├─────────────────────────────────────────────────────────────┤
│  Manifest V3                                                │
│  ├── Content Scripts (content.js)                          │
│  ├── Background Service Worker (background.js)             │
│  ├── Options Page (options.html/js/css)                    │
│  └── Storage API (Chrome Storage Sync)                     │
├─────────────────────────────────────────────────────────────┤
│  External Dependencies                                      │
│  └── Google Translate API (translate.googleapis.com)       │
└─────────────────────────────────────────────────────────────┘
```

### Data Flow

1. **Message Detection**: Content script monitors Slack DOM for new messages
2. **Filtering**: Messages are filtered based on regex patterns (if configured)
3. **Translation Request**: Valid messages are sent to Google Translate API
4. **Response Processing**: Translated text is formatted and displayed
5. **UI Update**: Translation is integrated into Slack's message interface

## Features

### Auto-Translate Mode
- **Automatic Processing**: Messages are translated immediately when they appear
- **Dual Display**: Shows both original and translated text
- **Loading States**: Visual feedback during translation process
- **Error Handling**: Graceful fallbacks for failed translations

### Manual Translate Mode
- **On-Demand Translation**: Users click "View Translation" button to translate
- **Button Integration**: Seamlessly integrated into Slack's message UI
- **Customizable Labels**: Users can customize button text

### Advanced Features
- **Language Detection**: Automatic source language detection
- **Regex Filtering**: Show translate functionality only for specific character sets
- **Persistent Settings**: User preferences saved across sessions
- **Dark/Light Theme Support**: Adapts to user's system preferences

## Installation & Setup

### Prerequisites
- Google Chrome browser (version 88+)
- Active internet connection
- Slack web application access

### Installation Steps

1. **Download Extension**
   ```bash
   git clone https://github.com/maverick-OO7/slack-translate-extension.git
   cd slack-translate-extension
   ```

2. **Build Extension**
   ```bash
   npm run build
   ```

3. **Load in Chrome**
   - Open Chrome and navigate to `chrome://extensions/`
   - Enable "Developer mode"
   - Click "Load unpacked" and select the `src` directory

4. **Configure Settings**
   - Click the extension icon in Chrome toolbar
   - Set your preferred source and target languages
   - Choose between auto-translate or manual translate mode

## Configuration

### Settings Options

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `translateFrom` | String | "auto" | Source language (auto-detect or specific language code) |
| `translateTo` | String | "en" | Target language code |
| `translateLabel` | String | "View Translation" | Custom label for translate button |
| `translateRegex` | String | "" | Regex pattern for message filtering |
| `autoTranslate` | Boolean | false | Enable automatic translation mode |

### Language Codes
The extension supports 100+ languages using standard ISO language codes:
- `en` - English
- `es` - Spanish
- `fr` - French
- `de` - German
- `ja` - Japanese
- `ko` - Korean
- `zh-CN` - Chinese (Simplified)
- `zh-TW` - Chinese (Traditional)
- And many more...

### Regex Examples
```javascript
// Show translate button only for Thai characters
/([\u0e00-\u0e7f])/

// Show translate button only for Korean characters
/([\u1100-\u11ff])/

// Show translate button only for Japanese characters
/([\u4e00-\u9fbf\u3040-\u309f\u30a0-\u30ff])/

// Show translate button only for Arabic characters
/([\u0600-\u06ff])/
```

## API Reference

### Content Script Functions

#### `sgtTranslateMessage(sourceText, targetElement, isAutoTranslate)`
Translates text using Google Translate API.

**Parameters:**
- `sourceText` (String): Text to translate
- `targetElement` (HTMLElement): DOM element to display translation
- `isAutoTranslate` (Boolean): Whether this is auto-translate mode

**Returns:** Promise (resolves when translation is complete)

#### `init(eleName)`
Initializes the extension for a specific Slack view container.

**Parameters:**
- `eleName` (String): CSS selector for the container element

**Returns:** void

### Storage API

#### `chrome.storage.sync.get(keys, callback)`
Retrieves user settings from Chrome's sync storage.

#### `chrome.storage.sync.set(items, callback)`
Saves user settings to Chrome's sync storage.

### Google Translate API

#### Endpoint
```
https://translate.googleapis.com/translate_a/single?client=gtx&sl={source}&tl={target}&dt=t&q={text}
```

**Parameters:**
- `sl`: Source language code
- `tl`: Target language code
- `q`: Text to translate (URL encoded)

**Response Format:**
```javascript
[
  [
    ["Translated text", "Original text", null, null, 0]
  ],
  "detected_language_code"
]
```

## File Structure

```
slack-translate-extension/
├── src/
│   ├── manifest.json          # Extension manifest (Manifest V3)
│   ├── content.js             # Main content script
│   ├── background.js          # Background service worker
│   ├── options.html           # Options page HTML
│   ├── options.js             # Options page JavaScript
│   ├── options.css            # Options page styles
│   ├── style.css              # Content script styles
│   └── icons/                 # Extension icons
│       ├── 16.png
│       ├── 48.png
│       ├── 128.png
│       └── logo.png
├── build/                     # Build output directory
├── package.json               # NPM package configuration
├── README.md                  # User documentation
├── DOCUMENTATION.md           # This technical documentation
└── LICENSE                    # MIT license
```

## Development Guide

### Local Development

1. **Setup Development Environment**
   ```bash
   git clone <repository-url>
   cd slack-translate-extension
   npm install
   ```

2. **Make Changes**
   - Edit files in the `src/` directory
   - Test changes by reloading the extension in Chrome

3. **Build for Production**
   ```bash
   npm run build
   ```

### Code Style Guidelines

- **JavaScript**: Use ES6+ features, prefer `const`/`let` over `var`
- **CSS**: Use CSS custom properties for theming, follow BEM methodology
- **HTML**: Use semantic HTML, include proper ARIA attributes
- **Comments**: Document complex logic and API interactions

### Testing

1. **Manual Testing**
   - Test in different Slack workspaces
   - Verify with various languages
   - Test both auto-translate and manual modes

2. **Browser Compatibility**
   - Test in Chrome (primary target)
   - Verify Manifest V3 compatibility
   - Check for console errors

### Debugging

1. **Content Script Debugging**
   - Open Chrome DevTools on Slack page
   - Check Console tab for errors
   - Use Network tab to monitor API calls

2. **Options Page Debugging**
   - Right-click extension icon → "Inspect popup"
   - Check Console for JavaScript errors

3. **Storage Debugging**
   ```javascript
   // In Chrome DevTools Console
   chrome.storage.sync.get(null, console.log)
   ```

## Troubleshooting

### Common Issues

#### Translation Not Working
**Symptoms:** Messages not being translated
**Solutions:**
- Check internet connection
- Verify Google Translate API is accessible
- Check browser console for errors
- Ensure extension has proper permissions

#### Auto-Translate Not Triggering
**Symptoms:** Auto-translate mode not working
**Solutions:**
- Verify `autoTranslate` setting is enabled
- Check regex filter (if configured)
- Ensure messages match the target selectors
- Reload the Slack page

#### UI Not Appearing
**Symptoms:** Translate buttons/containers not showing
**Solutions:**
- Check if extension is enabled
- Verify content script is loading
- Check for CSS conflicts
- Ensure Slack page is fully loaded

#### Settings Not Saving
**Symptoms:** Configuration changes not persisting
**Solutions:**
- Check Chrome sync storage permissions
- Verify storage quota limits
- Clear extension data and reconfigure
- Check for JavaScript errors in options page

### Performance Optimization

1. **Reduce API Calls**
   - Implement debouncing for rapid message updates
   - Cache translations for repeated content
   - Use efficient DOM selectors

2. **Memory Management**
   - Clean up event listeners
   - Remove unused DOM elements
   - Monitor memory usage in DevTools

3. **Network Optimization**
   - Batch translation requests when possible
   - Implement retry logic for failed requests
   - Use appropriate timeout values

## Contributing

### Getting Started

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

### Contribution Guidelines

- **Code Quality**: Follow existing code style and patterns
- **Testing**: Test changes in multiple scenarios
- **Documentation**: Update documentation for new features
- **Backward Compatibility**: Ensure changes don't break existing functionality

### Pull Request Process

1. **Description**: Clearly describe the changes and motivation
2. **Testing**: Include testing steps and results
3. **Screenshots**: Provide screenshots for UI changes
4. **Documentation**: Update relevant documentation files

### Issue Reporting

When reporting issues, please include:
- Chrome version
- Extension version
- Steps to reproduce
- Expected vs actual behavior
- Console error messages (if any)
- Screenshots (if applicable)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support and questions:
- Create an issue on GitHub
- Check existing documentation
- Review troubleshooting section
- Test with different configurations

---

**Version:** 1.1.0  
**Last Updated:** December 2024  
**Maintainer:** maverick-OO7