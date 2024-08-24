# simenandre/publish-with-pnpm

This composite action will publish your package to NPM using PNPM.

It parses tag version and set that in `package.json` before publishing, and pushes that
to the default branch after publishing.

```yaml
name: Release to NPM

on:
  release:
    types: [published]

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout 🛎️
        uses: actions/checkout@v4

      - uses: pnpm/action-setup@v4

      - name: Use Node LTS ✨
        uses: actions/setup-node@v4
        with:
          node-version: lts/*
          registry-url: https://registry.npmjs.org
          cache: pnpm

      - name: Install dependencies 📦️
        run: pnpm install --frozen-lockfile

      - name: Build 🔨
        run: pnpm build

      - uses: simenandre/publish-with-pnpm@v2
        with:
          npm-auth-token: ${{ secrets.NPM_TOKEN }}
```

## Other actions

- [simenandre/publish-with-yarn](https://github.com/simenandre/publish-with-yarn)
- [simenandre/publish-with-yarn-classic](https://github.com/simenandre/publish-with-yarn-classic)
