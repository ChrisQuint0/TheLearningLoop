## **How to Install Tailwind and DaisyUI**

> ⚠️ Make sure you have installed Node.js

## **Step 0: In your project root, Initialize it as a new Node.js project**

```bash
mkdir my_project # Making the directory of your project
cd my_project #Going inside the directory of your project
npm init -y
```

---

## **Step 1: Install Tailwind CSS with PostCSS**

```bash
npm install -D tailwindcss @tailwindcss/postcss postcss autoprefixer postcss-cli
```

- `tailwindcss` → the framework
- `@tailwindcss/postcss` → Tailwind plugin for PostCSS v4
- `postcss` → PostCSS processor
- `autoprefixer` → adds browser prefixes
- `postcss-cli` → lets you run PostCSS from the terminal

---

## **Step 2: Create PostCSS configuration**

Create `postcss.config.cjs` in your project root and paste this:

```js
module.exports = {
  plugins: {
    "@tailwindcss/postcss": {},
  },
};
```

---

## **Step 3: Create your CSS input file**

```bash
mkdir src
#Then create an input.css inside this directory
```

Add Tailwind import to `src/input.css`:

```css
@import "tailwindcss";
```

---

## **Step 4: Inside src create index.html**

Add a simple HTML template in index.html:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Tailwind CSS v4</title>
    <link rel="stylesheet" href="output.css" />
  </head>
  <body class="bg-gray-100 text-gray-900">
    <h1 class="text-4xl font-bold text-center py-8">Hello Tailwind v4</h1>
  </body>
</html>
```

---

## **Step 5: Compile your CSS**

Add scripts to `package.json`:

You will see that there is already a scripts portion of the json just like this:

```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
}
```

Just add into it. It should look like this.

```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build:css": "postcss src/input.css -o src/output.css",
    "watch:css": "postcss src/input.css -o src/output.css --watch"
},
```

Run these commands in command prompt to compile the CSS:

```bash
npm run build:css   # for one-time compilation
npm run watch:css   # for automatic update, just like in the live server extenstion of VSCode
```

## **How to Install DaisyUI**

### **1. Install daisyUI**

```bash
npm install daisyui
```

---

### **2. Update your input CSS**

`src/input.css`:

```css
@import "tailwindcss";
@plugin "daisyui";
```

> `@plugin "daisyui";` is **required in v4** to enable all daisyUI components in the compiled CSS.

---

### **3. Compile CSS**

```bash
npm run build:css
```
