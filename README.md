# monorepo-demo-turborepo

## Getting Started

```sh
npm install -g pnpm
pnpm install
```

## Develop

```sh
pnpm turbo run dev --scope=web-1
# > web-1:dev
# https://turborepo.org/docs/features/scopes
# 
# About the `--scope` issue and the new flag `--filter`
# https://github.com/vercel/turborepo/issues/417
# https://github.com/vercel/turborepo/pull/887

pnpm turbo run build --scope=web-1 --include-dependencies
# > @demo/ui:build
# > web-1:build

pnpm turbo run web-1#deploy
# > web-1 lint
# > @demo/ui build
# > web-1 test
# > web-1 build
# > web-1 deploy

pnpm turbo run test --scope=web-1 --scope=web-2
# > web-1 test
# > web-2 test

pnpm turbo run test
# > @demo/ui test
# > web-1 test
# > web-2 test

pnpm turbo run test --since=origin/main
# (no tasks)

echo "export const foo = 'foo';" >> packages/ui/index.ts
pnpm turbo run test --since=origin/main
# > @demo/ui:test
# > web-1:test
# https://turborepo.org/docs/reference/command-line-reference#--since

# Install a package
pnpm add <pkg> --filter web-1
```

## Task Graph

```sh
# Generate the current task graph.
# https://turborepo.org/docs/reference/command-line-reference#--graph
pnpm turbo run build --graph=graph_build.png
pnpm turbo run build --scope=web-1 --graph=graph_build_scope=web-1.png
pnpm turbo run build --scope=web-1 --include-dependencies --graph=graph_build_scope=web-1_include-dependencies.png
pnpm turbo run web-1#deploy --graph=graph_web-1#deploy.png
```

|`build`|`build --scope=web-1`|`build --scope=web-1 --include-dependencies`|`web-1#deploy`|
|--|--|--|--|
|![graph_build.png](https://raw.githubusercontent.com/ryotah/monorepo-demo-turborepo/main/graph_build.png)|![graph_build_scope=web-1.png](https://raw.githubusercontent.com/ryotah/monorepo-demo-turborepo/main/graph_build_scope=web-1.png)|![graph_build_scope=web-1_include-dependencies.png](https://github.com/ryotah/monorepo-demo-turborepo/blob/main/graph_scope=web-1_include-dependencies.png?raw=true)|![graph_web-1#deploy.png](https://raw.githubusercontent.com/ryotah/monorepo-demo-turborepo/main/graph_web-1%23deploy.png)|
