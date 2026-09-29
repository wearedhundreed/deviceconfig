# secure-password-manager profile

[`secure-password-manager.mobileconfig`](secure-password-manager.mobileconfig) is an unsigned, removable configuration profile for **MOREDESA LLC**. It adds one Home Screen Web Clip named **Secure Password** that opens the existing HTTPS authentication test service in Safari.

The profile does not enroll or supervise the iPhone, install an MDM identity, convert a personal Apple Account into a Managed Apple Account, or provide access to Mail, Messages, passwords, verification codes, or device secrets.

## Manual installation

1. Open `https://auth-services-safari.onrender.com/profiles/` in Safari.
2. Download **secure-password-manager**.
3. Open **Settings → Profile Downloaded**, or **Settings → General → VPN & Device Management**.
4. Confirm the organization is **MOREDESA LLC**, the only payload is a removable Web Clip, and the URL is `https://auth-services-safari.onrender.com/`.
5. Tap **Install**, then open **Secure Password** from the Home Screen.

Because this repository version is unsigned, iOS may show an unverified-publisher warning. Signing requires a valid organization signing identity or delivery through an authorized MDM. Never add an Apple Account password, app-specific password, recovery key, verification code, private key, or session token to this file.

## Business domain

`secure-password-manager.com` is the public business domain. The profile intentionally points to the currently deployed HTTPS service until that domain is connected to the deployment and serves the application successfully. Universal Links and Password AutoFill association require an `apple-app-site-association` file on the public domain and matching application entitlements; a configuration profile alone cannot establish either relationship.

## Current enrollment status

The iPhone is not enrolled in Apple Business or device management. This profile is therefore a user-approved manual installation and remains removable. Apple Business verification, domain verification, Managed Apple Account creation, and device enrollment must be completed through Apple's official services.
