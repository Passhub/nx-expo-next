# Nx-Next-Expo

<a alt="Nx logo" href="https://nx.dev" target="_blank" rel="noreferrer"><img src="https://raw.githubusercontent.com/nrwl/nx/master/images/nx-logo.png" width="45"></a>

✨ A monorepo setup with **Next.js + Tailwind** (Web) and **Expo** (Mobile) using `Nx` ✨.

## 🔧 Technical Stack

- **Node.js**: v22.x
- **React Native**: v0.76.x
- **Expo**: Latest compatible with RN 0.76
- **Next.js**: v14.x
- **ESLint**: v9.x with eslint-config-next (using higher version for compatibility)
- **TypeScript**: Latest stable
- **Nx**: Latest stable

## ⚠️ Important Notes

- This setup uses a higher version of `eslint-config-next` for compatibility with ESLint v9
- The project is configured to work with Node.js v22, which might require specific configurations for some tools
- React Native 0.76 is used as the base for mobile development

## 🚀 Features

- **Monorepo with Nx** – Manage web and mobile apps in a single repository.
- **Next.js + Tailwind** – Optimized frontend for web.
- **Expo** – Smooth mobile development experience with React Native.
- **Shared Code** – Easily share utilities, components, and logic between web and mobile.
- **TypeScript Support** – Fully typed for a better developer experience.

## 📂 Project Structure

```
nx-next-expo
│── apps/
│   ├── mobile/  # Expo (React Native App)
│   ├── web/     # Next.js + Tailwind (Web App)
│── packages/    # Shared packages and utilities
│── tools/       # Build and compatibility scripts
│── .nx/         # Nx cache and metadata
│── .vscode/     # VS Code settings
│── nx.json      # Nx workspace configuration
│── package.json # Monorepo dependencies
│── tsconfig.base.json # TypeScript configuration
│── README.md    # This file
```

---

## 📦 Installation

### Prerequisites

- Node.js v22.x
- npm or yarn
- iOS/Android development environment for mobile development

### 1️⃣ Clone the repository

```sh
git clone https://github.com/your-repo/nx-next-expo.git
cd nx-next-expo
```

### 2️⃣ Install dependencies

```sh
npm install
```

### 3️⃣ Reset Nx Cache (Recommended)

```sh
nx reset
```

### 4️⃣ Environment Setup

Make sure your development environment is properly configured:

- For iOS development: XCode and CocoaPods installed
- For Android development: Android Studio, JDK, and Android SDK
- For web development: Some browser required

---

## 🚀 Running Projects

### 📱 **Start Expo (Mobile App)**

```sh
nx start mobile
```

or, if you prefer to use Expo CLI:

```sh
npx expo start
```

### 🌐 **Start Next.js (Web App)**

```sh
nx dev web
```

### 🔁 **Run both apps in parallel**

```sh
npm run start
```

---

## 🛠️ Building & Testing

### 📦 **Build Next.js**

```sh
nx build web
```

### 📦 **Build Expo**

```sh
nx build mobile
```

### 🧪 **Running Tests**

```sh
nx test web
nx test mobile
```

---

## 📦 Adding New Projects

### ➕ **Create a new Next.js app**

```sh
nx g @nx/next:app apps/new-web
```

### ➕ **Create a new Expo app**

```sh
nx g @nx/expo:app apps/new-mobile
```

### 🔄 **Create a shared package (library)**

```sh
nx g @nx/js:lib shared-utils
```

---

## ⚙️ Configuration Details

### ESLint Configuration

The project uses ESLint v9 with a higher version of `eslint-config-next` for compatibility. This setup ensures:

- Proper linting for both Next.js and React Native code
- Consistent code style across the monorepo
- TypeScript support and type checking

### Metro Bundler Configuration

#### 📁 `tools/scripts/eas-build-post-install.mjs`

This script patches the `@nx/expo` package for compatibility with EAS Build (Expo Application Services).

### How it works:

- Runs **after installing dependencies** in the Expo project
- Creates a **symlink** from project's `node_modules` to workspace root
- Ensures **Metro bundler can find shared dependencies**

```js
import { symlink, existsSync } from 'fs';
import { join } from 'path';

const [workspaceRoot, projectRoot] = process.argv.slice(2);

if (existsSync(join(workspaceRoot, 'node_modules'))) {
  console.log('Symlink already exists');
  process.exit(0);
}

symlink(join(projectRoot, 'node_modules'), join(workspaceRoot, 'node_modules'), 'dir', (err) => {
  if (err) console.log(err);
  else {
    console.log('Symlink created');
  }
});
```

💡 **Why do we need this?**

- When using `Nx` with `Expo`, `node_modules` is usually at the monorepo root
- Expo's bundler **expects dependencies inside the app's folder**
- This script **creates a symbolic link** to ensure proper module resolution

### Node.js Version Notes

The project is configured for Node.js v22.x, which may require:

- Specific Metro bundler configurations for React Native
- Updated Babel settings
- Modified TypeScript configurations

---

## 🔗 Useful Links

- [Nx Documentation](https://nx.dev)
- [Next.js Documentation](https://nextjs.org/docs)
- [Expo Documentation](https://docs.expo.dev)
- [React Native 0.76 Documentation](https://reactnative.dev/docs/0.76/getting-started)
- [TailwindCSS Documentation](https://tailwindcss.com/docs)
- [Node.js v22 Documentation](https://nodejs.org/docs/latest-v22.x/api/)
- [ESLint Documentation](https://eslint.org/docs/latest/)

---

## ⭐ Contributing

If you'd like to contribute, feel free to fork the repo and submit a PR!

---

## 📜 License

This project is licensed under the MIT License.
