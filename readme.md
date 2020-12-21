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

- Note that `generateBuildId` in `next.config.js` returns a constant value. The expectation is that build assets will be named the same because of this.

- If you build the project twice in the same folder, all of the asset files will be named the same. Even if you delete the `.next` folder and rebuild, the files will have the same names.

- This doesn't seem to be fixed by naming the project folders the same, just in different parent directories. It seems to have to do with the full cwd.

- I've also tried building in one of the project folders, saving the build-manifest.json file, deleting the entire project folder, re-cloning to the same folder name, building again, and comparing the next build-manifest.json to the old one. They're the same.

- I tried doing the "Setup" described above, saved each manifest, swapped he folder names (e.g. renamed `nextjs-build-id-issue-1` to `nextjs-build-id-issue-2` and vice versa), removed `.nextjs`, and rebuilt. The manifests matched the saved versions from their new names (i.e. the build seems to match cwd).
