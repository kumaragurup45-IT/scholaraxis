## ScholarAxis Setup

1. Install frontend dependencies:
   `npm install`

2. Configure [.env.local](.env.local):
   `GEMINI_API_KEY=your_gemini_api_key`
   `VITE_FIREBASE_API_KEY=...`
   `VITE_FIREBASE_AUTH_DOMAIN=...`
   `VITE_FIREBASE_PROJECT_ID=...`
   `VITE_FIREBASE_STORAGE_BUCKET=...`
   `VITE_FIREBASE_MESSAGING_SENDER_ID=...`
   `VITE_FIREBASE_APP_ID=...`
   `VITE_FIREBASE_FUNCTIONS_REGION=us-central1`
   `VITE_DECISION_EMAIL_SENDER=client` (optional: `client` or `function`)

3. Run frontend:
   `npm run dev`

## Firebase Backend (Firestore + Functions)

1. Login to Firebase CLI:
   `firebase login`

2. Install Functions dependencies:
   `cd functions && npm install && cd ..`

3. Set Gmail secrets for functions (use Gmail App Password):
   `firebase functions:secrets:set GMAIL_USER`
   `firebase functions:secrets:set GMAIL_APP_PASSWORD`

4. Deploy Firestore rules:
   `firebase deploy --only firestore:rules`

5. Deploy Functions:
   `firebase deploy --only functions`

## Notes

- Frontend data is fully on Firestore (`users`, `scholarships`, `applications`, `notifications`, `reminders`).
- Decision mail sender is controlled by `VITE_DECISION_EMAIL_SENDER`:
  - `client` (default): send via EmailJS from frontend and mark as notified.
  - `function`: send via Cloud Functions (Nodemailer + Gmail secrets).
- Cloud Functions deployment requires Firebase Blaze plan.
- Current `firestore.rules` is permissive because the app still uses internal role login (not Firebase Auth).
