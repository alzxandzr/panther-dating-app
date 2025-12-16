# Panther Dating App - Project Setup Guide

## Tech Stack

### Frontend
- **React Native (Expo)** - Cross-platform mobile development for iOS and Android
- **TypeScript** - Type-safe JavaScript
- **React Navigation** - Navigation between screens

### Backend & Services
- **Firebase Authentication** - FIU email-only sign-up (@fiu.edu)
- **Cloud Firestore** - Real-time database for profiles, matches, messages
- **Firebase Cloud Messaging (FCM)** - Push notifications
- **Firebase Storage** - Profile photos and media

### Future ML Integration
- **Two-tower recommendation model** (Python service) for intelligent matching
- Embeddings stored in Firestore or separate vector DB

### Design & Collaboration
- **Figma** - UI/UX design and component library
- **Notion** - Team workspace for planning, specs, and roadmap
- **GitHub** - Version control and issue tracking

---

## Project Structure

```
panther-dating-app/
├── src/
│   ├── screens/              # Page-level components
│   │   ├── LoginScreen.tsx
│   │   ├── SignupScreen.tsx
│   │   ├── SwipeScreen.tsx
│   │   ├── MatchesScreen.tsx
│   │   ├── ChatListScreen.tsx
│   │   └── ChatRoomScreen.tsx
│   ├── components/           # Reusable UI components
│   │   ├── ProfileCard.tsx
│   │   ├── MessageBubble.tsx
│   │   └── Button.tsx
│   ├── navigation/           # Navigation setup
│   │   ├── AppNavigator.tsx
│   │   └── AuthNavigator.tsx
│   ├── services/             # API and Firebase logic
│   │   ├── firebase.ts       # Firebase config
│   │   ├── auth.ts           # Auth helpers (FIU check)
│   │   └── firestore.ts      # Database helpers
│   ├── hooks/                # Custom React hooks
│   │   ├── useAuth.ts
│   │   └── useChat.ts
│   ├── types/                # TypeScript types
│   │   └── index.ts
│   └── constants/            # Colors, spacing, typography
│       └── theme.ts
├── assets/                   # Images, icons from Figma
├── app.json                  # Expo configuration
├── package.json
└── README.md
```

---

## Getting Started

### Prerequisites
- Node.js 18+ and npm/yarn
- Expo CLI: `npm install -g expo-cli`
- Git installed
- Firebase account (free tier works)

### Initial Setup

1. **Clone the repo**
   ```bash
   git clone https://github.com/alzxandzr/panther-dating-app.git
   cd panther-dating-app
   ```

2. **Create development branch**
   ```bash
   git checkout -b dev
   ```

3. **Install dependencies** (once package.json is set up)
   ```bash
   npm install
   ```

4. **Set up Firebase**
   - Create Firebase project at console.firebase.google.com
   - Enable Authentication (Email/Password)
   - Create Firestore database
   - Add Firebase config to `src/services/firebase.ts`

5. **Run the app**
   ```bash
   npx expo start
   ```
   - Scan QR code with Expo Go app (iOS/Android)
   - Or press `i` for iOS simulator, `a` for Android emulator

---

## Workflow

### Branch Strategy
- `main` - Stable, production-ready code
- `dev` - Integration branch for ongoing work
- `feature/*` - Individual feature branches (e.g., `feature/login-screen`)

### Development Process
1. Pick a GitHub Issue
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Make changes and commit regularly
4. Push and open a Pull Request to `dev`
5. Get code review from a teammate
6. Merge after approval

### Figma → Code Handoff
1. Designer creates/updates screens in Figma
2. Add annotations for interactions and states
3. Export assets to `assets/` folder
4. Developer inspects spacing, colors, typography in Figma
5. Build components in `src/components/` and screens in `src/screens/`
6. Match Figma design system tokens in `src/constants/theme.ts`

---

## Firebase Data Model

### Collections

**users**
```typescript
{
  id: string,           // Firebase Auth UID
  email: string,        // @fiu.edu address
  displayName: string,
  age: number,
  bio: string,
  interests: string[],
  photos: string[],     // Firebase Storage URLs
  createdAt: timestamp
}
```

**chats**
```typescript
{
  id: string,
  participants: string[],  // Array of user IDs
  isGroup: boolean,
  groupName?: string,
  lastMessage: string,
  lastMessageAt: timestamp,
  createdAt: timestamp
}
```

**chats/{chatId}/messages** (subcollection)
```typescript
{
  id: string,
  senderId: string,
  text: string,
  createdAt: timestamp,
  read: boolean
}
```

**matches**
```typescript
{
  id: string,
  user1: string,
  user2: string,
  matchedAt: timestamp
}
```

---

## Adding Collaborators

1. Go to: https://github.com/alzxandzr/panther-dating-app/settings/access
2. Click **"Add people"**
3. Enter GitHub username or email
4. Give **Write** access for developers
5. They'll receive an email invitation

---

## First 5 Tasks (See GitHub Issues)

1. **Set up Expo + base project structure**
2. **Add Firebase to the app**
3. **Implement FIU-only email authentication**
4. **Create placeholder screens + navigation**
5. **Define Firestore data model**

Check the Issues tab for detailed descriptions of each task.

---

## MVP Features (Must-Have)

- ✅ FIU email-only sign-up/login (@fiu.edu)
- ✅ Hinge-style card stack browsing
- ✅ Like/pass system with match notifications
- ✅ 1-1 chat for matches
- ✅ Basic group/event chat rooms
- ✅ Push notifications for new matches and messages

## Nice-to-Have (Post-MVP)

- PantherConnect event integration
- ML-based match ranking (two-tower model)
- Advanced profile prompts and filters
- Video chat
- Event-based speed dating rounds

---

## Questions?

Reach out in the team Notion workspace or Slack channel.
