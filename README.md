# Next.js Tailwind Turborepo

This is a portfolio monorepo for professionals.

## What's inside?

This Turborepo includes the following packages/apps:

### Apps and Packages

- `@repo/*`: [Next.js](https://nextjs.org/) apps with [Tailwind CSS](https://tailwindcss.com/)
- `@repo/ui`: a React component library with [Tailwind CSS](https://tailwindcss.com/) shared by both `web` and `docs` applications
- `@repo/eslint-config`: `eslint` configurations (includes `eslint-config-next` and `eslint-config-prettier`)
- `@repo/tailwind-config`: `tailwind` configs used throughout the monorepo
- `@repo/typescript-config`: `tsconfig.json`s used throughout the monorepo

Each package/app is 100% [TypeScript](https://www.typescriptlang.org/).

### Getting Started

- `pnpm install` install & init dependencies
- `pnpm dev` run dev commands in all modules
- `pnpm build` build artifacts (used for deployment really)

- Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.
- You can start editing the page by modifying `apps/web/app/page.tsx`. The page auto-updates as you edit the file.
- This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

### Building packages/ui

This example is set up to produce compiled styles for `ui` components into the `dist` directory. The component `.tsx` files are consumed by the Next.js apps directly using `transpilePackages` in `next.config.js`. This was chosen for several reasons:

- Make sharing one `tailwind.config.js` to apps and packages as easy as possible.
- Make package compilation simple by only depending on the Next.js Compiler and `tailwindcss`.
- Ensure Tailwind classes do not overwrite each other. The `ui` package uses a `ui-` prefix for it's classes.
- Maintain clear package export boundaries.

Another option is to consume `packages/ui` directly from source without building. If using this option, you will need to update the `tailwind.config.js` in your apps to be aware of your package locations, so it can find all usages of the `tailwindcss` class names for CSS compilation.

For example, in [tailwind.config.js](packages/tailwind-config/tailwind.config.js):

```js
  content: [
    // app content
    `src/**/*.{js,ts,jsx,tsx}`,
    // include packages if not transpiling
    "../../packages/ui/*.{js,ts,jsx,tsx}",
  ],
```

If you choose this strategy, you can remove the `tailwindcss` and `autoprefixer` dependencies from the `ui` package.

### Utilities

This Turborepo has some additional tools already setup for you:

- [Tailwind CSS](https://tailwindcss.com/) for styles
- [TypeScript](https://www.typescriptlang.org/) for static type checking
- [ESLint](https://eslint.org/) for code linting
- [Prettier](https://prettier.io) for code formatting
