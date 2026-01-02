# EisenPower Releases

Eisenhower Matrix task management app for macOS with automatic updates.

## Installation

1. Download `EisenPower-X.X.X.dmg` from the [latest release](https://github.com/gb221/eisenpower-releases/releases/latest)
2. Open the DMG file
3. Drag **EisenPower** to your **Applications** folder

## Automatic Updates

The app checks for updates daily. When a new version is available:
- You'll see a notification prompt
- Click **Install Update** to download and install
- The app restarts with the new version
- All your todos are preserved

You can also manually check: **EisenPower menu → Check for Updates...**

## Data Storage

Your todos are stored locally at:
```
~/Library/Application Support/EisenPower/
```

This location is separate from the app bundle, so your data is preserved across updates and reinstalls.

## Troubleshooting

### "App is damaged" error
Run in Terminal:
```bash
xattr -cr /Applications/EisenPower.app
```

### Data backup
Copy this folder to back up your todos:
```
~/Library/Application Support/EisenPower/
```
