# Internationalization (i18n) Features

## Overview
The dashboard now supports multiple languages with full internationalization using `next-intl`. Users can switch between languages and the entire interface will be translated.

## Supported Languages
- **English (en)** - Default
- **Spanish (es)** - Español
- **French (fr)** - Français
- **German (de)** - Deutsch
- **Japanese (ja)** - 日本語

## Features Added

### 1. **Language Switcher**
- Located in the top header next to the theme selector
- Dropdown menu with all available languages
- Instant language switching without page reload
- Accessible with keyboard navigation

### 2. **Translated Components**
- **Navigation**: All sidebar menu items are translated
- **Dashboard**: Page titles, descriptions, and content
- **User Menu**: Profile, billing, notifications options
- **Recent Sales**: Card title and description
- **Common UI**: Buttons, form elements, and error messages

### 3. **URL Structure**
- All routes now include locale prefix (e.g., `/en/dashboard`, `/es/dashboard`)
- Automatic locale detection and redirects
- Locale-aware routing with middleware

### 4. **SEO Friendly**
- Proper HTML lang attribute set for each locale
- Locale-specific metadata
- Search engine optimized URL structure

## File Structure

```
src/
├── i18n/
│   └── config.ts              # i18n configuration
├── messages/
│   ├── en.json               # English translations
│   ├── es.json               # Spanish translations
│   ├── fr.json               # French translations
│   ├── de.json               # German translations
│   └── ja.json               # Japanese translations
├── app/
│   └── [locale]/             # Locale-aware routing
│       ├── layout.tsx        # Root layout with i18n provider
│       ├── page.tsx          # Homepage
│       ├── dashboard/        # Dashboard pages
│       └── auth/             # Authentication pages
├── components/
│   └── language-switcher.tsx # Language switcher component
└── middleware.ts             # Updated with locale handling
```

## How to Preview the Updated Version

### 1. **Start the Development Server**
```bash
npm run dev
```

### 2. **Access Different Languages**
The server will be running at `http://localhost:3000`. You can access different languages using these URLs:

- **English**: `http://localhost:3000/en/dashboard/overview`
- **Spanish**: `http://localhost:3000/es/dashboard/overview`
- **French**: `http://localhost:3000/fr/dashboard/overview`
- **German**: `http://localhost:3000/de/dashboard/overview`
- **Japanese**: `http://localhost:3000/ja/dashboard/overview`

### 3. **Test Language Switching**
1. Navigate to any page in the dashboard
2. Click the language switcher in the top header (globe icon)
3. Select a different language from the dropdown
4. The page will instantly update to the selected language

### 4. **Test Features**
- **Navigation**: Check that all sidebar items are translated
- **Dashboard Content**: Verify the overview page content is translated
- **User Menu**: Open the user dropdown to see translated options
- **Recent Sales**: Check the sales card title and description
- **URL Updates**: Notice how the URL changes when switching languages

### 5. **Authentication Flow**
The authentication pages are also locale-aware:
- **Sign In**: `http://localhost:3000/[locale]/auth/sign-in`
- **Sign Up**: `http://localhost:3000/[locale]/auth/sign-up`

## Adding New Languages

To add a new language:

1. **Add locale to configuration**:
   ```typescript
   // src/i18n/config.ts
   export const locales = ['en', 'es', 'fr', 'de', 'ja', 'pt'] as const;
   ```

2. **Create translation file**:
   ```json
   // messages/pt.json
   {
     "navigation": {
       "dashboard": "Painel",
       "product": "Produto",
       ...
     }
   }
   ```

3. **Update language switcher**:
   ```json
   // In all message files, add:
   "language": {
     "pt": "Português"
   }
   ```

## Development Notes

- The i18n system uses React Context for client-side translations
- All translations are loaded at build time for optimal performance
- The middleware handles locale detection and routing
- TypeScript support ensures type safety for translation keys

## Browser Compatibility

The i18n implementation works in all modern browsers and provides:
- Automatic language detection from browser preferences
- Fallback to default language (English) if unsupported locale
- Proper handling of right-to-left languages (ready for Arabic, Hebrew, etc.)

## Performance

- **Bundle size**: Translation files are split by locale
- **Loading**: Only the current locale's translations are loaded
- **Caching**: Translation files are cached for optimal performance
- **Streaming**: Compatible with React Server Components and streaming