# How I Got Started (Work in Progress)
## Frontend
```bash
# Create the project
npm create vite@latest frontend-tutorial -- --template vue-ts
cd frontend-tutorial
# Install dependencies
npm install
# Start the development server
npm run dev
```

## Backend
```bash
# Create the backend folder
mkdir backend-tutorial
cd backend-tutorial
npm init -y
# Install dependencies
npm install express
npm install -D typescript ts-node-dev @types/node @types/express
# Initialize TypeScript
npx tsx --init
```

* In `tsconfig.json`, set `"outDir": "./dist"` and `"rootDir": "./src"`

```bash
# Create the source folder and entry file
mkdir src
touch src/index.ts
```

* Edit src/index.ts
```javascript
import express from 'express';

const app = express();
const port = 3000;

app.get('/', (_req, res) => {
  res.send('Hello from Express + TypeScript!');
});

app.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});
```

* Add a dev script to package.json
```json
{
  // ...existing code...
  "scripts": {
    "dev": "ts-node-dev --respawn src/index.ts"
  }
  // ...existing code...
}
```

* Start the backend
```bash
npm run dev
```

### Allow CORS in Backend
```bash
npm install cors
npm install -D @types/cors
```

* Update src/index.ts to use CORS
```javascript
import express from 'express';
import cors from 'cors';

const app = express();
const port = 3000;

app.use(cors()); // Allow all origins

app.get('/', (_req, res) => {
  res.send('Hello from Express + TypeScript!');
});
```

## Fetch Data from the Backend in Vue
* In your Vue component (e.g., src/components/HelloWorld.vue), add a method to fetch data from the backend:
```vue
<script lang="ts" setup>
import { ref, onMounted } from 'vue';

const message = ref('Loading...');

onMounted(async () => {
  const res = await fetch('http://localhost:3000/');
  message.value = await res.text();
});
</script>

<template>
  <div>
    <h1>{{ message }}</h1>
  </div>
</template>
```

# Run Both Servers
* In the root of each of the two projects, run `npm run dev`
