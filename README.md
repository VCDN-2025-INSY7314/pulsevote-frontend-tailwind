# Vite + React + Tailwind + Daisy UI Setup Guide

## Method 1: Start Fresh with Vite

### Step 1: Create New Vite Project
```bash
# Create new Vite project with React
npm create vite@latest my-react-app -- --template react
```
# Navigate to project
```
cd my-react-app
```
# Install dependencies
```
npm install
```

### Step 2: Install Tailwind CSS
Install Tailwind CSS and its peer dependencies
```bash
npm install -D tailwindcss postcss autoprefixer
```

# Generate Tailwind config files
```
npx tailwindcss init -p
```

### Step 3: Configure Tailwind CSS
Edit `tailwind.config.js`:
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

### Step 4: Install Daisy UI
# Install Daisy UI
```bash
npm install -D daisyui@latest
```

Update `tailwind.config.js` to include Daisy UI:
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [require("daisyui")],
  
  // Optional: Configure Daisy UI
  daisyui: {
    themes: ["light", "dark", "cupcake", "cyberpunk"],
  },
}
```

### Step 5: Add Tailwind Directives
Replace the content of `src/index.css`:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Step 6: Update Vite Config (Optional Optimizations)
Edit `vite.config.js`:
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
    open: true
  },
  build: {
    outDir: 'dist',
    sourcemap: true
  }
})
```

## Method 2: Manual Vite Config Creation

If you don't have a `vite.config.js` file, create one:

### Create `vite.config.js` in your project root:
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
    open: true,
    host: true
  },
  build: {
    outDir: 'dist',
    sourcemap: true,
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
        },
      },
    },
  },
  css: {
    postcss: './postcss.config.js',
  },
})
```

### Create `postcss.config.js`:
```js
export default {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

## Method 3: Complete Package.json Setup

Ensure your `package.json` has the correct scripts and dependencies:

```json
{
  "name": "my-react-app",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "@types/react": "^18.2.43",
    "@types/react-dom": "^18.2.17",
    "@vitejs/plugin-react": "^4.2.1",
    "autoprefixer": "^10.4.16",
    "daisyui": "^4.4.19",
    "eslint": "^8.55.0",
    "eslint-plugin-react": "^7.33.2",
    "eslint-plugin-react-hooks": "^4.6.0",
    "eslint-plugin-react-refresh": "^0.4.5",
    "postcss": "^8.4.32",
    "tailwindcss": "^3.3.6",
    "vite": "^5.0.8"
  }
}
```

## Testing Your Setup

### Create a test component in `src/App.jsx`:
```jsx
import { useState } from 'react'

function App() {
  const [count, setCount] = useState(0)

  return (
    <div className="min-h-screen bg-base-200 flex items-center justify-center">
      <div className="card w-96 bg-base-100 shadow-xl">
        <div className="card-body items-center text-center">
          <h2 className="card-title">Vite + React + Tailwind + Daisy UI</h2>
          <p className="py-4">Count: {count}</p>
          <div className="card-actions">
            <button 
              className="btn btn-primary"
              onClick={() => setCount(count + 1)}
            >
              Increment
            </button>
            <button 
              className="btn btn-secondary"
              onClick={() => setCount(0)}
            >
              Reset
            </button>
          </div>
        </div>
      </div>
    </div>
  )
}

export default App
```

# Class Activity:
# 💳 Activity: Build a Simple Payment Portal

In this activity, we’ll create a **payment portal UI** using React, TailwindCSS, and DaisyUI.  
⚠️ This is **frontend only** — it won’t actually process payments.

---

## Step 1: Replace `App.jsx`

Open `src/App.jsx` and paste this code:

```jsx
import { useState } from "react";

function App() {
  const [formData, setFormData] = useState({
    name: "",
    cardNumber: "",
    expiry: "",
    cvv: "",
  });

  const handleChange = (e) => {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`💸 Payment Submitted!\n\nName: ${formData.name}`);
  };

  return (
    <div className="min-h-screen bg-base-200 flex items-center justify-center">
      <div className="card w-96 bg-base-100 shadow-xl">
        <div className="card-body">
          <h2 className="card-title text-center">💳 Payment Portal</h2>
          <form onSubmit={handleSubmit} className="form-control space-y-3">
            
            <input
              type="text"
              name="name"
              placeholder="Cardholder Name"
              className="input input-bordered w-full"
              value={formData.name}
              onChange={handleChange}
              required
            />

            <input
              type="text"
              name="cardNumber"
              placeholder="Card Number"
              className="input input-bordered w-full"
              value={formData.cardNumber}
              onChange={handleChange}
              required
            />

            <div className="flex space-x-2">
              <input
                type="text"
                name="expiry"
                placeholder="MM/YY"
                className="input input-bordered w-1/2"
                value={formData.expiry}
                onChange={handleChange}
                required
              />
              <input
                type="password"
                name="cvv"
                placeholder="CVV"
                className="input input-bordered w-1/2"
                value={formData.cvv}
                onChange={handleChange}
                required
              />
            </div>

            <button className="btn btn-primary mt-4">Pay Now</button>
          </form>
        </div>
      </div>
    </div>
  );
}

export default App;
```
## Step 2: Experiment 🎨
Change the card theme by adding bg-primary text-primary-content to the card div.

Add a select dropdown for payment method:

jsx
```
<select className="select select-bordered w-full">
  <option disabled selected>Select Payment Method</option>
  <option>Visa</option>
  <option>MasterCard</option>
  <option>PayPal</option>
</select>
```
Add a loading state to the button:

jsx```
Copy code
<button className="btn btn-primary loading">Processing...</button>
```

### Run the development server:
```bash
npm run dev

## Troubleshooting Common Issues

### Issue 1: "vite.config.js not found"
**Solution**: Make sure you're in the correct directory and the file exists. Create it manually using Method 2 above.

### Issue 2: Tailwind styles not working
**Solution**: 
- Check that `@tailwind` directives are in `src/index.css`
- Verify `tailwind.config.js` content paths include your source files
- Restart the dev server after config changes

### Issue 3: Daisy UI components not styled
**Solution**:
- Ensure `daisyui` is in the plugins array in `tailwind.config.js`
- Check that you're using correct Daisy UI class names
- Verify PostCSS is processing Tailwind correctly

### Issue 4: Module resolution errors
**Solution**:
- Make sure `"type": "module"` is in your `package.json`
- Use ES6 import/export syntax consistently
- Check that all dependencies are properly installed

### Issue 5: Development server won't start
**Solution**:
- Delete `node_modules` and `package-lock.json`
- Run `npm install` again
- Check for port conflicts (try changing port in vite.config.js)

## Quick Commands Summary

```bash
# Create project
npm create vite@latest my-app -- --template react
cd my-app

# Install everything
npm install
npm install -D tailwindcss postcss autoprefixer daisyui

# Generate configs
npx tailwindcss init -p

# Start development
npm run dev
```

## Alternative: Using the Vite Template

There are community templates that include this entire stack:

```bash
npm create vite@latest my-app -- --template react-tailwind-daisyui
```

Or search for templates:
```bash
npm create vite@latest my-app -- --template
```
# Then select from available templates
