# Reproduction for ESLint Issue

- eslint/eslint#20358


I cannot ignore eslint-suppressions.json file when running eslint

## Wanted behavior

I want eslint to show me the problem about unused 'unusedVar' in main.ts

## Actual behavior

Because of suppressions, simply running esling show no problem:

```bash
yarn eslint .
```

Pointing eslint to an inexisting suppressions file isn't working either, because eslint check file existence

```bash
yarn eslint --suppressions-location "inexisting.json"
```

## Work arounds

It need to create another file, but I can point eslint to an empty suppressions file, it will then show the error :

```bash
yarn eslint --suppressions-location "empty.json"
```

I also can rename the eslint-suppressions.json file to something else, and then run eslint normally:

```bash
mv eslint-suppressions.json temp.json
yarn eslint .
mv temp.json eslint-suppressions.json
```

## Ideal solution

The ideal solution would be to have a way to tell eslint to ignore the suppressions file.

For example, a flag like:

```bash
yarn eslint --ignore-suppressions
```

That would make eslint behave as if there was no suppressions file at all, showing all the problems in the codebase.
