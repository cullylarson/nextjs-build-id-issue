# Next.js generateBuildId issue demo

This repo demonstrates an issue where build assets are named differently, depending on the name of the cwd folder, even if `generateBuildId` (in `next.config.js`) returns the same ID.

## Setup

1. Clone this repo into two folders:

```
git clone https://github.com/cullylarson/nextjs-build-id-issue.git nextjs-build-id-issue-1
git clone https://github.com/cullylarson/nextjs-build-id-issue.git nextjs-build-id-issue-2
```

2. Build the project in both folders:

```
cd nextjs-build-id-issue-1
npm install
npm run build
cd ../nextjs-build-id-issue-2
npm install
npm run build
```

3. Diff the two build manifests:

```
diff nextjs-build-id-issue-1/.next/build-manifest.json nextjs-build-id-issue-2/.next/build-manifest.json
```

## Notes

Note that `generateBuildId` in `next.config.js` returns a constant value. The expectation is that build assets will be named the same because of this.
