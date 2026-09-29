# Apple Business profile host

[`apple-business-profile-host.mobileconfig`](apple-business-profile-host.mobileconfig) adds a removable **Business Setup** Home Screen shortcut to `https://auth-services-safari.onrender.com/profiles/`.

The profile contains one Web Clip. It does not enroll the iPhone in device management, create a Managed Apple Account, convert a personal Apple Account, verify an organization, or grant Apple Business status. It contains no Apple Account identifier, password, token, certificate, private key, or recovery code.

## Install

1. Download the profile from the HTTPS profile host in Safari.
2. Open **Settings → Profile Downloaded**, or **Settings → General → VPN & Device Management**.
3. Review that the only payload is a removable Web Clip for the profile-host URL.
4. Install it and open **Business Setup** from the Home Screen.

The repository copy is unsigned, so iOS may identify the publisher as unverified. A verified organization can sign it through an authorized MDM or profile-signing process after Apple Business and device management are configured.

## Use the iCloud Mail address safely

An address hosted by iCloud Mail at `secure-password-manager.com` can be used as the Apple Business organization contact or administrator email if it is controlled by the organization. Receive Apple's messages in the normal Mail app. Never put the mailbox password, Apple app-specific password, verification code, or recovery key in this profile, GitHub, or the profile host.

## Required Apple Business steps

Apple, not a configuration profile or this host, decides whether an organization and its accounts are managed:

1. Create the organization at `https://business.apple.com/` using the authorized organization contact and complete Apple's organization verification.
2. In Apple Business, add `secure-password-manager.com` under **Settings → Domains**.
3. Copy Apple's unique verification value into the domain's DNS as the exact TXT record Apple supplies.
4. After Apple reports the domain verified, create Managed Apple Accounts manually, synchronize them from a supported identity provider, or configure OIDC federation.
5. Resolve any existing personal Apple Account conflicts on the domain using Apple's Domain Capture process. Do not attempt to overwrite or impersonate those accounts.
6. Turn on Apple's built-in device management or connect a legitimate external MDM, then enroll only devices the organization owns or is authorized to manage.

A personal Apple Account remains personal until Apple's official domain and account workflows are completed. Installing this profile does not change its account type.
