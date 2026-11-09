# Voice Email demo (BizPleaser.AI)

Big-button, talking email for people with low vision. It's one file, `index.html`, with no server.

**Live link:** https://htmlpreview.github.io/?https://github.com/Jortega1085/voice-email-demo/blob/main/index.html
(Once GitHub Pages is turned on, under repo Settings → Pages → Deploy from branch `main` / root: https://jortega1085.github.io/voice-email-demo/)

## 1. Demo right now (mock mode, zero setup)
1. Open the live link on the phone (Safari on iPhone, Chrome on Android).
2. Turn the volume up and the silent switch off.
3. Tap **START**. The phone says "You have 3 unread messages."
4. Tap **Read next**: "Message 1 of 3, from Sarah (your daughter), subject Dinner on Sunday?"
5. Tap **Read full message**, then **Reply by voice**, then the green mic button. Say your reply.
6. The draft shows in huge yellow text and is read back. Tap **SEND**, or tap the voice button and say "send".
7. You hear "Demo: Your reply was sent." The yellow banner reads **DEMO MODE - nothing is actually sent**.

If the mic doesn't work, type in the box instead, or use the keyboard's mic key.

## 2. Real Gmail (about 10 min on a laptop, or later)
1. Go to https://console.cloud.google.com and create a project (e.g. "Voice Email").
2. Open **APIs & Services → Library**, find **Gmail API**, and click **Enable**.
3. Open **APIs & Services → OAuth consent screen** (Google Auth Platform):
   User type **External**, app name, your support email. Add scopes `gmail.readonly` and `gmail.send`.
   Leave the app in **Testing**. Under **Test users / Audience**, add the Gmail address that will be read (e.g. the mother's).
4. Open **Credentials → Create credentials → OAuth client ID**. Pick type **Web application**.
   For **Authorized JavaScript origins**, add the exact origin you open the app from (no path, no trailing slash):
   - `https://htmlpreview.github.io` (current live link)
   - `https://jortega1085.github.io` (if you use GitHub Pages)
   Then click Create and copy the **Client ID** (`....apps.googleusercontent.com`).
5. In the app, tap **Settings**, paste the Client ID, tap **Real Gmail**, then **Sign in with Google**.
   Shortcut: `...index.html?client_id=YOUR_ID&mode=real`
6. Google shows **"Google hasn't verified this app"**. Tap **Advanced → Go to (app)**. This is expected.
   Gmail scopes are *restricted*, so only the listed test users can sign in until Google verifies the app (a security review is needed for public launch). Testing-mode sign-ins expire after about 7 days; sign in again when that happens.

The app reads the 10 newest unread inbox messages. It does not mark them read; it only needs read and send access. Replies go out in the same thread with the proper `In-Reply-To` and `References` headers.

## 3. Limitations and notes
- **iPhone:** Use Safari, iOS 14.5 or later. On first mic use, tap **Allow** for Microphone *and* Speech Recognition. If you tapped Don't Allow, go to Settings → Safari → Microphone, or aA → Website Settings. Voice typing needs **Siri & Dictation** enabled (Settings → Siri, and Settings → General → Keyboard → Enable Dictation).
- iOS only plays speech after a tap, which is why the app starts with the big START button. Keep the silent switch off.
- **Android:** Use Chrome. Allow the mic when asked.
- The Google sign-in pop-up must be allowed (pop-up blockers can stop it).
- **Privacy:** There's no backend. The Google token lives only in the browser tab's memory. Only the Client ID and speech speed are saved on the phone. Speech-to-text may be processed by Apple or Google's speech services.
- This is a proof of concept, not a finished product (no attachments, no compose-new, no contact lookup).
