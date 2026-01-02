# EisenPower Releases

Eisenhower Matrix task management app for macOS with automatic updates.

## Installation (Target Mac)

1. Download `EisenPower-X.X.X.dmg` from the [latest release](https://github.com/gb221/eisenpower-releases/releases/latest)
2. Open the DMG file
3. Drag **EisenPower** to your **Applications** folder
4. **First launch only** (to bypass Gatekeeper):
   - Right-click the app → Select **Open** → Click **Open** in the dialog
   - Or run in Terminal: `xattr -cr /Applications/EisenPower.app`
5. Future launches work normally from Dock or Spotlight

## Automatic Updates

The app checks for updates daily. When a new version is available:
- You'll see a notification prompt
- Click **Install Update** to download and install
- The app restarts with the new version
- All your todos are preserved

You can also manually check: **EisenPower menu → Check for Updates...**

---

## Releasing a New Version (Developer)

### 1. Update Version Number

Edit `EisenPower/EisenPower/Info.plist`:
```xml
<key>CFBundleShortVersionString</key>
<string>1.1</string>  <!-- Increment this -->
<key>CFBundleVersion</key>
<string>2</string>     <!-- Increment this -->
```

### 2. Build the Release

```bash
cd /Users/alex/Documents/eisenpower
./scripts/release.sh
```

This creates in the `releases/` folder:
- `EisenPower-X.X.dmg` - For manual installation
- `EisenPower-X.X.zip` - For Sparkle auto-updates
- `appcast.xml` - Update feed (signed with EdDSA)

### 3. Update the Appcast URL

Edit `releases/appcast.xml` and update the version in the URL:
```xml
url="https://github.com/gb221/eisenpower-releases/releases/download/vX.X/EisenPower-X.X.zip"
```

### 4. Create GitHub Release

```bash
gh release create vX.X \
  --repo gb221/eisenpower-releases \
  --title "EisenPower vX.X" \
  --notes "Release notes here" \
  releases/EisenPower-X.X.dmg \
  releases/EisenPower-X.X.zip \
  releases/appcast.xml
```

### Release Checklist

- [ ] Version bumped in Info.plist
- [ ] `./scripts/release.sh` completed successfully
- [ ] Appcast URL updated to match new version tag
- [ ] GitHub release created with all 3 files
- [ ] Tested update on target Mac

---

## Data Storage

Your todos are stored locally at:
```
~/Library/Application Support/EisenPower/
```

This location is **separate from the app bundle**, so your data is preserved across updates and reinstalls.

## Troubleshooting

### "App is damaged" error
Run in Terminal:
```bash
xattr -cr /Applications/EisenPower.app
```

### Updates not working
1. Check **EisenPower menu → Check for Updates...**
2. Verify `appcast.xml` is accessible: https://github.com/gb221/eisenpower-releases/releases/latest/download/appcast.xml
3. Ensure the ZIP file URL in appcast.xml matches the GitHub release

### Data backup
Your Core Data database is at:
```bash
~/Library/Application Support/EisenPower/
```
Copy this folder to back up your todos.
