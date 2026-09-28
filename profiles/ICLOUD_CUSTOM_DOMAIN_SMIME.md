# secure-password-manager.com iCloud Mail profile

## Preferred iPhone setup

An iCloud custom email domain is part of the iPhone's existing iCloud Mail account. On the iPhone, open **Settings → [your name] → iCloud → Mail → Custom Email Domain**, confirm that `secure-password-manager.com` is connected, and create or confirm the exact mailbox address you intend to use.

Use Apple's iCloud setup screen for the domain's DNS records. The verification and mail records shown there are specific to the domain. Copy them exactly into the DNS provider for `secure-password-manager.com`; do not substitute example values from this repository.

If the address already sends and receives through the built-in iCloud Mail account, no additional Mail profile is needed.

## Optional managed Mail profile

[`icloud-secure-password-manager-smime.mobileconfig`](icloud-secure-password-manager-smime.mobileconfig) creates a separate IMAP account for the domain. It uses Apple's iCloud Mail servers:

- Incoming: `imap.mail.me.com`, SSL, port `993`
- Outgoing: `smtp.mail.me.com`, SSL, port `587`

The profile intentionally contains no email address, username, password, certificate, or private key. Install it interactively on the iPhone and enter the requested values there:

1. Use the exact mailbox, such as `name@secure-password-manager.com`, for the email address.
2. For the incoming username, use the iCloud Mail account name Apple specifies for the account. For the outgoing username, Apple specifies the full iCloud Mail address.
3. Use an Apple app-specific password created at `account.apple.com`, not the Apple Account password.

Because the profile creates another Mail account, installing it while the same mailbox is already active through iCloud can show duplicate mailboxes. Use the built-in iCloud account unless a separate managed account is required.

## S/MIME signing and encryption

The profile exposes S/MIME signing, default encryption, and per-message encryption controls. It leaves them off until a matching identity certificate is installed and selected.

S/MIME requires a certificate issued for the exact mailbox address. Obtain a certificate from a trusted certificate authority, install its identity (certificate plus private key) through a private delivery method or your MDM, and select it for this Mail account in **Settings → Apps → Mail → Mail Accounts → secure-password-manager.com iCloud Mail → Advanced**.

Never commit a `.p12` file, private key, certificate password, Apple app-specific password, or recovery code to this repository. The domain name alone cannot create or recover an S/MIME identity.

## Manual installation

1. Download the `.mobileconfig` file in Safari or save it to Files and open it.
2. In **Settings**, open **Profile Downloaded**, or go to **General → VPN & Device Management**.
3. Review the account servers and install the profile.
4. Enter the account details only in the iOS installation prompts.
5. Send a test message to yourself, then verify receipt and sending before enabling S/MIME.

The repository copy is unsigned, so iOS may label its publisher unverified. An organization distributing it through MDM should sign the profile and supply credentials or certificates through its protected MDM secret and certificate workflows.
