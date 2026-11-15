# Security and privacy — ConnectChat

This repository is a **learning/portfolio project**, not an audited secure messaging product.

## Current controls

- Firebase Authentication handles email/password authentication.
- Firestore security rules restrict conversation reads and messages to authenticated conversation members.
- Message text is escaped when rendered to avoid inserting untrusted HTML.
- This site is static and does not require committing a Firebase administrator credential.

## Important limitations

- **Not end-to-end encrypted.** Messages are stored in Cloud Firestore and are not protected by end-to-end encryption.
- **Email discovery:** the current Firestore rules allow any signed-in user to read the `users` collection, including email addresses. The application displays emails for search/discovery. Do not use private or sensitive addresses in a public demo. A future upgrade should separate public discoverable profiles from private account data.
- **Firebase config != Firestore rules.** The web `apiKey` in `firebase-config.js` is a public identifier. Do not treat it as a secret or as a permission system. Publish and test `firestore.rules` in Firebase Console.
- No production abuse monitoring, email verification enforcement, rate limits, security audit, or account deletion workflow is included.
- The project uses Firebase's hosted JavaScript SDK and requires internet connectivity.

## Do not commit

- Firebase service-account JSON files or admin credentials
- `.env` files that contain backend secrets
- Private keys, third-party API tokens, user exports, or production data

## What to test before public launch

1. Publish the included Firestore rules in Firebase Console.
2. Verify a logged-out user cannot read user documents or message documents.
3. Verify a signed-in user cannot read or write conversations of which they are not a member.
4. Register two test users and confirm messaging works both directions.
5. Confirm the domain listed under Firebase Authentication authorized domains matches the deployed Netlify hostname.

## Responsible use

Use fictional accounts and non-sensitive test messages while the application is in this development stage.
