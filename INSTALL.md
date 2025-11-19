# Installation Guide

## Installing Safe Paste Chrome Extension

### Method 1: From Source (Developer Mode)

1. **Download the Extension**
   - Clone this repository or download as ZIP
   ```bash
   git clone https://github.com/A-H-Pooladvand/safe-paste.git
   cd safe-paste
   ```

2. **Open Chrome Extensions Page**
   - Open Chrome browser
   - Navigate to `chrome://extensions/`
   - Or use menu: `⋮` → `More tools` → `Extensions`

3. **Enable Developer Mode**
   - Toggle the "Developer mode" switch in the top right corner

4. **Load the Extension**
   - Click "Load unpacked" button
   - Navigate to the `safe-paste` directory
   - Click "Select Folder"

5. **Verify Installation**
   - You should see the Safe Paste extension in your extensions list
   - The icon should appear in your Chrome toolbar (🔒)
   - Status should show as "Enabled"

### Method 2: Install from Chrome Web Store (Coming Soon)

When published to Chrome Web Store:
1. Visit the Safe Paste page on Chrome Web Store
2. Click "Add to Chrome"
3. Click "Add extension" in the confirmation dialog

## Using Safe Paste

### Basic Usage

Safe Paste works automatically once installed:

1. **Copy** any text containing sensitive information
2. **Navigate** to any text input field (text area, input box, contentEditable element)
3. **Paste** (`Ctrl+V` or `Cmd+V`)
4. **See** the sanitized version inserted automatically
5. **Notice** the green notification confirming sanitization

### Controlling the Extension

#### Enable/Disable Protection

1. Click the Safe Paste icon (🔒) in the Chrome toolbar
2. Toggle the "Enable Safe Paste" checkbox
3. Status indicator shows current state:
   - ✓ Protection Active (green) = Enabled
   - ✗ Protection Disabled (red) = Disabled

#### Default Behavior

- Extension is **enabled by default**
- Protection works on **all websites**
- Works in **all text input fields**

### Testing the Extension

Use the included `demo.html` file to test:

1. Open `demo.html` in Chrome
2. Copy one of the provided examples
3. Paste into the text area
4. Observe the sanitization in action

### What Gets Sanitized

The extension detects and sanitizes:

**Security Credentials:**
- API keys (generic and service-specific)
- AWS Access Keys (AKIA format)
- AWS Secret Keys
- JWT tokens
- Private keys (PEM format)
- Certificates (PEM format)

**Cryptographic Hashes:**
- MD5 (32 hex characters)
- SHA-1 (40 hex characters)
- SHA-256 (64 hex characters)

**Personal Information:**
- Email addresses
- Credit card numbers
- Social Security Numbers (US format)
- Phone numbers

**Network Information:**
- IPv4 addresses
- IPv6 addresses
- URLs containing tokens/keys

**Supported Formats:**
- Plain text
- JSON (structured data)
- YAML (configuration files)
- Mixed content

### Replacement Strategy

Sensitive data is replaced with realistic dummy values:

| Original | Replacement |
|----------|-------------|
| john@company.com | user123@example.com |
| sk_live_abc123 | DUMMY_TOKEN_xyz789 |
| myPassword123 | DUMMY_PASSWORD_123 |
| 4532-1234-5678-9012 | 4532-1234-5678-9010 |
| 192.168.1.100 | 192.0.2.1 |
| AKIAIOSFODNN7EXAMPLE | AKIAxxxxxxxxxxxx |

### Keyboard Shortcuts

Safe Paste integrates seamlessly with standard shortcuts:

- **Paste:** `Ctrl+V` (Windows/Linux) or `Cmd+V` (Mac)
- Works with right-click → Paste
- Works with Edit menu → Paste

### Visual Feedback

When content is sanitized:
- A green notification appears in the top-right corner
- Message: "🔒 Safe Paste: Sensitive data sanitized"
- Auto-dismisses after 3 seconds

## Troubleshooting

### Extension Not Working

**Check if extension is enabled:**
1. Go to `chrome://extensions/`
2. Find Safe Paste
3. Ensure toggle is switched to ON

**Check if protection is enabled:**
1. Click Safe Paste icon
2. Verify "Enable Safe Paste" is checked

**Reload the webpage:**
- Extensions only work on pages loaded after installation
- Press `F5` or `Ctrl+R` to reload

### No Notification Appears

If sanitization happens but no notification:
- This is normal - notification only appears when changes are made
- If content contains no sensitive data, no notification is shown

### Content Not Being Sanitized

**Verify content contains detectable patterns:**
- Test with the examples in `demo.html`
- Check if your data matches known patterns

**Some websites might prevent paste events:**
- Banking sites or security-focused sites may block paste
- This is a website restriction, not an extension issue

**Special input types:**
- Password fields may not trigger paste events
- Some custom input components may not be supported

### Permissions

Safe Paste requires these permissions:

- **clipboardRead:** To read pasted content
- **storage:** To save your enable/disable preference
- **host_permissions (all_urls):** To work on all websites

These are minimal permissions necessary for functionality.

## Uninstalling

To remove Safe Paste:

1. Go to `chrome://extensions/`
2. Find Safe Paste extension
3. Click "Remove"
4. Confirm removal

Your settings and any stored data will be deleted.

## Privacy

Safe Paste respects your privacy:

- ✅ All processing is done **locally** in your browser
- ✅ **No data** is sent to external servers
- ✅ **No analytics** or tracking
- ✅ **No data storage** beyond enable/disable preference
- ✅ Pasted content is **not logged or saved**
- ✅ **Open source** - you can audit the code

## Support

For issues or questions:

1. Check this guide first
2. Review the [README](README.md) for detailed information
3. Open an issue on GitHub
4. Include:
   - Chrome version
   - Extension version
   - Steps to reproduce
   - Expected vs actual behavior

## Updates

The extension checks for updates automatically:

- Updates are delivered through Chrome Web Store (when published)
- Or manually update by pulling latest code and reloading extension
- Release notes available on GitHub

## Advanced Usage

### For Developers

Test the sanitizer directly:

```javascript
// In browser console on any page with the extension
const sanitizer = new Sanitizer();
const result = sanitizer.sanitize("Email: test@example.com");
console.log(result);
```

### Customization

To modify detection patterns:

1. Edit `sanitizer.js`
2. Update the `patterns` object
3. Add your custom pattern
4. Reload extension in `chrome://extensions/`

See [README](README.md) for development guide.
