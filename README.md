# ConnectChat — Real-Time Messaging Website

A clean, responsive, real-time **one-to-one chat** website for a software-development portfolio. Users register with email and password, discover other users, exchange messages, and edit their profiles.

**Live website:** _Add your Netlify link here after deployment._

> **Which version is this?** This repository contains the **static Firebase + Netlify edition** of ConnectChat (HTML, CSS, JavaScript, Firebase Authentication, Cloud Firestore). It is **not** the separate React + Node.js + Socket.IO edition. No PHP, XAMPP, or Node.js server is needed for this repository.

## Features

| Feature | Status |
| --- | --- |
| Sign up and log in using email/password | ✅ Implemented |
| Find registered users | ✅ Implemented |
| Private one-to-one text conversations | ✅ Implemented |
| Live message updates through Firestore listeners | ✅ Implemented |
| Persistent chat history in Firestore | ✅ Implemented |
| Edit display name and profile description | ✅ Implemented |
| Responsive desktop and mobile interface | ✅ Implemented |
| Online presence and typing indicators | ❌ Not included in this Firebase edition |
| Read receipts, attachments and group chats | ❌ Not included |
| End-to-end encrypted messaging | ❌ Not included |

**Privacy notice:** Chat access is controlled by Firestore Security Rules, but **messages are not end-to-end encrypted**. In the current version, any signed-in user can discover the **names and email addresses of other registered users**. Use test email addresses for a public demo. Do not claim the app is suitable for sensitive communications.

## Tech stack

- **Frontend:** HTML5, CSS3, vanilla JavaScript (ES modules)
- **Authentication:** Firebase Authentication (Email/Password)
- **Database and real-time sync:** Cloud Firestore
- **Deployment:** Netlify (static hosting)
- **Firebase SDK:** loaded as browser ESM modules from Google's Firebase CDN

## Project structure

```text
connect-chat/
├── README.md
├── .gitignore
├── SECURITY.md
├── netlify.toml                      # Netlify Git deployment from repo root
└── ConnectChat_Firebase_Netlify_Ready/
    ├── index.html                   # Main website
    ├── style.css                    # Responsive design
    ├── app.js                       # Authentication and chat logic
    ├── firebase-config.js           # Public Firebase web app configuration
    ├── firestore.rules              # Rules to publish manually in Firebase
    ├── netlify.toml                 # Also supports using this folder as deploy root
    └── SETUP.txt                    # Short setup guide
```

## Run locally

This is a static website and does not need npm, React, or a database server installed on your laptop.

1. Clone or download this repository.
2. Confirm that `ConnectChat_Firebase_Netlify_Ready/firebase-config.js` points to your Firebase project.
3. In Firebase Console, enable **Authentication → Sign-in method → Email/Password**.
4. Create a Firestore database and publish the included `firestore.rules` under **Firestore Database → Rules**. Uploading the rules file to GitHub does **not** activate them.
5. Run a small static server from the repository root. One option if Python is installed:

   ```bash
   python -m http.server 5500 --directory ConnectChat_Firebase_Netlify_Ready
   ```

6. Visit **http://127.0.0.1:5500/**. Keep that terminal open.

Opening `index.html` directly via `file://` may fail because the application uses JavaScript modules and Firebase services. Use a local web server instead.

### Firebase configuration

`firebase-config.js` already contains a Firebase **web** configuration for project `connect-chat-6dc01`. Verify it belongs to **your** Firebase project; replace it with the web SDK configuration from **Firebase Console → Project settings → Your apps** if necessary.

A Firebase **web API key is not an administrator secret**. Authentication and data protection depend on Firebase Authentication and properly published Firestore Security Rules. **Never commit Firebase Admin SDK private keys, service-account JSON files, or credentials to GitHub.**

### Firestore security rules

The rules file is:

[**ConnectChat_Firebase_Netlify_Ready/firestore.rules**](ConnectChat_Firebase_Netlify_Ready/firestore.rules)

