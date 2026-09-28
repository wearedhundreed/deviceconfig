# Native Mail S/MIME profile for Intune

[`native-mail-smime-intune.mobileconfig`](native-mail-smime-intune.mobileconfig) configures a Microsoft 365 Exchange Online account in Apple's native Mail app. It enables the account's S/MIME controls with these defaults:

| Setting | Profile value |
|---|---|
| S/MIME | Enabled |
| Sign | Off; user can turn it on |
| Encrypt by default | Off; user can turn it on |
| Per-message encryption | Available |
| Signing certificate | User-selectable |
| Encryption certificate | User-selectable |
| Server | `outlook.office365.com` over OAuth and SSL |
| Account identity | Intune `{{userprincipalname}}` and `{{mail}}` tokens |

## Required certificate setup

This profile contains no certificate or private key. Before signing or decrypting can work, assign an S/MIME certificate profile to the same Intune user. Microsoft recommends a PKCS signing certificate and imported historical encryption certificates so the same user can decrypt mail on every enrolled device. The certificate email identity must match the mailbox address.

Use Intune's built-in **iOS/iPadOS Email** template when it is available because it links the chosen PKCS, SCEP, or imported certificate profile directly. Use this custom file when you specifically need a `.mobileconfig` artifact.

## Import into Intune

1. In the Intune admin center, go to **Devices → Manage devices → Configuration → Create → New policy**.
2. Choose **iOS/iPadOS → Templates → Custom** and upload `native-mail-smime-intune.mobileconfig`.
3. Choose the device deployment channel and assign the profile to a small user test group first.
4. Assign the matching certificate and trusted-root profiles to the same group.
5. On the iPhone, open **Settings → Apps → Mail → Mail Accounts → Work Mail (S/MIME) → Account → Advanced → Sign** and select the delivered identity if iOS does not associate it automatically. Repeat for encryption.

The profile is intended for Intune distribution. If installed directly, the literal `{{userprincipalname}}` and `{{mail}}` values are not expanded. Replace them with the actual mailbox identity before manual installation. Installing it alongside another managed Exchange profile for the same mailbox can create a duplicate account.

Encryption works only when Mail has a valid public encryption certificate for every recipient. Face ID and passkeys do not replace the S/MIME identity certificate.
