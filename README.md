# 📚 Bookify – University Library Management System

A modern, full-stack university library book borrowing platform built using **Next.js**, **Tailwind CSS**, **Drizzle ORM**, and powerful third-party integrations like **ImageKit** and **Upstash**.

---

## 🚀 Tech Stack

| Technology            | Role                                                                       |
| --------------------- | -------------------------------------------------------------------------- |
| **Next.js**           | React-based framework for routing, server-side rendering, and SSR          |
| **Tailwind CSS**      | Utility-first CSS framework for styling                                    |
| **shadcn/ui**         | Beautifully styled, accessible components using Tailwind                   |
| **Drizzle ORM**       | Type-safe, minimal ORM for PostgreSQL                                      |
| **Neon.tech**         | Serverless Postgres hosting                                                |
| **ImageKit.io**       | Image storage, optimization, and CDN delivery                              |
| **Upstash Redis**     | Real-time, low-latency cache and session management                        |
| **Upstash Workflows** | Serverless automation for multi-step tasks (emails, activity checks, etc.) |

---

## 🛠️ Day-by-Day Learning Notes

### 🔧 Project Setup

* **Install Prettier for code formatting**

  ```bash
  npm install --save-dev prettier
  ```
* **ESLint** comes bundled with Next.js. Configure `.eslintrc.js` as needed.

---

### 🎨 Styling with Tailwind & Fonts

* Installed and configured **Tailwind CSS** and **shadcn/ui** components.
* **Local fonts** added inside `/app/fonts`, using `next/font/local`.

<details>
<summary>📝 Tailwind Config & Font Setup</summary>

```tsx
// tailwind.config.ts
theme: {
  extend: {
    fontFamily: {
      bebas: ["var(--bebas-neue)"],
    },
    backgroundImage: {
      pattern: "url('/images/pattern.webp')",
    },
  }
}
```

```tsx
// layout.tsx

import localFont from "next/font/local";

const ibmPlexSans = localFont({
  src: [
    { path: '/fonts/IBMPlexSans-Regular.ttf', weight: '400', style: 'normal' },
    { path: '/fonts/IBMPlexSans-Medium.ttf', weight: '500', style: 'normal' },
    { path: '/fonts/IBMPlexSans-SemiBold.ttf', weight: '600', style: 'normal' },
    { path: '/fonts/IBMPlexSans-Bold.ttf', weight: '700', style: 'normal' },
  ],
});

const bebasNeue = localFont({
  src: [{ path: '/fonts/BebasNeue-Regular.ttf', weight: "400", style: "normal" }],
  variable: "--bebas-neue",
});
```

</details>

---

### 🧱 UI Library – shadcn/ui

* `shadcn/ui` for form elements, buttons, cards, etc.
* Customizable components, powered by Tailwind and Radix UI.

📎 [Installation Guide](https://ui.shadcn.com/docs/installation/next)

---

### 🗄️ Database & ORM

* **Drizzle ORM + Neon.tech** = effortless type-safe Postgres.
* `.env` stores DB credentials securely.
* Schema management directly in code.

---

### 📷 Image Management

* **ImageKit.io** used for storing & serving optimized book covers.
* Fallback image: `https://placehold.co/400x600.png`

---

### ⚡ Real-time Features with Upstash

<details>
<summary>🔄 Redis (Caching & Session Management)</summary>

* Low-latency access to user session or frequently-read book data.
* Perfect for managing real-time stats like "currently borrowed", etc.

</details>

<details>
<summary>📬 Workflows (Email & Automation)</summary>

* Automate onboarding flows, send reminders if users are inactive.
* Ideal for email verification, overdue notifications, etc.

</details>

---

### 🧼 Code Quality

* `Prettier` for formatting.
* `ESLint` for consistent code style.
* Type safety using **TypeScript interfaces**, e.g., in `/constants/index.ts`.

---

### 🧠 Helpful Patterns & Tricks

<details>
<summary>🔄 Highlight Active Nav using usePathname()</summary>

```tsx
import { usePathname } from "next/navigation";

const pathname = usePathname();
<Link href="/library" className={cn('text-base cursor-pointer capitalize', pathname === '/library' ? 'text-light-200' : 'text-light-100')}>
```

</details>

<details>
<summary>🧠 Utility Function: cn()</summary>

Utility function to conditionally join Tailwind class names.

```tsx
import { cn } from '@/lib/utils';
<Link href="/library" className={cn('text-base cursor-pointer capitalize', pathname === '/library' ? 'text-light-200' : 'text-light-100')}>
```

Used like:

```tsx
<div className={cn("base-class", isActive && "highlight")} />
```

</details>

<details>
<summary>🧩 Next.js Config for External Images</summary>

```ts
// next.config.ts
const nextConfig = {
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'placehold.co',
      },
      {
        protocol: 'https',
        hostname: 'm.media-amazon.com',
      },
    ],
  },
};

export default nextConfig;
```

</details>

---

### 🐞 Common Errors & Fixes

| Error Message                    | Solution                                                                             |
| -------------------------------- | ------------------------------------------------------------------------------------ |
| `Invalid src prop on next/image` | Add the domain to `images.remotePatterns` in `next.config.ts`                        |
| `JSX does not allow prop`        | Check if the component is correctly imported, e.g. `import Image from 'next/image';` |

---
