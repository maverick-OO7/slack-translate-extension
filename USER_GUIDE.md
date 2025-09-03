# Slack Translate Extension - User Guide

## Quick Start

### Installation
1. **Manual Installation** (for developers)
   - Download the extension files
   - Open Chrome → Extensions → Developer mode → Load unpacked

### First-Time Setup
1. Click the extension icon in your Chrome toolbar
2. Choose your preferred languages:
   - **Translate From**: Select source language or "Auto Detect"
   - **Translate To**: Select your target language
3. Choose your translation mode:
   - **Auto-translate**: Messages translate automatically
   - **Manual translate**: Click button to translate (default)

## Translation Modes

### 🔄 Auto-Translate Mode
**Best for:** Continuous translation of messages in foreign languages

**How it works:**
- Messages are automatically translated when they appear
- Shows both original and translated text
- No clicking required

**When to use:**
- Working with international teams
- Following conversations in multiple languages
- Real-time communication needs

### 🔘 Manual Translate Mode
**Best for:** Occasional translation needs

**How it works:**
- Shows "View Translation" button on messages
- Click button to see translation
- Original message remains unchanged until clicked

**When to use:**
- Selective translation
- Preserving original message format
- Lower bandwidth usage

## Language Settings

### Supported Languages
The extension supports 100+ languages including:

**Popular Languages:**
- Japanese, Korean, Arabic
- English, Spanish, French, German
- Chinese (Simplified & Traditional)
- Portuguese, Russian, Italian
- And many more...

### Language Configuration
1. **Source Language Options:**
   - **Auto Detect**: Automatically detects message language
   - **Specific Language**: Choose a fixed source language

2. **Target Language:**
   - Select your preferred language for translations
   - Default is English

## Advanced Features

### Smart Filtering
Use regex patterns to show translate functionality only for specific character sets:

**Examples:**
- **Thai Messages**: `/([\u0e00-\u0e7f])/`
- **Korean Messages**: `/([\u1100-\u11ff])/`
- **Japanese Messages**: `/([\u4e00-\u9fbf\u3040-\u309f\u30a0-\u30ff])/`
- **Arabic Messages**: `/([\u0600-\u06ff])/`

**How to use:**
1. Go to extension options
2. Find "Advanced Settings"
3. Enter your regex pattern in the filter field
4. Click "Learn more" for more examples

### Custom Button Labels
Customize the translate button text:
- Default: "View Translation"
- Examples: "Translate", "翻訳", "Traducir"

## Usage Tips

### For International Teams
1. **Enable Auto-translate** for seamless communication
2. **Set source to "Auto Detect"** for mixed-language channels
3. **Use regex filtering** to only translate specific languages

### For Language Learning
1. **Use Manual mode** to compare original and translated text
2. **Set specific source language** to practice reading
3. **Keep original text visible** for context

### For Performance
1. **Use Manual mode** to reduce API calls
2. **Apply regex filtering** to limit translation scope
3. **Disable when not needed** to save bandwidth

## Troubleshooting

### Translation Not Working
**Check these:**
- ✅ Internet connection is active
- ✅ Extension is enabled in Chrome
- ✅ You're on the Slack web app (not desktop app)
- ✅ Language settings are configured

**Try these solutions:**
1. Refresh the Slack page
2. Check extension permissions
3. Verify language codes are correct
4. Test with a simple message

### Auto-Translate Not Triggering
**Common causes:**
- Auto-translate mode is disabled
- Regex filter is too restrictive
- Messages don't match the target selectors

**Solutions:**
1. Enable auto-translate in options
2. Check or remove regex filter
3. Test with different message types

### UI Issues
**If translate buttons/containers don't appear:**
1. Ensure you're on `app.slack.com`
2. Check if extension is loaded
3. Try refreshing the page
4. Verify extension permissions

### Settings Not Saving
**If your preferences don't persist:**
1. Check Chrome sync storage
2. Clear extension data and reconfigure
3. Ensure you're signed into Chrome
4. Check for storage quota limits

## Best Practices

### Performance Optimization
- **Use Manual mode** for better performance
- **Apply regex filtering** to reduce unnecessary translations
- **Close unused Slack tabs** to free up resources

### Privacy Considerations
- Translations are processed by Google Translate
- Messages are sent to Google's servers
- No data is stored locally by the extension
- Review Google's privacy policy for translation services

### Team Collaboration
- **Coordinate settings** with team members
- **Use consistent language preferences**
- **Share regex patterns** for team-wide filtering
- **Test in different Slack workspaces**

## Frequently Asked Questions

### Q: Does this work with Slack desktop app?
A: No, this extension only works with the Slack web application (`app.slack.com`).

### Q: Can I translate messages in private channels?
A: Yes, the extension works in all Slack channels and direct messages.

### Q: Is there a limit on translation requests?
A: The extension uses Google Translate's free API, which has usage limits. For heavy usage, consider Google's paid translation services.

### Q: Can I translate file attachments?
A: No, the extension only translates text messages, not file contents or images.

### Q: Does it work with Slack threads?
A: Yes, the extension works with both main messages and thread replies.

### Q: Can I use multiple target languages?
A: No, you can only set one target language at a time. You can change it in the options page.

### Q: Will translations be saved in Slack?
A: No, translations are only displayed temporarily in your browser. They don't modify the original Slack messages.

## Getting Help

### Support Resources
- **GitHub Issues**: Report bugs and request features
- **Chrome Web Store**: Leave reviews and ratings
- **Documentation**: Check technical documentation for developers

### Reporting Issues
When reporting problems, please include:
- Chrome version
- Extension version
- Steps to reproduce the issue
- Screenshots (if applicable)
- Console error messages (if any)

### Feature Requests
We welcome feature suggestions! Please:
- Check existing issues first
- Provide clear use cases
- Explain the expected behavior
- Consider implementation complexity

---

**Need more help?** Check the [Technical Documentation](DOCUMENTATION.md) for developers or create an issue on GitHub.

**Version:** 1.1.0  
**Last Updated:** December 2024