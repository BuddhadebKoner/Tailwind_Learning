### 1. **Directory Structure**

Start by setting up your project directory like this:

```
telwindTest/
│
├── src/
│   ├── input.css          // Tailwind CSS input file
│   └── output.css         // Tailwind CSS output file (generated after build)
│
├── index.html             // HTML test page
├── package.json           // Node.js project configuration
├── tailwind.config.js     // Tailwind configuration
└── postcss.config.js      // PostCSS configuration
```

---

### 2. **File Setup**

#### a. **Initialize Node.js Project**
Start by creating a Node.js project in your root directory:

```bash
npm init -y
```

This will generate a `package.json` file.

#### b. **Install Tailwind and Dependencies**

Install Tailwind CSS and its required dependencies:

```bash
npm install -D tailwindcss postcss autoprefixer
```

#### c. **Configure Tailwind**

Generate the `tailwind.config.js` file:

```bash
npx tailwindcss init
```

Your project’s `tailwind.config.js` should look like this:

```js
module.exports = {
  content: ["./src/**/*.{html,js}", "./index.html"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

This ensures that Tailwind CSS scans both the `index.html` and files in the `src` directory for classes.

#### d. **Create Input and Output CSS Files**

- Create `src/input.css` and add the following Tailwind directives:

  ```css
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
  ```

- The `src/output.css` file will be generated automatically when you build the CSS.

#### e. **Create PostCSS Configuration**

Create a `postcss.config.js` file in the root directory:

```bash
touch postcss.config.js
```

Inside, add the following configuration:

```js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

---

### 3. **Setting Up `package.json` Scripts**

In `package.json`, add a script to build Tailwind CSS:

```json
"scripts": {
  "build:css": "npx tailwindcss -i ./src/input.css -o ./src/output.css --watch"
}
```

This script tells Tailwind to take `input.css` as the input, generate `output.css`, and watch for changes.

---

### 4. **Test HTML Page**

Create an `index.html` file in the root directory with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tailwind Test</title>
  <link rel="stylesheet" href="./src/output.css">
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen">
  <div class="bg-white p-8 rounded-lg shadow-lg">
    <h1 class="text-3xl font-bold text-center mb-4">Hello, Tailwind!</h1>
    <p class="text-gray-700 text-center">This is a test project to see if Tailwind is working properly.</p>
  </div>
</body>
</html>
```

This page uses basic Tailwind classes to test if everything is working properly.

---

### 5. **Build and Watch Tailwind CSS**

Now, build and watch the Tailwind CSS file by running the following command:

```bash
npm run build:css
```

This command will:
- Process the `src/input.css` file.
- Output the generated CSS to `src/output.css`.
- Automatically rebuild the CSS when any changes are detected in the source files.

---

### 6. **Verify the Output**

Once the build is successful:
- Open `index.html` in a browser.
- You should see a styled page with a centered card that contains the text "Hello, Tailwind!".
  
If Tailwind is properly configured, the styles will be applied as expected.

---

### Troubleshooting:

- **No utility classes detected**: If you get the warning `No utility classes were detected`, check that:
  - Your `content` option in `tailwind.config.js` points to all relevant files (`index.html`, `src/**/*.{html,js}`).
  - You're using Tailwind CSS utility classes like `bg-gray-100`, `text-center`, etc., in your HTML.
  
- **File paths**: Double-check that the file paths in the `build:css` script and the HTML `<link>` tag are correct.

---

### Example Commands Recap:
1. Install Tailwind CSS:
   ```bash
   npm install -D tailwindcss postcss autoprefixer
   ```

2. Build Tailwind CSS and watch for changes:
   ```bash
   npm run build:css
   ```