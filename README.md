# Shield VPN: Ad-Blocker & Network Unlocking

Shield VPN is a production-ready Android application that provides device-wide ad-blocking and network unlocking capabilities using the native Android `VpnService` API.

## Features

- **One-Tap Connection**: Simple, intuitive Jetpack Compose UI to start/stop the VPN.
- **Ad-Blocking**: Intercepts DNS requests and blocks known ad-serving domains.
- **Network Unlocking**: Routes traffic through an encrypted tunnel to bypass regional restrictions.
- **Automated CI/CD**: GitHub Actions workflow included to build and release your APK automatically.
- **Material 3 Design**: Modern, responsive interface.

## Prerequisites

- **Android Studio Hedgehog** (2023.1.1) or newer.
- **JDK 17**.
- **Android Device/Emulator** running API 26 (Android 8.0) or higher.

## Installation & Setup

1.  **Clone the repository**:
    `git clone https://github.com/yourusername/shield-vpn.git`

2.  **Open in Android Studio**:
    Open the root directory. Let Gradle sync.

3.  **Run the App**:
    Select your device/emulator and click the 'Run' button (Shift + F10).

## How it Works

### Ad-Blocking (`DnsFiltering.kt`)
The app defines a blocklist of ad domains. When the VPN is active, DNS queries are checked against this list. If a match is found, the query is resolved to `0.0.0.0`, effectively killing the ad request before it leaves the device.

### VPN Service (`AdBlockVpnService.kt`)
The service creates a Virtual Network Interface (TUN). All device traffic is routed through this interface. The service manages the lifecycle and ensures the "Always-on VPN" feature can be supported.

## Configuration

To add your own proxy for network unlocking:
1. Update `ProxyConfig.kt` with your SOCKS5 or HTTP proxy details.
2. In `AdBlockVpnService.kt`, use the `setHttpProxy` method on the `VpnService.Builder` to route traffic.

## Troubleshooting

- **VPN won't connect**: Ensure you have granted the VPN permission in the Android dialog.
- **Ads still showing**: Some apps cache DNS. Try clearing the cache of the browser or app where ads appear.
- **Build failures**: Ensure your `local.properties` file points to the correct Android SDK path.

## Project Structure

- `app/src/main/java/.../vpn`: Core VPN logic and filtering.
- `app/src/main/java/.../MainActivity.kt`: UI logic and permission handling.
- `.github/workflows`: CI/CD automation for building the APK.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
