# Vite + React + Tailwind + Daisy UI Setup Guide

# Why Use TailwindCSS and DaisyUI Instead of Traditional CSS?

## 1. Traditional CSS is powerful, but slow for modern development
- CSS is the foundation of web styling, but as projects grow it becomes harder to manage.  
- Developers often end up with long stylesheets, repeated code, and confusing class names.  

**Example (Traditional CSS):**
```css
.btn {
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  background-color: blue;
  color: white;
}
```

# TailwindCSS makes styling faster

Tailwind provides utility classes that let us apply styles directly in HTML/JSX.

This eliminates the need to switch between files and avoids repetitive CSS rules.

Example (TailwindCSS):
```
<button class="px-4 py-2 rounded bg-blue-500 text-white">Click Me</button>
```

## DaisyUI makes components look professional instantly

DaisyUI builds on top of Tailwind and provides pre-designed, customizable components.

Components like buttons, cards, navbars, and modals look polished out of the box.

Example (DaisyUI):
```
<button class="btn btn-primary">Pay Now</button>
```


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
npm install -D tailwindcss@3 postcss autoprefixer
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

In this activity, we’ll create a **payment portal UI** using React, TailwindCSS, and DaisyUI. This one is extremely barebones and does not include any tailwind or daisy styling at all. App.jsx is fine as is for now. Focus on the **Index.html** and alter it based on your design preferences.
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

## HTML Code:
```
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Payment Portal</title>
  <link href="/src/style.css" rel="stylesheet">
</head>
<body class="min-h-screen bg-base-200 flex items-center justify-center">

  <div class="card w-96 bg-base-100 shadow-xl">
    <div class="card-body">
      <h2 class="card-title text-center">💳 Payment Portal</h2>
      <form class="form-control space-y-3" onsubmit="handleSubmit(event)">
        
        <input
          type="text"
          name="name"
          placeholder="Cardholder Name"
          class="input input-bordered w-full"
          id="name"
          required
        />

        <input
          type="text"
          name="cardNumber"
          placeholder="Card Number"
          class="input input-bordered w-full"
          id="cardNumber"
          required
        />

        <div class="flex space-x-2">
          <input
            type="text"
            name="expiry"
            placeholder="MM/YY"
            class="input input-bordered w-1/2"
            id="expiry"
            required
          />
          <input
            type="password"
            name="cvv"
            placeholder="CVV"
            class="input input-bordered w-1/2"
            id="cvv"
            required
          />
        </div>

        <button class="btn btn-primary mt-4" type="submit">Pay Now</button>
      </form>
    </div>
  </div>

  <script>
    function handleSubmit(event) {
      event.preventDefault();
      const name = document.getElementById("name").value;
      alert(`💸 Payment Submitted!\n\nName: ${name}`);
    }
  </script>
  
</body>
</html>
```

Now that you have seen the frontend with zero styling, lets take a look at our app with some Tailwind CSS and Daisy UI components:

