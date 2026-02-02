# Remote HMI Tester via VNC/SSH

A Flutter application for industrial users to remotely test edge-device HMIs via VNC (GUI) and SSH (tools, diagnostics, and MQTT).

## Features

- SSH connection management and command execution
- VNC remote desktop viewing
- MQTT publish/subscribe tools (over SSH)
- Diagnostics utilities

## How Connections Work

- VNC is a direct TCP connection to the target host on port 5900 (via `flutter_rfb`).
- SSH is used separately for diagnostics, terminal commands, and MQTT tooling.
- This app does not create an SSH tunnel for VNC. If you need VNC-over-SSH, you must set up tunneling outside the app, and the current UI assumes the same host for both VNC and SSH.

## Target Device Requirements

- A running VNC server on port 5900 with a configured password.
- An SSH server with password authentication enabled.
- `mosquitto_pub` and `mosquitto_sub` available on the device if you use MQTT tools.

## Getting Started

This project is built with Flutter and supports multiple platforms including Android, iOS, Windows, macOS, and Linux.

### Prerequisites

- [Flutter SDK](https://docs.flutter.dev/get-started/install)
- Development environment for your target platform

### Building and Running

#### For Windows

To build a Windows executable:

1. See the [Windows Build Instructions](WINDOWS_BUILD_INSTRUCTIONS.md) for detailed steps
2. Use the provided `build_windows.bat` script for an automated build process

#### For Other Platforms

For other platforms, follow the standard Flutter build process:

```bash
# Enable the platform you want to build for
flutter config --enable-<platform>

# Get dependencies
flutter pub get

# Build the application
flutter build <platform>
```

Replace `<platform>` with one of: `android`, `ios`, `macos`, `linux`, or `web`.

## Usage

1. Open the Settings page and set:
   - Edge Device IP (used for both VNC and SSH connections)
   - SSH username, password, and port
   - VNC password
2. Save settings and optionally test the SSH connection.
3. Open the VNC page and click “Connect to VNC”.
4. Use the SSH page for terminal commands and the MQTT tools for publish/subscribe.

## Security Notes

- Credentials are stored in shared preferences on the client device.
- SSH host key verification is not configured, so you should only connect to trusted hosts.

## Development Resources

- [Flutter Documentation](https://docs.flutter.dev/)
- [Dart Documentation](https://dart.dev/guides)
