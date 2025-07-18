# macOS Support for Kind Action

This document describes the changes made to add macOS support to the Kind Action.

## Changes Made

### 1. Platform Detection Functions

Added three new functions to `kind.sh`:

- `detect_os()`: Detects the operating system (darwin, linux, or unsupported)
- `get_checksum_cmd()`: Returns the appropriate checksum command for the platform
- `get_platform()`: Returns the platform name for binary downloads

### 2. Checksum Command Compatibility

- **Linux**: Uses `sha256sum` (existing behavior)
- **macOS**: Uses `shasum -a 256` (macOS equivalent)

### 3. Binary Downloads

Updated the download URLs to use platform-specific binaries:

- **kind**: Downloads `kind-{platform}-{arch}` instead of `kind-linux-{arch}`
- **kubectl**: Downloads from `bin/{platform}/{arch}/` instead of `bin/linux/{arch}/`

### 4. Cloud Provider Handling

- **Linux**: Installs and runs cloud-provider-kind as before
- **macOS**: Skips cloud-provider-kind installation with a warning message (not available for macOS)

### 5. Documentation Updates

- Updated `README.md` to indicate macOS support
- Added example workflow for macOS
- Noted that cloud provider feature is not available on macOS

## Testing

The changes have been tested to ensure:

1. ✅ OS detection works correctly on macOS (detects "darwin")
2. ✅ Checksum command selection works (uses "shasum -a 256" on macOS)
3. ✅ Platform detection works (detects "darwin" on macOS)
4. ✅ Architecture detection works (detects "arm64" on Apple Silicon)
5. ✅ Checksum command is available on macOS
6. ✅ Cloud provider logic correctly skips on macOS

## Compatibility

- **Ubuntu runners**: All existing functionality preserved
- **macOS runners**: Full support except for cloud provider feature
- **Other platforms**: Falls back to Linux behavior

## Files Modified

1. `kind.sh` - Added platform detection and compatibility functions
2. `README.md` - Updated documentation to reflect macOS support

## Files Unchanged

- `action.yml` - No changes needed
- `main.js` - No changes needed  
- `main.sh` - No changes needed
- `registry.sh` - Already compatible with macOS
- `cleanup.sh` - Already compatible with macOS
- `cleanup.js` - No changes needed 