```
<!doctype html>
<html lang="en" data-theme="light">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Payment Portal</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://cdn.jsdelivr.net/npm/daisyui@4.12.10/dist/full.min.css" rel="stylesheet" type="text/css" />
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
</head>
<body class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 flex items-center justify-center p-4">
  <div class="card w-full max-w-md bg-base-100 shadow-2xl border border-base-300">
    <div class="card-body p-8">
      <!-- Header -->
      <div class="text-center mb-6">
        <div class="avatar placeholder mb-4">
          <div class="bg-primary text-primary-content rounded-full w-16 h-16">
            <i class="fas fa-credit-card text-2xl"></i>
          </div>
        </div>
        <h2 class="card-title text-2xl font-bold text-center justify-center text-base-content">
          Secure Payment
        </h2>
        <p class="text-base-content/70 text-sm mt-2">Enter your payment details below</p>
      </div>

      <form class="space-y-4" onsubmit="handleSubmit(event)">
        <!-- Cardholder Name -->
        <div class="form-control">
          <label class="label">
            <span class="label-text font-medium">
              <i class="fas fa-user mr-2 text-primary"></i>Cardholder Name
            </span>
          </label>
          <input
            type="text"
            name="name"
            placeholder="John Doe"
            class="input input-bordered input-primary w-full focus:input-primary transition-all duration-200"
            id="name"
            required
          />
        </div>

        <!-- Card Number -->
        <div class="form-control">
          <label class="label">
            <span class="label-text font-medium">
              <i class="fas fa-credit-card mr-2 text-primary"></i>Card Number
            </span>
          </label>
          <input
            type="text"
            name="cardNumber"
            placeholder="1234 5678 9012 3456"
            class="input input-bordered input-primary w-full focus:input-primary transition-all duration-200"
            id="cardNumber"
            maxlength="19"
            required
          />
        </div>

        <!-- Expiry and CVV -->
        <div class="flex gap-4">
          <div class="form-control flex-1">
            <label class="label">
              <span class="label-text font-medium">
                <i class="fas fa-calendar mr-2 text-primary"></i>Expiry
              </span>
            </label>
            <input
              type="text"
              name="expiry"
              placeholder="MM/YY"
              class="input input-bordered input-primary w-full focus:input-primary transition-all duration-200"
              id="expiry"
              maxlength="5"
              required
            />
          </div>
          <div class="form-control flex-1">
            <label class="label">
              <span class="label-text font-medium">
                <i class="fas fa-lock mr-2 text-primary"></i>CVV
              </span>
            </label>
            <input
              type="password"
              name="cvv"
              placeholder="123"
              class="input input-bordered input-primary w-full focus:input-primary transition-all duration-200"
              id="cvv"
              maxlength="4"
              required
            />
          </div>
        </div>

        <!-- Security Badge -->
        <div class="alert alert-info bg-info/10 border-info/20">
          <i class="fas fa-shield-alt text-info"></i>
          <span class="text-sm">Your payment information is encrypted and secure</span>
        </div>

        <!-- Submit Button -->
        <button class="btn btn-primary w-full mt-6 text-lg font-semibold h-12 hover:scale-[1.02] transition-transform duration-200" type="submit">
          <i class="fas fa-lock mr-2"></i>
          Process Payment
        </button>
      </form>

      <!-- Footer -->
      <div class="text-center mt-6 pt-4 border-t border-base-300">
        <p class="text-xs text-base-content/60">
          <i class="fas fa-shield-alt mr-1"></i>
          Protected by 256-bit SSL encryption
        </p>
      </div>
    </div>
  </div>

  <script>
    // Format card number input
    document.getElementById('cardNumber').addEventListener('input', function(e) {
      let value = e.target.value.replace(/\s/g, '').replace(/[^0-9]/gi, '');
      let formattedValue = value.match(/.{1,4}/g)?.join(' ') || value;
      e.target.value = formattedValue;
    });

    // Format expiry input
    document.getElementById('expiry').addEventListener('input', function(e) {
      let value = e.target.value.replace(/\D/g, '');
      if (value.length >= 2) {
        value = value.substring(0,2) + '/' + value.substring(2,4);
      }
      e.target.value = value;
    });

    // CVV input restriction
    document.getElementById('cvv').addEventListener('input', function(e) {
      e.target.value = e.target.value.replace(/\D/g, '');
    });

    function handleSubmit(event) {
      event.preventDefault();
      const name = document.getElementById("name").value;
      const button = event.target.querySelector('button[type="submit"]');
      
      // Loading state
      button.innerHTML = '<i class="fas fa-spinner fa-spin mr-2"></i>Processing...';
      button.disabled = true;
      
      setTimeout(() => {
        // Success state
        button.innerHTML = '<i class="fas fa-check mr-2"></i>Payment Successful!';
        button.classList.remove('btn-primary');
        button.classList.add('btn-success');
        
        // Show success alert
        const alertHtml = `
          <div class="alert alert-success mt-4 animate-pulse">
            <i class="fas fa-check-circle"></i>
            <div>
              <h3 class="font-bold">Payment Successful!</h3>
              <div class="text-sm">Thank you, ${name}. Your payment has been processed.</div>
            </div>
          </div>
        `;
        
        const form = event.target;
        form.insertAdjacentHTML('afterend', alertHtml);
        
        // Reset after 3 seconds
        setTimeout(() => {
          button.innerHTML = '<i class="fas fa-lock mr-2"></i>Process Payment';
          button.classList.remove('btn-success');
          button.classList.add('btn-primary');
          button.disabled = false;
          const alert = document.querySelector('.alert-success');
          if (alert) alert.remove();
        }, 3000);
      }, 2000);
    }
  </script>
</body>
</html>
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
jsx
```
Copy code
<button className="btn btn-primary loading">Processing...</button>
```

### Run the development server:
```bash
npm run dev
```

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
