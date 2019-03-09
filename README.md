# Mongoose OS Captive Portal WiFi Stack

[![Gitter](https://badges.gitter.im/cesanta/mongoose-os.svg)](https://gitter.im/cesanta/mongoose-os?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

- [Mongoose OS Captive Portal WiFi Stack](#mongoose-os-captive-portal-wifi-stack)
  - [Author](#author)
  - [Demo Application](#demo-application)
  - [Installation/Usage](#installationusage)
    - [Use specific branch of library](#use-specific-branch-of-library)
  - [Included Libraries](#included-libraries)
    - [Captive Portal `captive-portal`](#captive-portal-captive-portal)
      - [Features](#features)
    - [WiFi Setup `captive-portal-wifi-setup`](#wifi-setup-captive-portal-wifi-setup)
      - [Features](#features-1)
    - [WiFi RPC `captive-portal-wifi-rpc`](#wifi-rpc-captive-portal-wifi-rpc)
      - [Features](#features-2)
    - [Captive Portal Web UI `captive-portal-wifi-web`](#captive-portal-web-ui-captive-portal-wifi-web)
      - [Features](#features-3)
  - [Changelog](#changelog)
  - [License](#license)

This library adds a full captive portal solution to any Mongoose OS device. When a client connects (desktop/mobile, etc), it will prompt the user to "Sign in to Network", and will display a webpage for the user to setup/configure wifi.

This library is a complete remake of my original [WiFi Captive Portal](https://github.com/tripflex/wifi-captive-portal) library, separating all features into separate libs to allow using only the features you need.

**This library is the full stack and includes all libraries listed below** -- providing a full stack solution for a Captive Portal

![OSX Captive Portal](https://raw.githubusercontent.com/tripflex/captive-portal-wifi-web/master/osx-portal.gif)

## Author
Myles McNamara ( https://smyl.es )

## Demo Application
If you want to test out the full stack solution, I have created a test/demo application you can use to flash to your device and play around with it:
[https://github.com/tripflex/captive-portal-wifi-stack-demo](https://github.com/tripflex/captive-portal-wifi-stack-demo)

## Installation/Usage
Add this lib your `mos.yml` file under `libs:`

```yaml
  - origin: https://github.com/tripflex/captive-portal-wifi-stack
```

### Use specific branch of library
To use a specific branch of this library (as example, `dev`), you need to specify the `version` below the library

```yaml
  - origin: https://github.com/tripflex/captive-portal-wifi-stack
   version: dev
```

## Included Libraries

Below is a list of all the libraries included in this one.  There is **NO** code associated with this library, it's just a wrapper around all the Captive Portal libraries, to make it easy for installation of a full stack Captive Portal solution.

**It's STRONGLY recommended** that you read the README for each individual library, to see the available config options, and features -- __as this may not be the latest list of features__!

### [Captive Portal](https://github.com/tripflex/captive-portal) `captive-portal`

This library handles all the DNS, and redirection required for Captive Portal prompts, etc.  

See the library [**FULL README**](https://github.com/tripflex/captive-portal) for all details on this library.

#### Features
- Mobile and desktop devices prompt the "Login to network" window/notification
- Support for GZIP files
- Checks device Accepts header to make sure that it supports GZIP before sending/using GZIP files
- Support for Samsung Android devices that do not follow Captive Portal 302 redirect standards

### [WiFi Setup](https://github.com/tripflex/captive-portal-wifi-setup) `captive-portal-wifi-setup`

This library is for testing, saving, and setting up Mongoose OS device's WiFi.  The main feature of this library is the ability to test WiFi credentials, and then save or update them in the configuration.

See the library [**FULL README**](https://github.com/tripflex/captive-portal-wifi-setup) for all details on this library.

#### Features
- Test WiFi SSID and Passwords
- Automatically save SSID and Password after validating SSID and Password
- Automatically disable AP after successful WiFi test
- Automatically reboot the device after saving and successful test
- Set which STA index to save configuration to `wifi.sta` `wifi.sta1` or `wifi.sta2`
- Set custom timeout for testing connection and credentials (`30` seconds by default `cportal.setup.timeout`)
- Mongoose OS successful, failed, and started test events
- Callback for failed/successful test for use in `C` or `mJS`
- Disable Captive Portal setting after successful test

### [WiFi RPC](https://github.com/tripflex/captive-portal-wifi-rpc) `captive-portal-wifi-rpc`

This library adds RPC endpoints for Mongoose OS to Scan for WiFi networks (same as `rpc-service-wifi` lib), and test WiFi credentials (from the `captive-portal-wifi-setup` lib).

See the library [**FULL README**](https://github.com/tripflex/captive-portal-wifi-rpc) for all details on this library.

#### Features
- RPC Endpoint to Scan for Wireless Networks
- RPC Endpoint to Test WiFi connection and credentials
- Disable RPC endpoints after successful wifi test

### [Captive Portal Web UI](https://github.com/tripflex/captive-portal-wifi-web) `captive-portal-wifi-web`

This library is **only** the Captive Portal WiFi Web UI.  It does not include any C or mJS files, and is specifically for use in the Captive Portal WiFi Stack.  This library was built with minimal space in mind, and as such, it **DOES NOT** include any libs like `axios`, `jquery` or anything else that would add unecessary bloat to your already limited space on embedded device!  **Completely vanilla JavaScript!**

See the library [**FULL README**](https://github.com/tripflex/captive-portal-wifi-web) for all details on this library.

#### Features
- Provides web UI for testing and configuring WiFi
- **Completely vanilla JavaScript**, no jQuery, Zepto, or other libraries required (because we all know space is limited)
- **Unminified and non-gzipped** files are only `14.2kb` total in size ( `wifi_portal.css - 2.87 KB`, `wifi_portal.html - 1.45kb`, `wifi_portal.js - 14.2 KB` )
- **Minified** files are only `14.2kb` total in size ( `wifi_portal.css -  1.81 KB`, `wifi_portal.html - 1007 Bytes`, `wifi_portal.js - 6.79 KB` )
- **Minified and gzipped** files are only `3.26kb` total in size ( `wifi_portal.css.gz - 735b`, `wifi_portal.html.gz - 561b`, `wifi_portal.js.gz - 2kb` )
- Displays a dropdown of available networks to connect to
- Included minified files by default on device `fs_min` directory (are copied to device)
- Source files are available in the `fs` directory (are not copied to device)
- Minified and GZIP files are available in the `fs_min_gzip` directory (are not copied to device)


## Changelog
**1.0.0** (TBD) - Initial release

## License
Apache 2.0
