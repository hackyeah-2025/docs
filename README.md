# HackYeah 2025 – Full Setup Guide

## Project Name

Traveho

## Team Name

JustATeam

## Team Members

Piotr Bukowiec Walker91XD#7696
Sebastian Andre Coronado Chichiraky coronado03


## Tech Stack

### Backend

- **NestJS (TypeScript)**
- **TypeORM (Active Record)**
- **PostgreSQL**
- **Yarn package manager**
- **Node.js ≥ 24.9.0 (required)**

### Frontend

#### Frameworks

- **React** ([react](https://www.npmjs.com/package/react), [react-dom](https://www.npmjs.com/package/react-dom)) – frontend library for building user interfaces
- **Next.js** ([next](https://nextjs.org/)) – React framework for server-side rendering, routing, and full-stack apps

#### Styling and UI

- **Tailwind CSS** ([tailwindcss](https://tailwindcss.com/)) – utility-first CSS framework for styling
- **Tailwind CSS Animate** ([tailwindcss-animate](https://www.npmjs.com/package/tailwindcss-animate)) – animation utilities for Tailwind CSS
- **DaisyUI** ([daisyui](https://daisyui.com/)) – component library built on top of Tailwind CSS

#### Icons

- **Lucide React** ([lucide-react](https://www.npmjs.com/package/lucide-react)) – icon library for React

#### Security and Sanitization

- **Isomorphic DOMPurify** ([isomorphic-dompurify](https://www.npmjs.com/package/isomorphic-dompurify)) – sanitizes HTML to prevent XSS attacks (works on client and server)

#### Development Tools

- **TypeScript** ([typescript](https://www.typescriptlang.org/)) – strongly typed superset of JavaScript
- **ESLint** ([eslint](https://eslint.org/)), [@eslint/eslintrc](https://www.npmjs.com/package/@eslint/eslintrc), [eslint-config-next](https://www.npmjs.com/package/eslint-config-next) – code linter

#### Type Definitions

- [@types/node](https://www.npmjs.com/package/@types/node), [@types/react](https://www.npmjs.com/package/@types/react), [@types/react-dom](https://www.npmjs.com/package/@types/react-dom) – type definitions for TypeScript

#### Build and PostCSS Plugins

- [@tailwindcss/postcss](https://www.npmjs.com/package/@tailwindcss/postcss) – Tailwind CSS plugin for PostCSS

---

## System Requirements

### 🐧 Linux (Ubuntu/Debian)

```bash
sudo apt update && sudo apt install -y curl ca-certificates git postgresql postgresql-contrib python3 python3-venv python3-pip build-essential
```

### 🍎 macOS

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install git postgresql python3 node
brew services start postgresql
```

### 🪟 Windows

1. Install **[Git for Windows](https://git-scm.com/)**
2. Install **[Node.js ≥ 24.9.0 (LTS)](https://nodejs.org/)**
3. Install **[PostgreSQL](https://www.postgresql.org/download/windows/)**
4. Install **[Python 3](https://www.python.org/downloads/)**
5. Restart your system and open **PowerShell** or **Windows Terminal**

---

## PostgreSQL Setup

PostgreSQL must be **running locally** before you start the backend.

### Start PostgreSQL Service

#### Linux

```bash
sudo service postgresql start
```

#### macOS

```bash
brew services start postgresql
```

#### Windows

- PostgreSQL usually starts automatically as a Windows service.
- To check: open **Services**, find **postgresql-x64**, ensure it’s _Running_.

---

### Create User and Database

Run these commands to set up your local development environment.

#### Linux and macOS

```bash
sudo -u postgres psql
```

Inside `psql`:

```sql
CREATE USER postgres WITH PASSWORD 'postgres';
ALTER ROLE postgres WITH SUPERUSER;
CREATE DATABASE hackyeah_2025 OWNER postgres;
\q
```

#### Windows (via SQL Shell)

Open **SQL Shell (psql)** and run:

```sql
CREATE USER postgres WITH PASSWORD 'postgres';
ALTER ROLE postgres WITH SUPERUSER;
CREATE DATABASE hackyeah_2025 OWNER postgres;
\q
```

> ⚠️ If PostgreSQL fails to start or `psql` cannot connect, verify the service status and ensure `pg_hba.conf` allows `local` connections using `md5` authentication.

---

## Backend-Services (AI Module – FastAPI)

### All Systems

```bash
# create and activate virtual environment
python3 -m venv hackyeah_env
# linux/mac
source hackyeah_env/bin/activate
# windows
hackyeah_env\Scripts\activate

# install dependencies
pip install fastapi google-genai uvicorn

# clone repository
git clone https://github.com/hackyeah-2025/backend-services.git
cd backend-services

# run the service
uvicorn main:app --reload --host 0.0.0.0
```

To keep it running in the background:

```bash
nohup uvicorn main:app --reload --host 0.0.0.0 &
```

---

## Main Backend (NestJS + TypeORM + PostgreSQL)

### Step 1: Install Node ≥ 24.9.0 and Yarn

#### Linux and macOS

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
source ~/.bashrc
nvm install 24.9.0
nvm use 24.9.0
npm install -g yarn
```

#### Windows

Install Node.js ≥ 24.9.0 from [nodejs.org](https://nodejs.org/).  
Then run:

```powershell
npm install -g yarn
```

---

### Step 2: Clone and Configure Backend

```bash
git clone https://github.com/hackyeah-2025/backend.git
cd backend
cp .env.example .env
```

Edit `.env`:

```env
PORT=3001
DATABASE_HOST=127.0.0.1
DATABASE_PORT=5432
DATABASE_USER=postgres
DATABASE_PASSWORD=postgres
DATABASE_NAME=hackyeah_2025
JWT_SECRET=any_secret_string
```

---

### Step 3: Install Dependencies and Run Backend

```bash
yarn install
yarn start:dev
```

Backend should now be available at: [http://localhost:3001](http://localhost:3001)

> 💡 If you see `ECONNREFUSED` or `connection refused` errors, ensure PostgreSQL is running and accessible on port `5432`.

---

## Frontend (React + Next.js + Tailwind)

### Step 1: Install Dependencies

```bash
cd ../frontend
npm install
```

### Step 2: Configure API URL

Create a `.env.local` file:

```env
NEXT_PUBLIC_API_URL=http://localhost:3001
```

### Step 3: Start Development Server

```bash
npm run dev
```

Frontend will be available at: [http://localhost:3000](http://localhost:3000)

---

## Keeping the Backend Running

### Linux and macOS

```bash
nohup yarn start:dev &
```

### Windows

Use **pm2**:

```powershell
npm install -g pm2
pm2 start dist/main.js --name "hackyeah-backend"
```

---

## Verification

- **Backend:** [http://localhost:3001](http://localhost:3001)
- **AI Service:** [http://localhost:8000](http://localhost:8000)
- **Frontend:** [http://localhost:3000](http://localhost:3000)
- Ensure frontend requests successfully reach the backend (check logs).

---

## Final Checklist

1. Install Python, Node ≥ 24.9.0, Yarn, and PostgreSQL
2. Set up PostgreSQL user and database
3. Run **backend-services** (FastAPI module)
4. Run **main backend** (NestJS + PostgreSQL)
5. Run **frontend** (Next.js + React + Tailwind)
6. Verify all services communicate correctly
