# API Reference

## Content Script API

### `sgtTranslateMessage(sourceText, targetElement, isAutoTranslate)`
Translates text using Google Translate API.

**Parameters:**
- `sourceText` (String): Text to translate
- `targetElement` (HTMLElement): DOM element to display translation
- `isAutoTranslate` (Boolean): Whether this is auto-translate mode

**Returns:** Promise (resolves when translation is complete)

### `init(eleName)`
Initializes the extension for a specific Slack view container.

**Parameters:**
- `eleName` (String): CSS selector for the container element

## Storage API

### Settings Schema
```javascript
{
  translateFrom: "auto" | string,    // Source language code
  translateTo: "en" | string,        // Target language code  
  translateLabel: "View Translation" | string, // Button text
  translateRegex: "" | string,       // Regex pattern
  autoTranslate: false | boolean     // Auto-translate mode
}
```

### Methods
- `chrome.storage.sync.get(keys, callback)` - Retrieve settings
- `chrome.storage.sync.set(items, callback)` - Save settings

## Google Translate API

### Endpoint
```
GET https://translate.googleapis.com/translate_a/single
```

### Parameters
- `client=gtx` - Client identifier
- `sl={source}` - Source language code
- `tl={target}` - Target language code  
- `dt=t` - Data type (text)
- `q={text}` - Text to translate (URL encoded)

### Response Format
```javascript
[
  [
    ["Translated text", "Original text", null, null, 0]
  ],
  "detected_language_code"
]
```

## DOM Selectors

### Slack Message Elements
- `.p-rich_text_block` - Rich text message blocks
- `.c-message_kit__attachments` - Message attachments
- `.p-workspace__primary_view_body` - Main message container
- `.p-view_contents--secondary` - Secondary view container
- `.c-virtual_list__scroll_container` - Virtual list container

### Extension Elements
- `.___sgt-translate-button` - Manual translate button
- `.___sgt-translate-container` - Auto-translate container
- `.___sgt-translate-attribution` - Google Translate attribution

## Event Handlers

### Content Script Events
- `MutationObserver` - Monitors DOM changes for new messages
- `click` - Handles translate button clicks (manual mode)
- `storage.onChanged` - Responds to settings changes

### Background Script Events  
- `chrome.action.onClicked` - Extension icon click handler

## Error Handling

### Translation Errors
- Network failures: Show "Translation failed" message
- API errors: Log to console, show error state
- Invalid responses: Graceful fallback

### DOM Errors
- Missing elements: Retry with timeout
- Invalid selectors: Skip processing
- Permission errors: Log and continue

## Performance Considerations

### Optimization Strategies
- Debounce rapid DOM changes
- Cache translation results
- Use efficient selectors
- Clean up event listeners
- Monitor memory usage

### Best Practices
- Minimize API calls
- Batch DOM updates
- Use requestAnimationFrame for UI updates
- Implement proper error boundaries