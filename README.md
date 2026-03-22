# LoyaltyIQ Entity Relationship Diagram (ERD)

Below is the main database entity relationship diagram for the LoyaltyIQ platform, rendered using Mermaid. GitHub will display this diagram visually below:

```mermaid
erDiagram
    clients ||--o{ loyalty_tier_config : "has"
    clients ||--o{ members : "has"
    clients ||--o{ products : "has"
    clients ||--o{ campaigns : "has"
    clients ||--o{ images : "has"
    clients ||--o{ brochures : "has"
    clients ||--o{ points_transactions : "has"

    loyalty_tier_config }o--|| clients : "belongs to"
    members }o--|| clients : "belongs to"
    members ||--o{ points_transactions : "has"
    members }o--o| members : "refers to (referred_by_id)"
    products }o--|| clients : "belongs to"
    campaigns }o--|| clients : "belongs to"
    images }o--|| clients : "belongs to"
    brochures }o--|| clients : "belongs to"
    points_transactions }o--|| clients : "belongs to"
    points_transactions }o--|| members : "for"
    points_transactions }o--o| campaigns : "may reference"
    points_transactions }o--o| products : "may reference"

    campaigns ||--o{ campaign_audiences : "has"
    campaigns ||--o{ campaign_channels : "has"
    campaigns ||--o{ campaign_products : "has"
    campaign_products }o--|| products : "references"
    campaign_audiences }o--|| campaigns : "belongs to"
    campaign_channels }o--|| campaigns : "belongs to"

    images ||--o{ image_campaign_usage : "used in"
    image_campaign_usage }o--|| campaigns : "references"
    image_campaign_usage }o--|| images : "references"

    brochures ||--o{ brochure_products : "has"
    brochures ||--o{ brochure_images : "has"
    brochure_products }o--|| products : "references"
    brochure_images }o--|| images : "references"

    audit_log }o--|| clients : "may reference (changed_by)"
```

---

# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Oxc](https://oxc.rs)
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/)

## React Compiler

The React Compiler is enabled on this template. See [this documentation](https://react.dev/learn/react-compiler) for more information.

Note: This will impact Vite dev & build performances.

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type-aware lint rules:

```js
export default defineConfig([
  globalIgnores(['dist']),
  {
    files: ['**/*.{ts,tsx}'],
    extends: [
      // Other configs...

      // Remove tseslint.configs.recommended and replace with this
      tseslint.configs.recommendedTypeChecked,
      // Alternatively, use this for stricter rules
      tseslint.configs.strictTypeChecked,
      // Optionally, add this for stylistic rules
      tseslint.configs.stylisticTypeChecked,

      // Other configs...
    ],
    languageOptions: {
      parserOptions: {
        project: ['./tsconfig.node.json', './tsconfig.app.json'],
        tsconfigRootDir: import.meta.dirname,
      },
      // other options...
    },
  },
])
```

You can also install [eslint-plugin-react-x](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-x) and [eslint-plugin-react-dom](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-dom) for React-specific lint rules:

```js
// eslint.config.js
import reactX from 'eslint-plugin-react-x'
import reactDom from 'eslint-plugin-react-dom'

export default defineConfig([
  globalIgnores(['dist']),
  {
    files: ['**/*.{ts,tsx}'],
    extends: [
      // Other configs...
      // Enable lint rules for React
      reactX.configs['recommended-typescript'],
      // Enable lint rules for React DOM
      reactDom.configs.recommended,
    ],
    languageOptions: {
      parserOptions: {
        project: ['./tsconfig.node.json', './tsconfig.app.json'],
        tsconfigRootDir: import.meta.dirname,
      },
      // other options...
    },
  },
])
```
# loyalty
