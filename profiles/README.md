# iPhone configuration profile: Safari Passkey Lab

[`safari-passkey-lab.mobileconfig`](safari-passkey-lab.mobileconfig) is an iOS/iPadOS configuration profile with one Web Clip payload. It adds a **Passkey Lab** Home Screen icon for `https://auth-services-safari.onrender.com/`. The clip opens in Safari (`FullScreen` is false), so the normal HTTPS origin and Safari passkey flow are used. The icon and profile are removable.

This file can be imported into an existing MDM as a custom iOS/iPadOS configuration profile or installed manually on an iPhone. It is **not** an MDM enrollment profile: this repository contains settings catalog reference exports, but no Apple Push Notification service certificate, enrollment service, device identity, or MDM check-in endpoints. It grants no device management authority and does not carry a password, token, certificate, or private key.

## Manual installation

1. Download the `.mobileconfig` file to the iPhone using Safari or Files. Review that it contains only one Web Clip pointing to the HTTPS URL above. This repository version is unsigned, so iOS may identify its publisher as unverified.
2. In **Settings**, open **Profile Downloaded** (or **General → VPN & Device Management**) and install the profile after reviewing iOS's prompts. If the browser displays XML instead of offering a profile download, save the `.mobileconfig` file to Files and open it there, or serve it from your own HTTPS endpoint with content type `application/x-apple-aspen-config`.
3. Open **Passkey Lab** from the Home Screen. Register or sign in using Safari's standard passkey prompt. Remove it from **Settings → General → VPN & Device Management** when finished.

## Intune custom profile

In Intune, create an **iOS/iPadOS → Templates → Custom** configuration profile, upload the `.mobileconfig` file, and assign it only to devices you manage. The Intune admin must review assignment scope and the exact payload before distribution. Do not use this profile as a replacement for enrollment or for the OAuth server's Vercel connector configuration.

## Validation

The file is an XML property list with a `Configuration` top-level payload and a `com.apple.webClip.managed` child payload. Its identifiers and UUIDs are stable so an updated profile can replace the same installation. Its URL is the existing Safari web app, not the OAuth authorization server.
