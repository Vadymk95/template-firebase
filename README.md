## Template 1 · Enterprise-Grade React Starter

A battle-tested, high-performance starter for building modern React apps. Optimized for speed, scalability, and developer experience. Ships with state management, data fetching, routing, and a complete CI/CD pipeline.

> **Note:** Targets **Node.js v24**. Includes strict version management via `.nvmrc` and `package.json` engines.

### 🚀 Key Features

#### Tech Stack

- **React 19** (Latest features ready)
- **Vite** (Powered by **Rolldown** + **Oxc** minification for blazing fast builds)
- **TypeScript** with strict rules and `@/*` path aliases
- **React Router v7** for robust routing
- **Zustand** for global state (with devtools & auto-selectors)
- **TanStack Query v5** for async state management
- **React Hook Form + Zod** for type-safe forms
- **Firebase** (Firestore, Analytics) - Ready to use with simplified configuration

#### UI & Styling

- **Tailwind CSS v4** ready configuration
- **Shadcn UI** components (Button, Input, etc.)
- **Inter Font** (Self-hosted automatically for GDPR & Performance)
- **Modern "Google Blue"** design system tokens

#### Performance & Optimizations ⚡️

- **Brotli Compression:** (`.br`) assets generated at build time.
- **Self-hosted Fonts:** Google Fonts are downloaded and served locally (0 external requests).
- **Smart Chunking:** Vendor splitting (`react-vendor`, `ui-vendor`, `state-vendor`) for optimal caching.
- **Bundle Analysis:** Visualizer report generated in `dist/bundle-analysis.html`.

#### Developer Experience

- **Dev Playground:** Built-in UI showcase at `/dev/ui` (Development only).
- **VS Code Integrated:** Pre-configured `.vscode` settings, extensions recommendations, and snippets.
- **Linting:** ESLint (Flat Config) + Prettier + Import Sorting.
- **Git Hooks:** Husky + Lint Staged + Commitlint to enforce quality.

### 🛠 Project Structure

```
src/
  components/       // UI primitives, layout shell, ErrorBoundary
  hocs/             // Custom HOCs (e.g. WithSuspense)
  hooks/            // Custom hooks
  lib/              // Utilities and Firebase configuration
    firebase.ts     // Firebase initialization (Firestore, Analytics)
  pages/            // Route-level components (Lazy loaded)
    DevPlayground/  // UI Kit showcase (Dev only)
  router/           // React Router setup
  store/            // Zustand store with utilities
  test/             // Vitest setup and helpers
  main.tsx          // App entry point

firebase.json        // Firebase CLI configuration
firestore.rules      // Firestore security rules
firestore.indexes.json // Firestore indexes
.env.example         // Environment variables template
```

### 🚦 Getting Started

1.  **Clone & Install:**

    ```bash
    # Ensure you are on Node 24 (use nvm)
    nvm use
    npm install
    ```

2.  **Configure Firebase:**
    - Create a new Firebase project at [Firebase Console](https://console.firebase.google.com/)
    - Create a **Firestore Database** (choose location, e.g., `eur3` for Europe)
    - Enable **Google Analytics** (optional, for measurementId)
    - Go to **Project Settings** > **General** > **Your apps** > **Web app** (</> icon)
    - Copy your Firebase config values

    - Create `.env` file in the root directory:

    ```bash
    cp .env.example .env
    ```

    - Fill in your Firebase credentials in `.env`:

    ```env
    VITE_FIREBASE_API_KEY=your-api-key-here
    VITE_FIREBASE_AUTH_DOMAIN=your-project-id.firebaseapp.com
    VITE_FIREBASE_PROJECT_ID=your-project-id
    VITE_FIREBASE_STORAGE_BUCKET=your-project-id.appspot.com
    VITE_FIREBASE_MESSAGING_SENDER_ID=your-messaging-sender-id
    VITE_FIREBASE_APP_ID=your-app-id
    VITE_FIREBASE_MEASUREMENT_ID=your-measurement-id
    ```

    - Update `firebase.json` if your Firestore location differs from `eur3`:

    ```json
    {
        "firestore": {
            "location": "your-location" // e.g., "us-central1", "eur3"
        }
    }
    ```

    - Deploy Firestore rules and indexes (optional):

    ```bash
    # Login to Firebase CLI
    firebase login

    # Deploy Firestore rules
    firebase deploy --only firestore:rules

    # Deploy Firestore indexes
    firebase deploy --only firestore:indexes
    ```

3.  **Run Development Server:**

    ```bash
    npm run dev
    ```

    > Open <http://localhost:3000> to see the app.
    > Open <http://localhost:3000/dev/ui> to see the UI Playground.

4.  **Production Build:**

    ```bash
    npm run build
    ```

    > Generates optimized, compressed, and analyzed assets in `dist/`.

5.  **Deploy to Firebase Hosting:**
    ```bash
    npm run build
    firebase deploy --only hosting
    ```

### 📜 Available Scripts

| Command           | Description                          |
| ----------------- | ------------------------------------ |
| `npm run dev`     | Start Vite dev server                |
| `npm run build`   | Type-check & Build with Oxc + Brotli |
| `npm run preview` | Serve the production build locally   |
| `npm run lint`    | Run ESLint                           |
| `npm run format`  | Format codebase with Prettier        |
| `npm run test`    | Run Unit Tests (Vitest)              |

### 🔥 Firebase Integration

This template includes a simplified Firebase setup focused on Firestore and Analytics:

#### Features

- **Firestore**: Real-time database with direct export (`db` from `@/lib/firebase`)
- **Firebase Analytics**: Automatic initialization (if `measurementId` is provided)
- **Security Rules**: Pre-configured Firestore rules for `feedbacks` collection
- **Hosting**: Configured for Firebase Hosting with SPA routing

#### Configuration Files

- `firebase.json`: Firebase CLI configuration (hosting, firestore with location)
- `firestore.rules`: Security rules for Firestore (currently configured for `feedbacks` collection)
- `firestore.indexes.json`: Firestore indexes (empty by default, add as needed)
- `.env.example`: Template for environment variables

#### Current Firestore Rules

The template includes rules for a `feedbacks` collection(Example):

- ✅ Anyone can **create** feedback (no authentication required)
- ❌ Reading is **denied** (only admins via console can view)
- ❌ Update/Delete are **denied** (feedbacks are immutable)

> **Important**: Update `firestore.rules` to match your data model before deploying to production!

### 🤖 CI Pipeline

A GitHub Actions workflow (`.github/workflows/ci.yml`) runs on every Push/PR:

1.  Installs dependencies (cached).
2.  Runs **Linter**.
3.  Checks **Formatting**.
4.  Runs **Tests**.
