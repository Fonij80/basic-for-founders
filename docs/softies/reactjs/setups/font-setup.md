# Font setup

## Persian fornts

1- install

```bash
npm install @fontsource/vazirmatn
```

2- import below packages to the first line of index.css:

```css
@import "@fontsource/vazirmatn/300.css";
@import "@fontsource/vazirmatn/400.css";
@import "@fontsource/vazirmatn/500.css";
@import "@fontsource/vazirmatn/700.css";
@import "@fontsource/vazirmatn/900.css";
```

3- add below code to index.css:

```css
@layer base {
  :root {
    --font-sans: "Vazirmatn", Tahoma, sans-serif;
  }

  /* all shadcn components */
  * {
    @apply border-border;
  }

  body {
    @apply bg-background text-foreground font-sans;
  }
}
```

4- change tailwind.config.js:

```javascript
extend: {
      fontFamily: {
        sans: ["Vazirmatn", "Tahoma", "sans-serif"],
        vazir: ["Vazirmatn", "Tahoma", "sans-serif"],
      },
      fontWeight: {
        thin: 100,
        extralight: 200,
        light: 300,
        normal: 400,
        medium: 500,
        semibold: 600,
        bold: 700,
        extrabold: 800,
        black: 900,
      },
    },
```

5- change Layout.tsx:

```typescript
import { Footer, Navbar, ScrollToTop } from "@/components";
import { Outlet, ScrollRestoration } from "react-router-dom";
import { cn } from "@/lib/utils";
import { useTranslation } from "react-i18next";

export const Layout = () => {
  const { i18n } = useTranslation();

  return (
    <div
      className={cn(
        "flex min-h-screen flex-col bg-background antialiased",
        i18n.language === "fa" && "font-vazir dir-rtl",
      )}
      dir={i18n.dir()}
    >
      <Navbar showLanguageSwitcher={false} />

      <main className="flex-1">
        <div className="container mx-auto p-8">
          <Outlet />
        </div>
      </main>

      <Footer />
      <ScrollToTop />
      <ScrollRestoration />
    </div>
  );
};
```
