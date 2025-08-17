# Importing a Font in Next.js

This guide explains how to properly add and use the **Press Start 2P** Google Font in a Next.js project with Tailwind CSS.

## 1. Import the Font

In your project, import the font from `next/font/google`:

```javascript
import { Press_Start_2P } from "next/font/google";
```

## 2. Create a Font Variable

Define the font with its configuration:

```javascript
const pressStart = Press_Start_2P({
  subsets: ["latin"],
  weight: "400",
  display: "swap",
  variable: "--font-press-start",
});
```

## 3. Add the Font to the Root Layout

Update your `RootLayout` component:

```javascript
return (
  <html lang="en" className={pressStart.variable}>
    <body>{children}</body>
  </html>
);
```

## 4. Update `globals.css`

Inside your `globals.css`, add the font variable under the `@theme inline` directive:

```css
@theme inline {
  --font-press-start: var(--font-press-start);
}
```

## 5. Use the Font in Your Pages

You can now apply the font anywhere in your project using Tailwind’s `font-press-start` class:

```jsx
<h1 className="font-press-start">Hello</h1>
```
