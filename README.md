# Next.js with Supabase and i18n

<p align="center">
  A modern Next.js application template with Supabase authentication and database integration, plus internationalization (i18n) support for multilingual applications.
</p>

<p align="center">
  <a href="#features"><strong>Features</strong></a> ·
  <a href="#demo"><strong>Demo</strong></a> ·
  <a href="#getting-started"><strong>Getting Started</strong></a> ·
  <a href="#internationalization"><strong>Internationalization</strong></a> ·
  <a href="#supabase-integration"><strong>Supabase Integration</strong></a> ·
  <a href="#deployment"><strong>Deployment</strong></a>
</p>

## Features

- **Next.js App Router** - Modern React application architecture
- **Supabase Integration** - Authentication and database functionality
- **Internationalization (i18n)** - Support for multiple languages
- **Cookie-based Auth** - Secure authentication across the entire app
- **TypeScript** - Type safety for robust applications
- **Tailwind CSS** - Utility-first CSS framework
- **shadcn/ui** - High-quality UI components
- **Dark/Light Mode** - Theme switching with next-themes

## Demo

[Link to your deployed demo]

## Getting Started

### Prerequisites

- Node.js 18 or later
- npm, yarn, or pnpm

### Setup

1. **Clone the repository**

```bash
git clone https://github.com/yourusername/your-repo-name.git
cd your-repo-name
```

2. **Install dependencies**

```bash
npm install
# or
yarn
# or
pnpm install
```

3. **Set up Supabase**

- Create a [Supabase project](https://database.new)
- Copy your project URL and anon key from the [API settings](https://app.supabase.com/project/_/settings/api)
- Rename `.env.example` to `.env.local` and update:

```
NEXT_PUBLIC_SUPABASE_URL=[YOUR SUPABASE PROJECT URL]
NEXT_PUBLIC_SUPABASE_ANON_KEY=[YOUR SUPABASE PROJECT API ANON KEY]
```

4. **Run the development server**

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

The application will be available at [http://localhost:3000](http://localhost:3000).

## Internationalization

This template includes a robust internationalization (i18n) setup that supports multiple languages and automatic language detection.

### Supported Languages

Currently, the application supports:
- Arabic (ar) - Default
- English (en)

### How It Works

1. **Language Detection**:
   - The middleware automatically detects the user's preferred language based on browser settings
   - Redirects to the appropriate language path (e.g., `/en/dashboard` or `/ar/dashboard`)

2. **Dictionary System**:
   - Translations are stored in JSON files in the `dictionaries` directory
   - Each language has its own dictionary file (e.g., `en.json`, `ar.json`)

3. **Adding Translations**:
   - Update the dictionary files with your translation keys and values
   - Import and use the dictionary in your components

### Adding a New Language

1. Add the language code to the `locales` array in `i18n-config.ts`:

```typescript
export const i18n = {
  defaultLocale: "ar",
  locales: ["ar", "en", "fr"], // Added French (fr)
} as const;
```

2. Create a new dictionary file in the `dictionaries` directory:

```json
// dictionaries/fr.json
{
  "server-component": {
    "welcome": "Bienvenue"
  },
  "counter": {
    "increment": "Augmenter",
    "decrement": "Diminuer"
  }
}
```

3. Add the dictionary to `get-dictionary.ts`:

```typescript
const dictionaries = {
  ar: () => import("./dictionaries/ar.json").then((module) => module.default),
  en: () => import("./dictionaries/en.json").then((module) => module.default),
  fr: () => import("./dictionaries/fr.json").then((module) => module.default), // Added French
};
```

### Usage in Components

```tsx
// In a page component
import { getDictionary } from "@/get-dictionary";

export default async function Page({ params: { lang } }) {
  const dict = await getDictionary(lang);
  
  return (
    <div>
      <h1>{dict.server-component.welcome}</h1>
    </div>
  );
}
```

## Supabase Integration

This template uses Supabase for authentication and database functionality.

### Authentication

The template includes:
- Cookie-based authentication
- Auth middleware for protected routes
- Auth components for sign-in, sign-up, and sign-out

### Database Access

To access Supabase from your components:

```tsx
// Server Component
import { createServerClient } from '@/utils/supabase/server';

export default async function ServerComponent() {
  const supabase = createServerClient();
  const { data } = await supabase.from('your_table').select();
  
  return <div>{/* Render your data */}</div>;
}

// Client Component
import { createBrowserClient } from '@/utils/supabase/client';

export default function ClientComponent() {
  const supabase = createBrowserClient();
  
  const handleClick = async () => {
    const { data } = await supabase.from('your_table').select();
    // Process data
  };
  
  return <button onClick={handleClick}>Load Data</button>;
}
```

## Deployment

### Deploy to Vercel

The easiest way to deploy is with Vercel:

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fyourusername%2Fyour-repo-name)

Vercel's Supabase integration will guide you through creating a Supabase account and project, automatically assigning all the required environment variables.

### Environment Variables for Production

Make sure to set these environment variables in your deployment platform:

```
NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-supabase-anon-key
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

[Your chosen license]