Go to **Firebase Console → Firestore Database → Rules**, paste that file, and select **Publish**. Rules are not deployed by Netlify, and they do not take effect just because the file is present in this repository.

To verify permissions, sign in as two separate test users and confirm that each can send/receive messages but cannot read other conversations.

## Deploy to Netlify from GitHub

This repository includes **root-level `netlify.toml`** so Netlify can find the site without moving files.

1. Open [Netlify](https://app.netlify.com/) and choose **Add new project → Import an existing project → GitHub**.
2. Select `yanshu411/connect-chat`.
3. Use these settings:

   | Field | Value |
   | --- | --- |
   | Base directory | _leave blank (repository root)_ |
   | Build command | _leave blank_ |
   | Publish directory | `ConnectChat_Firebase_Netlify_Ready` |

   These settings are also specified in the root `netlify.toml`.
4. Deploy, then copy your real `*.netlify.app` URL.
5. Go to **Firebase Console → Authentication → Settings → Authorized domains** and add your exact Netlify domain (without `https://`).
6. Ensure **Email/Password** authentication is enabled and **Firestore rules** are published.
7. Test signup and messaging between two accounts in different browsers or an incognito window.

If an earlier Netlify site used `ConnectChat_Firebase_Netlify_Ready` as the **base directory**, either keep its existing working settings or change its base directory to blank and publish directory to `ConnectChat_Firebase_Netlify_Ready`. Do not combine a nested base directory with the root-relative publish path.

### Manual Netlify deployment

From a downloaded checkout, drag the **`ConnectChat_Firebase_Netlify_Ready` folder** into [Netlify Drop](https://app.netlify.com/drop). That folder contains `index.html` at its top level. The README and root-level configuration are for GitHub-managed deployment; they are not required for drag-and-drop.

## Troubleshooting

| Symptom | Check |
| --- | --- |
| Website displays a Firebase setup error | Confirm `firebase-config.js` matches your Firebase project |
| "Operation not allowed" during signup | Enable Email/Password in Firebase Authentication |
| Firebase unauthorized-domain error | Add your real Netlify domain to Firebase authorized domains |
| "Permission denied" when sending a message | Publish `firestore.rules` and verify the signed-in user is in that conversation |
| Netlify 404 | Check the publish directory and ensure `index.html` is inside it |
| Blank page in local testing | Serve files using `http://127.0.0.1:5500/` rather than `file://`; check browser console |
| Missing Firestore indexes | Follow the suggested index creation link from Firebase's error message |

## Testing checklist

- [ ] Account A can register with an email and password.
- [ ] Account B can register in a separate browser or incognito window.
- [ ] Both accounts can discover one another.
- [ ] A can send a message to B; B receives it without reloading.
- [ ] B can reply, and A receives the reply.
- [ ] Messages remain after refresh.
- [ ] Profile edits save.
- [ ] A user cannot read conversations they are not a member of (verify rules).
- [ ] The layout works on a narrow mobile screen.

## Security and limitations

Read [SECURITY.md](SECURITY.md). This is an **educational portfolio project**, not a security-audited messenger. User profiles are discoverable to signed-in users, and private messaging is based on Firestore access rules rather than end-to-end encryption. Do not share real financial information, passwords, or other sensitive data in the chat.

## Resume / LinkedIn

**ConnectChat — Real-Time Messaging Website:** Built a responsive, browser-based messaging application using HTML, CSS, JavaScript, Firebase Authentication, Cloud Firestore and Netlify, featuring user accounts, real-time one-to-one chat, persistent message history, and editable profiles.

## Future improvements

- Optional opt-in user discovery that does not reveal email addresses
- Online status, typing indicators, unread counts, and read receipts
- File uploads and profile avatars with appropriate storage policies
- Authentication abuse protections, monitoring, and automated security-rule tests
- A hosted demo URL and screenshots in this README
