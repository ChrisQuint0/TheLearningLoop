# Next.js Fullstack Project Setup Guide and Other Things
By Christopher A. Quinto

This guide walks you through setting up a fullstack Next.js project with Tailwind CSS, shadcn/ui, Supabase, Framer Motion, Gemini AI, dark mode support, and toast notifications using Sonner.

---

## Installation

### Step 1: Install Node.js

1. Go to the [Node.js website](https://nodejs.org/).
2. Download the Windows installer (.msi).
3. Run the installer and follow the setup wizard.
4. Confirm installation by running:

```bash
node -v
npm -v
```

---

## Creating a Next.js + Tailwind Project

```bash
npx create-next-app@latest my-project
```

- Replace `my-project` with the name of your project.
- Choose "Yes" for all options except "Import alias customization".

### Start the development server

```bash
cd my-project
npm run dev
```

Visit [http://localhost:3000](http://localhost:3000) in your browser.

---

## shadcn/ui Initialization

Initialize shadcn:

```bash
npx shadcn@latest init
```

- Pick any base color when prompted.

Add a component (example: button):

```bash
npx shadcn@latest add button
```

---

## Supabase Setup

### Install Supabase packages

```bash
npm install @supabase/supabase-js
npm install @supabase/auth-helpers-nextjs
npm install @supabase/auth-helpers-react
```

### Add environment variables

Create a `.env.local` file in the project root:

```
NEXT_PUBLIC_SUPABASE_URL=your-database-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```

### Create the Supabase client

In `lib/supabase.ts`:

```ts
import { createPagesBrowserClient } from "@supabase/auth-helpers-nextjs";

export const supabase = createPagesBrowserClient();
```

---

## Session Provider Setup

In `app/providers.tsx`:

```tsx
"use client";

import { createPagesBrowserClient } from "@supabase/auth-helpers-nextjs";
import { SessionContextProvider } from "@supabase/auth-helpers-react";
import { useState } from "react";

export function Providers({ children }: { children: React.ReactNode }) {
  const [supabaseClient] = useState(() => createPagesBrowserClient());

  return (
    <SessionContextProvider supabaseClient={supabaseClient}>
      {children}
    </SessionContextProvider>
  );
}
```

Update `app/layout.tsx` to wrap `children` with `Providers`:

```tsx
import { Providers } from "./providers";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>
        <Providers>{children}</Providers>
      </body>
    </html>
  );
}
```

---

## Testing Supabase Connection

In `app/page.tsx`:

```tsx
import { supabase } from "@/lib/supabase";
import { useEffect } from "react";

export default function Home() {
  useEffect(() => {
    const testConnection = async () => {
      const { data, error } = await supabase.from("test").select();
      console.log(data, error);
    };

    testConnection();
  }, []);

  return <div>Home</div>;
}
```

Ensure a table named `test` exists in your Supabase database with:

- `id` (int8, primary key)
- `created_at` (timestamptz)

---

## Framer Motion Installation

```bash
npm install framer-motion
```

---

## Gemini API Integration

### 1. Get an API Key

Go to [Google AI Studio](https://makersuite.google.com/app) and generate an API key.

### 2. Install the SDK

```bash
npm install @google/generative-ai
```

### 3. Create the route

In `app/api/gemini/route.ts`:

```ts
import { GoogleGenerativeAI } from "@google/generative-ai";
import { NextResponse } from "next/server";

export async function POST(request: Request) {
  const { prompt } = await request.json();

  if (!prompt) {
    return NextResponse.json({ error: "Prompt is required" }, { status: 400 });
  }

  const apiKey = process.env.GEMINI_API_KEY;

  if (!apiKey) {
    console.error("GEMINI_API_KEY is not set in environment variables");
    return NextResponse.json(
      { error: "Environment variable not set" },
      { status: 500 }
    );
  }

  const genAI = new GoogleGenerativeAI(apiKey);

  try {
    const model = genAI.getGenerativeModel({ model: "gemini-2.5-pro" });
    const result = await model.generateContent(prompt);
    const response = await result.response;
    const text = response.text();

    return NextResponse.json({ generatedText: text }, { status: 200 });
  } catch (error) {
    console.error("Gemini API error:", error);
    return NextResponse.json(
      { error: "An API error occurred" },
      { status: 500 }
    );
  }
}
```

---

## Dark Mode with next-themes

### Install

```bash
npm install next-themes
```

### Setup in layout

Import:

```tsx
import { ThemeProvider } from "next-themes";
```

Update `app/layout.tsx`:

- Add `suppressHydrationWarning` to the `<html>` tag.
- Wrap `Providers` with `ThemeProvider`.

```tsx
<ThemeProvider attribute="class" defaultTheme="system" enableSystem>
  <Providers>{children}</Providers>
</ThemeProvider>
```

---

## Add Theme Toggle with shadcn Dropdown Menu

### Add dropdown component

```bash
npx shadcn@latest add dropdown-menu
```

### Example toggle

```tsx
import { Moon, Sun } from "lucide-react";
import { useTheme } from "next-themes";
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu";
import { Button } from "@/components/ui/button";

const { setTheme } = useTheme();

<DropdownMenu>
  <DropdownMenuTrigger asChild>
    <Button variant="outline" size="icon">
      <Sun className="h-[1.2rem] w-[1.2rem] transition-all dark:scale-0 dark:-rotate-90" />
      <Moon className="absolute h-[1.2rem] w-[1.2rem] scale-0 rotate-90 transition-all dark:scale-100 dark:rotate-0" />
      <span className="sr-only">Toggle theme</span>
    </Button>
  </DropdownMenuTrigger>
  <DropdownMenuContent align="end">
    <DropdownMenuItem onClick={() => setTheme("light")}>Light</DropdownMenuItem>
    <DropdownMenuItem onClick={() => setTheme("dark")}>Dark</DropdownMenuItem>
    <DropdownMenuItem onClick={() => setTheme("system")}>
      System
    </DropdownMenuItem>
  </DropdownMenuContent>
</DropdownMenu>;
```

---

## Toast Notifications with Sonner

### Add Sonner component

Make sure you installed Sonner from shadcn:

```bash
npx shadcn@latest add sonner
```

In `app/layout.tsx`:

```tsx
import { Toaster } from "@/components/ui/sonner";

<body>
  <ThemeProvider attribute="class" defaultTheme="system" enableSystem>
    <Providers>{children}</Providers>
    <Toaster position="top-center" richColors />
  </ThemeProvider>
</body>;
```

### Use toast in pages

```tsx
import { toast } from "sonner";

toast.success("Success");
toast.error("Something went wrong");
toast.warning("Be careful");
toast.info("Just so you know");
```

---

This setup provides a fully integrated stack with modern UI, authentication, database access, animations, AI features, dark mode, and user feedback components—all ready to build your app.
