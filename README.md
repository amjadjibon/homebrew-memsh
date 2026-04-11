# Homebrew Tap for memsh

This is the official Homebrew tap for [memsh](https://github.com/amjadjibon/memsh), a virtual bash shell implemented in Go with an in-memory filesystem.

## Installation

```bash
brew tap amjadjibon/memsh
brew install memsh
```

## Update

To upgrade to the latest version:

```bash
brew update
brew upgrade memsh
```

## Uninstallation

```bash
brew uninstall memsh
brew untap amjadjibon/memsh
```

## macOS Security Warning

When first running `memsh` on macOS, you may see this warning:

> "Apple could not verify 'memsh' is free of malware"
> "Apple checked it for malicious software and none was detected"

### This is Expected

This warning appears because `memsh` uses **ad-hoc code signing** for macOS binaries. The binary is safe to use - this is a false positive from macOS Gatekeeper.

### How to Fix

**Option 1: Right-click to Open (Recommended)**
1. Open Finder
2. Navigate to `/opt/homebrew/bin/` (or run `which memsh` to find the location)
3. Right-click on `memsh`
4. Select "Open"
5. Click "Open" in the dialog
6. The binary is now trusted and can be run from terminal

**Option 2: Remove Quarantine Attribute**
```bash
xattr -d com.apple.quarantine $(which memsh)
```

**Option 3: Allow via System Settings**
1. Try to run `memsh` in terminal
2. Click "Cancel" on the security warning
3. Go to **System Settings → Privacy & Security**
4. Find the message about `memsh` being blocked
5. Click "Open Anyway"

After any of these steps, `memsh` will run normally without warnings.

### Why This Happens

macOS requires apps to be:
1. **Code signed** ✅ (we do this with ad-hoc signing)
2. **Notarized by Apple** ❌ (requires paid Apple Developer account)

The `memsh` project uses ad-hoc signing to ensure compatibility with Apple Silicon, but does not yet participate in Apple's notarization program.

## Verification

After installation, verify it's working:

```bash
memsh --version
```

Or run the interactive shell:

```bash
memsh
```

## Documentation

For full documentation, usage examples, and API reference, visit:
- [Main memsh repository](https://github.com/amjadjibon/memsh)
- [memsh Documentation](https://github.com/amjadjibon/memsh#readme)

## Is it Safe?

Yes! `memsh` is open-source software:
- **Source code**: https://github.com/amjadjibon/memsh
- **License**: MIT
- **Binary generation**: Automated via [GoReleaser](https://goreleaser.com/)
- **Build logs**: Public on GitHub Actions

You can verify the binary by:
1. Checking the source code
2. Building from source: `go install github.com/amjadjibon/memsh@latest`
3. Comparing checksums on the [releases page](https://github.com/amjadjibon/memsh/releases)

## Troubleshooting

### "command not found: memsh"

Make sure Homebrew is in your PATH:
```bash
# For Intel Macs
export PATH="/usr/local/bin:$PATH"

# For Apple Silicon Macs
export PATH="/opt/homebrew/bin:$PATH"
```

Add this to your `~/.zshrc` or `~/.bash_profile` to make it permanent.

### "memsh is damaged and can't be opened"

This means the quarantine attribute needs to be removed:
```bash
xattr -d com.apple.quarantine $(which memsh)
```

### Check installed version

```bash
brew info memsh
```

## License

See the [memsh license](https://github.com/amjadjibon/memsh/blob/main/LICENSE) for details.
