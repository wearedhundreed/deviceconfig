# Password App Test profile

[`password-app-test.mobileconfig`](password-app-test.mobileconfig) adds a removable **Password Test** Home Screen shortcut to `https://auth-services-safari.onrender.com/?mode=password-test`. It opens the site in Safari so iOS can use its normal Password AutoFill, passkey, Face ID, and device-consent interfaces.

The profile contains only a Web Clip. It does not install a password manager, read saved passwords, create credentials without consent, change the default AutoFill provider, or bypass Face ID or the device passcode. After successful registration or sign-in, the test server records the normalized test email and timestamp in PostgreSQL. The authenticated session can see only its own audit history.

## Install

1. Download the `.mobileconfig` file on the iPhone and open it from Safari or Files.
2. Open **Settings → Profile Downloaded**, or **Settings → General → VPN & Device Management**.
3. Review the URL and install the unsigned testing profile.
4. Open **Password Test** from the Home Screen.

## Prepare Password AutoFill

1. Open **Settings → General → AutoFill & Passwords**.
2. Turn on **AutoFill Passwords and Passkeys**.
3. Select the password provider you want to test. For Apple's Passwords app, enable **Passwords** or **iCloud Passwords & Keychain**, depending on the iOS version.

## Passkey test

1. In **Password Test**, use the site's registration flow with an email address dedicated to testing. Do not use another person's address.
2. Confirm the system passkey sheet appears for `auth-services-safari.onrender.com`.
3. Approve creation using Face ID, Touch ID, or the device passcode.
4. Sign out, then use the sign-in flow.
5. Select the saved passkey and complete the system verification.
6. Confirm the site reports a successful WebAuthn assertion.
7. Confirm **Secure Audit** displays the signed-in test email and successful event timestamp.

## Internal test mailbox

After signing in, use **Test Mailbox** to view **Inbox**, **Outbox**, **Sent**, or **All**, or compose a text-only message to another registered test email. The server submits the message to an isolated Email Sandbox, which captures it without delivering to a real person. A captured message is copied into the authenticated recipient's internal Inbox. Failed submissions remain in the sender's Outbox. The mailbox does not access iCloud Mail.

Canceling the system sheet should produce a normal cancellation result. If no matching passkey exists, use the site's registration flow. Passkeys are scoped to the site's relying-party domain; a passkey created for this Render domain will not automatically work on another domain.

## Remove

Remove the profile from **Settings → General → VPN & Device Management**. Removing the Web Clip does not automatically delete a passkey. Manage any test passkey separately in the Passwords app.
