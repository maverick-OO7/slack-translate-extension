# Changelog

All notable changes to the Slack Translate Extension will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2024-12-XX

### Added
- **Auto-translate mode**: Messages are automatically translated when they appear
- **Dual display format**: Shows both original and translated text in auto-translate mode
- **Toggle switch**: Easy on/off control for auto-translate functionality
- **Loading states**: Visual feedback during translation process ("Translating..." indicator)
- **Enhanced error handling**: User-friendly error messages for failed translations
- **Improved UI styling**: Better visual distinction between original and translated content
- **Comprehensive documentation**: Technical documentation and user guide
- **Advanced configuration**: Auto-translate setting with helpful tooltips

### Changed
- **Translation function**: Refactored `sgtTranslateMessage()` to support both auto and manual modes
- **Options page**: Added auto-translate toggle with explanatory information
- **Storage schema**: Added `autoTranslate` boolean setting
- **CSS styling**: Enhanced styles for auto-translate containers and toggle switches
- **Version numbers**: Updated across all files (manifest, package.json, options page)

### Enhanced
- **User experience**: Seamless translation without manual clicking
- **Visual feedback**: Clear loading states and error handling
- **Documentation**: Comprehensive guides for users and developers
- **Accessibility**: Better contrast and visual hierarchy
- **Performance**: Optimized DOM manipulation and API calls

### Technical Details
- **Backward compatibility**: Existing manual translate mode remains unchanged
- **Error resilience**: Graceful fallbacks for network and API failures
- **Memory management**: Proper cleanup of DOM elements and event listeners
- **Cross-browser support**: Maintained Chrome Manifest V3 compatibility

## [1.0.6] - Previous Version

### Features
- Manual translation with "View Translation" button
- 100+ language support via Google Translate API
- Regex filtering for specific character sets
- Persistent user settings
- Customizable button labels
- Dark/light theme support

### Technical Implementation
- Chrome Manifest V3
- Content script integration with Slack DOM
- MutationObserver for message detection
- Chrome Storage API for settings persistence
- Google Translate API integration

---

## Version History Summary

| Version | Release Date | Key Features |
|---------|--------------|--------------|
| 1.1.0 | 2024-12-XX | Auto-translate mode, enhanced UI, comprehensive documentation |
| 1.0.6 | Previous | Manual translation, language support, regex filtering |

## Migration Guide

### Upgrading from 1.0.6 to 1.1.0

**No breaking changes** - existing settings and functionality are preserved.

**New features available:**
1. **Auto-translate mode**: Enable in extension options
2. **Enhanced UI**: Automatic visual improvements
3. **Better error handling**: Improved user feedback

**Settings migration:**
- All existing settings are automatically preserved
- New `autoTranslate` setting defaults to `false` (manual mode)
- Users can enable auto-translate in the options page

**Recommendations:**
- Test auto-translate mode in a development environment first
- Consider using regex filtering to limit auto-translation scope
- Monitor API usage if enabling auto-translate for high-volume channels

## Future Roadmap
- [ ] Translation caching to reduce API calls
- [ ] Multiple target language support
- [ ] Translation history
- [ ] Custom translation providers
- [ ] Keyboard shortcuts for quick translation

---

**Note:** This changelog follows semantic versioning principles. Major version changes indicate breaking changes, minor versions add new features, and patch versions include bug fixes and improvements.