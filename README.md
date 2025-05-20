# TypeScript Node.js Project Setup Guide

This README provides a comprehensive guide for setting up a TypeScript Node.js project with proper linting, formatting, and development configurations.

## Installation Steps

### Prerequisites

- Node.js (v14 or higher)
- npm

### Step 1: Clone the repository

```bash
git clone <repository-url>
cd nodejs-typescript
```

### Step 2: Install dependencies

Using npm:

```bash
npm install
```

### Step 3: Set up environment variables

Create a `.env` file in the root directory with your configuration variables.

### Step 4: Run the development server

Using npm:

```bash
npm run dev
```

### Step 5: Build for production

When you're ready to deploy, build the project:

Using npm:

```bash
npm run build
```

### Step 6: Run in production mode

Using npm:

```bash
npm start
```

## Initial Setup

```bash
# Initialize project with package.json
npm init -y

# Install TypeScript as a development dependency
npm i typescript -D

# Add TypeScript types for Node.js
npm i @types/node -D

# Install development tools (linting, formatting, etc.)
npm install eslint prettier eslint-config-prettier eslint-plugin-prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser ts-node tsc-alias tsconfig-paths rimraf nodemon -D
```

## Configuration Files

### tsconfig.json

```json
{
  "compilerOptions": {
    "module": "CommonJS",
    "moduleResolution": "node",
    "target": "ES2020",
    "outDir": "dist",
    "esModuleInterop": true,
    "strict": true,
    "skipLibCheck": true,
    "baseUrl": ".",
    "paths": { "~/*": ["src/*"] }
  },
  "ts-node": { "require": ["tsconfig-paths/register"] },
  "files": ["src/type.d.ts"],
  "include": ["src/**/*"]
}
```

### .eslintrc

```json
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint", "prettier"],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "eslint-config-prettier",
    "prettier"
  ],
  "rules": {
    "@typescript-eslint/no-explicit-any": "off",
    "@typescript-eslint/no-unused-vars": "off",
    "prettier/prettier": [
      "warn",
      {
        "arrowParens": "always",
        "semi": false,
        "trailingComma": "none",
        "tabWidth": 2,
        "endOfLine": "auto",
        "useTabs": false,
        "singleQuote": true,
        "printWidth": 120,
        "jsxSingleQuote": true
      }
    ]
  }
}
```

### .eslintignore

```
node_modules/
dist/
```

### .prettierrc

```json
{
  "arrowParens": "always",
  "semi": false,
  "trailingComma": "none",
  "tabWidth": 2,
  "endOfLine": "auto",
  "useTabs": false,
  "singleQuote": true,
  "printWidth": 120,
  "jsxSingleQuote": true
}
```

### .prettierignore

```
node_modules/
dist/
```

### .editorconfig

```
indent_size = 2;
indent_style = space;
```

### .gitignore

Generate a comprehensive .gitignore file for Node.js projects from:
https://www.toptal.com/developers/gitignore

### nodemon.json

```json
{
  "watch": ["src"],
  "ext": ".ts,.js",
  "ignore": [],
  "exec": "npx ts-node ./src/index.ts"
}
```

## NPM Scripts

Add these scripts to your `package.json`:

```json
"scripts": {
  "dev": "npx nodemon",
  "build": "rimraf ./dist && tsc && tsc-alias",
  "start": "node dist/index.js",
  "lint": "eslint .",
  "lint:fix": "eslint . --fix",
  "prettier": "prettier --check .",
  "prettier:fix": "prettier --write ."
}
```

## Usage

- **Development**: Run `npm run dev` to start the development server with hot-reloading
- **Building**: Run `npm run build` to compile TypeScript to JavaScript in the dist folder
- **Production**: Run `npm start` to run the compiled JavaScript (must build first)
- **Linting**: Run `npm run lint` to check for linting errors or `npm run lint:fix` to automatically fix them
- **Formatting**: Run `npm run prettier` to check formatting or `npm run prettier:fix` to automatically fix formatting issues

## Project Structure

```
📦nodejs-typescript
┣ 📂dist                # Compiled output (generated)
┣ 📂src                 # Source code
┃ ┣ 📂constants         # Constants definitions
┃ ┃ ┣ 📜enum.ts         # Enumeration constants
┃ ┃ ┣ 📜httpStatus.ts   # HTTP status codes
┃ ┃ ┗ 📜message.ts      # Response messages
┃ ┣ 📂controllers       # Request handlers
┃ ┃ ┗ 📜users.controllers.ts
┃ ┣ 📂middlewares       # Middleware functions
┃ ┃ ┣ 📜error.middlewares.ts
┃ ┃ ┣ 📜file.middlewares.ts
┃ ┃ ┣ 📜users.middlewares.ts
┃ ┃ ┗ 📜validation.middlewares.ts
┃ ┣ 📂models            # Data models
┃ ┃ ┣ 📂database        # Database models
┃ ┃ ┃ ┣ 📜Blacklist.ts
┃ ┃ ┃ ┣ 📜Bookmark.ts
┃ ┃ ┃ ┣ 📜Follower.ts
┃ ┃ ┃ ┣ 📜Hashtag.ts
┃ ┃ ┃ ┣ 📜Like.ts
┃ ┃ ┃ ┣ 📜Media.ts
┃ ┃ ┃ ┣ 📜Tweet.ts
┃ ┃ ┃ ┗ 📜User.ts
┃ ┃ ┣ 📜Error.ts        # Error model
┃ ┃ ┗ 📜Success.ts      # Success model
┃ ┣ 📂routes            # API routes
┃ ┃ ┗ 📜users.routes.ts
┃ ┣ 📂services          # Business logic
┃ ┃ ┣ 📜bookmarks.services.ts
┃ ┃ ┣ 📜database.services.ts
┃ ┃ ┣ 📜followers.services.ts
┃ ┃ ┣ 📜hashtags.services.ts
┃ ┃ ┣ 📜likes.services.ts
┃ ┃ ┣ 📜medias.services.ts
┃ ┃ ┣ 📜tweets.services.ts
┃ ┃ ┗ 📜users.services.ts
┃ ┣ 📂utils             # Utility functions
┃ ┃ ┣ 📜crypto.ts       # Encryption utilities
┃ ┃ ┣ 📜email.ts        # Email utilities
┃ ┃ ┣ 📜file.ts         # File handling
┃ ┃ ┣ 📜helpers.ts      # Helper functions
┃ ┃ ┗ 📜jwt.ts          # JWT utilities
┃ ┣ 📜index.ts          # Application entry point
┃ ┗ 📜type.d.ts         # Global type declarations
┣ 📜.editorconfig       # Editor configuration
┣ 📜.env                # Environment variables
┣ 📜.eslintignore       # ESLint ignore patterns
┣ 📜.eslintrc           # ESLint configuration
┣ 📜.gitignore          # Git ignore patterns
┣ 📜.prettierignore     # Prettier ignore patterns
┣ 📜.prettierrc         # Prettier configuration
┣ 📜nodemon.json        # Nodemon configuration
┣ 📜package.json        # Project metadata and scripts
┣ 📜tsconfig.json       # TypeScript configuration
┗ 📜yarn.lock           # Yarn dependencies lock file
```

### Directory Explanations

- **dist**: Contains the compiled JavaScript files after build
- **src**: Contains all the source code
  - **constants**: Contains constant definitions like enumerations, HTTP status codes, and messages
  - **middlewares**: Contains middleware functions for validation, token checking, file handling, etc.
  - **controllers**: Contains request handlers that receive requests, call services, and return responses
  - **services**: Contains business logic and database operations
  - **models**: Contains data models for the application
    - **database**: Database model definitions
  - **routes**: API route definitions
  - **utils**: Utility functions for encryption, email sending, file handling, JWT, etc.
- Configuration files at the root (.eslintrc, .prettierrc, etc.) set up the development environment
